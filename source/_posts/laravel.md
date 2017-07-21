---
title: Laravel简单安装和配置
date: 2017-07-13 21:00:20
categories: PHP
tags: Laravel
thumbnail: "/images/PHP/laravel.jpg"
---
![](/images/PHP/laravel.jpg)

## 目的
如何在Ubuntu16.04安装和配置Laravel，PHP >= 5.6.4。

<!--more-->

## Composer
![](/images/PHP/composer.png)
在正式安装Laravel前，你需要安装Composer，它是管理PHP依赖关系的工具。
1. 下载`composer.phar`可执行文件。
```php
$ php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
$ php composer-setup.php
$ php -r "unlink('composer-setup.php');"
```
2. 执行完上面的命令后，你可以在当前目录找到`composer.phar`文件，将该文件放置全局路径里面。
```bash
$ mv composer.phar /usr/local/bin/composer
```
3. 查看Composer信息。
```bash
$ composer
```

## Laravel
1. 使用Composer进行安装。
```bash
$ composer global require "laravel/installer"
```
2. 配置环境变量,打开文件`/home/garfield/.bashrc`，将`~/.composer/vendor/bin`路径加到 PATH。
```
export PATH=/home/garfield/.config/composer/vendor/bin:$PATH
```
2. 让修改后的配置文件立即生效。
```bash
$ source /home/garfield/.bashrc
```
3. 配置完毕后，查看Laravel信息。
```bash
$ laravel -v
```
4. 新建Laravel项目。
```
$ laravel new projectName
```
5. 如果遇到下面的php zip模块异常，执行命令安装。
```bash
# [RuntimeException]                                                        
# The Zip PHP extension is not installed. Please install it and try again.
$ sudo apt install php-zip
```
6. 如果遇到下面php mbstring模块异常，执行命令安装。
```bash
# laravel/framework v5.4.28 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
$ sudo apt install php-mbstring
```
7. 安装完毕后，使用PHP自带的服务器运行项目，运行后地址为[http://127.0.0.1:8000/](http://127.0.0.1:8000/)。
```bash
$ php artisan serve
```

参考资料
[Download Composer](https://getcomposer.org/download/)
[Composer](https://getcomposer.org/doc/00-intro.md)
[Laravel](https://laravel.com/docs/5.4/installation)
