---
title: Sahi 快速入门
date: 2017-03-23 17:27:07
categories: AutomationTesting
tags: Sahi
---

## 目的
使用 Sahi Pro 进行自动化测试。

## 准备工作
* 需要 Java 环境1.5版本以上。
* 在 [Sahi](http://sahipro.com/downloads-archive/) 官网下载安装包。

## 安装 Sahi
Sahi 的安装包为 jar 包，双击安装包 install_sahi_pro_xxx.jar 进行安装。

## 启动 Sahi 监控台
双击桌面快捷键就可以打开 Sahi 监控台。

![](/images/Automation/Sahi/SahiEntrance/Sahi_Pro_Console.png)

## 通过 Sahi 录制脚本
1. 在监控台里面选择一个浏览器，打开浏览器，这里选择 Google Chrome。
![](/images/Automation/Sahi/SahiEntrance/Sahi_Browser_View.png)

2. 你可以在浏览器里面点击 Sahi Controller 打开控制面板，或者使用快捷键：按住ATL键后鼠标左键双击浏览器也能打开控制面板。

3. 选择控制面板的 Record ，打开录制标签页。
![](/images/Automation/Sahi/SahiEntrance/Sahi_Record_Tab.png)

4. 在 Script Name 里面输入 first_script.sah 作为录制脚本名，点击 Record。

5. 在浏览器里面点击 “Sample Application”，你就会打开 Sahi 自带的测试应用。
![](/images/Automation/Sahi/SahiEntrance/recording-sample-app.png)

6. 输入 username 为 “test”，password 为 “secret”，点击 “Login”。
![](/images/Automation/Sahi/SahiEntrance/recording-page1.png)
在 “Evaluate Expression” 框里面，你可以看到被记录的最后一步。

7. 在新的页面里面，展示的是一个购物车场景，在 “Add quantity to cart” 里面分别输入2,3,1 ，然后点击 “Add”。
![](/images/Automation/Sahi/SahiEntrance/recording-page2.png)

## 添加断言（assertions）
一个脚本通常由2部分组成：网页的操作过程和操作过程的校验，对于校验，Sahi 使用断言。Sahi 允许在录制脚本的过程中添加断言。

1. 按住 “CTRL” 键，在网页里面移动鼠标去定位网页元素。
2. 首先我们先把鼠标移动到 “Grand Total” 的输入框，在录制标签页里面，你可以看到 “Accessor” 会拿到当前鼠标定位的网页元素路径。
3. 点击 “Assert” 按钮为当前元素添加断言。
4. 你可以在 “Evaluate Expression” 里面看到程序自动生成的断言。
5. 点击 “Test-->”，可以看到测试结果为 true。
6. 如果没有问题，你可以点击 “Append to Script”，将断言添加到你的脚本里面去。
7. 点击 “Logout” 退出当前应用。
8. 在控制面板里面点击 “Stop” 结束脚本录制。

![Assertions](/images/Automation/Sahi/SahiEntrance/recording-assertions.png)

## 回放脚本
1. 打开 “Playback” 标签页，在 “File” 里面输入你的脚本名字 “first_script.sah”。
2. 输入初始URL，这里为 “ http://sahi.co.in/demo/training/login.html ” 。
3. 点击 “Play” 开始执行录制的脚本。
4. 脚本结束后会在下面显示执行的结果 SUCCESS 或者 FAILURE 。

![](/images/Automation/Sahi/SahiEntrance/controller-playback.png)

## 查看日志
在控制面板的回放标签页下面，点击 “Logs”，可以查看所有脚本跑完后的结果。
