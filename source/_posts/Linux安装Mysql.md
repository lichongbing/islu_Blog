---
title: Linux安装Mysql
author: 闲花
img: "https://files.islu.cn/article/Linux+Mysql"
top: false
toc: true
categories: Linux
tags:
  - Linux
  - MySQL
keywords: "Linux,MySQL,虚拟机配置MySQL,MySQL远程连接,Navicat无法连接虚拟机MySQL"
essay: false
summary: Linux安装Mysql（需联网）
abbrlink: 35752
date: 2021-05-20 22:09:05
update: 2021-05-20 22:09:05
---

## **安装 MySQL**

```shell
wget https://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm

rpm -ivh mysql-community-release-el7-5.noarch.rpm

yum update

yum install mysql-server
```

若未找到 wget

![](https://files.islu.cn/article/NotFindwget#id=lxBbt&originHeight=765&originWidth=984&originalType=binary&ratio=1&status=done&style=none)

则需要先安装 wget：

```
yum -y install wget
```

![](https://files.islu.cn/article/installWget#id=lblwj&originHeight=765&originWidth=984&originalType=binary&ratio=1&status=done&style=none)

### 权限设置

```shell
chown mysql:mysql -R /var/lib/mysql
```

### 初始化 MySQL

```shell
mysqld --initialize
```

### 启动 MySQL：

```shell
systemctl start mysqld
```

### 查看 MySQL 运行状态：

```shell
systemctl status mysqld
```

### 使用 MySQL ClientMysql 客户端 Mysql 客户端 执行简单的 SQL 命令

```shell
mysql
```

### 创建 root 用户密码并登录

```shell
# 设置密码
set password for 'root'@'localhost'=password('root');
# 推出Mysql
exit
# 登录MySQL
mysql -u root -p
```

远程链接了一下 MySQL，出现了以下错误，查了一下，是因为 MySQL 没有允许远程登陆，所以要授权 MySQL 远程登陆。

![](https://files.islu.cn/article/mysql_1130error.png#id=DNyAv&originHeight=126&originWidth=501&originalType=binary&ratio=1&status=done&style=none)

从任何主机上使用 root 用户，密码：yourpassword（你的 root 密码）连接到 mysql 服务器：

```mysql
# 完成登录操作mysql -u root -p root # 修改访问权限mysql>GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'root' WITH GRANT OPTION;操作完后切记执行以下命令刷新权限 FLUSH PRIVILEGES
```

这时再通过 navicat 远程链接 MySQL，链接测试。
