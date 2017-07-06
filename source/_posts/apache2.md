---
title: Apache Http Server简单配置和使用
date: 2017-07-06 22:40:35
categories: Server
tags: Apache
thumbnail: "/images/Server/Apache/apache2.png"
---
![](/images/Server/Apache/apache2.png)

## 目的
如何在Ubuntu16.04配置和使用Apache Http Server。

<!--more-->

## 简介
在Linux系统中，Apache是最常用的web应用服务器

## 内容

1. 安装Apache Http Server，成功安装后，默认会启动服务器，端口号为80。
```
$ sudo apt-get update
$ sudo apt-get install apache2
```
2. 默认的资源路径为`/var/www/html`。

3. Apache web server 系统安装目录`/etc/apache2/`。

4. `/etc/apache2/apache2.conf` 是主配置文件，它引用了所有的配置文件，可以在这里设置默认的资源路径。

5. `/etc/apache2/ports.conf` 设置端口号。

参考资料
[Ask Ubuntu](https://help.ubuntu.com/lts/serverguide/httpd.html)
