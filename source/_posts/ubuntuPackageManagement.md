---
title: Ubuntu Package Management
date: 2017-07-04 20:26:10
categories: Linux
tags: Ubuntu
thumbnail: "/images/Linux/Ubuntu/pkg.png"
---
![](/images/Linux/Ubuntu/pkg.png)

## 目的
如何在Ubuntu系统下进行软件管理，介绍Ubuntu常用的包管理器。

<!--more-->

## 简介
对于刚刚入门Ubuntu操作系统的同学来说，软件的管理简直是一头雾水，不像Window操作系统，Ubuntu操作系统是通过包管理器进行软件管理，大部分需要通过命令执行。以下介绍的是Ubuntu系统下常用软件管理的正确姿势。

## 内容
大多数Unix-like系统都提供一个中央仓库,软件以包(package)的方式存放在库(repository)里面。包管理器(package management system)提供软件的安装，升级，移除，查询等工作。
+ Apt-get
+ Apt-cache
+ Apt
+ Dpkg
+ Synaptic

### Apt-get
`apt-get`是Ubuntu最常用的命令，大部分的软件安装都是通过该命令进行，可以从远程仓库下载软件包，并且自动管理软件包的依赖关系。
1. 系统会在本地存储中央仓库可用的软件包信息，在你开始安装包之前，最好更新这个列表，拿到最新的软件包信息。
```bash
$ sudo apt-get update
```
2. 软件包升级，在升级之前，先执行`apt-get update`操作，让系统知道最新的软件包信息。
```bash
# 仅仅升级已经安装好的包
$ sudo apt-get upgrade
# 不但会升级包，而且会根据新的依赖关系新增和移除相关的包
$ sudo apt-get dist-upgrade
```
3. 搜索软件包。
```bash
$ apt-cache search package
```
4. 查询具体软件包的详细信息。
```bash
$ apt-cache show package
$ dpkg -s package
```
5. 从远程仓库下载并安装软件包。
```bash
$ sudo apt-get install package
# 安装特定版本的软件包
$ sudo apt-get install package=version
```
6. 有时候，你并不想直接进行包的安装，你想知道执行安装命令的过程是怎么样的。你可以使用参数`-s`进行模拟安装。你可以看到当前安装依赖了哪些包，而且并不需要`root`的权限。
```bash
$ apt-get install -s package
```
7. 只从远程仓库下载软件包。不需要`root`权限，下载后的位置是执行当前命令的位置。
```bash
$ apt-get download package
```
8. 卸载软件包。
```bash
# 卸载大部分的文件，但是会保存相关的配置文件以备下次重新安装使用
$ sudo apt-get remove package
# 卸载所有的文件和配置
$ sudo apt-get purge package
```
9. 自动删除没有被引用的软件包。
```bash
$ sudo apt-get autoremove
# 自动删除所有没有被引用的软件包以及其配置文件
$ sudo apt-get --purge autoremove
```
### Apt
`apt`集成了`apt-get`和`apt-cache`的功能，提供了更简便的命令。

apt-get/apt-cache   | apt
------------------- | --------------
apt-get update      | apt update
apt-get upgrade | apt upgrade
apt-get dist-upgrade | apt full-upgrade
apt-cache search package | apt search package
apt-get install package | apt install package
apt-get remove package | apt remove package
apt-get purge package | apt purge package

### Dpkg
1. Ubuntu是基于Debian系统开发的，所以`.deb`安装包可以使用`dpkg`进行安装。`dpkg`可以安装，卸载和构建(build)软件包，但是无法自动下载软件包和处理包之间的依赖关系。
```bash
# 安装zip包
$ sudo dpkg -i zip_3.0-4_i386.deb
```
2. 特别注意，`dpkg`并不会处理软件包之间的依赖关系，如果你所安装的包依赖了本地没有的包，那么安装就会失败。你需要执行下面的命令去安装依赖的包。
```bash
$ sudo apt-get install -f
```
3. 大多数情况并不推荐使用`dpkg`卸载软件包。`dpkg -r zip`将会移除zip软件包，但是跟zip依赖的软件包不会被卸载掉，为了保证系统一致性（consistent state），最好使用其他包管理器进行卸载。
```bash
# 卸载zip包
$ sudo dpkg -r zip
```
### Synaptic
除了命令行以外，还有一款图形化操作界面。
1. 需要使用命令行进行安装。
```
$ sudo apt-get install synaptic
```
2. System > Administration > "Synaptic Package Manager"，启动图形化界面。

参考资料
[Basic package management](https://www.digitalocean.com/community/tutorials/package-management-basics-apt-yum-dnf-pkg)
[Ubuntu and debian package management essentials](https://www.digitalocean.com/community/tutorials/ubuntu-and-debian-package-management-essentials)
[Package Management](https://help.ubuntu.com/lts/serverguide/package-management.html)
[Installing Software](https://help.ubuntu.com/community/InstallingSoftware)
[Synaptic](http://www.nongnu.org/synaptic/)
[How to use Synaptic](https://help.ubuntu.com/community/SynapticHowto)
