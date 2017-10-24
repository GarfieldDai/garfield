---
title: Git 常见问题
date: 2017-10-24 10:56:38
categories: Git
thumbnail: "/images/Git/gitpro.jpg"
---
![](/images/Git/gitpro.jpg)

## 目的
记录一下Git使用过程中出现的问题。

<!--more-->

## 内容

+ 使用`git push`命令的时候，一直停留在`writing object: 100%`。
```shell
$ git config --global sendpack.sideband false
```
