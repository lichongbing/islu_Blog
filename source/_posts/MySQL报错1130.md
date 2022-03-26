---
title: MySQL报错1130
author: 闲花
img: "https://files.islu.cn/article/MySQL.jpeg"
top: false
toc: true
mathjax: false
categories: MySQL
tags:
  - MySQL(1130错误码)
  - Navicat
keywords: "MySQL报错,MySQL1130错误码,Navicat远程连接错误"
essay: false
summary: "解决Navicat远程连接MySQL数据库报错,错误码1130"
abbrlink: 13413
date: 2021-05-31 18:02:40
update: 2021-05-31 18:02:40
---

## 错误截图

![](https://files.islu.cn/article/mysql_1130CodeError#id=FMh5D&originHeight=490&originWidth=483&originalType=binary&ratio=1&status=done&style=none)

## 错误原因

> 错误：ERROR 1130: Host ‘192.168.XX.XXX’ is not allowed to connect to thisMySQL serve
>
> 错误 1130：主机 192.168.XX.XXX”不允许连接到 thismysql 服务
>
> 原因：被连接的数据不允许使用 192.168.XX.XXX 访问，只允许是用 localhost;

## 解决办法

在 localhost 的那台电脑，登入 mysql 后，更改”mysql” 数据库里的 “user” 表里的 “host”项，从”localhost”改称”%”

命令详情

```mysql
mysql -u root -p

use mysql;

select 'host' from user where user='root';

update user set host = '%' where user ='root';

flush privileges;

select 'host'   from user where user='root';
```
