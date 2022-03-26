---
title: Docker安装Redis
author: 闲花
img: "https://files.islu.cn/article/docker+redis.png"
coverImg: /images/1.jpg
toc: true
mathjax: false
categories: Docker
tags:
  - Docker
  - Redis
keywords: "Docker安装Redis,Docker配置Redis环境,Linux虚拟机中Redis服务"
essay: false
summary: "在Docker容器中拉去Redis镜像,远程连接Redis服务"
abbrlink: 41794
date: 2021-05-24 19:06:42
update: 2021-05-24 19:06:42
---

## Docker 安装 Redis

Docker 镜像市场 [传送门](https://hub.docker.com/_/redis)

### 安装 Redis 镜像

```shell
# sudo 以超级管理员权限运行命令
# docker pull 镜像名:镜像版本
# docker pull 镜像名 即不加:版本号为默认安装最新版本镜像
$ sudo docker pull redis
```

### 查询已安装的镜像

使用命令 `sudo docker images` 查询已安装的镜像

### 创建实例并启动

运行命令 `mkdir -p /mydata/redis/conf`

再运行 `touch /mydata/redis/conf/redis.conf`

运行命令实现挂载

```shell
$ sudo docker run -p 6379:6379 --name redis \
-v /mydata/redis/data:/data/log \
-v /mydata/redis/conf:/etc/redis/redis.conf \
-d redis redis-server /etc/redis/redis.conf
```

### 设置 Docker 中 Redis 开机自启动

管理员权限运行命令 (su root)

```shell
docker update redis --restart=always
```

---

### 使用 Redis 客户端

运行`docker ps -a` 查询运行中的容器中是否有`redis`正在运行

![](https://files.islu.cn/article/docker%20ps%20-a.png#id=cmlAa&originHeight=766&originWidth=1468&originalType=binary&ratio=1&status=done&style=none)

使用命令`docker exec -it redis redis-cli` 进行客户端连接

### 使用工具 RedisDesktopManager 远程连接 Redis

工具下载地址 [传送门](https://github.com/uglide/RedisDesktopManager/releases/tag/0.9.3)

微云下载连接 [传送门](https://share.weiyun.com/i9rfHd7U)

安装后在 linux 中输入 `ip addr` 查询 id 地址进行登录即可
