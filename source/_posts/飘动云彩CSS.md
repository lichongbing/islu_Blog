---
title: 飘动云彩背景
author: 闲花
img: "https://files.islu.cn/article/clouds_CSS.png"
top: false
toc: true
mathjax: false
essay: false
categories: Other
tags:
  - 飘动云彩背景(白昼交替)
keywords: "HTML5,CSS3,飘动云彩"
abbrlink: 6643
date: 2021-10-04 16:35:41
update: 2021-10-04 16:35:41
summary: 没文章水了，把一个局部样式拿来水一下
---

# 飘动云彩背景

## 效果

![](https://files.islu.cn/article/clouds_CSS.png#id=xd05B&originHeight=497&originWidth=1602&originalType=binary&ratio=1&status=done&style=none)

> 假装此处云彩会飘动和白昼交换

## 源码

```html
<style>
.sky .clouds_one {
    background: url("https://files.islu.cn/detail/cloud_one.png");
    position: absolute;
    left: 0;
    top: 0;
    height: 100%;
    width: 300%;
    -webkit-animation: cloud_one 50s linear infinite;
    -moz-animation: cloud_one 50s linear infinite;
    -o-animation: cloud_one 50s linear infinite;
    animation: cloud_one 50s linear infinite;
    -webkit-transform: translate3d(0, 0, 0);
    -ms-transform: translate3d(0, 0, 0);
    -o-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
}

.sky .clouds_two {
    background: url("https://files.islu.cn/detail/cloud_two.png");
    position: absolute;
    left: 0;
    top: 0;
    height: 100%;
    width: 300%;
    -webkit-animation: cloud_two 75s linear infinite;
    -moz-animation: cloud_two 75s linear infinite;
    -o-animation: cloud_two 75s linear infinite;
    animation: cloud_two 75s linear infinite;
    -webkit-transform: translate3d(0, 0, 0);
    -ms-transform: translate3d(0, 0, 0);
    -o-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
}

.sky .clouds_three {
    background: url("https://files.islu.cn/detail/cloud_three.png");
    position: absolute;
    left: 0;
    top: 0;
    height: 100%;
    width: 300%;
    -webkit-animation: cloud_three 100s linear infinite;
    -moz-animation: cloud_three 100s linear infinite;
    -o-animation: cloud_three 100s linear infinite;
    animation: cloud_three 100s linear infinite;
    -webkit-transform: translate3d(0, 0, 0);
    -ms-transform: translate3d(0, 0, 0);
    -o-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
}

@-webkit-keyframes sky_background {
    0% {
        background: #007fd5;
        color: #007fd5
    }
    50% {
        background: #000;
        color: #a3d9ff
    }
    100% {
        background: #007fd5;
        color: #007fd5
    }
}
@-moz-keyframes sky_background {
    0% {
        background: #007fd5;
        color: #007fd5
    }
    50% {
        background: #000;
        color: #a3d9ff
    }
    100% {
        background: #007fd5;
        color: #007fd5
    }
}
@keyframes sky_background {
    0% {
        background: #007fd5;
        color: #007fd5
    }
    50% {
        background: #000;
        color: #a3d9ff
    }
    100% {
        background: #007fd5;
        color: #007fd5
    }
}

@-webkit-keyframes cloud_one {
    0% {
        left: 0
    }
    100% {
        left: -200%
    }
}
@-moz-keyframes cloud_one {
    0% {
        left: 0
    }
    100% {
        left: -200%
    }
}
@keyframes cloud_one {
    0% {
        left: 0
    }
    100% {
        left: -200%
    }
}

@-webkit-keyframes cloud_two {
    0% {
        left: 0
    }
    100% {
        left: -200%
    }
}
@-moz-keyframes cloud_two {
    0% {
        left: 0
    }
    100% {
        left: -200%
    }
}
@keyframes cloud_two {
    0% {
        left: 0
    }
    100% {
        left: -200%
    }
}

@-webkit-keyframes cloud_three {
    0% {
        left: 0
    }
    100% {
        left: -200%
    }
}
@-moz-keyframes cloud_three {
    0% {
        left: 0
    }
    100% {
        left: -200%
    }
}
@keyframes cloud_three {
    0% {
        left: 0
    }
    100% {
        left: -200%
    }
}
</style>
<a href="/contact" rel="noopener noreferrer" class="sky">

    <div class="clouds_one"></div>
    <div class="clouds_two"></div>
    <div class="clouds_three"></div>

​    <img src="https://files.islu.cn/detail/friends.png" style="max-width: 100%" alt="交个朋友叭" title="交个朋友叭">
</a>
```
