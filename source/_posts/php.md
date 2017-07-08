---
title: LAMP(Linux+Apache+Mysql+PHP)应用架构搭建
date: 2017-07-08 13:11:06
categories: PHP
tags: LAMP
thumbnail: "/images/PHP/lamp.png"
---
![](/images/PHP/lamp.png)

## 目的
如何在Ubuntu16.04搭建LAMP架构。

<!--more-->

## 简介
PHP作为世界上最好的语言，有着其内在的理由，据统计，大约70%左右的网站都使用该门语言进行开发。PHP语言对新手入门简单，学习成本底，现成解决方案成熟，其开发成本比其他语言底，是中小型企业网站建设开发和个人博客建设的首选语言。

## LAMP Application
Ubuntu系统已经提供了简单的命令进行LAMP项目的搭建。
1. 安装`tasksel`。
```bash
$ sudo apt install tasksel
```
2. 搭建LAMP架构，只需要简单一条命令即可，之后按照提示操作即可。
```bash
$ sudo tasksel install lamp-server
```
3. 在`/var/www/html`创建php文件`phpinfo.php`。
```
<?php
  phpinfo();
?>
```
4. 浏览器打开[http://localhost/phpinfo.php](http://localhost/phpinfo.php)，你就可以看到PHP相关的配置信息。

## PHP 安装
![](/images/PHP/php.png)
如果你通过`tasksel`安装LAMP，下面的内容就可不用看了。
以下内容假设你已经安装和配置好了Apache2 Web 服务器和Mysql数据库，可以在本网站查看相关的安装教程。

1. 安装PHP和Apache PHP模块（module）。
```bash
$ sudo apt install php libapache2-mod-php
```
2. 安装Mysql模块。
```bash
$ sudo apt install php-mysql
```
3. 重启Mysql服务。
```bash
$ sudo systemctl restart apache2.service
```
4. 在`/var/www/html`创建php文件`phpinfo.php`。
```
<?php
  phpinfo();
?>
```
5. 浏览器打开[http://localhost/phpinfo.php](http://localhost/phpinfo.php)，你就可以看到PHP相关的配置信息。

参考资料
[LAMP Application](https://help.ubuntu.com/lts/serverguide/lamp-overview.html)
[PHP - Scripting Language](https://help.ubuntu.com/lts/serverguide/php.html)
