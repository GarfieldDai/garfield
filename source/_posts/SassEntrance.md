---
title: Sass 快速入门
date: 2017-04-13 16:56:54
categories: CSS
tags: SASS
thumbnail: "/images/CSS/SASS/SASS.png"
---
![](/images/CSS/SASS/SASS.png)

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
Sass 其实是 CSS 的预编译器，主要对 CSS 进行预编译。Sass 会让CSS的编写变得更加简便，能够更好得进行维护，
它为 CSS 提供了语法特性：变量（variables），嵌套（nesting），mixins，继承 (inheritance)等。

## 内容

### 预编译
  `sass input.scss output.css`
  input.scss 是你编写的 Sass 文件，output.css 是编译后的 CSS 文件。
  Sass 有两种格式，一种为 .sass, 另一种为 .scss，后者格式跟 CSS 一样，这里使用后者的格式进行讲解。

### 变量（Variables）
Sass 使用美元符号 $ 进行变量的声明。

Sass 源代码：

    $font-stack:    Helvetica, sans-serif;
    $primary-color: #333;

    body {
      font: 100% $font-stack;
      color: $primary-color;
    }

编译后代码：

    body {
      font: 100% Helvetica, sans-serif;
      color: #333;
    }

### 嵌套 (Nesting)

Sass 源代码：

    nav {
      ul {
        margin: 0;
        padding: 0;
        list-style: none;
      }

      li { display: inline-block; }

      a {
        display: block;
        padding: 6px 12px;
        text-decoration: none;
      }
    }

编译后代码：

    nav ul {
      margin: 0;
      padding: 0;
      list-style: none;
    }

    nav li {
      display: inline-block;
    }

    nav a {
      display: block;
      padding: 6px 12px;
      text-decoration: none;
    }

### Partials
为了方便代码维护，你可以将你得代码模块化。创建一个文件`_partial.scss`，文件需要用下划线开头，这样做的目的是告诉Sass你这个文件只是一个模块文件，并且Sass不会去编译这个文件。只有在其他文件使用`@import`把当前的文件导入后，会自动将文件编译到目标文件里面。

### 导入（Import）
CSS 同样也有导入功能，可以让你的代码精简并且更好维护。唯一的缺点就是每次使用 `@import`的时候都需要创建http请求。Sass 在此基础之上克服了这个缺点，它会在编译的时候，把引用的代码合并到目标文件。
下面有两个文件，目的是把`_reset.scss` 合并到`base.scss`。

Sass 源代码：

    // \_reset.scss

    html,
    body,
    ul,
    ol {
       margin: 0;
       padding: 0;
    }

    // base.scss

    @import 'reset';

    body {
      font: 100% Helvetica, sans-serif;
      background-color: #efefef;
    }

你可以看到我们使用 `@import 'reset'` 的时候，并没有加上下划线和后缀名，因为Sass会自动进行识别。

编译后代码：

    html, body, ul, ol {
      margin: 0;
      padding: 0;
    }

    body {
      font: 100% Helvetica, sans-serif;
      background-color: #efefef;
    }

### Mixins
这个功能方便你重用代码块，你也可以传递参数给你的代码块。
使用`@mixin`进行声明代码块，使用`$radius`声明参数，使用`@include`进行引用。

Sass 源代码：

    @mixin border-radius($radius) {
      -webkit-border-radius: $radius;
         -moz-border-radius: $radius;
          -ms-border-radius: $radius;
              border-radius: $radius;
    }

    .box { @include border-radius(10px); }

编译后代码：

    .box {
      -webkit-border-radius: 10px;
      -moz-border-radius: 10px;
      -ms-border-radius: 10px;
      border-radius: 10px;
    }

### 继承（Extend/Inheritance）
`@extend` 能够让你的代码进行继承。

Sass 源代码：

    .message {
      border: 1px solid #ccc;
      padding: 10px;
      color: #333;
    }

    .success {
      @extend .message;
      border-color: green;
    }

    .error {
      @extend .message;
      border-color: red;
    }

    .warning {
      @extend .message;
      border-color: yellow;
    }

编译后代码：

    .message, .success, .error, .warning {
      border: 1px solid #cccccc;
      padding: 10px;
      color: #333;
    }

    .success {
      border-color: green;
    }

    .error {
      border-color: red;
    }

    .warning {
      border-color: yellow;
    }

### 运算符（Operators）
Sass 支持 +, -, \*, /, % 运算。

Sass 源代码：

    .container { width: 100%; }

    article[role="main"] {
      float: left;
      width: 600px / 960px * 100%;
    }

    aside[role="complementary"] {
      float: right;
      width: 300px / 960px * 100%;
    }

编译后代码：

    .container {
      width: 100%;
    }

    article[role="main"] {
      float: left;
      width: 62.5%;
    }

    aside[role="complementary"] {
      float: right;
      width: 31.25%;
    }

## 常用命令
监听单个文件
`sass --watch style.scss:style.css`

监听文件夹
`sass --watch sassFileDirectory:cssFileDirectory`

css文件转成sass/scss文件
`sass-convert style.css style.sass`
`sass-convert style.css style.scss`

编译后的css格式有四种取值：nested，expanded，compact，compressed
`sass --watch style.scss:style.css --style compact`

参考资料
[Sass official guide](http://sass-lang.com/guide)
