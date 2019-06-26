---
title: Jenkins安装以及如何使用Pipeline
date: 2017-11-01 15:21:13
categories: DevOps
tags: Jenkins
thumbnail: "/images/DevOps/jenkins.png"
---
![](/images/DevOps/jenkins.png)

## 目的
简单介绍如何部署Jenkins，讲解一下如何使用Pipeline，版本为Jenkins ver. 2.73.2。

<!--more-->

## 简介
Jenkins是进行项目持续集成(Continuous Integration)的必备利器，可以实现项目的自动化构建，测试和部署。

## 安装
任何环境下都需要预装JDK或者JRE，安装Jenkins默认端口为8080。
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

## Pipeline
Jenkins Pipeline简单的讲就是将项目的构建，测试和部署等相关的动作进行脚本化，然后让Jenkins自动执行相关的脚本命令。这里介绍如何使用`Jenkinsfile`文件让Jenkins自动化执行脚本，该脚本使用的语法格式为 [Pipeline Domain Specific Language (DSL) syntax](https://jenkins.io/doc/book/pipeline/syntax/)。
![Pipeline Flow](/images/DevOps/pipeline_flow.png)
`Jenkinsfile`放在项目的根目录，方便项目进行版本控制和跟踪，示例代码使用Maven管理项目。
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'mvn test'
            }
            post {
                always {
                    junit 'reports/**/*.xml'
                }
                success {
                    echo 'I succeeeded!'
                }
                unstable {
                    echo 'I am unstable :/'
                }
                failure {
                    echo 'I failed :('
                    mail to: 'team@example.com',
                         subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
                         body: "Something is wrong with ${env.BUILD_URL}"
                }
                changed {
                    echo 'Things were different before...'
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh 'mvn install'
            }
        }
    }
}
```
+ `agent`：表示Jenkins要分配执行器(executor)和工作区间(workspace)给该Pipeline。
+ `stage`：表示Pipeline所处的阶段，如构建阶段，或者测试阶段，可自定义，方便在控制台进行图形化展示。
+ `steps`：表示当前阶段需要执行的任务，告诉Jenkins需要做什么，可以执行相关的脚本命令，可自定义。
+ `sh`：执行shell脚本命令，如果是在Windows下，可以使用`bat`来替换。
+ `post`：发送信息提示，可以设置信息提醒。
+ `junit`：使用Junit插件输出报告到指定目录。


参考资料
[Jenkins Download](https://jenkins.io/download/)
[Jenkins Debian packages](https://pkg.jenkins.io/debian-stable/)
[Getting Started with the Guided Tour](https://jenkins.io/doc/pipeline/tour/getting-started/)
[Using Jenkins to build a Java application with Maven](https://jenkins.io/doc/tutorials/building-a-java-app-with-maven/)
