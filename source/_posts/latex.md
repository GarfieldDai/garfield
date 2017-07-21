---
title: LaTex进行技术文档编写
date: 2017-07-21 09:46:56
categories: Document
tags: LaTex
thumbnail: "/images/Document/latex.png"
---
![](/images/Document/latex.png)

## 目的
如何在Ubuntu16.04使用LaTex进行技术文档编写。

<!--more-->

## 简介
LaTex是一个高质量的文档排版系统(Document preparation system for high-quality typesetting)，经常被用来发布中大型技术文档或者科学文章。LaTeX不是一个文档处理器(Word processor)，LaTeX让使用者专注于文档的内容而不是怎么呈现文档。

## 内容

### Installation
1. 下载软件压缩包`install-tl-unx.tar.gz`，解压。
[http://mirrors.ustc.edu.cn/CTAN/systems/texlive/tlnet/](http://mirrors.ustc.edu.cn/CTAN/systems/texlive/tlnet/)
2. 进入文件夹路径，执行命令进行安装。
```bash
$ sudo perl install-tl
```
3. 安装完后，配置环境变量`/home/garfield/.bashrc`，将下面代码加到最后面。
```
PATH=/usr/local/texlive/2017/bin/x86_64-linux:$PATH; export PATH
```
4. 更新配置信息。
```bash
$ source /home/garfield/.bashrc
```
5. 检查安装成功。
```bash
$ tex --version
# TeX 3.14159265 (TeX Live 2017)
# kpathsea version 6.2.3
# Copyright 2017 D.E. Knuth.
# ......
```

参考资料
[Formatting information](http://latex.silmaril.ie/formattinginformation/)
[An Introduction to Using TeX](http://www.math.harvard.edu/texman/)
[LaTex](http://www.latex-project.org/about/)
[Quick install](http://www.tug.org/texlive/quickinstall.html)
[Help Links](http://www.latex-project.org/help/links/)
