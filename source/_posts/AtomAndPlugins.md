---
title: Atom 常用插件介绍
date: 2017-05-22 22:36:11
categories: Editor
tags: Atom
thumbnail: "/images/Editor/Atom/atom.jpg"
---
![](/images/Editor/Atom/atom.jpg)

## 目的
简单介绍如何安装Atom，以及常用插件的介绍和安装。

<!--more-->

## 简介
+ Windows 用户直接下载安装即可使用。
+ Debian Linux (Ubuntu) 仅支持64位操作系统，直接在官网下载`atom-amd64.deb`，并用以下命令进行安装。
```
$ sudo dpkg --install atom-amd64.deb
```

## 内容
### [Script](https://atom.io/packages/script)
该插件允许你直接在编辑器运行你的代码，基本上覆盖了所有常用的编程语言。
```
$ sudo apm install script
```
+ `shift-ctrl-b`：如果没有指定运行哪行，就会执行整个文件。

参考资料
[Atom](https://github.com/atom/atom)
[Script](https://atom.io/packages/script)
