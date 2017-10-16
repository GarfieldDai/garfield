---
title: MySQL简单配置和使用
date: 2017-07-08 11:45:53
categories: Databases
tags: MySQL
thumbnail: "/images/Databases/Mysql/mysql.jpg"
---
![](/images/Databases/Mysql/mysql.jpg)

## 目的
如何在Ubuntu16.04配置和使用MySQL。

<!--more-->

## 内容
1. 安装。
```bash
$ sudo apt-get update
$ sudo apt-get install mysql-server
```
2. 完成安装后，mysql自动启动运行，可以使用下面命令检查mysql是否运行。
```bash
$ sudo netstat -tap | grep mysql
# tcp 0 0 localhost:mysql *:* LISTEN 2556/mysqld
```
3. 如果mysql服务没有正确运行，可以使用该命令重启mysql服务。
```bash
$ sudo systemctl restart mysql.service
```
4. 常用命令。
```bash
# 帮助手册
$ mysql --help
# 查看数据库状态
$ sudo service mysql status
# 停止数据库
$ sudo service mysql stop
# 启动数据库
$ sudo service mysql start
# 卸载数据库
$ sudo apt-get remove mysql-server
$ sudo apt-get autoremove
```
5. 安装mysql图形化操作软件workbench。
```bash
$ sudo apt-get install mysql-workbench
```

6. Shell登录数据库，`mysql -h host -u user -p`。
```bash
# 登录远程数据库，host为IP地址
$ mysql -h host -u root -p
# 登录本地数据库
$ mysql -u root -p
```

参考资料
[MYSQL Ubuntu wiki](https://help.ubuntu.com/lts/serverguide/mysql.html)
[A Quick Guide to Using the MySQL APT Repository](https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/)
[Connecting to and Disconnecting from the Server](https://dev.mysql.com/doc/refman/5.7/en/connecting-disconnecting.html)
