---
title: Python虚拟环境
date: 2017-12-03 19:59:57
categories: Python
thumbnail: "/images/Python/python.jpg"
---
![](/images/Python/python.jpg)

## 目的
使用virtualenv创建独立的Python开发环境。

<!--more-->

## 简介
在开发Python项目的时候，如果两个项目引用了同一个包，但是版本不同，可能会导致另外的项目无法运行，为了避免包冲突问题，需要创建一个独立干净的开发环境。

## 安装配置
这里主要介绍如何使用virtualenvwrapper。
+ 安装virtualenv。
```shell
$ [sudo] pip install virtualenv
```

+ 安装virtualenvwrapper，这个是对virtualenv的扩展，提供了更便捷的命令。
```shell
$ [sudo] pip install virtualenvwrapper
```

+ 配置环境变量，保存以下命令至`~/.bash_profile`。
```shell
source /usr/local/bin/virtualenvwrapper.sh
```

+ 更新环境变量。
```shell
$ source ~/.bash_profile
```

## 常用命令
+ `workon`：列出当前所有的环境。
+ `mkvirtualenv myEnv`：创建虚拟环境`myEnv`。
+ `mkvirtualenv myEnv -p python3`：指定虚拟环境的Python版本。
+ `workon myEnv`：切换当前环境到`myEnv`。
+ `lsvirtualenv`：列出当前所有的环境。
+ `showvirtualenv`：查看环境详细信息。
+ `rmvirtualenv`：移除环境。
+ `deactivate`：退出虚拟环境。

\* 虚拟环境目录在`/Users/garfield/.virtualenvs`下面。

参考资料
[virtualenv](https://pypi.python.org/pypi/virtualenv)
[virtualenv Documentation](https://virtualenv.pypa.io/en/stable/)
[virtualenvwrapper](https://pypi.python.org/pypi/virtualenvwrapper)
[virtualenvwrapper Documentation](http://virtualenvwrapper.readthedocs.io/en/latest/)
