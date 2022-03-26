---
title: Hexo-更文自动打开编辑器
author: 闲花
img: "https://files.islu.cn/article/TyporaForPost.jfif"
top: false
toc: true
mathjax: false
categories: Hexo
tags:
  - Typora
  - Hexo
  - 写博文自动打开Typora编辑器
keywords: "Hexo,Tpyora,hexo文章,自动打开编辑器,自动生成文章格式,Tpyora使用"
summary: 写博文自动打开Typora编辑器
abbrlink: 10895
date: 2021-03-14 17:02:28
update: 2021-03-14 17:02:28
---

# 更新博客文章自动打开编辑器

## 在博客文件根目录`scripts`中新建`new.js`文件

```javascript
var spawn = require("child_process").exec;

// Hexo 2.x 用户复制这段
// hexo.on('new', function(path){
//   spawn('start  "markdown编辑器绝对路径.exe" ' + path);
// });

// Hexo 3 用户复制这段
hexo.on("new", function (data) {
  spawn('start  "D:TyporaTypora.exe" ' + data.path);
});
```

D:\Typora\Typora.exe 为编辑器绝对路径

### 运行命令`hexo cl&&hexo g&&hexo d`后即可

### 新建文章命令`hexo new "文章名"`

## 可选项：

### 更改`scaffolds`文件夹中`post.md`内容

### 可将默认生成文件头部格式更改为

```markdown
---
title: { { title } }
date: { { date } }
update: { { date } }
author: 卢慧军 # 文章作者
img: /source/images/xxx.jpg # 文章特征图
top: true # 推荐文章（文章是否置顶），如果 top 值为 true，则会作为首页推荐文章
cover: false # 表示该文章是否需要加入到首页轮播封面中
coverImg: /images/1.jpg # 表示该文章在首页轮播封面需要显示的图片路径，如果没有，则默认使用文章的特色图片
password: # 文章阅读密码，如果要对文章设置阅读验证密码的话，就可以设置 password 的值，该值必须是用 SHA256(https://www.jsons.cn/sha/) 加密后的密码，防止被他人识破
toc: false # 是否开启 TOC(目录)，可以针对某篇文章单独关闭 TOC 的功能。前提是在主题的 config.yml 中激活了 toc 选项
mathjax: false # 是否开启数学公式支持 ，本文章是否开启 mathjax
summary: # 这是你自定义的文章摘要内容，如果这个属性有值，文章卡片摘要就显示这段文字，否则程序会自动截取文章的部分内容作为摘要
categories: 工具 # 文章分类，本主题的分类表示宏观上大的分类，只建议一篇文章一个分类
tags: # 文章标签，一篇文章可以多个标签
  - blog
  - hexo
---
```
