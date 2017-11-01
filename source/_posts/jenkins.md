---
title: Jenkins配置和构建Maven项目
date: 2017-11-01 15:21:13
categories: CI
tags: Jenkins
thumbnail: "/images/CI/jenkins.png"
---
![](/images/CI/jenkins.png)

## 目的
如何在Maven项目中使用Jenkins。

<!--more-->

## 简介
Jenkins是进行项目持续集成(Continuous Integration)的必备利器，可以实现项目的自动化构建，测试和部署。

## 安装
任何环境下都需要预装JDK或者JRE，安装后默认的端口为8080。
+ Windows：Jenkins的安装在Windows非常简单，只需要下载Windows的`.msi`文件，按照提示安装即可。
+ macOS：可以直接下载安装包，或者使用Homebrew进行安装。
```shell
# 安装最新版本
$ brew install jenkins
# 安装LTS版本
$ brew install jenkins-lts
```
+ Debian/Ubuntu：安装LTS版本。
```shell
$ wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
$ deb https://pkg.jenkins.io/debian-stable binary/
$ sudo apt-get update
$ sudo apt-get install jenkins
```
+ WAR：可以直接下载`WAR`包，然后放到Tomcat webapps目录下运行。或者使用Java命令，使用自带的服务器Jetty运行。
```shell
$ java -jar jenkins.war --httpPort=8080
```
+ Docker：通过Docker容器运行。
```shell
$ docker pull jenkins/jenkins
$ docker run -d -p 49001:8080 -v $PWD/jenkins:/var/jenkins_home -t jenkins/jenkins
```


参考资料
[Jenkins Download](https://jenkins.io/download/)
[Jenkins Debian packages](https://pkg.jenkins.io/debian-stable/)
[Getting Started with the Guided Tour](https://jenkins.io/doc/pipeline/tour/getting-started/)
[Using Jenkins to build a Java application with Maven](https://jenkins.io/doc/tutorials/building-a-java-app-with-maven/)
