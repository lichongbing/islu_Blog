---
title: Hexo-live2D添加
author: 闲花
img: "https://files.islu.cn/article/hexo_live2d.png"
top: false
toc: true
mathjax: false
categories: Hexo
tags:
  - Hexo
  - Hexo添加二次元动漫角色
keywords: "materyLive2D,hexo-theme-matery动漫人物,matery主题二次元,hexo模型,Live2D,hexo"
summary: 添加二次元动漫角色
abbrlink: 47141
date: 2021-03-14 16:06:02
update: 2021-03-14 16:06:02
---

### 安装插件

`npm install --save hexo-helper-live2d`

等待加载就 OK！

### 添加配置

hexo 的配置文件 `_config.yml` 中添加如下配置:

```yaml
# 看板娘
live2d:
  enable: true # 是否开启看板娘
  scriptFrom: local
  pluginRootPath: live2dw/
  pluginJsPath: lib/
  pluginModelPath: assets/
  tagMode: false
  log: false
  model:
    use: live2d-widget-model-shizuku # 模型名称
  display:
    superSample: 2 # rate for super sampling rate 超采样等级
    position: right # Left of right side to show 显示位置：左或右
    width: 150 # Width to the canvas which shows the model canvas的长度
    height: 300 # Height to the canvas which shows the model canvas的高度
    hOffset: 75 # Horizontal offset of the canvas canvas水平偏移
    vOffset: -20 # Vertical offset of the canvas canvas垂直偏移
  mobile:
    show: true # Whether to show on mobile device 是否在移动设备上显示
    scale: 0.5 # Scale on mobile device 移动设备上的缩放
  react:
    opacity: 0.7 # opacity 透明度
  name:
    canvas: "live2dcanvas" # ID name of the canvas canvas元素的ID
    div: "live2d-widget" # ID name of the div div元素的ID
  dev:
    border: false # Whether to show border around the canvas 在canvas周围显示边界
  dialog:
    enable: false # Display dialog 显示人物对话框
    hitokoto: false # Enable hitokoto 使用一言API
```

### 选择模型

下面提供模型参考图可根据需求选择

### 模型参考示例

可根据下列模型昵称选择自己喜欢的，如 hijiki 一只黑色的猫

进行安装模型时
`npm install --save live2d-widget-model-hijiki`

> 参考图提供 width,height 可供参考(配置文件 `_config.yml` 下修改)
