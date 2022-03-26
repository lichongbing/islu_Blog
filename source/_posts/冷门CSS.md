---
title: 冷门CSS样式
author: 闲花
img: "https://files.islu.cn/article/CodeCSS"
top: false
toc: true
mathjax: false
categories: CSS
tags:
  - CSS
  - 冷门CSS样式
keywords: "冷门但却很实用的css样式总汇,css样式,css"
summary: 冷门但却很实用的css样式总汇
abbrlink: 41083
date: 2021-03-15 14:14:04
update: 2021-03-15 14:14:04
---

# 冷门但却很实用的 css 样式总汇

## **::-Webkit-Input-Placeholder**

input 的 H5 placeholder 属性，很好用，可以直接定义输入文本框里面的内容，唯一的缺点就是不能更改默认显示字体的颜色，不过我们可以直接利用::input-placeholder 这个属性来设置字体颜色。

```css
::-webkit-input-placeholder {
  /* Chrome/Opera/Safari */
  color: pink;
}
::-moz-placeholder {
  /* Firefox 19+ */
  color: pink;
}
:-ms-input-placeholder {
  /* IE 10+ */
  color: pink;
}
:-moz-placeholder {
  /* Firefox 18- */
  color: pink;
}
```

## **使用 clearfix 清楚浮动，解决父类高度崩塌**

```css
.clearfix {
  zoom: 1;
}
.clearfix:after {
  visibility: hidden;
  display: block;
  font-size: 0;
  content: " "; /* 内容为空 */
  clear: both;
  height: 0;
}
```

## **p::selection 选中文本后的背景色**

```css
p::selection {
  background: rgb(188, 188, 188);
  color: #ffffff;
}
```

## **calc function, 计算属性值**

```css
div {
  width: calc(100% - 100px);
}
```

## **outline**属性值

不知道大家有没有一个困扰，就是在写 input 的时候，点击的时候总会有一个很丑的蓝色描边，但是找代码还找不到。这个其实很简单，用 outline 这个标签就可以很简单的解决掉这个烦人的问题。

```css
div {
  outline: none; //移动浏览器默认的状态线
  // outline: 5px dotted red; 也可以设置样式
}
```

## **Webkit-Playsinline**

支持 vedio 视频在手机页面内部播放，不用全屏。

```css
<video id="myvideo" src="test.mp4" webkit-playsinline="true"></video>
```

## **Css 实现文本的各种换行状态**

```css
//不换行
white-space: nowrap;
//自动换行
word-wrap: break-word;
word-break: normal;
//强制换行
word-break: break-all;
```

## **-webkit-line-clamp**

可以把 块容器 中的内容限制为指定的行数。并且在超过行数后，在最后一行显示”…” 这是正常的展示

```css
display: -webkit-box; /*值必须为-webkit-box或者-webkit-inline-box*/
-webkit-box-orient: vertical; /*值必须为vertical*/
-webkit-line-clamp: 2; /*值为数字，表示一共显示几行*/
overflow: hidden;
```

## **caret-color**

用来定义插入光标（caret）的颜色，这里说的插入光标，就是那个在网页的可编辑器区域内，用来指示用户的输入具体会插入到哪里的那个一闪一闪的形似竖杠 | 的东西。

```css
caret-color: red;
```
