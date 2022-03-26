---
title: Docker安装MySQL服务
author: 闲花
img: "https://files.islu.cn/article/docker+mysql.png"
top: false
toc: true
mathjax: false
categories: Docker
tags:
  - Docker
  - MySQL
keywords: "Docker安装MySQL,Docker配置MySQL环境,Navicat无法连接MySQL"
essay: false
summary: 在Docker容器中拉去MySQL镜像，并使用Navicat远程连接Docker中的MySQL客户端
abbrlink: 40075
date: 2021-05-23 22:29:15
update: 2021-05-23 22:29:15
---

## Docker 安装 MySQL

### 安装 MySQL 镜像

```shell
# sudo 以超级管理员权限运行命令
# docker pull 镜像名:镜像版本
# docker pull 镜像名 即不加:版本号为默认安装最新版本镜像
$ sudo docker pull mysql:5.7
```

### 查询已安装的镜像

使用命令 `sudo docker images` 查询已安装的镜像

### 创建实例并启动

运行命令实现挂载

```shell
$ docker run -p 3306:3306 --name mysql \
-v /mydata/mysql/log:/var/log/mysql \
-v /mydata/mysql/data:/var/lib/mysql \
-v /mydata/mysql/conf:/etc/mysql \
-e MYSQL_ROOT_PASSWORD=root \
-d mysql:5.7
####################################
# 若未成功可能为权限问题导致，运行 su root 提升至管理员权限
# 参数说明
# -p 3306:3306:    将容器的3306端口映射到主机的3306端口
# -v /mydata/mysql/log:/var/log/mysql    将日志文件夹挂在到主机
# -v /mydata/mysql/data:/var/lib/mysql    将配置文件夹挂在到主机
# -v /mydata/mysql/conf:/etc/mysql    将配置文件夹挂载到主机
# -e MYSQL_ROOT_PASSWORD=root    初始化root用户的密码
# -d mysql：5.7    以后台方式运行
###################################
```

安装后使用命令 `docker ps` 查询正在运行的服务

### 修改 MySQL 配置

将拉丁编码修改为 utf8 编码

在 cmd 中输入命令 `vi /mydata/mysql/conf/my.cnf`

在 `my.cnf` 中添加

```shell
[client]
default-character-set=utf8

[mysql]
default-character-set=utf8

[mysqld]
init_connect='SET collation_connection = utf8_unicode_ci'
init_connect='SET NAMES utf8'
character-set-server=utf8
collation-server=utf8_unicode_ci
skip-character-set-client-handshake
skip-name-resolve
```

运行命令`docker restart mysql` 重启 mysql 服务

### 设置 Docker 中 MySQL 开机自启动

管理员权限运行命令

```shell
docker update mysql --restart=always
```
