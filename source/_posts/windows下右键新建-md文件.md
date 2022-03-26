---
title: windows下右键新建.md文件
author: 闲花
img: "https://files.islu.cn/article/Markdown"
top: false
toc: true
mathjax: false
categories: Markdown
tags:
  - Markdown
  - Typora
  - windows右键管理
keywords: "Hexo,islu,闲花手札"
summary: 原本创建.md文件需要首先打开markdown文本编辑器，如Typora，或者新建.txt文件然后修改后缀名，本文介绍了如何在Windows操作系统中添加右键创建.md文件的方法
abbrlink: 26497
date: 2021-08-16 10:24:48
update: 2021-08-16 10:24:48
---

# windows 下右键新建.md 文件

原本创建.md 文件需要首先打开 markdown 文本编辑器，如 Typora，或者新建.txt 文件然后修改后缀名，本文介绍了如何在 Windows 操作系统中添加右键创建.md 文件的方法

## 效果

![](https://files.islu.cn/article/image-20210816104344113.png#id=fDWKq&originHeight=495&originWidth=671&originalType=binary&ratio=1&status=done&style=none)

## 步骤

### 打开注册表

1. `CMD+R`，打开运行对话框
2. 输入`regedit`，打开注册表编辑器

### 修改注册表

1.  在`计算机>HKEY_CLASSES_ROOT`右键查找，输入`Typora`，勾选项，取消勾选值和数据
    ![](https://files.islu.cn/article/image-20210816104530834.png#id=pWfqh&originHeight=347&originWidth=795&originalType=binary&ratio=1&status=done&style=none)
2.  确认运行的程序名字，我的电脑如图所示，运行文件是`Typora.exe`
    ![](https://files.islu.cn/article/image-20210816104623410.png#id=fnvl4&originHeight=1117&originWidth=1920&originalType=binary&ratio=1&status=done&style=none)

    > 如果使用的是 markdownpad 或者其他编辑器，同理

3.  在磁盘任意位置新建一个文件，后缀为`.reg`
4.  打开编辑刚刚创建好的注册表文件，写入以下内容：

```reg
Windows Registry Editor Version 5.00
[HKEY_CLASSES_ROOT\.md]
@="Typora.exe"
[HKEY_CLASSES_ROOT\.md\ShellNew]
"NullFile"=""
[HKEY_CLASSES_ROOT\Typora.exe]
@="Markdown"
```

> `@="Typora.exe"` 代表的是指定.md 文件的运行程序
>
> `@="Markdown"` 代表的是右键时默认的文件名字，这样写新建为`新建`Markdown.md`文件`
>
> 且右键菜单中显示`MarkDown`

5.  编辑好之后,另存为,设置如图所示
    ![](https://files.islu.cn//article/image-20210816104844808.png#id=QYKS8&originalType=binary&ratio=1&status=done&style=none)
    > 文件名可以随便设置，但是后缀必须是`.reg`文件,保存类型一定要是`文本文档(*.txt)`

## 编辑新建图标(可选)

1.  以`Typora`为例,在注册表`Typora.exe`下点击项`DefaultIcon`,右键修改
2.  将属性修改为想要设置的 `Markdown`文件图标
    ![](https://files.islu.cn/article/image-20210816105031062.png#id=QYn4U&originHeight=1117&originWidth=1920&originalType=binary&ratio=1&status=done&style=none)
