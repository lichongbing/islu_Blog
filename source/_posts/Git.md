---
title: Git入门
author: 闲花
img: "https://files.islu.cn/article/Git.png"
top: false
toc: true
mathjax: false
categories: Git
tags:
  - Git
  - Git基础命令
keywords: "Git,Git基础命令,Git分支,breach,repository,Git远程管理,Git提交"
essay: false
summary: Git入门的自我认知
abbrlink: 60322
date: 2021-03-29 09:51:25
update: 2021-03-29 09:51:25
---

![](https://files.islu.cn/article/Git.png#id=d3yrH&originHeight=92&originWidth=220&originalType=binary&ratio=1&status=done&style=none)

## Git

### 概述

> Git 是一个开源的**分布式**版本控制系统，用于敏捷高效地处理从很小到非常大的项目版本管理。支持克隆/下载。
>
> Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。
>
> Git 与常用的版本控制工具 CVS, Subversion 等不同，它采用了分布式版本库的方式，不必服务器端软件支持。

### 安装

[下载 git OSX 版](https://git-scm.com/download/mac)

[下载 git Windows 版](https://msysgit.github.io/)

[下载 git Linux 版](https://git-scm.com/download/linux)

安装验证

```bash
git -version
```

### 原理

> 你的本地仓库由 git 维护的三棵“树”组成。
>
> 第一个是你的 `工作目录`，它持有实际文件；
>
> 第二个是 `暂存区（Index）`，它像个缓存区域，临时保存你的改动；
>
> 最后是 `HEAD`，它指向你最后一次提交的结果。

> 工作区：沙箱环境 git 不会管理 随便更改操作

> 暂存区：记录文件的操作

> 版本库：最终的代码实现提交到这里 .git 目录就是版本库

![](https://files.islu.cn/article/git_trees.png#id=Z4QE6&originHeight=320&originWidth=900&originalType=binary&ratio=1&status=done&style=none)

### 配置

Git 操作配置的命令：

```bash
git  config
```

1.  –system ：系统中对所有用户都普遍适用的配置。使用 git config --system 命令会修改/etc/gitconfig 文件。
2.  –global ：用户目录下的配置文件只适用于该用户。使用 git config --global 读写的是~/.gitconfig
3.  文件不写参数，表示堆当前项目的 git 目录进行配置，使用 git config 可以直接针对当前项目配置，即工作目录下的.git/config 文件

优先级别以就近原则为准。

```
.git/config` > `~/.gitconfig` > `/etc/gitconfig
```

#### 初始化配置

安装完成后初始化配置用户名和邮件地址：

```bash
git config --_global user.name "ialoe"
git config --_global user.email "ialoe@qq.com"
```

查看已有配置：

```bash
git  config --list
```

#### 文件大小写问题

**现象：**文件或文件夹大小写导致找不到文件

git 默认是大小写不敏感的。 如果你大写的文件上次，有可能自己就变小写了。然后访问有可能找不到文件。

查询自己的配置：

```bash
git config --get core.ignorecase
```

配置开启大小写敏感：

(1)全局开启大小写敏感

```bash
git config --_global core.ignorecase false
```

(2)单个项目开启大小写敏感

```bash
git config core.ignorecase false
```

### 仓库

#### 创建仓库

创建新文件夹，打开，然后执行
`git init`
以创建新的 Git 仓库。

#### 目录结构

初始化之后，有一个`.git`隐藏文件，里面的目录结构大概如下：

| 文件夹、文件 | 作用                                         |
| ------------ | -------------------------------------------- |
| hooks/       | 目录包含服务端或客户端钩子脚本               |
| info/        | 包含一个全局性排除文件                       |
| logs/        | 保存日志信息                                 |
| objects/     | 目录存储所有数据内容，`重要`                 |
| refs/        | 目录存储指向数据提交对象的指针，分支，`重要` |
| config       | 文件包含项目特有的配置选项，`重要`           |
| description  | 用来显示对仓库的描述信息                     |
| HEAD         | 文件指示目前被检出的分支，`重要`             |
| index        | 文件保存暂缓区信息，`重要`                   |

#### 检出仓库

执行如下命令以创建一个本地仓库的克隆版本：
`git clone /path/to/repository`

```bash
# 将E盘下的Repository克隆到D盘
git clone E:/SourceRepository D:/DestinationRepository
```

如果是远端服务器上的仓库，你的命令会是这个样子：
`git clone username@host:/path/to/repository`

##### 已配置账户

`git clone git@host:/path/to/repository`

```bash
# 以我的GitHub的BlogCode仓库为例
git clone git@github.com:ialoe/BlogCode.git
```

##### 未配置账户

`git clone 用户名@github.com:ialoe/BlogCode.git`

然后按回车键执行 `git clone` 命令， Git 会提示你输入密码。

```bash
# 以我的GitHub的BlogCode仓库为例
git  clone   ialoe @ https://github.com/ialoe/BlogCode.git
```

##### 指定分支

我们可以通过-b 来指定要克隆的分支名

`git clone -b <name> git@host:/path/to/repository`

#### 添加提交

你可以提出更改（把它们添加到暂存区），使用如下命令：
`git add <filename>` 或者 `git add *`

这是 git 基本工作流程的第一步；使用如下命令以实际提交改动：
`git commit -m "代码提交信息"`
现在，你的改动已经提交到了 **HEAD**，但是还没到你的远端仓库。

#### 推送改动

你的改动现在已经在本地仓库的 **HEAD** 中了。执行如下命令以将这些改动提交到远端仓库：
`git push origin master` or `git push`
可以把 _master_ 换成你想要推送的任何分支。

如果你还没有克隆现有仓库，并欲将你的仓库连接到某个远程服务器，你可以使用如下命令添加：
`git remote add origin <server>`
如此你就能够将你的改动推送到所添加的服务器上去了。

若需强制推送 `git push -f` 《不建议》

### Git 基础命令

#### git init

**初始化工作空间**

初始化工作目录命令格式：

```bash
git init
```

生成 `.git` 目录，所有 git 需要的数据和资源都存在在这个目录。

#### git add

跟踪已修改文件到暂存区：

跟踪一个已修改文件到暂存区的命令格式：

```bash
git add ./
```

git add 命令将修改的文件生成 git 对象，加入暂存区。

过程：将将修改的文件生成成 git 对象，放入版本库，再将 Git 对象加入到暂存区，只是没有生成树对象。在这个过程中，生成 Git 对象是增量式的。

相当于执行了 N 次（N 个文件）：

```
git hash-object -w
git update-index
```

#### git status

跟踪文件状态：

```bash
git status [指定的文件]
```

status ：

- `untracked`：未跟踪，红色
- `tracked` ：已跟踪。
  - `unmodified`：未修改，已提交，一般不列出显示。
- `modified`：已修改，红色
  - `staged` ： 已暂存，绿色

跟踪新文件：

`git add` 命令执行之后使用 `git status`查看，出现`changes to be committed` 表示已经暂存。

暂存已修改文件：

已经暂存的文件进行再次修改，使用 `git status`查看，此时会出现

`changes to be committed` 表示该文件之前暂存区有一份，表示已暂存；同时也会出现

`changes not staged for commit` 表示改文件又有了新的修改。此时已修改文件的状态为`modified`；修改之后的 git 对象还没有生成。如果`git add` 重新暂存，在暂存区则会进行覆盖操作，并重新生成 git 对象的 hash。

#### git diff

查看已暂存和未暂存的更新：

`git status` 仅仅列出修改过的文件。

- 判断当前做的哪些更新还没有做暂存：

```bash
git diff
```

- 判断哪些更新已经暂存准备好了下次提交

```bash
git diff --cached

# 1.6 以上
git diff --staged
```

示例：查看哪些暂存还没提交的数据，这是之前操作的数据。

```bash
git diff --cached
diff --git a/bak/xctest.txt b/bak/xctest.txt
new file mode 100644
index 0000000..83baae6
--- /dev/null
+++ b/bak/xctest.txt
@@ -0,0 +1 @@
+version 1
diff --git a/new.txt b/new.txt
new file mode 100644
index 0000000..eae6142
--- /dev/null
+++ b/new.txt
@@ -0,0 +1 @@
+new v1
diff --git a/xctest.txt b/xctest.txt
new file mode 100644
index 0000000..0b6ca5d
--- /dev/null
+++ b/xctest.txt
@@ -0,0 +1,2 @@
+version 1
+xiaocai v2
```

#### git commit

提交文件：

```bash
git commit
```

没有参数会进入一个注释文件可以写大段注释。

```bash
 git commit -m " messgae info"
```

`-m` 一般写短小文字较少的注释。注释建议，带上关键信息，如完成进度，fix bug

2 条命令都是提交项目版本到本地库，生成树对象和提交对象。

相当于执行：

```bash
git write-tree
git commit-tree
```

跳过使用暂存区域：

```bash
git commit -a -m "xiaocai test"
```

通过`-a` 参数，git 可以自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过`git add`步骤。

注意：使用 -a 的前提是文件状态要已经被跟踪。

#### git rm

移除文件：

从 Git 中移除文件，就必须要从已跟踪文件清单中注册删除，其实就是从暂存区注册删除，然后提交。可以使用以下命令完成：

```bash
git rm
```

该命令将把文件从暂存区注册删除，并且同时从工作目录删除对应的文件，这样文件就不会出现在未跟踪文件清单中。

需要注意的是，删除之后进行`git add` 和 `git commit`操作，对应的 Git 对象永远不会删除，暂存区删除之后，版本库里进行的是新增操作，新增的是一个没有内容的 git 对象和一个树对象。如果要找回，可以找到对应的提交对象 hash，回退即可。

如果我们先手工删除了文件，可以执行`git rm` 即可，相当于执行了`git add ./` 和 `git commit` 也可以手工执行

```bash
git add ./
git commit`
```

其实就是删除工作目录中对应的文件，再将修改添加到暂存区。`git rm`

#### git mv

文件改名：

git 文件修改文件名称命令

```bash
# 重命名操作
git mv oldfile.suffix1  newfile.suffix2
```

使用，新建一个文件然后提交：

```bash
# 新建xiaocai.txt
echo "xiaocai de wen jian" > xiaocai.txt

#git add
git commit -a -m "new a file test"

# 再执行重命名操作
git mv xiaocai.txt  xc.txt
```

`git rm` 在旧的版本中类似相当于执行了三条命令：

```bash
mv xiaocai.txt  xc.txt
git rm  xiaocai.txt
git add  xiaocai.txt
```

我的 git 版本比较新，新的版本 status 显示的是 renamed，暂时没注意过程，后续清楚了再补上。`**TODO**`

查看状态，此时是 renamed 状态，属于修改操作，

```bash
git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        renamed:    xiaocai.txt -> xc.txt
```

`**git mv file1 file2**` 其实就是将工作目录中的文件进行重命名，再将修改添加到暂存区。

#### git log

查看历史记录：

在提交很多更新之后，想回顾查看提交历史，或者回退历史版本时，使用该命令。

```bash
git log
```

没有参数会按提交时间列出所有更新，最近在上面，倒序排列。

示例：

```bash
$ git log
commit c32a601099e6ca73b910829856bc4b1ba88c014e (HEAD -> master)
Author: small-rose <small-rose@qq.com>
Date:   Mon Nov 16 19:57:12 2020 +0800

    rename xiaocai.txt to xc.txt

commit d57678e00b1dea5ce92817f5ca495c2dc852496c
Author: small-rose <small-rose@qq.com>
Date:   Mon Nov 16 19:54:07 2020 +0800

    new a file test

commit 4e84326e84545905f106975a4ce32eb520b4bc98
Author: small-rose <small-rose@qq.com>
Date:   Mon Nov 16 19:46:44 2020 +0800

    first commit
```

按下箭头翻页， 按 `q` 退出。如果要回退，利用提交对象的 hash 即可。

不方便看还可以进行格式化显示：

```bash
git log --pretty=oneline
git log --oneline
```

效果：

```bash
$ git log --pretty=oneline
c32a601099e6ca73b910829856bc4b1ba88c014e (HEAD -> master) rename xiaocai.txt to xc.txt
d57678e00b1dea5ce92817f5ca495c2dc852496c new a file test
4e84326e84545905f106975a4ce32eb520b4bc98 first commit


$ git log --oneline
c32a601 (HEAD -> master) rename xiaocai.txt to xc.txt
d57678e new a file test
4e84326 first commit
```

### 分支

> Git 分支模型高效轻量。Git 亮点技能。
>
> 分支就是一个提交对象前面的指针，每次提交完成，指针就在提交对象的前面指向最新提交
>
> 分支是用来将特性开发绝缘开来的。
>
> 在你创建仓库的时候，`master` 是“默认的”分支。在其他分支上进行开发，完成后再将它们合并到主分支上。

> GitHub 已将默认分支 master 更改为 main

![](https://files.islu.cn/article/git_branches.png#id=yjezk&originalType=binary&ratio=1&status=done&style=none)

#### 创建分支

基础命令

```bash
git branch
```

没有参数时，显示分支列表。

后面带参数时，表示创建分支命令：

```bash
git branch  dev
```

执行之后，查看日志

```bash
git log --oneline
```

新建新的分支并切换到该分支上（一步到位式）

```bash
git checkout -b  dev_test
# 执行结果
Switched to a new branch 'dev_test'
```

#### 查看分支

```bash
$ git log --oneline --decorate --graph --all
```

#### 切换分支

```bash
git checkout dev
```

切换成功后 Git 的路径会有变化

执行之后，查看日志

```bash
git log --oneline
```

在新的`dev` 分支进行操作开发

在文件夹处右键==》Git Bash Here

```bash
git add ./

git commit -m "add dev code "
```

执行后查看日志

```bash
git log --oneline

37c967e (HEAD -> dev) add dev code
```

> 注意事项
>
> 1. 每次切换分支前，当前分支一定是干净的（所有文件都是已提交状态）。所以在切换分支前使用 git status 命令验证状态。
> 2. 问题发生于在切换分支时，如果当前分支上有未暂存的修改（一般是第一次）或者有未提交的暂存（一般是第一次），分支可以切换成功，但是会对其他分支造成污染。

#### 删除分支

删除之前一定要先切换分支

```bash
git checkout master
```

切换成功后，显示 master 分支

```bash
git log --oneline
```

删除分支命令：

```bash
git branch -d name
```

#### 其他分支相关

##### 查看每个分支最后一次提交

```bash
git branch -v
```

##### 新建一个分支并且使分支指向对应的提交对象

```bash
git branch  name commitHash
```

> 示例
>
> 现在创建一个分支想回第一次提交的时候看看代码怎么写的
>
> 此时新的 first 分支语句出现了，可以切换过去看看：

```bash
# 当前是master分支
git log --oneline
c32a601 (HEAD -> master) rename blog.txt to xc.txt
d57678e new a file test
4e84326 first commit
```

```bash
git branch  first 4e84326
# 新的分支出现了
git log --oneline
c32a601 (HEAD -> master) rename xiaocai.txt to xc.txt
d57678e new a file test
4e84326 (first) first commit
```

```bash
# 切换分支
git checkout first
Switched to branch 'first'

# 现在进入了 first分支
git log --oneline
4e84326 (HEAD -> first) first commit
```

##### 查看哪些分支已经合并到当前分支

```bash
git branch  -merged
```

在这个列表中分支名字前面没有`*`号的分支通常可以使用`git branch -d` 删除掉。

##### 查看所有包含未合并工作的分支

```bash
git branch --no-merged
```

尝试使用`git branch -d` 删除在这个列表中的分支时会失败。

如果真的确定要删除分支，可以使用`git branch -D` 进行强制删除。

**分支的本质是一个提交对象，HEAD 是一个指针，它默认指向 master，切换分支时，其实就是让 HEAD 指向不同的分支。每次有新的提交时，HEAD 都会带着当前指向的分支一起往前移动。**

#### 撤销重置

**撤销命令**

```bash
git commit -amend
```

该命令将暂存区的文件提起，如果上次提交以来你还未做任何修改，在你提交后马上执行此命令，那么快照会保持不变，而你所修改的只是提交信息。

如果提交后发现忘记了暂存某些需要的修改，可以像下面这样操作：

```bash
git commit -m 'some desc'
git add forgeotten_file
git commit -amend
```

最终只会有一个提交，第二次提交将代替第一次提交的结果。

**重置命令**

```
git reset HEAD  文件名
```

#### 配置别名

Git 没有自动推断命令功能，有些命令比较长，不想每次输入完整的命令，可以通过`git config`文件来轻松为每个命令设置一个别名。

```
git config --global alias.co  checkout
git config --global alias.br  branch
git config --global alias.cm  commit
git config --global alias.st  status
```

如果需要执行`git commit` 只需要输入 `git cm` 即可。

对于复杂命令，比如查看完整的分支图的命令：

```bash
git log --oneline --decorate --graph --all
```

执行结果：

```bash
git log --oneline --decorate --graph --all
* 37c967e (dev) add dev code
* c32a601 (master) rename blog.txt to i.txt
* d57678e new a file test
* 4e84326 (HEAD -> first) first commit
```

将该命令配置别名时需要带上双引号：

```bash
git config --_global alias.blog  "log --oneline --decorate --graph --all"
```

### Git 管理仓库(以 Github 为例)

#### 创建新的仓库然后提交

```bash
echo "# 仓库名" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/用户名/仓库名.git
git push -u origin main
```

#### 提交一个已经存在的仓库

```bash
git remote add origin https://github.com/用户名/仓库名.git
git branch -M main
git push -u origin main
```

#### Git 的免密使用

##### 客户端生成密钥

```bash
ssh-keygen -t rsa -C "这里换上你的邮箱"
```

然后会出现询问，大概意思如下：

```
1. 确认秘钥的保存路径（如果不需要改路径则直接回车）；
2. 如果上一步置顶的保存路径下已经有秘钥文件，则需要确认是否覆盖（如果之前的秘钥不再需要则直接回车覆盖，如需要则手动拷贝到其他目录后再覆盖）；
3. 创建密码（如果不需要密码则直接回车）；
4. 确认密码；
```

要免密登录请输密码的时候回车即可。根据提示找到密钥所在文件：

```
id_rsa  #私钥
id_rsa.pub  #公钥
```

> Github 配置 SSH 公钥登录 git 账户，Setting，SSH and GPG keys, New ssh key 把 id_rsa.pub 的内容粘贴到 key 的文本域，点击 Add SSH key 完成。后续的客户端 git 操作就不要密码了。
>
> 然后回到 Git 的命令行界面，测试一下是否与 Github 连接成功。输入下面的命令行：
>
> 点击回车，然后会出现一个询问内容，输入 `yes`，回车，会出现一段内容，`Hi ! You've successfully authenticated, but GitHub doesnot provide shell access.`。 说明连接成功。此处这个 `` 应该是你 Github 的用户名。

```shell
ssh -T git@github.com
```

##### 服务器配置 SSH 免密

注意：这里的 Git 服务器可以是云服务器或者自己的私服务器。本次操作环境是`Centos 7`。

###### 1. 客户端生成密钥

> 注意：同上，如果已经配置过`Github`的 ssh 免密上面已经有了可以不用重复生成，可以直接跳到第二步。

###### 2. 服务端导入客户端公钥

在/home/git 下已经创建.ssh 目录，然后创建 authorized_keys 文件，并将客户端生成的公钥导入进去。

```bash
cd /home/git/
mkdir .ssh
chmod 755 .ssh
touch .ssh/authorized_keys
chmod 644 .ssh/authorized_keys
```

将 `id_rsa.pub` 文件的内容写入`authorized_keys`

###### 3. 服务端`SSH`开启`RSA`认证

如果没有安装 SSH 服务，请先安装 SSH 服务。

```bash
vim /etc/ssh/sshd_config
```

其中三个地方的设置要确认如下：

```bash
RSAAuthentication yes
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
```

git 用户不允许登录 shell

```bash
vim /etc/passwd
```

将

```bash
git:x:502:502::/home/git:/bin/bash
```

改为

```bash
git:x:502:502::/home/git:/usr/local/git/bin/git-shell
```
