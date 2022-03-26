---
title: Matery主题友链实现随机排列
author: 闲花
img: "https://files.islu.cn/article/MateryFriends"
top: false
toc: true
mathjax: false
categories: Hexo
tags:
  - Hexo
  - Hexo友链实现随机排列
keywords: Hexo,Matery,友链,matery友链,随机友链,随机排序
essay: false
summary: 将Matery主题的友链由固定排列改为随机排列
abbrlink: 54953
date: 2021-04-06 14:22:13
update: 2021-04-06 14:22:13
---

# 友链随机排列

## 未添加友链朋友圈

### 友链信息抓取

将`/source/_data/friends.json` 复制至`/source/friends`目录下

> 以后友链信息在/friends/friends.json 中更新

### 更改 friends.ejs

```ejs
<%- partial('_partial/bg-cover') %>
<style>
.card .card-content p {
    height: 44.8px;
    line-height: 22.4px
}

#friends-link {
    height: auto !important
}

.friends-container {
    margin-top: -100px;
    margin-bottom: 30px;
}

.friend-div {
    height: 240px;
}

.friends-container .tag-title {
    margin-bottom: 10px;
    color: #3C4858;
    font-size: 1.75rem;
    font-weight: 400;
}

.frind-ship img {
    border-radius: 50%;
}

/* 一下是按钮样式 */

.frind-ship {
    padding: 10px 20px;
}

.frind-ship .title {
    display: flex;
    align-items: center;
}

.frind-ship .title div {
    color: #fff;
    padding-left: 10px;
}

.frind-ship .title img {
    width: 100px;
    height: 100px;
    flex-shrink: 0;
}

.frind-ship .title h1 {
    padding-bottom: 5px;
    border-bottom: 2px solid #fff;
    position: relative;
    top: -15px;
    left: 3px;
}

.friend-button {
    display: flex;
    justify-content: center;
    margin-bottom: -27px;
}

.friend-button a {
    border-radius: 40px;
}

.friend-all .tag-post {
    margin-bottom: 30px;
}

.button-caution {
    background-color: #FF4351;
    border-color: #FF4351;
    color: #FFF;
}

.button {
    font-weight: 300;
    font-size: 16px;
    font-family: "Helvetica Neue Light", "Helvetica Neue", Helvetica, Arial, "Lucida Grande", sans-serif;
    text-decoration: none;
    text-align: center;
    line-height: 40px;
    height: 40px;
    padding: 0 40px;
    margin: 0;
    display: inline-block;
    appearance: none;
    cursor: pointer;
    border: none;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
    -webkit-transition-property: all;
    transition-property: all;
    -webkit-transition-duration: .3s;
    transition-duration: .3s;
}

.title {
    margin-bottom: 0rem !important;
}

.card {
    margin: 3rem 0 1rem 0 !important;
}

.button-glow.button-caution {
    -webkit-animation-name: glowing-caution;
    animation-name: glowing-caution;
}

@-webkit-keyframes glowing-caution {
    from {
        -webkit-box-shadow: 0 0 0 rgba(255, 67, 81, 0.3);
        box-shadow: 0 0 0 rgba(255, 67, 81, 0.3);
    }

    50% {
        -webkit-box-shadow: 0 0 20px rgba(255, 67, 81, 0.8);
        box-shadow: 0 0 20px rgba(255, 67, 81, 0.8);
    }

    to {
        -webkit-box-shadow: 0 0 0 rgba(255, 67, 81, 0.3);
        box-shadow: 0 0 0 rgba(255, 67, 81, 0.3);
    }
}

@keyframes glowing-caution {
    from {
        -webkit-box-shadow: 0 0 0 rgba(255, 67, 81, 0.3);
        box-shadow: 0 0 0 rgba(255, 67, 81, 0.3);
    }

    50% {
        -webkit-box-shadow: 0 0 20px rgba(255, 67, 81, 0.8);
        box-shadow: 0 0 20px rgba(255, 67, 81, 0.8);
    }

    to {
        -webkit-box-shadow: 0 0 0 rgba(255, 67, 81, 0.3);
        box-shadow: 0 0 0 rgba(255, 67, 81, 0.3);
    }
}

.button-caution:hover {
    background-color: #ff7680;
    border-color: #ff7680;
    color: #FFF;
    text-decoration: none;
}

.frind-card1 {
    background-image: linear-gradient(to right, #4facfe 0%, #00f2fe 100%);
}

.frind-card2 {
    background-image: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

.frind-card3 {
    background-image: linear-gradient(to right, #b8cbb8 0%, #b8cbb8 0%, #b465da 0%, #cf6cc9 33%, #ee609c 66%, #ee609c 100%);
}

.frind-card4 {
    background-image: linear-gradient(to right, #6a11cb 0%, #2575fc 100%);
}

.frind-card5 {
    background-image: linear-gradient(to top, #c471f5 0%, #fa71cd 100%);
}

.frind-card6 {
    background-image: linear-gradient(to top, #48c6ef 0%, #6f86d6 100%);
}

.frind-card7 {
    background-image: linear-gradient(to top, #0ba360 0%, #3cba92 100%);
}

.frind-card8 {
    background-image: linear-gradient(to top, #0c3483 0%, #a2b6df 100%, #6b8cce 100%, #a2b6df 100%);
}

.frind-card9 {
    background-image: linear-gradient(to right, #ff758c 0%, #ff7eb3 100%);
}

.frind-card10 {
    background-image: linear-gradient(to top, #f77062 0%, #fe5196 100%);
}

article .card {
    overflow: visible !important;
}
</style>

<main class="content">
    <div class="container friends-container">
        <div class="card">
            <div class="card-content">
                <div class="tag-title center-align">
                    <i class="fas fa-address-book"></i>&nbsp;&nbsp;<%= __('friends') %>
                </div>
                <article id="friends-link" style="position: relative; height: 0px;">
                    <div class="row tags-posts friend-all"></div>
                </article>
            </div>
        </div>

        <% if (page.content && page.content.length > 0) { %>
            <div class="card">
                <div class="card-content">
                    <%- page.content %>
                </div>
            </div>
        <% } %>

        <div class="card">

            <% if (theme.gitalk && theme.gitalk.enable) { %>
            <%- partial('_partial/gitalk') %>
            <% } %>

            <% if (theme.gitment.enable) { %>
            <%- partial('_partial/gitment') %>
            <% } %>

            <% if (theme.disqus.enable) { %>
            <%- partial('_partial/disqus') %>
            <% } %>

            <% if (theme.livere && theme.livere.enable) { %>
            <%- partial('_partial/livere') %>
            <% } %>

            <% if (theme.valine && theme.valine.enable) { %>
            <%- partial('_partial/valine') %>
            <% } %>

            <% if (theme.twikoo && theme.twikoo.enable) { %>
            <%- partial('_partial/twikoo') %>
            <% } %>

        </div>
    </div>
</main>

<script>
    function randArr(arr){
        arr = arr || [];
        arr.sort(function(){return Math.random()-0.5;});
        return arr;
    }

    function initTemplate(List){
        List = List || [];
        var total = List.length
        console.log('friends size ' + total);
        List.forEach((friend,index) => {

            var tmp = `<div class="col s12 m6 l4 friend-div" data-aos="zoom-in-up">
                                                    <div class="card frind-card${(index % 10 ) +1}  ">
                                                        <div class="frind-ship">
                                                            <div class="title">
                                                                <img src="${friend.avatar}" alt="img">
                                                                <div>
                                                                    <h1 class="friend-name">
                                                                        ${friend.name}
                                                                    </h1>
                                                                    <p style="position: relative;top: -35px;">
                                                                        ${friend.introduction}
                                                                    </p>
                                                                </div>
                                                            </div>
                                                            <div class="friend-button">
                                                                <a href="${friend.url} " target="_blank" class="button button-glow button-rounded button-caution">
                                                                    ${friend.title}
                                                                </a>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>`;
            $(".friend-all").prepend(tmp);
        });
    };

    $(function() {
        getDate();
        function getDate() {
            var temp = '';
            $.ajax({
                type: "get",//请求方式
                url: "/friends/friends.json",//请求的url
                dataType: "json",//后台数据返回类
                success: function(res) {//响应成功执行的
                    var friendss = res;
                    var friends = randArr(friendss);

                    initTemplate(friends);

                }
            });
        }

        $('#friends-link').masonry({
            itemSelector: '.friend-div'
        });
    });
</script>
```

## 已添加友链朋友圈

### 更改友链 url

将主题目录下的`_config.yml` 中的友链`url` 从`/friends` 改为 `/links`

### 新建页面

在`/source` 目录下新建文件夹`links`

在`/links` 目录下新建`index.md`

内容如下

```markdown
---
title: 友情帐
date: 2021-03-05 11:02:58
type: "links"
layout: "links"
---
```

### 友链信息抓取

将`/source/_data/friends.json` 复制至`/source/links`目录下

> 以后友链信息在/friends/friends.json 中更新
>
> 朋友圈友链抓取信息在/\_data/friends.json 中更新
>
> 朋友圈友链信息抓取页面还是 friends，只是将 friends 页面进行隐藏，对外展示 links 页面

### 新建 links.ejs

```ejs
<style>
.card .card-content p {
    height: 44.8px;
    line-height: 22.4px
}

#friends-link {
    height: auto !important
}

.friends-container {
    margin-top: -100px;
    margin-bottom: 30px;
}

.friend-div {
    height: 240px;
}

.friends-container .tag-title {
    margin-bottom: 10px;
    color: #3C4858;
    font-size: 1.75rem;
    font-weight: 400;
}

.frind-ship img {
    border-radius: 50%;
}

/* 一下是按钮样式 */

.frind-ship {
    padding: 10px 20px;
}

.frind-ship .title {
    display: flex;
    align-items: center;
}

.frind-ship .title div {
    color: #fff;
    padding-left: 10px;
}

.frind-ship .title img {
    width: 100px;
    height: 100px;
    flex-shrink: 0;
}

.frind-ship .title h1 {
    padding-bottom: 5px;
    border-bottom: 2px solid #fff;
    position: relative;
    top: -15px;
    left: 3px;
}

.friend-button {
    display: flex;
    justify-content: center;
    margin-bottom: -27px;
}

.friend-button a {
    border-radius: 40px;
}

.friend-all .tag-post {
    margin-bottom: 30px;
}

.button-caution {
    background-color: #FF4351;
    border-color: #FF4351;
    color: #FFF;
}

.button {
    font-weight: 300;
    font-size: 16px;
    font-family: "Helvetica Neue Light", "Helvetica Neue", Helvetica, Arial, "Lucida Grande", sans-serif;
    text-decoration: none;
    text-align: center;
    line-height: 40px;
    height: 40px;
    padding: 0 40px;
    margin: 0;
    display: inline-block;
    appearance: none;
    cursor: pointer;
    border: none;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
    -webkit-transition-property: all;
    transition-property: all;
    -webkit-transition-duration: .3s;
    transition-duration: .3s;
}

.title {
    margin-bottom: 0rem !important;
}

.card {
    margin: 3rem 0 1rem 0 !important;
}

.button-glow.button-caution {
    -webkit-animation-name: glowing-caution;
    animation-name: glowing-caution;
}

@-webkit-keyframes glowing-caution {
    from {
        -webkit-box-shadow: 0 0 0 rgba(255, 67, 81, 0.3);
        box-shadow: 0 0 0 rgba(255, 67, 81, 0.3);
    }

    50% {
        -webkit-box-shadow: 0 0 20px rgba(255, 67, 81, 0.8);
        box-shadow: 0 0 20px rgba(255, 67, 81, 0.8);
    }

    to {
        -webkit-box-shadow: 0 0 0 rgba(255, 67, 81, 0.3);
        box-shadow: 0 0 0 rgba(255, 67, 81, 0.3);
    }
}

@keyframes glowing-caution {
    from {
        -webkit-box-shadow: 0 0 0 rgba(255, 67, 81, 0.3);
        box-shadow: 0 0 0 rgba(255, 67, 81, 0.3);
    }

    50% {
        -webkit-box-shadow: 0 0 20px rgba(255, 67, 81, 0.8);
        box-shadow: 0 0 20px rgba(255, 67, 81, 0.8);
    }

    to {
        -webkit-box-shadow: 0 0 0 rgba(255, 67, 81, 0.3);
        box-shadow: 0 0 0 rgba(255, 67, 81, 0.3);
    }
}

.button-caution:hover {
    background-color: #ff7680;
    border-color: #ff7680;
    color: #FFF;
    text-decoration: none;
}

.frind-card1 {
    background-image: linear-gradient(to right, #4facfe 0%, #00f2fe 100%);
}

.frind-card2 {
    background-image: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

.frind-card3 {
    background-image: linear-gradient(to right, #b8cbb8 0%, #b8cbb8 0%, #b465da 0%, #cf6cc9 33%, #ee609c 66%, #ee609c 100%);
}

.frind-card4 {
    background-image: linear-gradient(to right, #6a11cb 0%, #2575fc 100%);
}

.frind-card5 {
    background-image: linear-gradient(to top, #c471f5 0%, #fa71cd 100%);
}

.frind-card6 {
    background-image: linear-gradient(to top, #48c6ef 0%, #6f86d6 100%);
}

.frind-card7 {
    background-image: linear-gradient(to top, #0ba360 0%, #3cba92 100%);
}

.frind-card8 {
    background-image: linear-gradient(to top, #0c3483 0%, #a2b6df 100%, #6b8cce 100%, #a2b6df 100%);
}

.frind-card9 {
    background-image: linear-gradient(to right, #ff758c 0%, #ff7eb3 100%);
}

.frind-card10 {
    background-image: linear-gradient(to top, #f77062 0%, #fe5196 100%);
}

article .card {
    overflow: visible !important;
}
</style>
<%- partial('_partial/bg-cover') %>
    <main class="content" style="min-height: 131px;">
        <div class="container friends-container">
            <div class="card">
                <div class="card-content">
                    <div id="moments_container"></div>
                </div>
            </div>
            <div class="card">
                <div class="card-content">
                    <div class="tag-title center-align">
                        <i class="fas fa-address-book"></i>&nbsp;&nbsp;<%= __('friends') %>
                    </div>
                    <article id="friends-link" style="position: relative; height: 0px;">
                        <div class="row tags-posts friend-all"></div>
                    </article>
                </div>
            </div>
        </div>
    </main>

    <script>
        function randArr(arr){
            arr = arr || [];
            arr.sort(function(){return Math.random()-0.5;});
            return arr;
        }

        function initTemplate(List){
            List = List || [];
            var total = List.length
            console.log('friends size ' + total);
            List.forEach((friend,index) => {

                var tmp = `<div class="col s12 m6 l4 friend-div" data-aos="zoom-in-up">
                                                    <div class="card frind-card${(index % 10 ) +1}  ">
                                                        <div class="frind-ship">
                                                            <div class="title">
                                                                <img src="${friend.avatar}" alt="img">
                                                                <div>
                                                                    <h1 class="friend-name">
                                                                        ${friend.name}
                                                                    </h1>
                                                                    <p style="position: relative;top: -35px;">
                                                                        ${friend.introduction}
                                                                    </p>
                                                                </div>
                                                            </div>
                                                            <div class="friend-button">
                                                                <a href="${friend.url} " target="_blank" class="button button-glow button-rounded button-caution">
                                                                    ${friend.title}
                                                                </a>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>`;
                $(".friend-all").prepend(tmp);
            });
        };

        $(function() {
            getDate();
            function getDate() {
                var temp = '';
                $.ajax({
                    type: "get",//请求方式
                    url: "/links/friends.json",//请求的url
                    dataType: "json",//后台数据返回类
                    success: function(res) {//响应成功执行的
                        var friendss = res;
                        var friends = randArr(friendss);
                        initTemplate(friends);

                    }
                });
            }

            $('#friends-link').masonry({
                itemSelector: '.friend-div'
            });
        });
    </script>
<script src="<%- theme.jsDelivr.url %><%- url_for('/js/moments.js') %>"></script>
```
