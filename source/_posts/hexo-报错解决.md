---
title: Hexo-报错解决记录
author: 闲花
img: "https://files.islu.cn/article/hexo_error.jfif"
top: true
toc: true
mathjax: false
categories: Hexo
tags:
  - blog
  - Hexo
keywords: "Hexo,报错记录,报错解决,hexo g,卜蒜子错误,hexo空白"
summary: 使用Hexo过程中报错解决记录
abbrlink: 27752
date: 2021-03-14 17:16:49
update: 2021-03-14 17:16:49
---

## hexo generate (hexo g)

### Cannot read property ‘count’ of undefined

```sh
FATAL Something's wrong. Maybe you can find the solution here: https://hexo.io/docs/troubleshooting.html
TypeError: Cannot read property 'count' of undefined
    at Hexo.module.exports (C:\Users\L\Desktop\MyBlog-matery\node_modules\hexo-baidu-url-submit\lib\generator.js:4:41)
    at Hexo.tryCatcher (C:\Users\L\Desktop\MyBlog-matery\node_modules\bluebird\js\release\util.js:16:23)
    at Hexo. (C:\Users\L\Desktop\MyBlog-matery\node_modules\bluebird\js\release\method.js:15:34)
    at C:\Users\L\Desktop\MyBlog-matery\node_modules\hexo\lib\hexo\qipao.js:380:22
    at tryCatcher (C:\Users\L\Desktop\MyBlog-matery\node_modules\bluebird\js\release\util.js:16:23)
    at MappingPromiseArray._promiseFulfilled (C:\Users\L\Desktop\MyBlog-matery\node_modules\bluebird\js\release\map.js:68:38)
    at MappingPromiseArray.PromiseArray._iterate (C:\Users\L\Desktop\MyBlog-matery\node_modules\bluebird\js\release\promise_array.js:115:31)
    at MappingPromiseArray.init (C:\Users\L\Desktop\MyBlog-matery\node_modules\bluebird\js\release\promise_array.js:79:10)
    at MappingPromiseArray._asyncInit (C:\Users\L\Desktop\MyBlog-matery\node_modules\bluebird\js\release\map.js:37:10)
    at _drainQueueStep (C:\Users\L\Desktop\MyBlog-matery\node_modules\bluebird\js\release\async.js:97:12)
    at _drainQueue (C:\Users\L\Desktop\MyBlog-matery\node_modules\bluebird\js\release\async.js:86:9)
    at Async._drainQueues (C:\Users\L\Desktop\MyBlog-matery\node_modules\bluebird\js\release\async.js:102:5)
    at Immediate.Async.drainQueues [as _onImmediate] (C:\Users\L\Desktop\MyBlog-matery\node_modules\bluebird\js\release\async.js:15:14)
    at processImmediate (internal/timers.js:439:21)
```

> 因百度主动提交插件导致，已安装插件却未完成 `_config.yml`的信息完善

**解决方案**

1.  完善`_config.yml`

```yml
# hexo-baidu-url-submit  百度主动推送
baidu_url_submit:
  count: 80 # 提交最新的一个链接
  host: blog.cn # 在百度站长平台中注册的域名
  token: TGtEmSO8ZImXXXXX # 请注意这是您的秘钥， 所以请不要把博客源代码发布在公众仓库里!
  path: baidu_urls.txt # 文本文档的地址， 新链接会保存在此文本文档里
```

2.  删除百度主动推送插件

```shell
npm remove hexo-baidu-url-submit
hexo clean
hexo g
```

### 部署或本地预览网页为空白

运行`hexo g` 命令没有问题，但是编辑器打开 `public` 文件生成的 `index.html`中代码未自动生成

> 因 node.js 的版本过高

**解决方案**

降低 node.js 版本，建议使用 node.js (12.13.0)

[node.js 12.X 版本传送门](https://nodejs.org/dist/latest-v12.x/)

### 代码高亮问题({}被编译成#234)

在你博客的根目录。
输入指令 `npm uninstall hexo --save` 卸载 现在的版本
在输入 `npm install hexo@加要安装的版本 --save`即可

eg:`npm install hexo@4.2.0 --save`

### 卜蒜子统计未显示问题

在`matery.css`中添加如下代码

```css
#busuanzi_container_site_pv,
#busuanzi_value_site_pv,
#busuanzi_container_site_uv {
  display: inline !important;
}
```
