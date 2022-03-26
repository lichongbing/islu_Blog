---
title: Hexo-导航页
author: 闲花
img: "https://files.islu.cn/article/hexo_navigate.jfif"
top: false
toc: true
mathjax: false
categories: Hexo
tags:
  - Hexo
  - Hexo添加网址导航页
keywords: "Hexo,matery导航页,hexo-theme-matery常用网页,matery美化,hexo魔改"
summary: Hexo添加网址导航页
abbrlink: 29540
date: 2021-03-14 16:40:44
update: 2021-03-14 16:40:44
---

# Hexo 添加导航页

## 效果

[效果演示](https://blog.islu.cn/navigate)

## 新建页面

首先新建页面，执行下面的命令

`hexo new page navigate`

修改`navigate`目录下的`index.md`的格式

```markdown
---
title: 导航
date: 2020-10-18 15:19:14
type: "navigate"
layout: "navigate"
---
```

## 在主题配置文件中添加导航

```yml
# main menu navigation url and icon
# 配置菜单导航的名称、路径和图标icon.
menu:
  Index:
    url: /
    icon: fas fa-home
  标签:
    url: /tags
    icon: fas fa-tags
  时光轴:
    url: /archives
    icon: fas fa-hourglass-half
  留言板:
    url: /contact
    icon: fas fa-comments
  关于:
    url: /about
    icon: fas fa-user-circle
  友情链接:
    url: /friends
    icon: fas fa-address-book
  Select:
    icon: fas fa-life-ring
    children:
      - name: 导航
        url: /navigate
        icon: fas fa-location-arrow
      - name: 相册
        url: /galleries
        icon: fas fa-image
```

## 添加 navigate 页面

在 `matery/layout` 下新建 `navigate.ejs`

```ejs
<style>
dd,dl,dt,form,h1,h2,h3,h4,h5,h6,li,p,ul{margin:0;padding:0;font-size:14px;font-weight:400}img{border-style:none}li{list-style:none;float:left}a{text-decoration:none}.card{background-color:rgba(25,240,229,0);width:96%;margin-left:2%}.baidu{float:left;margin-left:100px}.baidu form{position:relative}.Select-box ul{height:40px;position:absolute;left:-1px;top:0;z-index:9999;background:#fff;border:1px solid #ccc;border-top:none;overflow:hidden}.Select-box li{width:60px;line-height:40px;font-size:14px;color:#484848;border:0;cursor:pointer}.Select-box li:hover{background:#3385ff;color:#fff}.Select-box .this_s{color:#317ef3}.Select-box .this_s:hover{background:#fff;color:#317ef3}.qingkong{position:absolute;right:120px;top:12px;width:18px;height:18px;background:rgba(0,0,0,.1);border-radius:18px;line-height:16px;color:#666;cursor:pointer;text-align:center;font-size:14px;display:none}.qingkong:hover{background:rgba(0,0,0,.2)}.qingkong:active{background:rgba(0,0,0,.3)}.baidu-2{width:100%;height:110px;margin:0 auto;background:0 0;padding-top:50px}.baidu-2 form{width:520px;margin:0 auto}.baidu-2 input{padding:13px 8px;opacity:.9;font-size:15px}#Select-2{float:left}.Select-box-2{text-align:center;float:left;position:relative}.Select-box-2 ul{height:46px;position:absolute;left:0;top:1px;z-index:9999;background:rgba(255,255,255,.9);border:1px solid #ccc;border-top:none;overflow:hidden}.Select-box-2 li{width:60px;line-height:46px;font-size:15px;color:#484848;border:0;cursor:pointer}.Select-box-2 li:hover{background:#3385ff;color:#fff}.Select-box-2 .this_s{color:#317ef3}.Select-box-2 .this_s:hover{background:0 0;color:#317ef3}#kw-2{width:335px;outline:0;border:1px solid #ccc;background:rgba(255,255,255,.2);color:#000;padding-left:70px;font-weight:700}#su-2{width:90px;background:#00f;border:none;border-top:#3385ff 1px solid;border-bottom:1px solid #2d78f4;color:#fff;cursor:pointer;outline:0}#su-2:hover{background:#00f;border-bottom:1px solid #00f}#su-2:active{background:#00f;box-shadow:inset 1px 1px 3px #00f;-webkit-box-shadow:inset 1px 1px 3px #00f}.jj-list-tit{font-size:16px;line-height:25px;color:#fff;width:100%;padding-left:38.5%}.jj-list-con{overflow:hidden;margin:0 auto}.jj-list-con li{width:31.333%;margin:1%}.link-3{display:block;background:rgba(0,0,0,.35);color:#fff;font-size:13px;text-align:center;line-height:35px;padding:4px 0;border-radius:2px;transition:all .2s}.link-3:hover{background:rgba(0,0,0,.45);font-size:15px;font-weight:700}@media only screen and (max-width:584px){.navi-height{height:1300px}.link-box{margin-top:5%}.large-screen{display:none}}@media only screen and (min-width:584px) and (max-width:993px){.navi-height{height:800px}.link-box{margin-top:5%}.large-screen{display:none}}@media only screen and (min-width:993px){.navi-height{position:absolute;width:100%;height:100%}}.page-footer{display:none}

</style>
<div class="navi-height bg-cover pd-header">
    <div class="link-box container">
        <div class="baidu baidu-2 large-screen">
            <form name="f" action="https://www.baidu.com/" target="_blank">
                <div id="Select-2">
                    <div class="Select-box-2" id="baidu">
                        <ul style="height:46px">
                            <li class="this_s">百 · 度</li>
                            <li class="bing_s">必 · 应</li>
                            <li class="google_s">谷 · 歌</li>
                            <li class="baidu_s">百 · 度</li>
                        </ul>
                    </div> <input name="wd" id="kw-2" maxlength="100" autocomplete="off" type="text">
                </div>
                <div class="qingkong" id="qingkong" title="清 · 空" style="display:none">x</div> <input value="搜 · 索" id="su-2" type="submit">
                <ul class="keylist"></ul>
            </form>
        </div>
        <div class="row tags-posts">
            <div class="col s12 m6 l4 friend-div aos-init" data-aos="zoom-in-up">
                <div class="card">
                    <div class="jj-list-tit">娱乐 · 影视</div>
                    <ul class="jj-list-con">
                        <li><a href="https://www.jd.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">京东</a>
                        </li><li><a href="https://www.taobao.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">淘宝</a></li>
                        <li><a href="https://www.tmall.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">天猫</a></li>

                        <li><a href="https://v.qq.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">腾讯视频</a></li>
                        <li><a href="https://www.iqiyi.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">爱奇艺</a></li>
                        <li><a href="https://www.bilibili.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">哔哩哔哩</a> </li>
                        <li><a href="https://music.163.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">网易云音乐</a></li>
                        <li><a href="https://y.qq.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">QQ音乐</a></li>
                        <li><a href="https://www.kugou.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">酷狗音乐</a></li>
                    </ul>
                </div>
            </div>
            <div class="col s12 m6 l4 friend-div aos-init" data-aos="zoom-in-up">
                <div class="card">
                    <div class="jj-list-tit">社区 · Code</div>
                    <ul class="jj-list-con">
                        <li><a href="https://www.mobaijun.com/contact/" rel="external nofollow noreferrer" class="link-3" target="_blank">留言</a></li>
                        <li><a href="https://github.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">GitHub</a></li>
                        <li><a href="https://coding.net/" rel="external nofollow noreferrer" class="link-3" target="_blank">Coding</a></li>
                        <li><a href="https://juejin.im/" rel="external nofollow noreferrer" class="link-3" target="_blank">掘金</a></li>
                        <li><a href="https://gitee.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">码云</a></li>
                        <li><a href="https://www.csdn.net/" rel="external nofollow noreferrer" class="link-3" target="_blank">CSDN</a></li>
                        <li><a href="https://www.jianshu.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">简书</a></li>
                        <li><a href="https://segmentfault.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">思否</a></li>
                        <li><a href="https://cloud.tencent.com/developer/" rel="external nofollow noreferrer" class="link-3" target="_blank">云+社区</a></li>
                    </ul>
                </div>
            </div>
            <div class="col s12 m6 l4 friend-div aos-init" data-aos="zoom-in-up">
                <div class="card">
                    <div class="jj-list-tit">实用 · 工具</div>
                    <ul class="jj-list-con">
                        <li><a href="https://mdnice.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">Markdown编辑器</a></li>
                        <li><a href="https://translate.google.cn/" rel="external nofollow noreferrer" class="link-3" target="_blank">谷歌翻译</a></li>
                        <li><a href="https://www.uupoop.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">在线PS</a></li>
                        <li><a href="https://www.processon.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">思维导图</a></li>
                        <li><a href="https://wallhaven.cc/" rel="external nofollow noreferrer" class="link-3" target="_blank">超清壁纸</a></li>
                        <li><a href="https://cli.im/" rel="external nofollow noreferrer" class="link-3" target="_blank">二维码生成</a></li>
                        <li><a href="https://tool.cc/pic-resizer/" rel="external nofollow noreferrer" class="link-3" target="_blank">图片在线压缩</a></li>
                        <li><a href="https://www.iconfont.cn/" rel="external nofollow noreferrer" class="link-3" target="_blank">阿里巴巴图标库</a></li>
                        <li><a href="https://my.openwrite.cn/" rel="external nofollow noreferrer" class="link-3" target="_blank">OW分发</a></li>
                    </ul>
                </div>
            </div>
            <div class="col s12 m6 l4 friend-div aos-init" data-aos="zoom-in-up">
                <div class="card">
                    <div class="jj-list-tit">编程 · 学习</div>
                    <ul class="jj-list-con">
                        <li><a href="https://www.oschina.net/" rel="external nofollow noreferrer" class="link-3" target="_blank">开源中国</a></li>
                        <li><a href="https://htmldog.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">HTML狗</a></li>
                        <li><a href="https://www.icourse163.org/" rel="external nofollow noreferrer" class="link-3" target="_blank">中国大学慕课</a></li>
                        <li><a href="https://www.imooc.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">慕课网</a></li>
                        <li><a href="https://www.wxapp-union.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">小程序</a></li>
                        <li><a href="https://www.runoob.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">菜鸟教程</a></li>
                        <li><a href="https://blog.51cto.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">51CTO</a></li>
                        <li><a href="https://www.shiyanlou.com/library/" rel="external nofollow noreferrer" class="link-3" target="_blank">实验楼</a></li>
                        <li><a href="https://spring.io/" rel="external nofollow noreferrer" class="link-3" target="_blank">Spring</a></li>
                    </ul>
                </div>
            </div>
            <div class="col s12 m6 l4 friend-div aos-init" data-aos="zoom-in-up">
                <div class="card">
                    <div class="jj-list-tit">资讯 · 趋势</div>
                    <ul class="jj-list-con">
                        <li><a href="https://www.huxiu.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">虎嗅</a></li>
                        <li><a href="https://insights.stackoverflow.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">技术调查</a></li>
                        <li><a href="https://www.asciiworld.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">摸鱼</a></li>
                        <li><a href="https://sspai.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">少数派</a></li>
                        <li><a href="https://zh.wikihow.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">WikeHom</a></li>
                        <li><a href="https://www.awesomes.cn/rank?sort=hot" rel="external nofollow noreferrer" class="link-3" target="_blank">前端趋势</a></li>
                        <li><a href="https://github-trending.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">GitHub趋势</a></li>
                        <li><a href="https://www.tiobe.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">编程趋势</a></li>
                        <li><a href="https://trends.google.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">Google趋势</a></li>
                    </ul>
                </div>
            </div>
            <div class="col s12 m6 l4 friend-div aos-init" data-aos="zoom-in-up">
                <div class="card">
                    <div class="jj-list-tit">搜索 · 其他</div>
                    <ul class="jj-list-con">
                        <li><a href="https://ac.scmor.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">谷歌镜像</a></li>
                        <li><a href="https://www.pansoso.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">网盘搜索</a></li>
                        <li><a href="https://tool.mkblog.cn/music/" rel="external nofollow noreferrer" class="link-3" target="_blank">音乐搜索</a></li>
                        <li><a href="https://www.upyun.com/?utm_source=lianmeng&amp;utm_medium=referral" rel="external nofollow noreferrer" class="link-3" target="_blank">又拍云</a></li>
                        <li><a href="https://carbon.now.sh/" rel="external nofollow noreferrer" class="link-3" target="_blank">代码图片</a></li>
                        <li><a href="https://www.zhipin.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">Boos</a></li>
                        <li><a href="https://www.fontawesome.com.cn/" rel="external nofollow noreferrer" class="link-3" target="_blank">图标库</a></li>
                        <li><a href="https://www.qvdv.com/tools/qvdv-guid.html" rel="external nofollow noreferrer" class="link-3" target="_blank">在线工具</a>
                        </li>
                        <li><a href="https://zhongguose.com/" rel="external nofollow noreferrer" class="link-3" target="_blank">中国色</a></li>
                    </ul>
                </div>
            </div>
        </div>
        <script>$(".Select-box ul").hover(function(){$(this).css("height","auto")},function(){$(this).css("height","40px")}),$(".Select-box-2 ul").hover(function(){$(this).css("height","auto")},function(){$(this).css("height","46px")}),$(".Select-box li").click(function(){var t=$(this).attr("class"),s=$(this).html();"baidu_s"==t&&(t="https://www.baidu.com/s",_name="wd"),"google_s"==t&&(t="https://www.google.com/search",_name="q"),"bing_s"==t&&(t="https://www.bing.com/search",_name="q"),$(".baidu form").attr("action",t),$(".this_s").html(s),$("#kw").attr("name",_name),$(".Select-box ul").css("height","40px")}),$(".Select-box-2 li").click(function(){var t=$(this).attr("class"),s=$(this).html();"baidu_s"==t&&(t="https://www.baidu.com/s",_name="wd"),"google_s"==t&&(t="https://www.google.com/search",_name="q"),"bing_s"==t&&(t="https://www.bing.com/search",_name="q"),$(".baidu form").attr("action",t),$(".this_s").html(s),$("#kw-2").attr("name",_name),$(".Select-box-2 ul").css("height","48px")})</script>
    </div>
</div>
```

## 预览部署

执行相关命令

预览

`hexo cl&&hexo g&&hexo s`

部署

`hexo cl&&hexo g&&hexo d`
