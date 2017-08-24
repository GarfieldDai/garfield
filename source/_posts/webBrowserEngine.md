---
title: 浏览器内核以及工作原理简述
date: 2017-08-23 14:03:05
categories: Front End
tags: Browser
thumbnail: "/images/FrontEnd/browser/browser.png"
---
![](/images/FrontEnd/browser/browser.png)

## 目的
介绍目前流行的浏览器内核，以及浏览器是怎么解析网页资源。

<!--more-->

## 简介
浏览器内核（Web Browser Engine, Web Layout Engine Or Web Rendering Engine）目的是进行网页资源的解析和渲染。

目前主流浏览器使用的内核：
1. Google Chrome：基于Webkit开发的[Blink](https://www.chromium.org/blink)
2. IE：Trident
3. Mozilla Firefox：[Gecko](https://developer.mozilla.org/en-US/docs/Mozilla/Gecko)
4. Opera：[Blink](https://www.chromium.org/blink)
5. Safari：[Webkit](https://webkit.org)
6. Microsoft Edge：EdgeHTML

## 内容
#### 浏览器架构
+ The user interface：浏览器用户界面。
+ The browser engine：浏览器引擎，用来查询和操作渲染引擎。
+ The rendering engine：渲染引擎，解析网页资源如HTML和CSS，并将解析后的结果进行渲染，显示给用户看。
+ Networking：网络操作，用来进行网络请求处理。
+ UI backend：用来绘制类似组合选择框及对话框等基本组件。
+ JavaScript interpreter：JS解析器，用来解析执行JS代码，如Nodejs使用的Chrome V8引擎就是JS解析器。
+ Data storage：浏览器端的数据存储如Cookie。

![](/images/FrontEnd/browser/browser_arch.png)

#### 浏览器内核
浏览器内核也叫渲染引擎，主要作用是进行网页资源的渲染，如将HTML和CSS解析并呈现给用户。

渲染引擎基本工作方式：
解析HTML，构建DOM树->构建Render树->布局Render树->绘制Render树

![](/images/FrontEnd/browser/mainflow.png)

1. 渲染引擎首先进行HTML文档解析，并将HTML标签转换为DOM节点来构建Content树。
![](/images/FrontEnd/browser/parse.png)
2. 接下来进行CSS样式解析来构建Render树。Render树由一些包含有颜色和大小等属性的矩形组成，并按照一定的顺序显示到屏幕上。
![](/images/FrontEnd/browser/style.png)
3. 构建好Render树后，进行布局管理，确定每个节点在屏幕上的确切坐标。
![](/images/FrontEnd/browser/layout.png)
4. 再下一步就是绘制，即遍历Render树，并使用UI后端层绘制每个节点。
![](/images/FrontEnd/browser/paint.png)
5. 这个过程是逐步完成的，为了更好的用户体验，渲染引擎将会尽可能早的将内容呈现到屏幕上，一边解析一边显示，并不会等到所有的HTML都解析完成之后再去构建和布局render树。期间还可通过网络下载其余内容。
![](/images/FrontEnd/browser/render.png)

以下是具体内核的工作方式：
![Webkit Flow](/images/FrontEnd/browser/webkitflow.png)
![Gecko Flow](/images/FrontEnd/browser/geckoflow.jpg)

参考资料
[How Browsers Work: Behind the scenes of modern web browsers](http://www.taligarsiel.com/Projects/howbrowserswork1.htm)
[Quantum CSS](https://hacks.mozilla.org/2017/08/inside-a-super-fast-css-engine-quantum-css-aka-stylo/)
[Blink](https://www.chromium.org/blink)
[Gecko](https://developer.mozilla.org/en-US/docs/Mozilla/Gecko)
[Webkit](https://webkit.org)
