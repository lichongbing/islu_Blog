---
title: PowerShell运行hexo命令
author: 闲花
img: "https://files.islu.cn/article/WindowsPowerShell"
toc: true
mathjax: false
categories: Hexo
tags:
  - Windows PowerShell
  - Hexo
keywords: "Windows PowerShell,hexo命令运行,Windows PowerShell无法运行hexo命令"
summary: 解决在Windows PowerShell无法运行hexo命令
abbrlink: 23584
date: 2021-08-03 23:00:02
update: 2021-08-03 23:00:02
---

# Windows PowerShell 运行 hexo 命令

## 前言

一个月前更新了 Windows11，在桌面右键可以直接开启 `Windows PowerShell` 便在安装 `git` 时没有选择在右键快捷打开的配置，便有了这篇水文

在新系统上装了 hexo 环境，可打开系统默认的 `Windows PowerShell` 运行命令却无法识别，以为是系统环境变量没设置好。可在 `Git bash` 和 `CMD` 终端却可以执行，再仔细看 `Windows PowerShell` 中的提示，原来是提示的无法加载文件，因此在此系统上禁止运行脚本。

## 错误示例

安装好 `npm` 和 `hexo` 后，在 `Windows PowerShell` 终端运行 `npm version` 没问题，运行 `hexo version` 则提示如下：

```powershell
hexo : 无法加载文件 C:\Users\username\AppData\Roaming\npm\hexo.ps1`，因为在此系统上禁止运行脚本。有关详细信息，请参阅 https:/go.microsoft.com/fwlink/?LinkID=135170 中的 `about_Execution_Policies`。
所在位置 行:1 字符: 1
```

> 此时，在 `CMD` 中执行以上命令都没问题，所以不是系统环境变量的问题。

## 解决方案

用管理员权限打开 `Windows PowerShell`  ，运行以下命令：

```powershell
Set-ExecutionPolicy -ExecutionPolicy UNRESTRICTED
```

在提示中输入 `Y` 即可(安全警示，如果不输入同意还是无法解决问题)

> 随后便可直接右键选择 `Windows PowerShell` 运行 hexo 命令了 ( : 记得要用 `cd` 跳转到你的文件夹目录哦~
