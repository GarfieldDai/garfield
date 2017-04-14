---
title: Http 缓存
date: 2017-04-10 11:14:00
tags: Cache
categories: Http
thumbnail: "/images/Http/Cache/HttpCaching01.jpg"
---

## 目的
理解什么是 Http 缓存。

<!--more-->

## 简介
在 Web 应用开发中，用户对网页的响应速度要求极高。如果每次刷新页面都要从服务器里面重新拿网页资源（HTML, CSS, Javascript, Image, Video, etc），不仅会影响网页的响应速度，而且也很占用服务器宝贵的带宽资源。

为了解决上述的问题，可以设置 Http 缓存（Http Caching）。在一定的条件范围内，用户重新访问相同的网页资源，只需在浏览器缓存中提取即可，并不需要从服务器中重新获取资源。
![](/images/Http/Cache/HttpCaching01.jpg)
目前所有的现代浏览器都实现了 Http 缓存，你只需要在服务器响应（Response）中设置 Http 协议头 ( Http header) 的参数，确保服务器正确的返回响应的参数。
![](/images/Http/Cache/HttpCaching02.jpg)
在设置缓存的同时，也要注意怎么处理缓存过期，避免用户看到过期的内容。

## 内容
有以下两种设置方式，HTTP cache headers 和 Conditional requests，它们的区别是后者加载资源的时候，会和服务器进行一次请求，如果请求的资源有更新，就重新去服务器加载资源，否则从本地缓存中加载资源，而前者不用和服务器进行请求，只是告诉浏览器怎么加载本地缓存。
### HTTP cache headers:
Http 协议头有两个重要的参数设置 Cache-Control 和 Expires 。
1. Cache-Control ：在设置 Http 缓存的时候，一定要在协议头里面加上 Cache-Control 属性，否则对其他协议头（caching headers）的设置都不会生效。

  ** Public ** ： 表示不仅在用户浏览器端进行缓存，而且在中转代理服务器中（intermediate proxies）也进行缓存。
  `Cache-Control:public`

  ** Privete ** ： 表示只在用户浏览器端进行缓存，一般涉及到用户个人隐私数据的时候使用。
  `Cache-Control:private`

  ** max-age ** : 设置缓存时间长度，单位为秒。
  `Cache-Control:public, max-age=30`
  当前设置是30秒后过期，需要重新去服务器请求资源。

2. Expires ： 这个属性是给缓存指定一个过期的时间点，如果超过当前时间点，需要重新去服务器加载资源。如果 Expires 和 max-age 同时设置，max-age 的优先级更高。
  `Cache-Control:public`
  `Expires: Mon, 25 Jun 2012 21:31:12 GMT`

![](/images/Http/Cache/HttpCaching04.jpg)

### Conditional requests :
Conditional requests 其实就是每次加载资源的时候，都会去服务器询问当前资源是否有更新，如果有，就返回最新的资源。如果没有，就返回 Http 状态码304。虽然每次加载资源都需要请求服务器，但是只要资源没有更新，返回的 response body 是空的，这样也就减轻的带宽的压力，同时也避免用户浏览器缓存更新不及时，看到过期内容的情况。
![](/images/Http/Cache/HttpCaching03.jpg)

1. Time-based : 基于时间的设置
  ** Last-Modified ** ：在第一次加载资源的时候，给当前资源标记最新的时间戳。
  `Cache-Control:public, max-age=30`
  `Last-Modified: Mon, 03 Jan 2011 17:45:57 GMT`

  重新加载资源的时候，浏览器自动会发送缓存资源的时间戳给服务器。
  `If-Modified-Since: Mon, 03 Jan 2011 17:45:57 GMT`
  如果在 * Mon, 03 Jan 2011 17:45:57 GMT * 之前，资源都没有更新，服务器会返回 304 状态码和空的响应体（empty response body）。

2. Content-based ：基于内容的设置
  ** ETag ** (or Entity Tag) ：类似 Last-Modified ，但是它的值是一组字符串（类似 MD5 hash），其实就是给服务器进行校验两个文件是否相同的文件校验码（checksum）。
  `Cache-Control:public, max-age=30`
  `ETag: "15f0fff99ed5aae4edffdd6496d7131f"`

  重新加载资源的时候，浏览器自动会发送文件校验码给服务器。
  `If-None-Match: "15f0fff99ed5aae4edffdd6496d7131f"`
  服务器检测到两个校验码相同，表示当前资源没有更新，服务器会返回 304 状态码和空的响应体（empty response body）。

![](/images/Http/Cache/HttpCaching05.jpg)

## 实践参考
### 静态资源缓存
在网站应用中，如果某些资源（Image，CSS，JavaScript，etc）在可预见的未来不会被更新，建议将 max-age 设置为1年（1年大概有31536000秒） ，并且设置1年后的 Expires 时间点。不建议把时间设置超过1年，参考[RFC](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)。
`Cache-Control:public; max-age=31536000`
`Expires: Mon, 25 Jun 2013 21:31:12 GMT`

### 停用缓存
对于一些资源需要每次都从服务器加载的，或者一些敏感的个人数据不方便缓存的，建议明确的设置缓存停用。因为基于各种不同浏览器的内部实现，很可能会自动帮你做了缓存处理。
`Cache-Control:no-cache, no-store, must-revalidate`

### ETag VS Cache-control Header or Expires
如果仅仅设置Etag，每次页面刷新都会重新对服务器进行请求。ETag 仅仅是为了校验文件是否更新。
`ETag: "15f0fff99ed5aae4edffdd6496d7131f"`

如果设置了max-age，那么在有效期30秒内，浏览器都只从本地缓存中加载资源，不会去请求服务器。
`Cache-Control:public, max-age=30`
`ETag: "15f0fff99ed5aae4edffdd6496d7131f"`

### 组合实现
假设一个情况，一个 CSS 文件你设置了缓存时间为24小时 (max-age=86400)，但是你发现里面有问题，马上进行了修改并且上线，但是客户端并不能马上进行缓存更新，这种情况怎么办？如何能够做到客户端能够长时间的缓存，但是又能够马上进行缓存的更新呢？

![](/images/Http/Cache/HttpCaching06.png)

你可以通过修改 URL 强制用户重新加载资源，类似Etage文件校验码的原理，你可以把校验码放在文件名中，比如 style.x234dff.css。HTML 里面 Cache-Control 设置为 “no-cache”，目的就是让浏览器每次都到服务器拿到最新的代码。通过组合 Etage，Cache-Control 和 URLs，不但能够拥有长时间的缓存，又能够满足对文件修改并及时生效的需求。

参考资料
[Increasing Application Performance with HTTP Cache Headers](https://devcenter.heroku.com/articles/increasing-application-performance-with-http-cache-headers)
[Mozilla : HTTP caching](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching)
[Google : HTTP Caching](https://developers.google.cn/web/fundamentals/performance/optimizing-content-efficiency/http-caching)
[How To Optimize Your Site With HTTP Caching](https://betterexplained.com/articles/how-to-optimize-your-site-with-http-caching/)
[ETag vs Header Expires](http://stackoverflow.com/questions/499966/etag-vs-header-expires)
