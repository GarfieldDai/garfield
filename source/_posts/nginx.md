---
title: NGINX简单配置和使用
date: 2017-07-02 19:25:32
categories: Server
tags: NGINX
thumbnail: "/images/Server/Nginx/nginx.png"
---
![](/images/Server/Nginx/nginx.png)

## 目的
如何在Ubuntu16.04配置和使用NGINX。

<!--more-->

## 简介
使用NGINX作为静态资源服务器。

## 内容

1.安装NGINX，成功安装后，默认会启动服务器，端口号为80。
```
$ sudo apt-get update
$ sudo apt-get install nginx
```

2.NGINX配置文件名默认为`nginx.conf`。一般放在目录`/usr/local/nginx/conf`，`/etc/nginx`，或者` /usr/local/etc/nginx`。

3.NGINX启动后，可以使用以下命令进行配置。
```
$ sudo nginx -s 'signal'
```
signal有以下四种操作：
+ stop -- 快速停止运行。
+ quit --（graceful shutdown），完成当前http服务请求后，停止运行。
+ reload -- 修改配置文件后，需要执行这个命令才能生效。
+ reopen -- 重新打开日志文件。

4.配置`nginx.conf`的根目录和端口号。
```
server {
    listen 8080;
    root /data/www;
}
```

参考资料
[Nginx Official Website](http://nginx.org/en/linux_packages.html)
[Beginners Guide](http://nginx.org/en/docs/beginners_guide.html)
