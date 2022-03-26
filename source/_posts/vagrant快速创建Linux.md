---
title: vagrant快速创建Linux
author: 闲花
img: "https://files.islu.cn/article/vagrant&virtualBox.jpg"
top: false
toc: true
mathjax: false
categories: Vagrant
tags:
  - Vagrant
  - Linux
keywords: "利用Vagrant快速创建Linux虚拟机并通过命令行快速启动,Vagrant,Linux,Vagrantfile,虚拟机,Centos7"
essay: false
summary: 利用Vagrant快速创建Linux虚拟机并通过命令行快速启动
abbrlink: 18967
date: 2021-03-26 12:54:58
update: 2021-03-26 12:54:58
---

# 利用 Vagrant 快速搭建 linux 虚拟机

## 下载并安装 VM VirtualBox

官方下载地址 [传送门](https://www.virtualbox.org/wiki/Downloads)

微云下载 [传送门](https://share.weiyun.com/oNxWsvB1)

安装过程同普通软件安装一样，选择安装路径即可

## 下载并安装 Vagrant

官方下载地址 [传送门](https://www.vagrantup.com/downloads) （翻墙者推荐使用）

微云下载 [传送门](https://share.weiyun.com/bsY62EZ3) （推荐使用）

安装过程同普通软件安装一样，选择安装路径即可

## 使用 Vagrant

### 检验 Vagrant 是否安装成功

打开命令行输入命令`vagrant`

```shell
vagrant # 出现大段命令提示即为成功
```

### 初始化操作系统以 centos/7 为例以 centos/7 为例

更多操作系统镜像仓库

在此以 centos/7 为例

命令行中输入命令 `vagrant init 镜像名`

```shell
# centos/7为cmd命令行相对路径下的box
vagrant init centos/7 #初始化centos/7镜像操作系统

# 若下载过慢可使用中科大镜像
vagrant init centos7 https://mirrors.ustc.edu.cn/centos-cloud/centos/7/vagrant/x86_64/images/CentOS-7.box
```

初始化成功后会在 cmd 运行目录中出现文件 `Vagrantfile`

### 启动虚拟机

cmd 中输入命令 `vagrant up` 启动虚拟机

运行至 `Rsyncing folder: /cygdrive/c/Users/L => /vagrant` 这行命令时使用 `Ctrl+C` 结束运行

### 运行并使用虚拟机

若**VirtualBox** 打开并运行虚拟机即可使用 `vagrant ssh` 命令进行操作

## 开机后快速启动并使用虚拟机

**VirtualBox** 未打开可在 cmd 中使用命令 `vagrant up` 启动虚拟机后再使用命令 `vagrant ssh` 登陆后对虚拟机进行操作
