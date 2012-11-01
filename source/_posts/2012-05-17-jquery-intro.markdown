---
layout: post
title: "jQuery 1.7 介绍（上）"
date: 2012-05-17 23:43
comments: true
categories: jQuery
tags: jQuery
---

建议不要看我写的文章，赶快到这里学会时下最火最流行的 jQuery!

[30 天学会jQuery](http://tutsplus.com/course/30-days-to-learn-jquery/)

## 神马是 jQuery？

地球上最受欢迎的 Javascript 函式库、软件攻城狮必备技能之一、网页看起来美妙的魔法之一。

2012.05.17 现在的版本是 1.7.2。

<!--more-->

## 去哪里获得 jQuery

通常有开发版本与生产版本 **32KB** ，建议本地开发使用开发版本 **247KB** ，使用 jQuery 时顺便研读源代码。

> 开发版本：无压缩、带注释；生产版本：压缩过、不堪入目。

[jQuery 官网](http://jquery.com/)

jQuery CDN: [1.7.2 development][172] [1.7.2 production][172-min]

> 不建议使用 CDN，可以参考我的不要使用 CDN 来放第三方 Javascript

## 怎么在 HTML 里面玩弄 Javascript 代码

把 JS 代码放在 script 标签内即可。

```javascript
<script>

</script>
```

## 如何引用 jQuery 至你的 HTML

假设我有一个 app 目录，下面有一个 js 文件夹、一个 index.html，js 目录下有一个 jquery-1.7.1.js。

使用 script 标签引用：

```html
<script src="js/jquery-1.7.1.js"></script>
```

使用 CDN 引用：

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.js"></script>
```

**建议摆放位置** `</body>` 标签的正上方。

理由：浏览器一旦碰到 script 得载入完或下载完才会继续往下载入，所以放在 `</body>` 上方可以确保你的页面先载入 HTML 以及 CSS。

## 第一个 jQuery 代码

### 如何引用 jQuery?

jQuery 其实就是一个函数，你可以这样子引用它：

```javascript
jQuery(...)
```

好，让我们看看怎么让 jQuery 玩弄页面的 CSS。

假设我们有一个 HTML 页面:

```html
<!doctype html>
<html>
<head>
	<meta charset=utf-8>
	<title></title>
	<style>
	.emphasis{ color: green; }
	</style>
</head>
<body>
<ul>
	<li>hello</li>
	<li>hello 2</li>
	<li>hello 3</li>
</ul>
<script src="js/jquery-1.7.1.js"></script>
<script>

</script>
</body>
</html>
```

以下代码添加至 `</body>` 上方的 script 标签。

要怎么样用 jQuery 来添加 CSS 样式？

```javascript
jQuery('ul li');
```

这一行的作用是，你跟 jQuery 说，帮我根据这个 CSS 选择器搜寻一下 DOM。

存到一个变量里，并打印到浏览器的 console 看看：

```javascript
var lis = jQuery('ul li');
console.log(lis);
```

阿哈，你打开浏览器、打开开发者工具，切换到 console tab，会看到

```javascript
[<li>​hello​</li>​, <li>​hello 2​</li>​, <li>​hello 3​</li>​]
```

`console.log()` 可以当之后调试代码的手段之一。

猛阿，基本上只要懂 CSS 选择器，jQuery 几乎都学会了！呵呵。。。

再举个例子，怎么给这些清单元素添加红色呢？

```javascript
jQuery('ul li').css('color','red');
```

> 尽量把所有的样式交给 CSS 来做，你偶尔才会需要用到 jQuery 来更改样式。

另一个例子，给这些清单元素添加 `style` 标签内的 `.emphasis` 这个类：

```javascript
jQuery('ul li').addClass('.emphasis');
```

### 使用缩写引用 jQuery

这一行

```javascript
jQuery('ul li').addClass('.emphasis');
```

等同于

```javascript
$('ul li').addClass('.emphasis');
```

等同于

```javascript
window.jQuery('ul li').addClass('.emphasis');
```

**你怎么知道的！？**

请看 [jQuery 源代码][172]的最下方：

```javascript
// Expose jQuery to the global object
window.jQuery = window.$ = jQuery;
```

呵呵，人家都写在那呢。

这篇就介绍到这儿吧。


[172]: https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.js
[172-min]: https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js