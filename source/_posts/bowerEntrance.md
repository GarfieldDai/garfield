---
title: Bower 快速入门
date: 2017-05-18 21:10:16
categories: Front End
tags: Bower
thumbnail: "/images/FrontEnd/bower/bower.png"
---
![](/images/FrontEnd/bower/bower.png)

## 目的
本文章主要讲如何使用 Bower。

<!--more-->

## 简介
Bower 是一个前端包管理器，帮助你安装前端框架和管理框架之间的依赖，但是并不帮助你压缩代码和做其他的任务。`bower.json` Bower 通过这个文件记录和管理相关的包。

## 内容
### 安装 Bower
首先需要安装 Node 和 npm，其次还需要安装Git。
`$ npm install -g bower`
通过这个命令进行Bower的安装。

### 使用 Bower 进行包的安装
`$ bower install <package>`
通过 `bower install` 进行安装，安装后的文件将会在`bower_components/`目录下面。

`<package>` 有以下几种类型。

`$ bower install`
安装所有在`bower.json`里面记录的包。

`$ bower install jquery`
安装jquery。

`$ bower install git://github.com/user/package.git`
安装github里面的包。

`$ bower install http://example.com/script.js`
安装当前链接的包。

### 查询安装包
[Search package](https://bower.io/search/)

### 记录和管理包
`bower init`
首先初始化当前项目，Bower 会在当前项目创建`bower.json`文件。
`bower install <package> --save`
通过`--save`命令记录下载过的包文件。

### 使用下载好的包
你可以直接引用包
`<script src="bower_components/jquery/dist/jquery.min.js"></script>`

但是推荐和其他管理工具一起使用，如`Grunt, RequireJS, Yeoman`等。

参考资料
[Bower official site](https://bower.io/)
