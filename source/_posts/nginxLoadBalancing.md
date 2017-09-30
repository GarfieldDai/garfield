---
title: NGINX反向代理和负载均衡
date: 2017-09-27 20:53:11
categories: Server
tags: NGINX
thumbnail: "/images/Server/Nginx/nginx_load.png"
---
![](/images/Server/Nginx/nginx_load.png)

## 目的
如何使用NGINX进行反向代理(Reverse Proxy)和负载均衡(Load Balancing)。

<!--more-->

## 简介
NGINX提供了应用程序的横向扩展(Horizontal Scaling)的能力，使用反向代理和负载均衡来构建应用系统，能够有效的提升系统整体性能，减少响应时间和提高网站安全，同时能够避免因为某个节点宕机而影响整个系统，NGINX支持HTTP，HTTPS，TCP和UDP协议的负载均衡。

## 反向代理 Reverse Proxy
反向代理是指代理服务器将客户端请求转发至不同的服务器，然后将服务器结果返回给客户端。比如百度等大型网站，网站入口只有`www.baidu.com`，但是其背后有成千上万个服务器提供请求服务。
+ 强大的处理并发请求的能力，内存消耗低，高性能。
+ 能够隐藏真实的服务器地址和服务器信息。
+ 由于无法直接访问真实服务器，能够有效的转移DDOS攻击。
+ 代理服务器只能提供有限的权限，请求必须通过代理服务器，不能直接访问真实的服务器。
+ 可以设置代理缓存，提供静态资源缓存服务，提高网站加载速度。
+ 反向代理将请求转发至不同的服务器，可以提高网站的负载能力。

在`location`里面使用`proxy_pass`转发请求。
`/some/path/page.html`将会被代理至`http://www.example.com/link/page.html`。
```xml
location /some/path/ {
    proxy_pass http://www.example.com/link/;
}
```

如下设置可以将路径为`/garfield/`的请求代理至服务器端口为`8090`的应用，并解决资源相对路径无法正确请求的问题。
```xml
location /garfield/ {
  proxy_pass http://www.garfieldwiki.com:8090/;
  proxy_redirect http://$host/ /garfield/;
  proxy_set_header Host $host;
}
```

## 负载均衡 Load Balancing
负载均衡就是根据某种方法，将客户端请求分发至服务器池的不同服务器进行处理。

负载均衡默认方法为轮询，可以使用`upstream`进行服务器池配置。
```xml
http {
    upstream myapp1 {
        server srv1.example.com;
        server srv2.example.com;
        server srv3.example.com;
    }

    server {
        listen 80;
        server_name example.com;

        location / {
            proxy_pass http://myapp1;
        }
    }
}
```

NGINX负载均衡有4种方式：
+ `Round-robin`：按客户端请求顺序分配，默认采用该方式。可以设置权重，权重越高，被分配的请求数越多，默认权重为1。
```xml
upstream backend {
   server backend1.example.com weight=3;
   server backend2.example.com;
   server backend3.example.com;
}
```
+ `least_conn`：将请求优先分配至活跃连接数最少的服务器。
```xml
upstream backend {
    least_conn;

    server backend1.example.com;
    server backend2.example.com;
}
```
+ `ip_hash`：将请求的IP地址通过哈希定位到后端服务器，其后的访问还是在同一台服务器，这样能够保持SESSION信息一致，但是无法保证后端服务器的负载均衡，可能有些服务器接收的请求多，有些接收的请求少。

  如果某个服务器需要临时移除，需要在后面加入`down`参数。如果直接删除该服务器地址，那么将会重新进行哈希计算，请求将重新分配至不同的服务器。
```xml
upstream backend {
    ip_hash;

    server backend1.example.com;
    server backend2.example.com;
    server backend3.example.com down;
}
```
+ `hash`：通过客户端请求的信息进行哈希，可以是IP地址，端口号或者URL。
```xml
upstream backend {
    hash $request_uri consistent;
    # hash $remote_addr$remote_port consistent;

    server backend1.example.com;
    server backend2.example.com;
}
```

参考资料
[Understanding Nginx HTTP Proxying, Load Balancing, Buffering, and Caching](https://www.digitalocean.com/community/tutorials/understanding-nginx-http-proxying-load-balancing-buffering-and-caching)
[NGINX LOAD BALANCING – HTTP LOAD BALANCER](https://www.nginx.com/resources/admin-guide/load-balancer/)
[Using nginx as HTTP load balancer](http://nginx.org/en/docs/http/load_balancing.html)
[NGINX REVERSE PROXY](https://www.nginx.com/resources/admin-guide/reverse-proxy/)
