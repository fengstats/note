# WebRTC + SRS

## 前言

> 参考资料

- [推流卡顿](https://github.com/ossrs/srs/issues/2677)
- [HLS 纯视频流在 Apple 设备上播放卡住 1](https://github.com/ossrs/srs/issues/2570)
- [HLS 纯视频流在 Apple 设备上播放卡住 2](https://github.com/ossrs/srs/issues/1326)
- [WebRTC 一对一信令协商过程图](https://developer.mozilla.org/zh-CN/docs/Web/API/WebRTC_API/Signaling_and_video_calling/webrtc_-_signaling_diagram.svg)
- [ICE CANDIDATE 交换](https://developer.mozilla.org/zh-CN/docs/Web/API/WebRTC_API/Signaling_and_video_calling/webrtc_-_ice_candidate_exchange.svg)

## Docker Hub 镜像加速配置

[国内教育机构与各大云服务商提供的镜像加速服务](https://gist.github.com/y0ngb1n/7e8f16af3242c7815e7ca2f0833d3ea6) - 推荐海交大镜像站，网速还行的情况下，拉取 mysql:8.0 镜像只用了 31s，大约 600MB 左右，不行的话再试试其他的。

```json
"registry-mirrors": [
  "https://docker.mirrors.sjtug.sjtu.edu.cn"
]
```

## FFmpeg - Homebrew

一个完整的跨平台解决方案，用于录制、转换和流式传输音频和视频，功能超级强大。

> 直接用 Homebrew 装，遇到问题解决问题，肯定是能装下来的。

```shell
brew install ffmpeg
```

将本地视频推送到 SRS 服务

```shell
# 需要更改本地视频地址以及 rtmp 服务地址
ffmpeg -readrate 1 -stream_loop -1 -i /Users/feng/Downloads/1.mp4 -vcodec copy -acodec copy -f flv 'rtmp://localhost/feng/fddm.flv'
```

播放 flv 视频

```shell
ffplay http://localhost:8080/feng/fddm.flv
```

## SRS - Docker

### 拉镜像

```shell
docker pull registry.cn-hangzhou.aliyuncs.com/ossrs/srs:5
```

### 启动服务

- [8080](http://localhost:8080/) 是 Web 端口，可以直接访问查看。
- `$(ifconfig en0 inet | grep 'inet ' | awk '{print $2}')`: 这个命令可以获取本地网络 IP 地址，`en0` 一般是网络连接（WIFI），`en6` 一般是网线连接，在下面的 `CANDIDATE` 就先写死了，这个参数后面连接 WebRTC 时有用，需要改成你自己的 IP 地址。

#### Docker Volume Driver

- 本质上是 Docker Host 文件系统里面的目录或文件，不是外部磁盘，容器可以直接读写 Volume 中的数据，即使使用它的容器被销毁，Volume 中数据也会被保存。
- `./objs/srs -c conf/rtc2rtmp.conf`: 这是在 Docker 容器内容执行的命令，对应目录位置是 `/usr/local/srs`，所以这才是真正的选择配置文件启动 SRS 服务。

```shell
CANDIDATE="192.168.1.3"
docker run -d \
--name billd-live-class-srs \
--env CANDIDATE=$CANDIDATE \
-p 8080:8080 -p 1935:1935 -p 1985:1985 -p 8000:8000/udp \
-v srs_conf:/usr/local/srs/conf \
-v srs_objs:/usr/local/srs/objs \
registry.cn-hangzhou.aliyuncs.com/ossrs/srs:5 \
./objs/srs -c conf/rtc2rtmp.conf
```

#### 本地磁盘目录挂载

> [!todo] 烦，一直有问题，暂时还是用之前的老方法，先启用一个临时服务，把需要的文件目录拷贝到本地目录，这里只需要 `conf` 和 `objs`，后面有时间了再研究看看，究竟是哪一步哪个东西导致不能正常挂载的。

- 要 **保证 LOCAL_SRS_PATH 存在**，替换成你自己的目录位置即可。
- 正常情况下，此命令在拷贝完成会自动停止并删除掉这个临时容器，出现异常时需要手动删除此容器服务。

```shell
LOCAL_SRS_PATH=/Users/feng/codebase/study-pro/billd-z-class/srs
docker run -d --rm --name temp-container registry.cn-hangzhou.aliyuncs.com/ossrs/srs:5 \
&& docker cp temp-container:/usr/local/srs/objs $LOCAL_SRS_PATH/objs \
&& docker cp temp-container:/usr/local/srs/conf $LOCAL_SRS_PATH/conf \
&& docker stop temp-container
```

> 有了启动配置文件，再执行下面的命令应该就没问题了。

```shell
LOCAL_SRS_PATH=/Users/feng/codebase/study-pro/billd-z-class/srs
CANDIDATE="192.168.1.3"
docker run -d \
--name billd-live-class-srs \
--env CANDIDATE=$CANDIDATE \
-p 8080:8080 -p 1935:1935 -p 1985:1985 -p 8000:8000/udp \
-v $LOCAL_SRS_PATH/conf:/usr/local/srs/conf \
-v $LOCAL_SRS_PATH/objs:/usr/local/srs/objs \
registry.cn-hangzhou.aliyuncs.com/ossrs/srs:5 \
./objs/srs -c conf/rtc2rtmp.conf
```

## MySql - Docker

[Mac App Store Navicat Premium 16.1.0 及后续版本激活](https://github.com/LiJunYi2/navicat-keygen-16V/issues/17) - 先在 App Store 下载 Navicat 但别打开，下载执行 Navicat Crack.dmg，等成功激活之后再打开从 App Store 下载的 Navicat。

### 拉镜像

```shell
docker pull mysql:8.0
```

### 启动服务

我们需要从容器内映射两个东西到本地磁盘：

1. 启动配置文件 `my.cnf`，容器内默认按照此路径顺序寻找启动：`/etc/my.cnf`、`/etc/mysql/my.cnf`、`/usr/etc/my.cnf`、`~/.my.cnf`，一般这个文件都在 `/etc/my.cnf`，因为我们后期可能需要修改配置启动，所以映射出来，方便更新和保存配置。
2. 数据目录 `/var/lib/mysql`，你的数据库信息都在这里面，后面就算容器删掉了也可以用这个来恢复。

#### 拷贝配置文件

2023-12-07 上次疑问解决了，就是挂载不出来，本地必须要有 `my.cnf` 这个文件，参考文章：[Docker Compose 安装 MySql](https://tuonioooo-notebook.gitbook.io/docker/docker-compose/docker-compose%E5%AE%89%E8%A3%85mySql)

> GitHub

- 官方的配置文件模板：[my.cnf](https://github.com/tuonioooo/docker/blob/master/docker-compose/mysql/default/my.cnf)
- 大佬的配置文件模板：[my.cnf](https://github.com/tuonioooo/docker/blob/master/docker-compose/mysql/my.cnf)

把这个文件放到本地对应的位置，下面的部分就可以跳过了，跳到启动的部分。

---

> 这是之前的老方法，不过目的都是一样的。

还是不知道为什么不能直接 `-v` 把 `my.cnf` 从容器内挂载出来，所以还是先用临时容器拷一份出来吧 🤡。

- 保证本地 **存在 $mysqlPath/conf 这个目录**，否则会拷贝失败或异常。
- 我在这里踩了个小坑，不能用 `path` 命名设置临时目录变量啊！！！这 TM 是系统变量，软件和系统配置启动文件都会追加在这个变量上，我这么设置临时变量相当于直接覆盖掉了，意味着连 docker 命令都没了，还好只是临时变量，把原来的内容设置回去或者重开一个终端就恢复啦。
- 所以设置临时变量前可以先用 `echo $xxx` 来检查一下这个变量是否存在。

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/Mac%20path%20%E7%B3%BB%E7%BB%9F%E5%8F%98%E9%87%8F.png)

```shell
mysqlPath=/Users/feng/codebase/study-pro/billd-z-class/mysql
docker run -d --rm --name temp mysql:8.0 \
&& docker cp temp:/etc/my.cnf $mysqlPath/conf \
&& docker stop temp
```

#### 这下可以启动了吧？原神…启动！

如果出现启动成功后，测试连接失败的情况可以试试添加 `-e MYSQL_ROOT_HOST=%`

我上次是加了这个才行的，这次没有也可以了，所以有点奇怪。

```shell
LOCAL_MYSQL_PATH=/Users/feng/codebase/study-pro/billd-z-class/mysql
docker run -d \
-p 3306:3306 \
--name billd-live-mysql \
-e MYSQL_ROOT_PASSWORD=mysql123. \
-v $LOCAL_MYSQL_PATH/conf/my.cnf:/etc/my.cnf \
-v $LOCAL_MYSQL_PATH/data:/var/lib/mysql \
mysql:8.0
```
