---
title: Sass 快速入门
date: 2017-04-13 16:56:54
categories: CSS
tags: SASS
thumbnail: "/images/CSS/SASS/SASS.png"
---
![](images/CSS/SASS/SASS.png)

## 目的
如何在 Linux Ubuntu 16.4 LTS 环境下安装 Sass，以及如何使用 Sass。

<!--more-->

## 准备工作
1. 首先需要安装 Ruby, 使用 Ubuntu apt package manager 进行安装。
  `$ sudo apt-get install ruby-full`

2. 安装 Sass。
  `sudo gem install sass`

3. 安装成功后，查看 Sass 版本号，当前使用版本为 ** Sass 3.4.23 ** 。
  `sass -v`

## 简介
Sass 其实是 CSS 的预编译器，主要对 CSS 进行预编译。随着项目的，CSS 会变得臃肿而且冗余，代码不断增加，重复代码有增不减，后期代码维护复杂而且困难，甚至牵一发而动全身。为了解决这个问题，Sass 能够为 CSS 提供语法特性：变量（variables），嵌套（nesting），mixins，inheritance（继承）。

## 内容

### 预编译
  input.scss 是你编写的 Sass 文件，output.css 是编译后的 css 文件。
  Sass 有两种格式，一种为 .sass, 另一种为 .scss，后者格式跟 css 一样，这里使用后者的格式进行讲解。
  `sass input.scss output.css`

### 变量（Variables）
  Sass 使用美元符号 $ 进行变量的声明。   

参考文献
[Sass official guide](http://sass-lang.com/guide)
