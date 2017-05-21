---
title: Video.js 快速入门
date: 2017-05-21 20:21:43
categories: Front End
tags: Video
thumbnail: "/images/FrontEnd/video/videojs.png"
---
![](/images/FrontEnd/video/videojs.png)

## 目的
如何使用 Video.js 播放视频。
<!--more-->

## 简介
Video.js 是一个开源的HTML视频播放器。

## 内容
### Video.js CDN
你可以通过CDN加载Video.js相关的文件。
```
<head>
  <link href="http://vjs.zencdn.net/5.19.2/video-js.css" rel="stylesheet">

  <!-- If you'd like to support IE8 -->
  <script src="http://vjs.zencdn.net/ie8/1.1.2/videojs-ie8.min.js"></script>
</head>

<body>
  <video id="my-video" class="video-js" controls preload="auto" width="640" height="264"
  poster="MY_VIDEO_POSTER.jpg" data-setup="{}">
    <source src="MY_VIDEO.mp4" type='video/mp4'>
    <source src="MY_VIDEO.webm" type='video/webm'>
    <p class="vjs-no-js">
      To view this video please enable JavaScript, and consider upgrading to a web browser that
      <a href="http://videojs.com/html5-video-support/" target="_blank">supports HTML5 video</a>
    </p>
  </video>

  <script src="http://vjs.zencdn.net/5.19.2/video.js"></script>
</body>
```
### Install via npm
```
$ npm install --save-dev video.js
```
### Install via Bower
```
$ bower install video.js
```

参考资料
[Video.js](http://videojs.com/getting-started/)