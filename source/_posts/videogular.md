---
title: Videogular快速入门
date: 2017-05-19 22:33:24
categories: Front End
tags: Video
thumbnail: "/images/FrontEnd/video/video.png"
---
![](/images/FrontEnd/video/video.png)

## 目的
如何使用 Videogular 播放视频。
<!--more-->

## 简介
Videogular是一个基于Angular的HTML5视频播放器，同时也支持移动端应用开发，但是不支持Flash。

## 内容
### 安装
推荐使用Node.js和npm进行安装。
```
npm install videogular
```
同时你也可以安装额外的主题和插件。
```
npm install videogular-themes-default
npm install videogular-controls
npm install videogular-buffering
npm install videogular-overlay-play
npm install videogular-poster
npm install videogular-ima-ads
npm install videogular-angulartics
npm install videogular-dash
```
或者你也可以使用[Bower](http://www.garfieldwiki.com/2017/05/18/bowerEntrance/#more)进行安装。
```
bower install videogular
```
同时你也可以安装额外的主题和插件。
```
bower install videogular-controls
bower install videogular-buffering
bower install videogular-overlay-play
bower install videogular-poster
bower install videogular-ima-ads
bower install videogular-angulartics
```
除此之外，你还需要安装AngularJS和AngularJS Sanitize。
```
bower install angular
bower install angular-sanitize
```
### First blood!
新建`index.html`文件，并且引入相关文件。新建`main.js`文件，放置JS代码。
```html
<script src="bower_components/angular/angular.min.js"></script>
<script src="bower_components/angular-sanitize/angular-sanitize.min.js"></script>
<script src="bower_components/videogular/videogular.js"></script>
<script src="bower_components/videogular-controls/vg-controls.js"></script>
<script src="bower_components/videogular-overlay-play/vg-overlay-play.js"></script>
<script src="bower_components/videogular-poster/vg-poster.js"></script>
<script src="bower_components/videogular-buffering/vg-buffering.js"></script>
<script src="js/main.js"></script>
```
### AngularJS Code
打开`main.js`文件，添加下面代码。
```javascript
'use strict';
angular.module('myApp',
    [
      "ngSanitize",
      "com.2fdevs.videogular",
      "com.2fdevs.videogular.plugins.controls",
      "com.2fdevs.videogular.plugins.overlayplay",
      "com.2fdevs.videogular.plugins.poster"
    ]
  )
  .controller('HomeCtrl',
    ["$sce", function ($sce) {
      this.config = {
        sources: [
          {src: $sce.trustAsResourceUrl("http://static.videogular.com/assets/videos/videogular.mp4"), type: "video/mp4"},
          {src: $sce.trustAsResourceUrl("http://static.videogular.com/assets/videos/videogular.webm"), type: "video/webm"},
          {src: $sce.trustAsResourceUrl("http://static.videogular.com/assets/videos/videogular.ogg"), type: "video/ogg"}
        ],
        tracks: [
          {
            src: "http://www.videogular.com/assets/subs/pale-blue-dot.vtt",
            kind: "subtitles",
            srclang: "en",
            label: "English",
            default: ""
          }
        ],
        theme: "bower_components/videogular-themes-default/videogular.css",
        plugins: {
          poster: "http://www.videogular.com/assets/images/videogular.png"
        }
      };
    }]
  );
```
### 创建HTML代码
为了使用Videogular，你可以使用`videogular`标签。
`vg-media`将会根据controller里面设置的`source`和`tracks`变量创建视频标签。
```html
<div ng-app="myApp">
  <div ng-controller="HomeCtrl as controller" class="videogular-container">
    <videogular vg-theme="controller.config.theme">
      <vg-media vg-src="controller.config.sources"
            vg-tracks="controller.config.tracks">
      </vg-media>

      <vg-controls>
        <vg-play-pause-button></vg-play-pause-button>
        <vg-time-display>{{ currentTime | date:'mm:ss' }}</vg-time-display>
        <vg-scrub-bar>
          <vg-scrub-bar-current-time></vg-scrub-bar-current-time>
        </vg-scrub-bar>
        <vg-time-display>{{ timeLeft | date:'mm:ss' }}</vg-time-display>
        <vg-volume>
          <vg-mute-button></vg-mute-button>
          <vg-volume-bar></vg-volume-bar>
        </vg-volume>
        <vg-fullscreen-button></vg-fullscreen-button>
      </vg-controls>

      <vg-overlay-play></vg-overlay-play>
      <vg-poster vg-url='controller.config.plugins.poster'></vg-poster>
    </videogular>
  </div>
</div>
```

### 创建响应式布局
以下的样式能够让你的视频保持16：9的比例。
```css
.videogular-container {
  width: 100%;
  height: 320px;
  margin: auto;
  overflow: hidden;
}

@media (min-width: 1200px) {
  .videogular-container {
    width: 1170px;
    height: 658.125px;
  }
}

@media (min-width: 992px) and (max-width: 1199px) {
  .videogular-container {
    width: 940px;
    height: 528.75px;
  }
}

@media (min-width: 768px) and (max-width: 991px) {
  .videogular-container {
    width: 728px;
    height: 409.5px;
  }
}
```
关于Videogular的基本配置就完成了。

参考资料
[videogular](http://www.videogular.com/tutorials/how-to-start/)
