---
title: Matery添加暗色模式
author: 闲花
img: "https://files.islu.cn/article/Dark+Light"
top: true
cover: false
coverImg: /images/1.jpg
toc: true
mathjax: false
categories: Hexo
tags:
  - blog
  - Hexo
keywords: "Hexo,islu,Matery主题的暗色模式"
summary: Matery主题的暗色模式
abbrlink: 21369
date: 2021-08-11 09:28:31
update: 2021-08-11 09:28:31
---

## 制作深色模式按钮

### 添加按钮

在主题的`layout.ejs`文件中找到 body 标签的开始标签在后面加上这些 js 和 html 代码，这里我放的位置为：`/layout/_partial/back-top.ejs`

```html
<!-- 回到顶部按钮 -->
<div id="backTop" class="top-scroll">
    <a class="btn-floating btn-large waves-effect waves-light" href="#!">
        <i class="fas fa-arrow-up"></i>
    </a>
</div>
```

改为

```html
<!-- 回到顶部按钮 -->
<div id="backTop" class="top-scroll">
    <a class="btn-floating btn-large waves-effect waves-light" href="#!">
        <i class="fas fa-arrow-up"></i>
    </a>
</div>
<a onclick="switchNightMode()" id="sma" title="模式切换">
    <i class="fa fa-moon-o" id="nightMode" aria-hidden="true"></i>
</a>
```

### 按钮的 css 样式

```css
/* 深色模式按钮设置 */
#sma {
  background: #000;
  width: 38px;
  height: 38px;
  display: block;
  position: fixed;
  border-radius: 50%;
  right: 15px;
  bottom: 170px;
  padding-top: 15px;
  margin-bottom: 0;
  z-index: 998;
  cursor: pointer;
}

#sma .fa-moon-o {
  position: absolute;
  right: 8px;
  bottom: 8px;
  font-size: 1.48rem !important;
}
#sma .fa-lightbulb-o {
  position: absolute;
  right: 13px;
  bottom: 8px;
  font-size: 1.5rem !important;
}

.fa-moon-o:before {
  content: "\f186";
}
.fa-comments:before {
  content: "\f086";
}
```

### 按钮的 js 代码

放在独立的 js 文件里即可，这里我放在`/souce/js/matery.js`里面

```javascript
/* 深色模式按钮设置 */
if (localStorage.getItem("dark") === "1") {
  document.body.classList.add("dark");
} else {
  /*定时开启暗色模式<默认晚22点至早6点默认开启>*/
  if (new Date().getHours() >= 22 || new Date().getHours() < 6) {
    document.body.classList.add("dark");
    $("#nightMode").removeClass("fa-moon-o").addClass("fa-lightbulb");
  } else {
    if (matchMedia("(prefers-color-scheme: dark)").matches) {
      document.body.classList.add("dark");
    }
  }
}

/*提醒开启功能*/
setTimeout(function () {
  if (
    (new Date().getHours() >= 19 || new Date().getHours() < 7) &&
    !$("body").hasClass("DarkMode")
  ) {
    let toastHTML =
      '<span style="color:#97b8b2;border-radius: 10px;>' +
      '<i class="fa fa-bell" aria-hidden="true"></i>晚上使用深色模式阅读更好哦。(ﾟ▽ﾟ)/</span>';
    M.toast({ html: toastHTML });
  }
}, 2200);

/* 深色模式设置*/
function switchNightMode() {
  var body = document.body;
  if (body.classList.contains("dark")) {
    document.body.classList.remove("dark");
    localStorage.setItem("dark", "0");
    $("#nightMode").removeClass("fa-lightbulb").addClass("fa-moon-o");
    return;
  } else {
    document.body.classList.add("dark");
    localStorage.setItem("dark", "1");
    $("#nightMode").removeClass("fa-moon-o").addClass("fa-lightbulb");
    return;
  }
}
```

## 引入 CSS 暗色文件

创建 css 文件并引入

```css
/*暗色模式按钮样式*/
#sma {
  box-shadow: #aaa 2px 5px 10px;
  background: #000;
  width: 38px;
  height: 38px;
  display: block;
  position: fixed;
  border-radius: 50%;
  right: 15px;
  bottom: 100px;
  padding-top: 15px;
  margin-bottom: 0;
  z-index: 998;
  cursor: pointer;
}

#sma .fa-moon-o {
  position: absolute;
  right: 8px;
  bottom: 8px;
  font-size: 1.48rem !important;
}

#sma .fa-lightbulb {
  position: absolute;
  right: 11px;
  bottom: 8px;
  font-size: 1.5rem !important;
}

.fa-moon-o:before {
  content: "\f186";
}

.fa-comments:before {
  content: "\f086";
}
/* 背景颜色变灰色 */
.dark tbody,
body.dark #artDetail .post-info .post-date,
body.dark #info_user_pool .moments_chart,
body.dark .bg-cover .post-title,
body.dark .biaotis span,
body.dark .card .card-content p,
body.dark .card .card-image .card-title,
body.dark .card .toc-title,
body.dark .card-content .categories-title,
body.dark .card-content .de,
body.dark .category-content a,
body.dark .chip-container .tag-title,
body.dark .fa-lightbulb:before,
body.dark .fa-moon-o:before,
body.dark .fab,
body.dark .fas,
body.dark .friends-container .tag-title,
body.dark .frind-ship .title h1,
body.dark .moments-item-info .moments-item-time,
body.dark .moments_load_button,
body.dark .notice,
body.dark .panel-info,
body.dark .post-info .info-break-policy,
body.dark .publish-info .post-category,
body.dark .publish-info .publish-date,
body.dark .row .text,
body.dark .statis .name,
body.dark .supervise_details,
body.dark .title,
body.dark .v[data-class="v"] .vcount,
body.dark .v[data-class="v"] .vcount .vnum,
body.dark .valine-card .comment_headling,
body.dark a body.dark table,
body.dark article .article-content .summary,
body.dark article .article-tags .chip,
body.dark div.jqcloud a,
body.dark footer .copy-right,
body.dark footer a,
body.dark h1,
body.dark h2,
body.dark h3,
body.dark h4,
body.dark h5,
body.dark h6,
body.dark header .side-nav .menu-list a,
body.dark header .side-nav .mobile-head .logo-desc,
body.dark header .side-nav .mobile-head .logo-name,
body.dark li,
body.dark p,
body.dark pre code {
  color: rgba(255, 255, 255, 0.85); /*.85为透明度，可依据需求修改*/
}
/* 背景颜色变黑色 */
body.dark,
body.dark #rewardModal .modal-content,
body.dark .archive-container,
body.dark .modal,
body.dark .v[data-class="v"] .vcount,
body.dark header .side-nav,
body.dark header .side-nav .menu-list .m-nav-show {
  background-color: #12121c;
}
/*首页文章滑动卡片文字*/
body.dark #thisTime,
body.dark .card-image-V .box-content .title {
  color: #8a2be2;
}
/*音乐播放器*/
body.dark .aplayer {
  background: #2f3742 !important;
}
/*图片滤镜*/
body.dark img,
body.dark strong {
  filter: brightness(0.7);
}
/*统计图表暗色样式*/
body.dark #categories-chart,
body.dark #category-radar,
body.dark #post-calendar,
body.dark #posts-chart,
body.dark #tags-chart {
  filter: invert(1);
}

/*toc目录滤镜*/
body.dark .skillbar .skill-bar-percent {
  color: #000;
}

/*加载动画（吃豆豆）文字颜色*/
body.dark .loading-text {
  color: #000;
}
/*一些细节背景*/
body.dark .block-with-text:after,
body.dark .card,
body.dark .collapsible-header,
body.dark .wxgzh,
body.dark table tr:nth-child(2n),
body.dark thead {
  background-color: #282c34;
}

/*about页面细节*/
body.dark .profile .author .title {
  color: #faebd7;
}
body.dark .my-projects .info .info-title a {
  color: tomato;
}

/*外挂标签*/
.swbk .label {
  color: currentColor;
}
```

## 如何修改部分细节冲突

此暗黑模式原理为在 `<body>` 标签添加 `class="dark"`

添加暗色模式时可依据 `body.dark 类名` 用 CSS 选择器来给含有`dark` 的 `<body>` 下的类添加属性

```css
/*给暗黑模式下的.test添加字体颜色变红样式*/
body.dark .test {
  color: red;
}
```

如若冲突可考虑 `!important` 来添加"权重"

```css
body.dark .test {
  color: red !important;
}
```
