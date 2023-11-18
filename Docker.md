## 基础命令

> 拉取镜像

```shell
docker pull 镜像地址/组织/项目名称:版本号
```

> 查看镜像

```shell
docker images
```

> 启动容器服务

```shell
# node-red 启动示例
docker run -d -p 1880:1880 -v D:\03-environment\node-red-one:/data --restart=always --name node-red [imageId]
```

命令详解：
- `--rm`: 容器停止运行后自动删除该容器（临时或一次性运行容器使用）
- `-d`: 保持后台挂起
- `--name=容器名称`: 指定容器名称
- `--env ENV_VARIABLE=xxx`: 向容器内传递环境变量
- `-p 外端口:内端口`: 指定内外映射端口，可指定多个（需要多个 `-p`）
- `-v 外目录:内目录`: 指定内外目录映射，可指定多个
- `--restart-always`: Docker 重启时总是重启该容器服务（跟随 Docker 一起启动）

> 停止容器服务

```shell
docker stop [CONTAINER ID]/[CONTAINER NAME]
```

> 删除容器服务

```shell
# 容器服务必须是 stop 状态
docker rm [CONTAINER ID]/[CONTAINER NAME]

docker rm $(docker ps -aq)
```

> 进入容器服务

```shell
docker exec -it [CONTAINER ID] /bin/bash
```

> 查看容器服务

```shell
docker ps

# 显示隐藏的服务
docker ps -a
```
