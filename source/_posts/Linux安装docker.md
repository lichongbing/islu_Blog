---
title: Linux安装Docker
author: 闲花
img: "https://files.islu.cn/article/Docker+Linux"
top: false
toc: true
mathjax: false
categories: Docker
tags:
  - Docker
  - Linux
keywords: "Docker,Linux,Linux安装Docker,Docker入门,Docker常用命令,Docker简介,Docker安装"
essay: false
summary: Linux系统安装Docker容器服务,配置阿里云镜像并使用简单命令操作Docker
abbrlink: 38496
date: 2021-05-22 22:45:06
update: 2021-05-22 22:45:06
---

# Linux 系统 Docker 安装及软件安装

## Docker 简介

Docker 是一个开源的应用容器引擎，基于 [Go 语言](https://www.runoob.com/go/go-tutorial.html) 并遵从 Apache2.0 协议开源。

Docker 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。

容器是完全使用沙箱机制，相互之间不会有任何接口（类似 iPhone 的 app）,更重要的是容器性能开销极低。

Docker 从 17.03 版本之后分为 CE（Community Edition: 社区版） 和 EE（Enterprise Edition: 企业版），我们用社区版就可以了。

## Docker 安装

官方链接 [传送门](https://docs.docker.com/engine/install/centos/)

### 1、卸载旧版本

```shell
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

由于我第一次安装，运行后显示如下图

![](https://files.islu.cn/article/docker-rm-rf.png#id=LZpeQ&originHeight=639&originWidth=1071&originalType=binary&ratio=1&status=done&style=none)

### 2、安装 Docker

1.  安装必要的依赖包设置存储库

```shell
# 安装必要依赖包
$ sudo yum install -y yum-utils

$ sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

2.  启动 Docker

#### 安装 Docker 引擎

```shell
$ sudo yum install docker-ce docker-ce-cli containerd.io
```

```shell
$ sudo systemctl start docker
```

## Docker 简单命令

### 查询 Docker 安装是否成功

```shell
# 使用命令查询Docker是否安装成功(查询Docker安装版本)
$ docker -v
```

![](https://files.islu.cn/article/docker-v.png#id=gevKD&originHeight=639&originWidth=1071&originalType=binary&ratio=1&status=done&style=none)

### 查看 Docker 下载的镜像

```shell
$ sudo docker images
```

![](https://files.islu.cn/article/docker-image#id=SP6xc&originHeight=639&originWidth=1071&originalType=binary&ratio=1&status=done&style=none)

### 设置 Docker 开机自启动

```shell
$ sudo systemctl enable docker
```

![](https://files.islu.cn/article/docker-systemctl#id=JrAYP&originHeight=639&originWidth=1071&originalType=binary&ratio=1&status=done&style=none)

### Docker 镜像加速

阿里云镜像源 [传送门](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors)

登陆后，左侧菜单选中镜像加速器就可以看到你的专属地址了

```shell
$ sudo mkdir -p /etc/docker

$ sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["专属加速地址"]
}
EOF

$ sudo systemctl daemon-reload

$ sudo systemctl restart docker
```
