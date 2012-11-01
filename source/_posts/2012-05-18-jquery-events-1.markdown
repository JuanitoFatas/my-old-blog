---
layout: post
title: "jQuery 事件简介（上）"
date: 2012-05-18 22:11
comments: true
categories: jQuery
tags: jQuery
---

什么是事件？

比如一个链接被按下、鼠标悬停在某元素上面，这都是事件。

假设今天我们想要实现，按下某个按钮套用不同的 CSS。

给定一个 HTML:

<!--more-->

```html
<!doctype html>
<html>
<head>
	<meta charset=utf-8>
	<title>jQuery 事件（上）</title>
	<link rel="stylesheet" href="day.css">
</head>
<body>

<h1>我的网站</h1>

<button>Day</button>
<button>Night</button>

<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js"></script>
<script>

</script>

</body>
</html>
```

以及两个 CSS, day.css, night.css:

#### night.css

```css
body {
	background: black;
	color: white;
}
```

#### night.css

```css
body {
	background: yellow;
}
```

下面讲述的代码请加至 `</body>` 上方的 script 标签内。


当按下 Day 按钮的时候要套用 day.css、按下 Night 按钮的时候要套用 night.css。

OK. 我们要怎么达到我们想做的功能呢？第一是我们要有一个监听按钮状态的方法，给按钮加上 event listener。

```javascript
(function(){

})();
```

首先这个奇怪的:

```javascript
(function(){

})();
```

是什么？这是一个 **自调用函数** (self invoke function)。

可以想成是这样子:

```javascript
function myFunc(){

}

myFunc();
```

这里宣告了 `myFunc()` ，在碰到这一行： `myFunc();` 的时候才会调用。

所以：

```javascript
(function(){

})();
```

一但载入这个 script 时，就会调用。

OK. 让我们继续往下看，那要怎么加入 event listener 呢？

## click() 函数

```javascript
(function(){
	$('button').click(function() {
		console.log('button was clicked!');
	});
})();
```

这跟 jQuery 说，哈罗，去 DOM 里帮我把 button 的元素都找出来，并在按下时在 cosole 记录信息：`'button was clicked!'`

你可以去浏览器试试看是否成功。

现在我们知道如何加入一个 click 事件，现在让我们看看如何在按下按钮时，换一个 CSS 样式表。

```javascript
(function(){
	$('button').click(function() {
		console.log('button was clicked!');
	});
})();
```

## this?

现在让我们简单的看一下 this。

```javascript
(function(){
	$('button').click(function() {
		console.log(this);
	});
})();
```

这里的 `this` 会参照到现在被按的这个按钮。但是要注意的是，这个 `this` 所返回的 **不是** 一个 jQuery 对象，仅是一个 DOM 对象，所以无法继续使用 jQuery 所提供的函数。

那如果我想要使用 *this* 来得到参照的对象，又想继续使用 jQuery 提供的函数呢？我们可以用 `$()` 把返回的 DOM 对象包起来：

`$(this)` 呵呵，这样大概理解了吧？

有的时候，我们可能常常要用到 `$(this)` ，用到两次以上的东西，都用个变量存起来，来避免 jQuery 一直跑到 DOM 查询，假设我们一个页面有三十个按钮，一直重复的去查询 DOM 会大幅降低效能。

比如说上面我们改变了被参照的对象的 text()，之后又替它加上一个类，之后可能又移除那个类：

```javascript
(function(){
	$('button').click(function() {
		$(this).text(...);

		// some code goes here...
		$(this).addClass(...);

		// ...other codes
		$(this).removeClass(...);
	});
})();
```

可以这样子重构代码：

```javascript
(function(){
	$('button').click(function() {
		$this = $(this);
		$this.text(...);

		// some code goes here...
		$this.addClass(...);

		// ...other codes
		$this.removeClass(...);
	});
})();
```

`$this` 前面的 **$** 号可以表明这是一个 jQuery 对象，this 可以代表是现在所参照的对象。

这 `$this` 称为是现在参照的对象 `this` 的缓存版本 (cached version)。

## attr()

现在回到我们刚刚的问题，如何按下按钮时，改变 CSS 样式表：

```javascript
(function(){
	$('button').click(function() {
		$('link').attr('href', 'night.css');
	});
})();
```

这个 `attr()` 当传入一个参数时，返回这个参数名字的属性:

```javascript
var href = $('link').attr('href');
```

我们就可以取得一个 link 的 href 属性。

传入两个参数时，是替第一个参数为名的属性设值:

```javascript
$('link').attr('href', 'night.css');
```

OK. 现在到浏览器试试看，你会发现无论按下哪个按钮时，样式表都会换成 night.css。

这样不行，我们要有一个办法来指定按下 day 按钮时，换成 day.css。

让我们试试看：

```javascript
(function(){
	$('button').click(function() {
		var stylesheet = $(this).text().toLowerCase();
		$('link').attr('href', stylesheet + '.css');
	});
})();
```

这样子在按下按钮时，我们得到按下按钮的 text，并转成小写，并替换 link 的 href。

这样是可以工作的，但是会被按钮的 text 限制了 css 文件的名字，以及有很大的不弹性，让我们看看怎么样做的更好：

改动 HTML：

```html
<button data-file="day">Day</button>
<button data-file="night">Night</button>
```

加上 `data-file` 属性。

也可以自定义属性，只要前缀是 `data-` 即可，比如 `data-yourCustomAttr`。

要取得这个 `data-file`，我们可以用刚刚学过的 `attr()`，仅传入一个参数：

```javascript
(function(){
	$('button').click(function() {
		var stylesheet = $(this).attr('data-file');
		$('link').attr('href', stylesheet + '.css');
	});
})();
```

但是 jQuery 有一个更好的方法：`data()`：

```javascript
$(this).data('file');
```

这里因为用的是，`data()` 方法，所以不需要使用多馀的 `data-` 前缀。

看看这行：

```javascript
$('link').attr('href', stylesheet + '.css');
```

每次我们按下按钮时，jQuery 都会跑到 DOM 里面去寻找符合选择器条件的元素，这样非常的没有效率，所以我们可以缓存起来：

```javascript
(function(){
	var $link = $('link');
	$('button').click(function() {
		var stylesheet = $(this).attr('data-file');
		$link.attr('href', stylesheet + '.css');
	});
})();
```

现在另一个问题来了，当前是 day.css，按下 night 按钮时，会换成 night.css，换成 night.css 再按下 night 按钮时，还是会调用这个自调用函数，并换成 night.css，这样子还是浪费资源，我们可以：

* 停用当前 CSS 的按钮（day.css 就停用 day 按钮、night.css 就停用 night 按钮）

* 写一个判断式侦测按下按钮是否为现下的 CSS，是的话就不做任何事，不是的话替换成另一个 CSS。

我们试试看第一个方法：

```javascript
(function(){
	var $link = $('link');
	$('button').click(function() {
		var $this = $(this);
		var stylesheet = $this.attr('data-file');
		$link.attr('href', stylesheet + '.css');
		$this.attr('disabled', 'disabled');
	});
})();
```

这边我们缓存了用到两次的 `$(this)` : `$this`。

记得 `attr()` 一个参数是返回属性、两个是设值：

```javascript
$this.attr('disabled', 'disabled');
// 等同于
$this.attr('disabled', '');
```

传入第二个参数是为了设值的目的。

你到浏览器试试看会发现一旦 disabled 以后，按钮就死了，回不去了。

## siblings()

`siblings()` 可以取得目前参照对象的 siblings (同层元素)，可以选择性的传入选择器来筛选匹配的元素。

> Get the siblings of each element in the set of matched elements, optionally filtered by a selector.

```javascript
(function(){
	var $link = $('link');
	$('button').click(function() {
		var $this = $(this);
		var stylesheet = $this.attr('data-file');

		$this.siblings('button').removeAttr('disabled');

		$link.attr('href', stylesheet + '.css');
		$this.attr('disabled', 'disabled');
	});
})();
```

哎呀，又发现一个可以重构的地方：

```javascript
var $this = $(this);
var stylesheet = $this.attr('data-file');
```

尽量使用单一个 var 来宣告变量：

```javascript
var $this = $(this),
		stylesheet = $this.attr('data-file');
```

并把相同的代码放在一起、把 `$link.attr(...)` 移上去，这样下面那行就可以结合：

```javascript
(function(){
	var $link = $('link');
	$('button').click(function() {
		var $this = $(this),
				stylesheet = $this.attr('data-file');

		$link.attr('href', stylesheet + '.css');

		$this
				.siblings('button').removeAttr('disabled')
				.removeAttr('disabled');

		$this.attr('disabled', 'disabled');
	});
})();
```

如果这样是不行的：

```javascript
	$this
			.siblings('button').removeAttr('disabled')
			.removeAttr('disabled')
			.attr('disabled', 'disabled');
```

因为这时第三行 `.attr('disabled', 'disabled');` 所参照的是 `siblings()` 而不是本来按下的按钮。

## end() 函数

如果想要这样子写的话，可以使用 jQuery 的 `end()` 函数。

> End the most recent filtering operation in the current chain and return the set of matched elements to its previous state.

终止最近的过滤操作，并返回到先前匹配的状态：

```javascript
	$this
			.siblings('button').removeAttr('disabled')
				.removeAttr('disabled')
				.end()
			.attr('disabled', 'disabled');
```

再提一下，这个 `click()` 函数也可以换成 `on()` ：

```javascript
$('button').click(function() { ... }) // 等同于
$('button').on('click', function() { ... })
```

我会建议你使用 jQuery 的 `on()` 函数，这个理由下集再谈吧。

有问题、讲错的欢迎下面留言发问。