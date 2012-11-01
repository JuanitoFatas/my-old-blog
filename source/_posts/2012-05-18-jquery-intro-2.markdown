---
layout: post
title: "jQuery 1.7 介绍（下）"
date: 2012-05-18 00:31
categories: jQuery
tags: jQuery
---

建议不要看我写的文章，赶快到这里学会时下最火最流行的 jQuery!

[30 天学会jQuery](http://tutsplus.com/course/30-days-to-learn-jquery/)

## ＄号

我希望你还记得 `$` 号是什么：

<!--more-->

	window.jQuery = window.$ = jQuery;

拿来引用 jQuery 函数的快捷方式。

首先讲 jQuery 之前，假定我们有一个 HTML 文件：

```html
<!doctype html>
<html>
<head>
	<meta charset=utf-8>
	<title></title>
	<style>
	.emphasis { font-weight: bold;}
	</style>
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.js"></script>
	<script>

	</script>
</head>
<body>
<ul>
	<li>hello</li>
	<li>hello 2</li>
	<li>hello 3</li>
</ul>

</body>
</html>
```

下面讲述的代码请填入 `</head>` 上方的 script 标签内。

OK. 开始。

假设我们要取得 `ul` 的第一个 `li`：

```javascript
$('li:first-child').addClass('emphasis');
```

打开你的浏览器看看，干，怎么不行，这是因为。。。

你的代码放在 head 标签内，下面的 HTML 都还没有载入完毕 (DOM)，就执行了这行代码，执行代码的时候，这会儿根本还没有看到 ul li 呢。

你可以把 `<script> ... </script>` 搬到 `</body>` 上方，这样就可以了。要是你很坚持你的代码要放在 head 标签内，没问题，使用 jQuery 的 ready 函数：

```javascript
var foo = function() {};
$(document).ready(foo);
```

`$(document)` 叫 jQuery 去把 DOM 抓出来。

等到 document 载入完毕，准备好要给我们玩弄的时候，执行 `ready` 函数内的 `foo` 函数。

更简洁的写法、传入匿名函数、或叫回呼函数 (callback function)：

```javascript
$(document).ready(function() {

});
```

接下来在这个匿名函数内放入我们之前想做的事儿：

```javascript
$(document).ready(function() {
		$('li:first-child').addClass('emphasis');
});
```

这个 ready 函数会大概每 10 ms 去检查 DOM 准备好给我们玩弄了没，准备好了就执行里面的函数。

把 `$(document).ready()` 变得更简洁一点：

```javascript
$(function() {
	$('li:first-child').addClass('emphasis');
});
```

好了，好奇的你又问了，这是为什么？

请看 [jQuery 源代码][172]，搜索这个关键字 `jQuery.fn = jQuery.prototype = {`

这下面一整段代码，说明了我们调用 jQuery 函数 `$()` 时，碰到选择器、函数、上下文时该怎么处理。

好，我们现在是传入了一个函数：

```javascript
$(function() {
	$('li:first-child').addClass('emphasis');
});
```

看到没有，`$( function() { ... } )`，我们来找找处理传入函数的源代码，一直往下找：

```javascript
// HANDLE: $(function)
// Shortcut for document ready
} else if ( jQuery.isFunction( selector ) ) {
	return rootjQuery.ready( selector );
}
```

阿哈，这里写的明明白白，document ready 的缩写。

这里的 `selector` 就是我们所传入的：

```javascript
function() {
	$('li:first-child').addClass('emphasis');
}
```

而它说:

```javascript
if ( jQuery.isFunction( selector ) ) {
	return rootjQuery.ready( selector );
}
```

如果传入的 `selector` 是函数的话，返回 `rootjQuery.ready( selector );`

呵呵。。。所以这两段代码是等效的：

```javascript
$(document).ready(function() {
	$('li:first-child').addClass('emphasis');
});

$(function() {
	$('li:first-child').addClass('emphasis');
});
```

很多人觉得使用第二种这个缩写不太好，第一种的可读性比较高，这是你个人的选择，如果你知道你在干什么，两个都很好。

本篇结束。

[172]: https://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.js









