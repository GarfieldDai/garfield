---
title: Http Caching
date: 2017-04-10 11:14:00
tags: Cache
categories: Http
thumbnail: "/images/Http/Cache/HttpCaching01.jpg"
---

## 目的
理解什么是 Http 缓存。

## 简介
在 Web 应用开发中，用户对网页的响应速度要求极高。如果每次刷新页面都要从服务器里面重新拿网页资源（HTML, CSS, Javascript, Image, Video, etc），不仅会影响网页的响应速度，而且也很占用服务器宝贵的带宽资源。

为了解决上述的问题，可以设置 Http 缓存（Http Caching）。在一定的条件范围内，用户重新访问相同的网页资源，只需在浏览器缓存中提取即可，并不需要从服务器中重新获取资源。
![](/images/Http/Cache/HttpCaching01.jpg)
目前所有的现代浏览器都实现了 Http 缓存，你只需要在服务器响应（Response）中设置 Http 协议头 ( Http header) 的参数。
![](/images/Http/Cache/HttpCaching02.jpg)

## 内容
有以下两种设置方式，HTTP cache headers 和 Conditional requests，它们的区别是后者加载资源的时候，会和服务器进行一次确认，如果请求的资源有更新，就重新去服务器请求资源，否则从本地缓存中加载资源，而前者不用和服务器确认。
### HTTP cache headers:
Http 协议头有两个重要的参数设置 Cache-Control 和 Expires 。
1. Cache-Control ：在设置 Http 缓存的时候，一定要在协议头里面加上 Cache-Control 属性，否则所有对 Http 缓存进行设置的操作都无效。

  ** Public ** ： 表示缓存不仅在用户浏览器端进行缓存，而且在中转代理服务器中（intermediate proxies）也进行缓存。
  `Cache-Control:public`

  ** Privete ** ： 表示只在用户浏览器端进行缓存。
  `Cache-Control:private`

  ** max-age ** : 设置缓存时间长度，单位为秒。
  `Cache-Control:public, max-age=30` 当前设置是30秒后过期，需要重新去服务器请求资源。

2. Expires ： 这个属性是给缓存指定一个过期的时间点。如果 Expires 和 max-age 同时设置，max-age 的优先级更高。
  `Cache-Control:public`
  `Expires: Mon, 25 Jun 2012 21:31:12 GMT`

### Conditional requests :


参考资料
[Increasing Application Performance with HTTP Cache Headers](https://devcenter.heroku.com/articles/increasing-application-performance-with-http-cache-headers)
[Mozilla : HTTP caching](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching)
[Google : HTTP Caching](https://developers.google.cn/web/fundamentals/performance/optimizing-content-efficiency/http-caching)
[How To Optimize Your Site With HTTP Caching](https://betterexplained.com/articles/how-to-optimize-your-site-with-http-caching/)
