---
title: GoAccess可视化服务器日志
date: 2017-11-09 15:07:36
categories: Server
tags: Dashboard
thumbnail: "/images/Server/GoAccess/goaccess.png"
---
![](/images/Server/GoAccess/goaccess.png)

## 目的
可视化服务器日志的轻量级解决方案。

<!--more-->

## 简介
GoAccess是一款开源的实时的服务器日志分析和可视化软件，可以直接运行在终端里面，也可以在浏览器查看日志报告。

## 内容
GoAccess支持自定义日志格式解析，默认格式支持有Apache, Nginx, Amazon S3, Elastic Load Balancing, CloudFront等。

本博文介绍在Ubuntu环境下如何查看Nginx日志。
+  安装
```shell
$ sudo apt install goaccess
```

+ 运行
Nginx默认日志目录为`/var/log/nginx`，Nginx默认日志格式为`COMBINED`。
```shell
# 终端模式
$ goaccess -f access.log --log-format=COMBINED
# 浏览器静态模式
$ goaccess -f access.log -o report.html --log-format=COMBINED
# 浏览器实时模式
$ goaccess -f access.log -o report.html --log-format=COMBINED --real-time-html
# 查看多个文件
$ goaccess access.log access.log.1
# 查看当前文件目录的所有日志
$ zcat access.log.*.gz | goaccess access.log -
```

+ 日志格式
COMBINED     | Combined Log Format
VCOMBINED    | Combined Log Format with Virtual Host
COMMON       | Common Log Format
VCOMMON      | Common Log Format with Virtual Host
W3C          | W3C Extended Log File Format
SQUID        | Native Squid Log Format
CLOUDFRONT   | Amazon CloudFront Web Distribution
CLOUDSTORAGE | Google Cloud Storage
AWSELB       | Amazon Elastic Load Balancing
AWSS3        | Amazon Simple Storage Service (S3)


参考资料
[Download GoAccess](https://goaccess.io/download)
[Get started](https://goaccess.io/get-started)
[Man Page](https://goaccess.io/man)
