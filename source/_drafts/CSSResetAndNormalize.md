---
title: CSS 统一浏览器样式
date: 2017-04-30 23:10:21
categories: CSS
thumbnail: "/images/CSS/css.jpg"
---
![](/images/CSS/css.jpg)

## 目的
在网页开发中，保证网页在不同浏览器包括手机浏览器能够给用户呈现统一的样式。

<!--more-->

## 简介
为什么需要统一浏览器样式呢？因为CSS在不同浏览器实现不一样，不同浏览器给CSS的初始值也不一样。即使你不给html页面添加任何样式，不同浏览器也会给html标签添加默认的样式。举个例子，`<a>`、`<img>`、`<h1>`到`<h6>`、`margin`、`padding`、等标签和样式属性，在不同浏览器的初始值不一样尤为明显。

## 内容
为了解决上述出现得问题，目前有以下两种方案，一种是重置化（Reset），另一种是标准化（Normalize）。

### 重置化（Reset）
目前比较常用的重置CSS样式是采用这个大神的方案[Eric Meyer's Reset CSS v2.0](http://meyerweb.com/eric/tools/css/reset/)，将这些样式添加到你的开发项目中即可。虽然该方案最近更新时间是2011年，但是目前比较流行的移动开发框架 Ionic 依旧引用这些代码。

### 标准化（Normalize）

参考资料
[CSS reset - What exactly does it do?](http://stackoverflow.com/questions/11578819/css-reset-what-exactly-does-it-do)
[CSS Tools: Reset CSS](http://meyerweb.com/eric/tools/css/reset/)
[Reset Reasoning](http://meyerweb.com/eric/thoughts/2007/04/18/reset-reasoning/)
[Reset Revisited](http://meyerweb.com/eric/thoughts/2011/01/03/reset-revisited/)
[Normalize vs Reset](http://nicolasgallagher.com/about-normalize-css/)
[The Best CSS Reset Stylesheets](http://sixrevisions.com/css/css-reset-stylesheets/)
[The History of CSS Resets](http://sixrevisions.com/css/the-history-of-css-resets/)
[A Comprehensive Guide to CSS Resets](http://sixrevisions.com/css/a-comprehensive-guide-to-css-resets/)
[Should You Reset Your CSS?](http://sixrevisions.com/css/should-you-reset-your-css/)
[]()
