---
title: Ubuntu 实用小工具
date: 2017-04-13 22:10:37
categories: Linux
tags: Ubuntu
thumbnail: "/images/Linux/Ubuntu/Ubuntu.png"
---
![](/images/Linux/Ubuntu/Ubuntu.png)

## 目的
本文章主要介绍一些在 Ubuntu 操作系统里面常用的一些工具，这些工具在日常的开发和学习中，能够给你很大的便利。本系统版本为 Ubuntu 16.04 LTS 64位 英文版。

<!--more-->

### 截图工具 （ Screenshot ）
1. 点击左侧工具栏的 Ubuntu 图标，输入 Screenshot 即可找到软件。
2. 该工具提供了3种不同选项，抓取全屏、抓取当前窗口和随意截屏。
3. 你也可以设置定时器，然后点击 Take Screenshot 即可截屏。
4. 你也可以使用快捷键进行操作。
  + PrtSc : 抓取全屏
  + Alt + PrtSc : 抓取当前窗口
  + Shift + PrtSc : 随意截屏

### 远程桌面客户端 （ Remmina Remote Desktop Client ）
1. 点击左侧工具栏的 Ubuntu 图标，输入 Remmina Remote Desktop Client 即可找到软件。
2. 打开后，点击 New 弹出设置窗口。
3. 设置 Name 给当前连接命名，设置连接协议 Protocol 为 SSH-Secure Shell, Server 为你的服务器IP地址，User name 为主机登录账户，选择 Password，然后点击 Connect 后输入密码即可连接到远程服务器。

### 左侧任务栏切换
1. 将左侧的任务栏切换到底部，跟Window一致。
```bash
gsettings set com.canonical.Unity.Launcher launcher-position Bottom
```
2. 恢复左侧任务栏。
```bash
gsettings set com.canonical.Unity.Launcher launcher-position Leftd
```
