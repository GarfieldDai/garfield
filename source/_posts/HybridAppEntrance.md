---
title: 混合移动应用开发(Hybrid App)
date: 2017-05-05 16:41:28
categories: Mobile
tags: Hybrid App
thumbnail: "/images/Mobile/Hybrid/Hybrid.png"
---
![](/images/Mobile/Hybrid/Hybrid.png)

## 目的
如何使用 Apache Cordova 和 Ionic 进行移动应用开发。

<!--more-->

## 简介
Apache Cordova是一个开源的移动应用开发框架。
能够让你使用Web前端技术(HTML5，CSS3，JavaScript)开发跨平台应用，通过配置能让你在网页端调用设备的硬件资源(网络状态，感应器，相机，联系人等)。
Ionic 提供了移动应用开发的前端框架，本篇章使用 Ionic v1 Framework, 该版本是基于 AngularJS v1实现。整个应用为一个单页面应用(Single Page Application)，其路由是借助 [UI-Router](https://ui-router.github.io/) 实现。

## 内容

### 环境配置
1. 安装 NodeJS。

2. 安装 Cordova 和 Ionic。
  ```
  npm install -g cordova ionic
  ```

3. 初始化项目,命名为 ‘myApp’。
  ```
  ionic start myApp tabs
  ```

4. 本地浏览器测试项目运行。
  ```
  ionic serve
  ```

### 安卓应用开发配置
1. 配置 JDK 和 Android SDK。

2. 配置 Gradle。

3. 设置环境变量。
  + JAVA_HOME
  + ANDROID_HOME
  + Path
    + Gradle
    + Platform-tools
    + Tools

4. 添加安卓开发平台。
  ```
  Cordova platform add android --save
  ```

5. 构建安卓项目。
  ```
  Cordova build android --verbose
  ```

6. 电脑运行安卓虚拟机。
  ```
  Cordova run android
  ```
