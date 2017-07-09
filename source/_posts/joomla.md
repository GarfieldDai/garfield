---
title: Joomla简单配置和使用
date: 2017-07-09 10:29:56
categories: CMS
tags: Joomla
thumbnail: "/images/CMS/joomla/joomla.jpg"
---
![](/images/CMS/joomla/joomla.jpg)

## 目的
如何在Ubuntu16.04安装和配置Joomla。

<!--more-->

## 简介
Joomla是一款强大的内容管理系统（Content Management System）。

## 内容
本博文假设你已经安装好LAMP架构。
+ PHP 5.6+or7+
+ Mysql 5.5.3+
+ Apache 2.4+
+ Joomla 3.7.3

1. 设置PHP.ini配置，`/etc/php/7.0/apache2/php.ini`。
  + memory_limit - 最小: 64M 推荐: 128M or better
  + upload_max_filesize - 最小: 20M
  + post_max_size - 最小: 20M
  + max_execution_time: 最小 120 推荐: 300

2. 为joomla初始化数据库。
```sql
create database joomla;
```
3. 安装php模块。
```bash
$ sudo apt-get install php7.0-mysql php7.0-curl php7.0-json php7.0-cgi php7.0 libapache2-mod-php7.0 php7.0-mcrypt php7.0-xml php7.0-xmlrpc
```
4. 到 Joomla 官网下载软件压缩包。
5. 清空`/var/www/html/`文件，解压压缩包到`/var/www/html/`。
```bash
rm -rf /var/www/html/*
```
6. 授权给`/var/www/html/`，重启服务器。
```bash
$ sudo chown -R www-data.www-data /var/www/html
$ sudo chmod -R 755 /var/www/html
$ sudo systemctl restart apache2.service
```
7. 打开[http://localhost/installation/index.php](http://localhost/installation/index.php)就可以启动程序安装。
8. 完成安装后，需要移除安装文件。
```bash
cd /var/www/html/
rm -rf installation/
```



参考资料
[Installing Joomla](https://docs.joomla.org/J3.x:Installing_Joomla)
[How to Install Joomla on Ubuntu 16](https://www.globo.tech/learning-center/install-joomla-ubuntu-16/)
