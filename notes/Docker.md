## 常用

### 拉镜像

```shell
docker pull 镜像地址/组织/项目名称:版本号
```

### 看镜像

```shell
docker images
```

### 启动容器

```shell
# node-red 启动示例
docker run -d -p 1880:1880 -v D:\03-environment\node-red-one:/data --restart=always --name node-red [imageId]
```

> 命令详解：

- `--rm`: 容器停止运行后自动删除该容器（临时或一次性运行容器使用）
- `-d`: 保持后台挂起
- `--name=容器名称`: 指定容器名称
- `--env ENV_VARIABLE=xxx`: 向容器内传递环境变量
- `-p 外端口:内端口`: 指定内外映射端口，可指定多个（需要多个 `-p`）
- `-v 外目录:内目录`: 指定内外目录映射，可指定多个
- `--restart-always`: Docker 重启时总是重启该容器服务（跟随 Docker 一起启动）

### 停止容器

```shell
docker stop [CONTAINER ID]/[CONTAINER NAME]
```

### 删除容器

```shell
# 容器服务必须是 stop 状态
docker rm [CONTAINER ID]/[CONTAINER NAME]

docker rm $(docker ps -aq)
```

### 进入容器

```shell
docker exec -it [CONTAINER ID] /bin/bash
```

### 查看容器

```shell
docker ps

# 显示隐藏的服务
docker ps -a
```

## Docker Volumes

### 创建 volume

```shell
docker volume create my-vol
```

### 删除 volume

```shell
docker volume rm my-vol
```

### 查看 volume 列表

```shell
docker volume ls
```

### 检查单个 volume 具体信息

```shell
docker volume inspect my-vol
```

## Docker Compose

### 在后台启动服务

```shell
# 所有服务
docker compose up -d

# NOTE: 启动单个服务，基本后面的命令都可以加 serverName
docker compose up -d [server name]
```

### 启动服务

```shell
docker compose start
```

### 停止并删除服务资源

```shell
docker compose down

# 删除创建的 Docker Volumes
docker compose down --volumes
```

### 列出所有运行中的服务

```shell
docker compose ps
```

### 查看日志

```shell
docker compose logs -f
```

### 构建镜像

```shell
docker comopse build
```
