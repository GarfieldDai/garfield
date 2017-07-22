---
title: LaTex
date: 2017-07-21 09:46:56
categories: Document
tags: LaTex
thumbnail: "/images/Document/latex.png"
---
![](/images/Document/latex.png)

## 目的
如何在Unix-like系统下面安装LaTex。

<!--more-->

## 简介
LaTex是一个高质量的文档排版系统(Document preparation system for high-quality typesetting)，可以处理复杂的数学公式，经常被用来发布技术文档或者科学文章。LaTex不是一个文档处理器(Word processor)，LaTex让使用者专注于文档的内容而不用关心怎么进行文档排版。

LaTex可以结合版本控制系统Git，能够实现多人同步编写文档，并且可以记录整个文档修改的历史记录，可以生成PDF格式的文档，是一种工业级别的文字排版系统，这种特性是Microsoft Word所无法比拟的。

LaTex是一门标记性语言，其他标记性语言如我们熟悉的HTML，Markdown等是同属一类。

## 内容

### Ubuntu
1. 在Ubuntu里面只需要简单一个命令就可以完成安装。
```bash
$ sudo apt install texlive-full
$ tex --version
```

2. 新建样例文本，命名为`hello.tex`。
```
\documentclass{article}
\usepackage{ctex}
\title{你好，世界}
\author{Mac}
\date{2015, July 4}
\begin{document}
  \maketitle
  这是我呐喊出来的第一句话。
\end{document}
```

3. 使用`XeLaTex`进行文档编译。
```bash
$ xelatex hello.tex
```

4. 你可以在当前目录看到生成的PDF文档`hello.pdf`。

5. 安装编辑器TexStudio
```bash
$ sudo apt install texstudio
```

### Unix-like系统手动安装
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
[Ubuntu LaTex](https://help.ubuntu.com/community/LaTeX)
[Formatting information](http://latex.silmaril.ie/formattinginformation/)
[TexStudio Support Chinese](http://blog.zhangliaoyuan.com/blog/2015/08/15/how-to-support-latex-chinese-editing-in-texstudio-under-mac/)
[WikiBooks LaTex](https://en.wikibooks.org/wiki/LaTeX)
[An Introduction to Using TeX](http://www.math.harvard.edu/texman/)
[LaTex](http://www.latex-project.org/about/)
[Quick install](http://www.tug.org/texlive/quickinstall.html)
[Help Links](http://www.latex-project.org/help/links/)
