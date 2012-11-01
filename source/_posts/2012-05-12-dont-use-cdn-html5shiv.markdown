---
layout: post
title: "不要使用 CDN 来放第三方 Javascript"
date: 2012-05-12 17:33
comments: true
categories: HTML5
tags: HTML5
---

[HTML5shiv](http://code.google.com/p/html5shiv/) 是一个让 IE 8 启用 HTML5 元素的第三方 JS，通常 CDN 引用的链接是：

http://html5shiv.googlecode.com/svn/trunk/html5.js

不要这么做的理由：

<!--more-->

1. 没有使用 HTTP 压缩

2. 没有 cached，通常这个文件只缓存 180 秒。

3. googlecode.com 不支援 partial response (可以提高效能的东东)

4. 你连到别人的地方，无法控制什么事情会发生，说不定那哥儿们不爽了直接删掉。。。

5. 实际上压缩后才 1200 Bytes，造成很多额外的 Overhead (DNS lookup, TCP handshake...etc.)

原始文章：[html5shiv and Serving Content From Code Repositories][no-cdn]


[no-cdn]:http://zoompf.com/blog/2012/05/html5shiv-and-serving-content-from-code-repositories



