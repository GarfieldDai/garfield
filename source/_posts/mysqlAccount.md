---
title: MySQL用户管理和权限管理
date: 2017-10-16 14:22:07
categories: Databases
tags: MySQL
thumbnail: "/images/Databases/Mysql/mysql.jpg"
---
![](/images/Databases/Mysql/mysql.jpg)

## 目的
使用MySQL管理不同用户，分别授予不同的权限。

<!--more-->

## 简介
在系统应用中，一个数据库可能为多个应用系统提供服务，不可能给每个系统都使用root用户权限，需要给不同的系统或者用户提供不同的用户权限，同时也避免root用户被泄露的安全风险。

## 用户管理
MySQL账户信息都保存在`mysql`这个database里面，账户名由用户名和主机名组成`'user_name'@'host_name'`。

+ 登录MySQL数据库
```shell
## 登录本地数据库
$ mysql --user=user_name --password db_name
$ mysql -u user_name -p db_name
## 登录远程数据库
$ mysql --host=host_name --user=myname --password db_name
$ mysql -h host_name -u myname -p db_name
```

+ 创建用户
```shell
mysql> CREATE USER 'garfield'@'localhost' IDENTIFIED BY 'password';
## 登陆后需修改密码才能继续操作
mysql> CREATE USER 'garfield'@'localhost' IDENTIFIED BY 'password' PASSWORD EXPIRE;
## 每隔180天需要重新修改密码
mysql> CREATE USER 'garfield'@'localhost' PASSWORD EXPIRE INTERVAL 180 DAY;
```

+ 用户密码管理
```shell
## 修改密码
mysql> ALTER USER 'garfield'@'localhost' IDENTIFIED BY 'new_password';
## 登陆后需修改密码才能继续操作
mysql> ALTER USER 'garfield'@'localhost' PASSWORD EXPIRE;
## 用户用新密码登录后需重新修改密码
mysql> ALTER USER 'garfield'@'localhost' IDENTIFIED BY 'new_password' PASSWORD EXPIRE;
## 每隔180天需要重新修改密码
mysql> ALTER USER 'garfield'@'localhost' PASSWORD EXPIRE INTERVAL 180 DAY;
## 取消密码过期
mysql> ALTER USER 'garfield'@'localhost' PASSWORD EXPIRE NEVER;
## 不推荐使用该方法修改密码，推荐使用ALTER
mysql> SET PASSWORD FOR 'garfield'@'localhost' = 'new_password';
```

+ 删除用户
```shell
mysql> DROP USER 'garfield'@'localhost';
```

+ 锁定用户账户
```shell
mysql> ALTER USER 'garfield'@'localhost' ACCOUNT LOCK;
mysql> ALTER USER 'garfield'@'localhost' ACCOUNT UNLOCK;
```

+ 更改账户信息
```shell
mysql> RENAME USER 'garfield'@'localhost' TO 'garfield'@'127.0.0.1';
```

## 权限管理
在授予用户权限的时候，应该遵守按需供给，根据需要赋予权限。
+ 查看用户权限
```shell
mysql> SHOW GRANTS FOR 'garfield'@'localhost';
## 查看当前用户权限
mysql> SHOW GRANTS;
mysql> SHOW GRANTS FOR CURRENT_USER;
mysql> SHOW GRANTS FOR CURRENT_USER();
```

MySQL权限有多个层面的权限控制:
1. Object Quoting Guidelines
2. Privileges Supported by MySQL
3. Global Privileges
4. Database Privileges
5. Table Privileges
6. Column Privileges
7. Stored Routine Privileges
8. Proxy User Privileges
9. Account Names and Passwords
10. Implicit Account Creation
11. Other Account Characteristics
12. MySQL and Standard SQL Versions of GRANT

本博文从数据库Database Privileges，数据表Table Privileges和数据表的列Column Privileges三个层面介绍权限管理。

+ Database Privileges
给用户授予数据库级别的操作权限。
```shell
mysql> GRANT ALL ON mydb.* TO 'someuser'@'somehost';
mysql> GRANT SELECT, INSERT ON mydb.* TO 'someuser'@'somehost';
```

+ Table Privileges
给用户授予数据库表级别的操作权限。
```shell
mysql> GRANT ALL ON mydb.mytbl TO 'someuser'@'somehost';
mysql> GRANT SELECT, INSERT ON mydb.mytbl TO 'someuser'@'somehost';
```

+ Column Privileges
给用户授予数据库表的列级别的操作权限。
```shell
mysql> GRANT SELECT (col1), INSERT (col1,col2) ON mydb.mytbl TO 'someuser'@'somehost';
```

+ 撤销权限
```shell
mysql> REVOKE INSERT ON *.* FROM 'garfield'@'localhost';
mysql> REVOKE ALL PRIVILEGES, GRANT OPTION FROM user [, user] ...
```

参考资料
[MySQL Security](https://dev.mysql.com/doc/refman/5.7/en/security.html)
[MySQL User Account Management](https://dev.mysql.com/doc/refman/5.7/en/user-account-management.html)
[Privileges Provided by MySQL](https://dev.mysql.com/doc/refman/5.7/en/privileges-provided.html)
