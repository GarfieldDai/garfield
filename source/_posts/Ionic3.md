---
title: 使用Ionic3进行移动开发
date: 2017-12-01 00:15:25
categories: Mobile
tags: Hybrid App
thumbnail: "/images/Mobile/ionic3.jpg"
---
![](/images/Mobile/ionic3.jpg)

## 目的
Ionic3搭建Android和IOS应用，以及Ionic CLI常用命令使用。

<!--more-->

## 简介
对比Ionic1.x，之后的版本进行了很大的改变，使用了基于Typescript开发的Angular，而且Angular内置了Sass进行样式管理，弥补了1.x版本需要自己进行样式管理的麻烦。

## 内容

### 项目创建
+ 环境配置。
```shell
$ npm install -g ionic cordova
```

+ 创建项目`demo`。使用参数`--type=ionic1`可以创建Ionic1.x项目。
```shell
$ ionic start demo tabs
# ionic start demo --type=ionic1
```
  Ionic3提供了以下几个模板，这里选用tabs进行初始化项目。
  1. tabs : a simple 3 tab layout
  2. sidemenu: a layout with a swipable menu on the side
  3. blank: a bare starter with a single page
  4. super: starter project with over 14 ready to use page designs
  5. tutorial: a guided starter project

+ 本地运行，可以使用浏览器进行调试开发。
```shell
$ cd demo
$ ionic serve
```

### IOS模拟器
+ 在Mac环境下，安装Xcode。
+ 安装好后，执行以下命令安装命令工具。
```shell
$ xcode-select --install
$ npm install -g ios-deploy
```
+ 使用Ionic CLI添加IOS环境
```shell
$ ionic cordova platform add ios
```
+ 模拟器运行APP。`--livereload`能够实时的同步修改到模拟器。
```shell
$ ionic cordova emulate ios --livereload
```

#### Android模拟器
+ 在Mac环境下安装好Java JDK，配置环境变量。
+ 下载Android Studio IDE，配置SDK和AVD。
+ 使用Ionic CLI添加Android环境
```shell
$ ionic cordova platform add android
```
+ 模拟器运行APP。`--livereload`能够实时的同步修改到模拟器。
```shell
$ ionic cordova emulate android --livereload
```

#### Ionic CLI常用命令使用
+ ionic docs：命令行打开Ionic开发文档。
+ ionic info：查看环境配置信息。
+ ionic start：新建Ionic项目。
+ ionic build：构建网页资源。
+ ionic serve：本地运行，可以使用浏览器进行调试开发。
+ ionic generate：快速生成pipes, components, pages, directives, providers, and tabs组件。
+ ionic cordova requirements：查看环境配置需求。
+ ionic cordova prepare：构建网页资源。
+ ionic cordova compile：编译移动项目。
+ ionic cordova build：构建网页资源，编译移动项目。
+ ionic cordova emulate：运行应用模拟器。
+ ionic cordova platform add：添加移动开发平台。
+ ionic cordova plugin：插件管理。
+ ionic cordova run：在真机运行应用。


参考资料
[Installing Ionic](http://ionicframework.com/docs/intro/installation/)
[iOS Platform Guide](https://cordova.apache.org/docs/en/latest/guide/platforms/ios/)
[Deploying to a Device](http://ionicframework.com/docs/intro/deploying/)
[sdkmanager](https://developer.android.google.cn/studio/command-line/sdkmanager.html)
