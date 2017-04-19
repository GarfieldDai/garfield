---
title: JSHint 配置与使用
date: 2017-04-19 10:51:31
categories: JavaScript
tags: JSHint
thumbnail: "/images/JavaScript/jsHint/jsHint.jpg"
---
![](/images/JavaScript/jsHint/jsHint.jpg)

## 目的
介绍什么是 JSHint，以及如何在Sublime Text中配置和使用。

<!--more-->

## 简介
在编写 JavaScript 的时候，JSHint 能够帮助你进行语法检查和校验，能够尽早的发现代码中出现的问题。

## 内容
在 Sublime Text 2 和 3 中使用 JSHint Gutter 插件，该插件是基于 JSHint 进行开发的。

1. 首先你需要安装 node.js。

2. 通过 Sublime Package Manager 进行安装。
  + 在编辑器里面使用快捷键 `Ctrl+Shift+P`。
  + 输入 `install` 后，选择 `Package Control: Install Package`。
  + 输入 `js gutter` 后，选择 `JSHint Gutter`即可安装。


## 使用方式
1. 快捷键 `Ctrl+Shift+P`，然后输入 `jshint`。
2. 右键选择 `JSHint`，点击 `Lint Code`。

参考资料
[JSHint Gutter for Sublime Text 2 and 3 via node.js](https://github.com/victorporof/Sublime-JSHint)
[JSHint](http://jshint.com/docs/)
