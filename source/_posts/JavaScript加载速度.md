---
title: JavaScript加载速度
author: 闲花
img: "https://files.islu.cn/article/jsUpdate.jpg"
top: false
toc: true
mathjax: false
categories: JavaScript
tags:
  - JavaScript
  - JS加载速度
keywords: "JS,JavaScript加载速度,解决JS加载速度慢,JS加速"
summary: 解决JS加载速度慢的问题
abbrlink: 55121
date: 2021-03-15 14:20:04
update: 2021-03-15 14:20:04
---

# 解决 JS 加载速度慢的问题

## **传统形式加载 js 文件**

```javascript
<script type="text/javascript" src="js调用地址"></script>
```

## **高速加载 js 文件**

```javascript
<script type="text/javascript">
 /* 请不要删除这段代码，因为这段代码起到了加速JS加载作用 */
 document.write("<scr"+"ipt src=\"你的js调用地址"></sc"+"ript>");
</script>
```
