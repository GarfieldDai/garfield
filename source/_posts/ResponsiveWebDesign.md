---
title: 响应式布局设计
date: 2017-05-15 10:29:40
categories: CSS
thumbnail: "/images/CSS/RWD/RWD.jpg"
---
![](/images/CSS/RWD/RWD.jpg)

## 目的
主要讲解如何设计响应式布局。

<!--more-->

## 简介
随着移动互联网的快速发展以及移动终端的多样化，单一的网站界面已经不能满足当前的需要。日常使用除了个人电脑外，还有不同屏幕大小的平板和手机。响应式布局的网站设计就是为了兼容各种不同的移动终端而设计的，同一套代码，能够在不同终端里面呈现不一样的界面。目前很多前端框架都是采用这样的布局设计。

## 内容
本文章主要分三个方面讲解如何设计响应式布局。

### 流式布局（Fluid Grids）
![](/images/CSS/RWD/RWD01.jpg)

上面是常见的网页布局，有头部栏（header），左侧菜单栏（menu），主体内容（main），右侧栏（right），底部栏（footer）还有最外层有一个DIV块（container）包裹着。
首先，最外层的DIV块属性是`overflow:hidden`，作用是将里面有`float`属性的DIV块包住，控制整个布局。然后，被包住的里面的DIV块都有两个相同的属性`width:percentage`和`float:left`。在流式布局的设计中，`width`的属性值都是用百分比例进行控制，目的是适应不同大小的屏幕的宽度。`float:left`可以让里面的DIV块能够像水流一样像左方向流动，如果当前位置宽度不够，当前的DIV块就会换行。

### 媒介查询（Media Query）
![](/images/CSS/RWD/RWD02.png)

`@media` 是CSS3的属性，该属性在响应式布局设计中非常重要。上述代码意思是，如果当前设备的宽度小于500px，那么执行里面的CSS代码。将当前浏览器宽度调整后，就会看到如下的界面显示。

![](/images/CSS/RWD/RWD03.png)

### 元信息（Meta）
最后，还要加上下面这句话。这句话就是告诉浏览器禁止当前页面进行缩放。
`<meta name="viewport" content="width=device-width, initial-scale=1.0">`

参考文献
[Using media queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries)
[响应式 Web 设计](http://www.runoob.com/css/css-rwd-viewport.html)
