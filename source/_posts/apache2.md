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

4. `/etc/apache2/apache2.conf` 是主配置文件，它引用了所有的配置文件。

5. `/etc/apache2/sites-available/000-default.conf`可以配置资源路径。

6. `/etc/apache2/ports.conf` 设置端口号。

7. Apache在Ubuntu系统下的操作需要加前缀才能执行`/etc/init.d/`。
```bash
# 查看服务器状态
$ /etc/init.d/apache2 status
# 启动服务器
$ /etc/init.d/apache2 start
# 重启服务器
$ /etc/init.d/apache2 restart
# 中断请求服务，停止服务器
$ /etc/init.d/apache2 stop
# 完成当前所有请求服务后，停止服务器
$ /etc/init.d/apache2 graceful-stop
# 重新加载配置文件
$ /etc/init.d/apache2 reload
# 和reload一样
$ /etc/init.d/apache2 force-reload
```

参考资料
[Ask Ubuntu](https://help.ubuntu.com/lts/serverguide/httpd.html)
[Apache official site](https://httpd.apache.org/docs/2.4/stopping.html)
[The difference between reload and force-reload](https://serverfault.com/questions/363409/difference-between-apache-reload-and-force-reload)
