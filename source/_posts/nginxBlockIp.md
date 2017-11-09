---
title: NGINX如何禁止或者限制IP访问
date: 2017-11-09 15:59:32
categories: Server
tags: NGINX
thumbnail: "/images/Server/Nginx/ddos.jpg"
---
![](/images/Server/Nginx/ddos.jpg)

## 目的
如果服务器被DDOS攻击，可以有效解决服务器压力。

<!--more-->

## 内容
+ NGINX使用`ngx_http_access_module`模块进行IP访问控制。语法如下:
  ```
  deny ipAddress;
  allow ipAddress;
  deny all;
  allow all;
  ```

+ 建立黑名单。
  1. 编辑`nginx.conf`文件，添加内容。
  ```
  include blacklist.conf
  ```
  2. 新建文件`blacklist.conf`，填写拉黑的IP地址。
  ```
  #屏蔽单个IP的命令是
  deny 123.45.6.7;
  #封整个段即从123.0.0.1到123.255.255.254的命令
  deny 123.0.0.0/8;
  #封IP段即从123.45.0.1到123.45.255.254的命令
  deny 124.45.0.0/16;
  #封IP段即从123.45.6.1到123.45.6.254的命令是
  deny 123.45.6.0/24;
  ```

+ 建立白名单，如果你希望自己的服务器仅提供给特定的IP使用。
  1. 编辑`nginx.conf`文件，添加内容。
  ```
  include whitelist.conf
  ```
  2. 新建文件`whitelist.conf`，填写可以访问的IP地址。
  ```  
  allow 1.2.3.4;   # 可以访问的IP，规则跟上面相同
  deny all;        # 禁止所有人访问
  ```


+ 特定的路径，设置特定的访问规则。
  ```
  location /private/ {
    allow 100.23.45.14;
    deny all;
  }
  ```

+ 如果IP被禁，服务器返回403错误，编辑`nginx.conf`，设置403提醒页面。
  ```
  error_page   403  /error403.html;
  ```

参考资料
[ngx_http_access_module](http://nginx.org/en/docs/http/ngx_http_access_module.html)
[Limiting Access to Proxied HTTP Resources](https://www.nginx.com/resources/admin-guide/restricting-access/)
[Nginx Block And Deny IP Address OR Network Subnets](https://www.cyberciti.biz/faq/linux-unix-nginx-access-control-howto/)
[Blocking/allowing IP-addresses in Nginx](https://support.hypernode.com/knowledgebase/blocking-allowing-ip-addresses-in-nginx/)
