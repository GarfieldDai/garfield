---
title: 计算机网络体系结构
date: 2017-09-10 20:22:59
tags: TCP
categories: Network
thumbnail: "/images/Network/tcp/tcp.jpg"
---
![](/images/Network/tcp/tcp.jpg)

## 目的
主要介绍 TCP/IP 网络体系结构。
<!--more-->

## 简介
计算机网络体系结构有两种，一种是国际标准 OSI（Open Systems Interconnection Reference Model），另一种是目前现行的事实上标准 TCP/IP 协议族（Transmission Control Protocol/Internet Protocol Suite），该协议族还有另一个名字是Internet协议族（Internet Protocol Suite）。

![](/images/Network/tcp/osi.gif)

OSI 由于该协议复杂又不实用等原因，该协议并没有在现实中应用，协议分为七层：
+ 应用层（Application Layer）
+ 表示层（Presentation Layer）
+ 会话层（Session Layer）
+ 运输层（Transport Layer）
+ 网络层（Network Layer）
+ 数据链路层（Data-Link Layer）
+ 物理层（Physical Layer）

TCP/IP 协议族分为四层，本博文只关注上面三层：
+ 应用层（Application Layer）：通过应用进程间的交互来完成特定网络应用。
+ 运输层（Transport Layer)：为两个主机中进程之间的通信提供通用的数据传输服务。该层主要使用两种协议，传输控制协议TCP(Transmission Control Protocol)，和用户数据报协议UDP(User Datagram Protocol)。TCP和UDP是两种最为著名的运输层协议，二者都使用IP作为网络层协议。
+ 网际层（Internet Layer）：也叫网络层或互联网层，为分组交换网上的不同主机提供通信服务，该层使用IP（网际）协议。
+ 网络接口层（Network Interface Layer）：也叫链路层或数据链路层。

![](/images/Network/tcp/tcpip.png)

下图详细的展示了TCP/IP协议族具体内容以及和OSI对应关系。

![](/images/Network/tcp/tcpipprotocols.png)

## 1. 应用层
#### 1.1 HTTP协议
HTTP(HyperText Transfer Protocol)：超文本传输协议，该协议定义了浏览器怎么向服务器请求文档，以及服务器怎么把文档传送给客户端。

#### 1.2 FTP协议
FTP(File Transfer Protocol)：文件传输协议，提供交互式的访问，允许客户指明文件的类型与格式，并允许文件具有存取权限。

#### 1.3 DNS
DNS(Domain Name System)：域名系统，是一个分布式数据库，由它来提供IP地址和主机名之间的映射信息。

#### 1.4 TELNET协议
Telnet(Telecommunication Network Protocol)：是标准的提供远程登陆功能的应用，使用TCP协议连接，几乎每个TCP/IP的实现都提供了这个功能。它能够运行在不同操作系统的主机之间，但是该连接是明文传输口令和数据，并不安全，推荐使用SSH加密进行远程登陆主机。
![](/images/Network/tcp/telnet.png)

#### 1.5 SSH协议
SSH(Secure Shell)：专为远程登录会话和其他网络服务提供安全性的协议。利用SSH协议可以有效防止远程管理过程中的信息泄露问题，可以把所有传输的数据进行加密。

```Shell
可以使用该命令登陆远程服务器
$ ssh root@127.0.0.1
```

#### 1.6 SMTP协议
SMTP(Simple Mail Transfer Protocol)：简单邮件传输协议，它是一组用于由源地址到目的地址传送邮件的规则，由它来控制信件的中转方式。

## 2. 运输层
#### 2.1 TCP协议
TCP(Transmission Control Protocol)：传输控制协议，为两台主机提供高可靠性的数据通信。虽然TCP使用不可靠的IP服务，但是它却提供一种可靠的运输层服务。
+ TCP提供一种面向连接的、可靠的字节流服务。
+ TCP为应用层提供全双工服务，数据能在两个方向上独立地进行传输。
+ TCP建立一个连接需要进行三次握手（three-way handshake)，这一过程与打电话很相似，先拨号振铃，等待对方摘机说“喂”，然后才说明自己是谁。而终止一个连接需要经过四次握手。

使用TCP协议的应用层协议：FTP, TELNET, SSH, HTTP, SMTP

#### 2.2 UDP协议
UDP(User Datagram Protocol)：用户数据报协议，为应用层提供一种非常简单的服务，它只是把称作数据报的分组从一台主机发送到另一台主机，但并不保证该数据报能到达另一端。和TCP不同，UDP是不可靠的，它不能保证数据报能安全无误地到达最终目的。

使用UDP协议的应用层协议：DNS, TFTP, DHCP

#### * 2.3 应用编程接口
使用TCP/IP协议的应用程序通常采用Socket进行网络编程，该编程接口可以使用TCP或UDP进行通信。严格的讲，Socket不是一种协议，而是一种编程方法。

## 3. 网络层
#### 3.1 IP协议
IP是TCP/IP协议族中最为核心的协议。所有的TCP，UDP，ICMP及IGMP数据都以IP数据报格式传输。IP提供不可靠(Unreliable)、无连接(Connectionless)的数据报传送服务，任何要求的可靠性必须由上层来提供（如TCP）。

## 4. Wireshark
可以使用Wireshark配合学习计算机网络各个层的数据包结构，它可以进行数据包抓取，是一款优秀的开源的网络嗅探和数据包分析利器。

参考资料
[TCP/IP Protocols Guide](http://www.tcpipguide.com/free/index.htm)
[Linux Tutorial TCP-IP](http://www.linux-tutorial.info/modules.php?name=MContent&obj=page&pageid=142)
[Wireshark](https://www.wireshark.org)
[Wikipedia Internet protocol suite](https://en.wikipedia.org/wiki/Internet_protocol_suite)
