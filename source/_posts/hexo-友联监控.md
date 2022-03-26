---
title: Hexo-友联监控
author: 闲花
img: "https://files.islu.cn/article/Uptimerobot.jpg"
top: false
toc: true
mathjax: false
categories: Hexo
tags:
  - Hexo
  - Hexo添加友链监控页面
keywords: "Hexo友链监控,hexo-theme-matery魔改,matery友链监控,Uptimerobot检测友链,Uptimerobot"
summary: Hexo添加友链监控页面
abbrlink: 38263
date: 2021-03-14 16:53:31
update: 2021-03-14 16:53:31
---

# 添加友链监测页面

## 效果

演示网址：[传送门](https://blog.islu.cn/supervise)

图标皆来自 [Font Awesome 中文网](https://www.fontawesome.com.cn/) 如有更好推荐，欢迎留言

有免费版也有付费版，以下只针对免费版。

## 简介

- Uptime Robot 是一个网站监控服务，每 5 分钟检查一次你设定的网站 或服务器，最多可以免费检查 50 个网站。
- 如果你的网站或者服务器宕机时，Uptime Robot 会通过邮件提醒你。
- 有多种监控方式、支持自定义域名

## 使用

1.  访问官网，注册账号 ： [传送门](https://uptimerobot.com/)
2.  注册账号
3.  添加监视器。点击`add new monitor`
    勾选“**Alert Contacts To Notify**“会有邮箱提醒。
    若想添加本博客同款，至此请继续阅读 Matery 模板

    > 有四种监控方式，分别为**Http(s)\*\_、\_Ping**、**Port**、**Keyword**，在这里我选择 Http(s)来监控我的网站，选择**Ping**来监控我的服务器。**Port**一般用于 VPS 监控。

4.  打开公共状态页。
    点击上方[**My Settings**](https://uptimerobot.com/dashboard#mySettings)，选择右下角**Add Public Status Pages**。填写**名称**，以及**Logo**以及**自定义域名**和是否设置密码。
    自定义域名我是用的 **bkjw.rogn.top**，还得去域名控制台添加一下解析信息，记录类型为**CNAME**，记录值为**stats.uptimerobot.com**
    > 虽然我没有用它自动生成的页面，但不排除会有需要的

## Matery 模板

### 新建页面

```shell
hexo new _page supervise
```

修改`supervise`目录下的`index.md`的格式

```yml
---
title: supervise
type: "supervise"
layout: "supervise"
date: 2020-12-07 13:04:17
---
```

### 在主题配置文件中添加导航

```yml
友链监测:
  url: /supervise
  icon: fa fa-desktop
```

### 添加 supervise.ejs

在 `matery/layout` 下新建 `supervise.ejs`

```ejs
<style>
table,td,th{border:0}.card-supervise{padding:24px;border-radius:0 0 2px 2px}.wname{font-size:16px}.card-panel{padding:0;color:#fff}.supervise_details{margin:38px 0 15px -4px;font-size:1.6rem;font-weight:700;line-height:1.7rem}.panel-heading{font-size:20px}.teal{margin-right:5px}.check>tbody>tr>td{padding-top:11px;padding-bottom:11px}.check th{text-align:center}.check .center{text-align:center;vertical-align:middle}.check .sertitle{vertical-align:middle}.status-success{color:#5cb85c}.status-warning{color:#f0ad4e}.status-danger{color:#d9534f}#server-container{border-bottom:1px solid #ddd}.barl>td{border-top:none!important;padding:0!important}.barl .progress{margin:0;border-radius:0;height:8px;box-shadow:none}.barl .progress .progress-bar{box-shadow:none;opacity:.7}.barl .progress .progress-bar:hover{opacity:1}.barl .progress .progress-bar-default{background-color:#efefef}.progress .tooltip .tooltip-inner .ttime{color:#a3a3a3;font-size:11px}.credit{font-size:12px;color:#bbb}.credit a{color:#999}.credit .pipe{padding-left:6px;padding-right:6px;color:#ddd}

</style>
<%- partial('_partial/bg-cover') %>
    <main class="content" style="min-height: 131px;">
        <div class="container chip-container">
            <div class="card">
                <div class="card-content">
                    <div class="tag-title center-align"><i class="fa fa-desktop"></i>&nbsp;&nbsp;友链状态监测</div>
                    <div class="supervise_details">本页面是友情链接状态监控，展示了全部链接的当前运行状态。</div>
                    <hr>
                    <div class="panel panel-info">
                        <div class="panel-heading">各友情链接当前状态</div>
                        <div class="panel-body">
                            <div id="panel-heading" class="alert alert-warning hide" role="alert">
                                <b>当前状态：</b>部分友链发生异常，我们将尽快修复。
                            </div>
                            <div id="stattip-ok" class="alert alert-success hide" role="alert">
                                <b>当前状态：</b>所有友链正常运行中，没有发现异常。
                            </div>
                            <div id="stattip-load" class="alert alert-info" role="alert">
                                <b>当前状态：</b>正在检测运行状态，请稍候..
                            </div>
                            <div class="table-responsive">
                                <table class="table table-hover check">
                                    <thead>
                                    <tr id="server-title">
                                    </tr>
                                    </thead>
                                    <tbody id="server-container"></tbody>
                                </table>
                            </div>
                        </div>
                        <div class="alert alert-info" style="text-align:center;margin-bottom:0">
                            距离下次监测刷新时间:
                            <span class="fa fa-refresh"></span> <span id="last-update"></span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </main>
    <script type="template/mustache" id="server-template">
        <tr class="{{alert}}">
            <td rowspan="2" class="sertitle">
                <span class="card-panel {{label}}"><span class="fa fa-{{statusicon}}"style="padding-left: 2px;"></span> {{statustxt}}</span>
                <span class="wname">{{friendlyname}}</span>
            </td>
            {{#charts}}
            <td class="center">
                <span class="status-{{uptype}} set-tooltip" data-toggle="tooltip" data-placement="top" title="{{uptime}}"><span class="fa fa-{{upsign}}"></span></span>
            </td>
            {{/charts}}
        </tr>
        <tr class="{{alert}} barl">
            <td colspan="8" class="barls">
                <div class="progress">
                    {{#progress}}
                    <div class="progress-bar progress-bar-{{types}} set-tooltip" style="width: {{len}}%" data-toggle="tooltip" data-placement="top" title="{{stattip}}"></div>
                    {{/progress}}
                </div>
            </td>
        </tr>
    </script>
    <script>function date(n,t){function e(n,t){return(n+="").length<t?new Array(++t-n.length).join("0")+n:n}var u=t?new Date(1e3*t):new Date,r=["Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"],o={1:"st",2:"nd",3:"rd",21:"st",22:"nd",23:"rd",31:"st"},a=["","January","February","March","April","May","June","July","August","September","October","November","December"],i={d:function(){return e(i.j(),2)},D:function(){return i.l().substr(0,3)},j:function(){return u.getDate()},l:function(){return r[i.w()]},N:function(){return i.w()+1},S:function(){return o[i.j()]?o[i.j()]:"th"},w:function(){return u.getDay()},z:function(){return(u-new Date(u.getFullYear()+"/1/1"))/864e5>>0},W:function(){var n,t=i.z(),e=364+i.L()-t,r=(new Date(u.getFullYear()+"/1/1").getDay()||7)-1;return e<=2&&(u.getDay()||7)-1<=2-e?1:t<=2&&4<=r&&6-r<=t?(n=new Date(u.getFullYear()-1+"/12/31"),date("W",Math.round(n.getTime()/1e3))):1+(r<=3?(t+r)/7:(t-(7-r))/7)>>0},F:function(){return a[i.n()]},m:function(){return e(i.n(),2)},M:function(){return i.F().substr(0,3)},n:function(){return u.getMonth()+1},t:function(){var n;return 2==(n=u.getMonth()+1)?28+i.L():1&n&&n<8||!(1&n)&&7<n?31:30},L:function(){var n=i.Y();return 3&n||!(n%100)&&n%400?0:1},Y:function(){return u.getFullYear()},y:function(){return(u.getFullYear()+"").slice(2)},a:function(){return 11<u.getHours()?"pm":"am"},A:function(){return i.a().toUpperCase()},B:function(){var n=60*(u.getTimezoneOffset()+60),t=3600*u.getHours()+60*u.getMinutes()+u.getSeconds()+n,e=Math.floor(t/86.4);return 1e3<e&&(e-=1e3),e<0&&(e+=1e3),1==String(e).length&&(e="00"+e),2==String(e).length&&(e="0"+e),e},g:function(){return u.getHours()%12||12},G:function(){return u.getHours()},h:function(){return e(i.g(),2)},H:function(){return e(u.getHours(),2)},i:function(){return e(u.getMinutes(),2)},s:function(){return e(u.getSeconds(),2)},O:function(){var n=e(Math.abs(u.getTimezoneOffset()/60*100),4);return n=0<u.getTimezoneOffset()?"-"+n:"+"+n},P:function(){var n=i.O();return n.substr(0,3)+":"+n.substr(3,2)},c:function(){return i.Y()+"-"+i.m()+"-"+i.d()+"T"+i.h()+":"+i.i()+":"+i.s()+i.P()},U:function(){return Math.round(u.getTime()/1e3)}};return n.replace(/[\\]?([a-zA-Z])/g,function(n,t){return ret=n==t&&i[t]?i[t]():t,ret})}</script>
    <script src="<%- theme.jsDelivr.url %><%- url_for('/js/mustache.min.js') %>"></script>
    <script src="<%- theme.jsDelivr.url %><%- url_for('/js/uptimerobot.js') %>"></script>
    <script src="<%- theme.jsDelivr.url %><%- url_for('/js/upscuits.js') %>"></script>
    <script type="text/javascript">jQuery(document).ready(myApp.dashboard.init)</script>
```

### 引入 JS 文件

1.  下载 JS 文件
    [mustache.min.js](https://cdn.jsdelivr.net/gh/ialoe/ialoe.github.io@master/js/mustache.min.js)
    [upscuits.js](https://cdn.jsdelivr.net/gh/ialoe/ialoe.github.io@master/js/upscuits.js)
2.  新建 JS 文件
    配置 JS 文件中 `uptimerobot.js` 内容

```javascript
var __apiKeys = [
  "xxxxxxxxxx", // API 1
  "xxxxxxxxxx", // API 2
];
//https://uptimerobot.com/ 设置要监控的域名或者ip 获取到key

// refresh interval (in seconds 暂定五分钟)
var __refresh = 300;
```

### 获取 API

将 API 复制到`uptimerobot.js` 中即可
