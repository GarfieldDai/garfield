---
title: HTTP Message
date: 2017-09-12 09:53:24
categories: Network
tags: Http
thumbnail: "/images/Network/Http/Message/fetchMessage.png"
---
![](/images/Network/Http/Message/fetchMessage.png)

## 目的
讲解HTTP/1.1报文格式，简单介绍HTTP协议版本的演变。

<!--more-->

## 简介
HTTP(HyperText Transfer Protocol)：超文本传输协议，该协议定义了浏览器怎么向服务器请求文档，以及服务器怎么把文档传送给客户端，该协议由Tim Berners-Lee在1989-1991年制定，使用TCP协议进行数据传输。

![](/images/Network/Http/Message/httpLayer.png)

## HTTP请求过程
浏览器是怎么向服务器请求资源？
1. 浏览器从URL中解析出服务器的主机名。
2. 浏览器将服务器的主机名通过DNS域名解析，转换成服务器的IP地址。
3. 浏览器将端口号从URL中解析出来，如果没有，就默认为80端口号。
4. 浏览器建立一条与Web服务器的TCP的连接。
5. 浏览器向服务器发送一条HTTP请求报文。
6. 服务器向浏览器回送一条HTTP响应报文。
7. 关闭连接，浏览器解析渲染文档给用户。

## HTTP报文(Message)
HTTP/1.1以及更久之前都使用纯文本的报文，可以直接阅读。HTTP有两种报文格式，分别是request message请求报文和response message响应报文。

两种报文结构类似，由以下组成：
+ 起始行(Start-Line)
+ 首部(HTTP headers)
+ 空行(Empty-Line)：HTTP首部总是应该以一个空行CRLF结束，即使没有首部和主体也是如此。
+ 主体(Body)
![](/images/Network/Http/Message/HTTPMsgStructure.png)

## HTTP Request
![Request Message](/images/Network/Http/Message/request.png)

#### 起始行 Start line
HTTP请求报文是从客户端发往服务器，起始行有三个字段组成，所有字段使用一个空格进行隔开：
1. 请求方法(Method)：表示请求服务器的方式，常用的有GET和POST两种方法。如果基于RESTful的架构设计，GET用来获取资源，POST用来新建资源或更新资源，PUT用来更新资源，DELETE用来删除资源。
2. 资源路径(Path)：通常是一个URL，可以是相对路径、绝对路径。可以在路径后面添加查询参数，一般用于表单提交或者异步请求。
3. HTTP版本(Version of the protocol)：显示当前使用的HTTP版本，通常是HTTP/1.1。

#### 首部 Headers
每个首部都包含一个名字，使用英文冒号`:`进行隔开。请求报文有三类首部：
+ 请求首部(Request Headers)：提供有关请求的信息。
+ 通用首部(General Headers)：既可出现在请求报文，也可出现在响应报文。可以在客户端或者服务器之间提供一些通用的功能。
+ 实体首部(Entity Headers)：描述主体的长度和内容，或者资源自身。
![](/images/Network/Http/Message/requestHeaders.png)

#### 主体 Body
主体放置着需要发送给服务器的信息，并不是所有的请求报文都有主体，如GET、HEAD、DELETE和OPTIONS就没有。POST和PUT就有主体。主体信息在浏览器上对用户不可见，一般账户登录的信息都是放在主体里面发送，表单提交默认使用POST。

## HTTP Response
![Response Message](/images/Network/Http/Message/response.png)

#### 起始行 Start line
HTTP响应报文是从服务器发往客户端，起始行也有三个字段组成，所有字段使用一个空格进行隔开：
1. HTTP版本(Version of the protocol)：显示当前使用的HTTP版本，通常是HTTP/1.1。
2. 状态码(Status Code)：表示当前请求成功或者失败。常见有200，404和302。
  + 100~199 信息提示
  + 200~299 成功
  + 300~399 重定向
  + 400~499 客户端错误
  + 500~599 服务器错误
3. 状态信息(Status Message)：一段简短的描述状态码意义的文本。
如`HTTP/1.1 404 Not Found`表示找不到资源。

#### 首部 Headers
响应报文也有三类首部：
+ 响应首部(Response Headers)：提供有关响应的信息。
+ 通用首部(General Headers)：同上。
+ 实体首部(Entity Headers)：同上。
![](/images/Network/Http/Message/responseHeaders.png)

#### 主体 Body
主体放着服务器返回给客户端的信息，并不是所有的响应报文都有主体，如状态码是201，204就没有。

## HTTP协议版本的演变
HTTP到目前为止经历了四次版本演变。

#### HTTP/0.9
该版本非常简单，request只有一行，只有GET请求，后面跟着资源路径，只能传输HTML文件。
```
GET /mypage.html
```
response也非常简单，只有HTML内容本身。
```
<HTML>
A very simple HTML page
</HTML>
```

#### HTTP/1.0
增加了协议版本号(Version of the Protocol)，状态码(Status Code)，状态信息(Status Message)，HTTP头部(header)和内容类型(Content-Type)，可以传输其他类型的文件。
```
GET /mypage.html HTTP/1.0
User-Agent: NCSA_Mosaic/2.0 (Windows 3.1)

200 OK
Date: Tue, 15 Nov 1994 08:12:31 GMT
Server: CERN/3.0 libwww/2.17
Content-Type: text/html
<HTML>
A page with an image
  <IMG SRC="/myimage.gif">
</HTML>
```

请求gif格式的图片
```
GET /myimage.gif HTTP/1.0
User-Agent: NCSA_Mosaic/2.0 (Windows 3.1)

200 OK
Date: Tue, 15 Nov 1994 08:12:32 GMT
Server: CERN/3.0 libwww/2.17
Content-Type: text/gif
(image content)
```

#### HTTP/1.1
初次标准化的HTTP协议，发布于1997年1月，仅仅在HTTP/1.0发布后几个月。对比之前的版本，该版本有了很多新的特性。该协议经过两个修订，一直沿用到至今20年(本博文写于2017年)。
```
GET /en-US/docs/Glossary/Simple_header HTTP/1.1
Host: developer.mozilla.org
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:50.0) Gecko/20100101 Firefox/50.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://developer.mozilla.org/en-US/docs/Glossary/Simple_header

200 OK
Connection: Keep-Alive
Content-Encoding: gzip
Content-Type: text/html; charset=utf-8
Date: Wed, 20 Jul 2016 10:55:30 GMT
Etag: "547fa7e369ef56031dd3bff2ace9fc0832eb251a"
Keep-Alive: timeout=5, max=1000
Last-Modified: Tue, 19 Jul 2016 00:59:33 GMT
Server: Apache
Transfer-Encoding: chunked
Vary: Cookie, Accept-Encoding

(content)


GET /static/img/header-background.png HTTP/1.1
Host: developer.cdn.mozilla.net
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:50.0) Gecko/20100101 Firefox/50.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://developer.mozilla.org/en-US/docs/Glossary/Simple_header

200 OK
Age: 9578461
Cache-Control: public, max-age=315360000
Connection: keep-alive
Content-Length: 3077
Content-Type: image/png
Date: Thu, 31 Mar 2016 13:34:46 GMT
Last-Modified: Wed, 21 Oct 2015 18:27:50 GMT
Server: Apache

(image content of 3077 bytes)
```

#### HTTP/2.0
经过了这么多年的发展，网页已经变得非常复杂，大量的多媒体应用，脚本交互和数据传输，这种富客户端的状况有增无减，使得应用性能瓶颈日益明显。为了应对这种状况，HTTP/2.0协议于2015年5月正式发布，截止2017年5月，13.7%的前1000万名的网站支持HTTP/2.0。比起HTTP/1.1版本使用纯文本数据传输，2.0版本使用二进制格式进行数据传输。

参考资料
[An overview of HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)
[HTTP Messages](https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages)
[Evolution of HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Evolution_of_HTTP)
[Wikipedia HTTP/2](https://en.wikipedia.org/wiki/HTTP/2)
