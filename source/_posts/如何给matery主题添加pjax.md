---
title: Matery主题添加Pjax
author: 闲花手札
img: 'https://files.islu.cn/banner/Pjax.png'
top: false
toc: true
mathjax: false
essay: false
categories: Hexo
tags:
  - Hexo
  - pjax
keywords: 'Hexo,Matery,pjax,音乐无中断播放,闲花手札'
date: 2022-01-23 13:33:03
update: 2022-01-23 13:33:03
summary: 如何使用Pjax技术实现音乐无中断播放及页面加载速度优化 
abbrlink: 28555
---

# 如何给matery主题添加Pjax

## Pjax优点

1. 减轻服务端压力

   > 按需请求，每次只需加载页面的部分内容，而不用重复加载一些公共的资源文件和不变的页面结构，大大减小了数据请求量，以减轻对服务器的带宽和性能压力，还大大提升了页面的加载速度。

2. 优化页面跳转体验

   > 使用pjax后，只刷新部分页面，切换效果更加流畅，而且可以定制过度动画，在等待页面加载的时候体验就比较舒服了。

> 我知道你们在意的是教程不是这些啰嗦的废话，下面就是正文

## 教程

### 基本了解

Pjax的使用可以在保证`Nav` `Header` `Footer` 不变的基础上改变 `Main` 的内容(适用于页面结构相对简单的主体)

![页面基本构成](https://files.islu.cn/banner/20220123135415.png)

### 步骤

#### 新建pjax.ejs

在 `_widget` 目录下新建 `pjax.ejs` 文件

```html
<%if(theme.pjax){%>
    <script type="text/javascript">
        $.getScript("https://cdn.jsdelivr.net/npm/pjax/pjax.min.js",loadPjax)
        function loadPjax(){
            var pjax = new Pjax({
                selectors: [
                    "head title",
                    'head meta[name="keywords"]',
                    'head meta[name="description"]',
                    "main#main_wrap"
                ],
                cache: true,
                cacheBust: false
            });
        }

        // Pjax请求错误时，跳转到404页面
        document.addEventListener('pjax:error', (err) => {
            if (err.request.status === 404) {
                pjax.loadUrl('/404.html')
            }
        })
    </script>
<%}%>
```

#### 添加容器

找到 `layout.eje` 为 `<%- body %>` 套一个 `<main>` 标签

```html
<main id="main_wrap">
    <%- body %>
</main>
```

#### 引入pjax.ejs

找到 `layout.ejs` 在底部(首次加载没必要优先加载Pjax)添加

```html
<%- partial('_widget/pjax') %>
```

#### 添加pjax开关

在 `themes\_config.yml`中添加

```yaml
pjax: true
```

#### bug的解决

由于Pjax会导致容器内的函数不会重载，要重载一下函数

在此仅提供重载方法，不一一做演示了

##### 部分修改页面

由于时间问题，仅提供一些需要修改的 `ejs` 内容作为参考

1. 评论页面ejs（我使用的是valine，故我需要将valine.ejs页面进行修改）
2. 谷歌统计页面（google-analytics.ejs）
3. 文章目录（post-detail-toc.ejs）
4. 说说页面（artitalk.ejs）
5. 标签页面（tags）的词云（tag-wordcloud.ejs）
6. 分类页面（categories）雷达图(category-radar.ejs)
7. 归档页面(archives)统计图(post-calendar.ejs)
8. 关于页面（about）的统计图(post-charts.ejs)

> 欢迎提交遗漏bug

##### 标签 (tags)页面为例

1. 当操作完以上步骤后从首页点进标签(tags)页面时会有一下报错

   ![image-20220123142844146](https://files.islu.cn/banner/20220123142844.png)

2. 打开 `tags.ejs` 该页面由 `tag-cloud` `tag-wordcloud` 两个ejs组成，故要查看这两个 `ejs` 页面哪里出现了 `jQCloud` 函数

   ![image-20220123142509712](https://files.islu.cn/banner/20220123142509.png)

3. 找到bug处进行修改，原页面

   1. 原页面

      ```html
      <link rel="stylesheet" type="text/css" href="<%- theme.jsDelivr.url %><%- url_for(theme.libs.css.jqcloud) %>">
      <div class="container" style="padding-bottom: 20px" data-aos="fade-up">
          <div id="tag-wordcloud" class="card-content"></div>
      </div>
      
      <script  type="text/javascript" src="<%- theme.jsDelivr.url %><%- url_for(theme.libs.js.jqcloud) %>"></script>
      <script  type="text/javascript">
          <%
          let tagWordArr = [];
          site.tags.map(function(tag) {
              tagWordArr.push({'text': tag.name, 'weight': tag.length, 'link': decodeURI(url_for(tag.path))});
          });
      
          let tagWords = JSON.stringify(tagWordArr);
          %>
      
          $('#tag-wordcloud').jQCloud(<%- tagWords %>, {
              autoResize: true
          });
      </script>
      ```

   2. 修改后

      ```html
      <link rel="stylesheet" type="text/css" href="<%- theme.jsDelivr.url %><%- url_for(theme.libs.css.jqcloud) %>">
      <style type="text/css">
          #tag-wordcloud {
              width: 100%;
              height: 300px;
          }
      </style>
      
      <div class="container" data-aos="fade-up">
          <div class="card">
              <div id="tag-wordcloud" class="card-content"></div>
          </div>
      </div>
      
      <script type="text/javascript">
          $.getScript("<%- theme.jsDelivr.url %><%- url_for(theme.libs.js.jqcloud) %>",function () {
              <%
              let tagWordArr = [];
              site.tags.map(function(tag) {
                  tagWordArr.push({'text': tag.name, 'weight': tag.length, 'link': decodeURI(url_for(tag.path))});
              });
      
              let tagWords = JSON.stringify(tagWordArr);
              %>
      
              $('#tag-wordcloud').jQCloud(<%- tagWords %>, {
                  autoResize: true
              });
          })
      </script>
      ```

   3. 修改内容

      > 将未重载的函数利用 `Jquery` 的 `getScript` 方法进行重载
      >
      > ```javascript
      > $.getScript("文件引用路径",function(){
      >     //重载函数
      > })
      > ```

##### 以评论(valine)为例

打开 `valine.ejs`

+ 原主代码

  ```html
  <script src="<%- theme.jsDelivr.url %><%- url_for('/libs/valine/av-min.js') %>"></script>
  <script src="<%- theme.jsDelivr.url %><%- url_for(theme.libs.js.valine) %>"></script>
  <script>
      let metaPlaceholder = <%-  JSON.stringify(theme.valine.metaPlaceholder) %> ;
      //这里要换行
      new Valine({
   		el: '#vcomments',
          appId: '<%- theme.valine.appId %>',
          appKey: '<%- theme.valine.appKey %>',
          notify: '<%- theme.valine.notify %>' === 'true',
          verify: '<%- theme.valine.verify %>' === 'true',
          visitor: '<%- theme.valine.visitor %>' === 'true',
          avatar: '<%- theme.valine.avatar %>',
          pageSize: '<%- theme.valine.pageSize %>',
          lang: '<% if (config.language == "zh-CN") { %>zh-cn<% } else { %>en<% } %>',
          placeholder: '<%= theme.valine.placeholder %>'
      });
  </script>
  ```

+ 修改后代码

  ```html
  <script>
  $.getScript("<%- theme.jsDelivr.url %><%- url_for('/libs/valine/av-min.js') %>", function () {
          $.getScript("<%- theme.jsDelivr.url %><%- url_for(theme.libs.js.valine) %>", function () {
              new Valine({
                  el: '#vcomments',
                  appId: '<%- theme.valine.appId %>',
                  appKey: '<%- theme.valine.appKey %>',
                  notify: '<%- theme.valine.notify %>' === 'true',
                  verify: '<%- theme.valine.verify %>' === 'true',
                  visitor: '<%- theme.valine.visitor %>' === 'true',
                  avatar: '<%- theme.valine.avatar %>',
                  pageSize: '<%- theme.valine.pageSize %>',
                  lang: '<% if (config.language == "zh-CN") { %>zh-cn<% } else { %>en<% } %>',
                  placeholder: '<%= theme.valine.placeholder %>'
              });
  
          })
      })
  </script>
  ```

  

### 推荐

#### 页面切换加载动画

1. 在 `pjax.ejs` 的 `script`标签中添加以下代码

   ```javascript
   // 清除时间
   var timer = null;
   // 执行进度条
   function ProgressStart(){
       // 设置初始进度
       var progress = 10;
       // 创建进度条 及 css样式
       var div = document.createElement('div');
       div.className = "pjax_progress";
       document.body.prepend(div);
       // 定义随机数最大值最小值
       var max=10,mini=3;
       var result=max-mini;
       // 清除
       clearInterval(timer);
       // 0.5秒内累加进度
       timer = setInterval(function(){
           // 随机数
           var num = parseInt(Math.random()*result);
           var randomResult = num+mini;
           // 累加
           progress+=randomResult
           $queryAll(".pjax_progress")[0].style.width = progress+"%";
           // 当进度达到95%时停止
           if(progress>95)progress=95
       },500)
   }
   // 加载进度条加载完毕
   function ProgressFinish(){
       clearInterval(timer);
       // 页面加载完毕后进度100% 并在0.7秒后删除
       var progress = $queryAll(".pjax_progress");
       progress[0].style.width = "100%";
       timer = setTimeout(function () {
           progress[0].parentNode.removeChild(progress[0])
       }, 700);
   }
   // 开始 PJAX 执行的函数
   document.addEventListener('pjax:send', function () {
   	// 执行进度条
       ProgressStart()
   });
   // PJAX 完成之后执行的函数，可以和上面的重载放在一起
   document.addEventListener('pjax:complete', function () {
   	// 加载进度条加载完毕
       ProgressFinish()
   });
   ```

   

2. 在 `my.css` 中添加以下样式代码

   ```css
   .pjax_progress{
       position: fixed;
       top: 0;
       left: 0;
       width: 10%;
       height: 2px;
       z-index: 103;
       background: linear-gradient(130deg, #ff0, red);
       transition: width .4s ease 0s;
   }
   ```



#### 页面切换加载进度条

1. 在 `pjax.ejs` 的 `script`标签中添加以下代码

   ```javascript
   // 开始 PJAX 执行的函数
   document.addEventListener('pjax:send', function () {
   	$("#loading").css("display","flex")
   });
   // PJAX 完成之后执行的函数，可以和上面的重载放在一起
   document.addEventListener('pjax:complete', function () {
   	$("#loading").css("display","none")
   });
   ```

2. 在 `my.css` 中添加以下样式代码

   ```css
   #loading {
     position: fixed;
     top: 0;
     left: 0;
     min-height: 100vh;
     width: 100vw;
     z-index: 9999;
     display: none;
     flex-direction: column;
     justify-content: center;
     align-items: center;
     text-align: center;
   }
   #loading .loader {
     width: 20em;
     height: 20em;
     font-size: 10px;
     position: relative;
     display: flex;
     align-items: center;
     justify-content: center;
   }
   #loading .loader .face {
     position: absolute;
     border-radius: 50%;
     border-style: solid;
     animation: CW 3s linear infinite;
   }
   #loading .loader .face:nth-child(1) {
     width: 100%;
     height: 100%;
     color: #ffd700;
     border-color: currentColor transparent transparent currentColor;
     border-width: 0.2em 0.2em 0 0;
     --deg: -45deg;
     animation-direction: normal;
   }
   #loading .loader .face:nth-child(2) {
     width: 70%;
     height: 70%;
     color: #0f0;
     border-color: currentColor currentColor transparent transparent;
     border-width: 0.2em 0 0 0.2em;
     --deg: -135deg;
     animation-direction: reverse;
   }
   #loading .loader .face .circle {
     position: absolute;
     width: 50%;
     height: 0.1em;
     top: 50%;
     left: 50%;
     background-color: transparent;
     transform: rotate(var(--deg));
     transform-origin: left;
   }
   #loading .loader .face .circle::before {
     position: absolute;
     top: -0.5em;
     right: -0.5em;
     content: '';
     width: 1em;
     height: 1em;
     background-color: currentColor;
     border-radius: 50%;
     box-shadow: 0 0 2em, 0 0 4em, 0 0 6em, 0 0 8em, 0 0 10em, 0 0 0 0.5em rgba(255,255,0,0.1);
   }
   ```

> Hexo相关文章 https://www.islu.cn/categories/Hexo/
