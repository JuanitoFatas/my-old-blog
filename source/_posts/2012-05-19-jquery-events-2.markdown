---
layout: post
title: "jQuery 事件简介（下）"
date: 2012-05-19 02:40
comments: true
categories: jQuery
tags: jQuery
---

注意，若是看不到下方的图片请留言，我再换到 GFW 友好的 HOST 服务上。

其实下面也就一张图。。。

OK，现在你有了基本的事件知识，现在我们看看如何实现一个简单的 FAQ，

<!--more-->

给定一个 HTML:

```html
<!doctype html>
<html>
<head>
	<meta charset=utf-8>
	<title>jQuery 事件（下）</title>
	<link rel="stylesheet" href="style.css">
</head>
<body>

<dl>
	<dt>FAQ 问题一</dt>
	<dd>答案一</dd>
	<dt>FAQ 问题二</dt>
	<dd>答案二</dd>
	<dt>FAQ 问题三</dt>
	<dd>答案三</dd>
	<dt>FAQ 问题四</dt>
	<dd>答案四</dd>
	<dt>FAQ 问题五</dt>
	<dd>答案五</dd>
</dl>

<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js"></script>
<script>

</script>
</body>
</html>
```

以及一些简单的 CSS 样式 **style.css** :

```css
body {
    width: 960px;
    margin: auto;
    text-align: center;
}

dd {
    margin: 0;
    padding: 1em 0;
}

dt {
    cursor: pointer;
    font-weight: bold;
    font-size : 1.5em;
    line-height: 2em;
    background: #b94846;
    border-bottom: 2px solid #6f2b2a;
    border-top: 2px solid white;
}

dt:first-child { border-top: none; }
dt:nth-last-child(2) { border-bottom: none; }

.hide { display: none;}
```

注意 `dt` 下方我们用了一个较深的红色 border，上方用白色 border，来与别的区块做区别。

```css
dt:first-child { border-top: none; }
dt:nth-last-child(2) { border-bottom: none; }
```

第一行是，最上方的 FAQ 有多馀的白色 border，因为没有上方元素，不需要加上白色来区别。

第二行是，最下方的 FAQ 有多馀的红色 border，因为是最后的元素，不需要加上红色来区别。

我用 `2px` 让它看起来更明显，实际上你可以使用 `1px`，或是你喜欢的大小。

你可能会使用 `dt:last-child` ，这是不对的，请参考我的这篇文章：[CSS 一个常见 Nth-child 的误区](http://blog.lisp.tw/blog/2012/05/12/nth-child-common-gotcha/)

{% img https://img.skitch.com/20120518-jgbpd1k1i2cjwt5eq7g31cf5gd.png %}

当我们鼠标悬停至 FAQ 标题时 (`dt`)，就显示相对应的答案 (`dd`)。

*下面讲述的代码请放至 `</body>` 上方的 script 标签内。*

## hide() show() fadeIn() slideDown() toggle()

好，现在让我们看看如何做到隐藏的效果:

```javascript
(function(){
	var $dd = $('dd');

	$dd.hide();
	// $dd.toggle();
	// $dd.show();
	// $dd.fadeIn();
	// $dd.slideDown();
})();
```

你可以试试看我放在注解里的代码，看看是什么效果。

> toggle() 可视变不可视、不可视变可视。

当我们使用 `dd.hide()` 的时候，实际上 jQuery 是把 `dd` 加上 `style="display: none;"`

第二种方法是先写一个 CSS 类别 `.hide { display: none; }`，把选中的元素添加类上去：

```javascript
`$dd.addClass('hide');
```

## filter()

OK。现在我们知道如何先把答案藏起来，不过通常用户来到我们页面时，我们通常会想显示第一个问题及第一个答案：

```javascript
(function(){
	var $dd = $('dd');
	$dd.(':nth-child(n+4)').addClass('hide');
})();
```

filter() 函数根据你传入的选择器，返回匹配的元素。

这个博大精深的 `:nth-child(n+4)` 是啥？看起来好可怕！DONT PANIC! 这是 CSS3 选择器，这其实是说，我要选中由第 4 个开始的所有元素，也就是

```html
<dl>
	<dt>FAQ 问题一</dt>
	<dd>答案一</dd>
	<dt>FAQ 问题二</dt>
	<dd>答案二</dd>
	<dt>FAQ 问题三</dt>
	<dd>答案三</dd>
	<dt>FAQ 问题四</dt>
	<dd>答案四</dd>
	<dt>FAQ 问题五</dt>
	<dd>答案五</dd>
</dl>
```

1, 2, 3, 4，选中 `<dd>答案二</dd>` 以及之后所有的元素。你可以试试看 console.log 一下，看看 `dd.(':nth-child(n+4)')` 选中的是什么，你就理解了。


OK. 讲解到这里，差不多 HTML CSS 都讲明白了，接下来看看怎么绑定事件上元素，来实现我们想要的功能。

## mouseenter() siblings()

先讲简单的方法：

```javascript
(function(){
	var $dd = $('dd');
	$dd.(':nth-child(n+4)').addClass('hide');

	$('dt').on('mouseenter', function() {
		$(this).next().show();
	});
})();
```

我们给 `dt` 绑定一个 mouseenter 事件，在鼠标进入 `dt` 时，我们知道 `dd` 是 `dt` 的下一个，我们显示它：

```javascript
$(this).next().show();
```

但是显示完我们还得隐藏它：

```javascript
(function(){
	var $dd = $('dd');
	$dd.(':nth-child(n+4)').addClass('hide');

	$('dt').on('mouseenter', function() {
		$(this).next().siblings('dd').hide();
		$(this).next().show();
	});
})();
```

我们鼠标移到某个特定 `dt` 时，把所有 `dd` 的 `siblings('dd')` 都隐藏起来就可以了。

注意到我故意使用重复的代码，让我们重构它：

```javascript
(function(){
	var $dd = $('dd');
	$dd.(':nth-child(n+4)').addClass('hide');

	$('dt').on('mouseenter', function() {
		$(this)
			.next()
				.show()
				.siblings('dd')
					.hide();
	});
})();
```

看你是要排成一行，还是像我这样有缩排，喜好问题。

OK. 成功拉，现在让我们加上 animation，与其隐藏，我们可以使用 `slideUp() slideDown()`：

```javascript
(function(){
	var $dd = $('dd');
	$dd.(':nth-child(n+4)').addClass('hide');

	$('dt').on('mouseenter', function() {
		$(this)
			.next()
				.slideDown(300)
				.siblings('dd')
					.slideUp(300);
	});
})();
```

`slideDown()`, `slideUp()` 这种函数你可以传入参数，指定毫秒数，通常 200-400 ms，看起来挺舒服的。

OK. 现在功能出来了，看看有没有什么可以改善的，永远记得，在 **功能完整后再改进** 。

现在我们的代码实际上只用到了一次 `$('dd')`，所以不需要将它存到变量里，节省空间：

```javascript
(function(){

	$('dd').(':nth-child(n+4)').addClass('hide');

	$('dt').on('mouseenter', function() {
		$(this)
			.next()
				.slideDown(300)
				.siblings('dd')
					.slideUp(300);
	});
})();
```

现在看看这行代码：

```javascript
$('dt').on('mouseenter', function() {
	...
}
```

这行代码不太好，要是咱页面有一百个 `dt`，那效能不好，最好是你给 `dl` 上一个 `id="FAQ"`，将选择器改为 `dl#FAQ`，这样子每次我们只会选中 FAQ，而不会去选到其他的，在这里我们演示的关系，选中 `$('dl')` 就好了。

```javascript
(function(){

	$('dd').(':nth-child(n+4)').addClass('hide');

	$('dl').on('mouseenter', 'dt', function() {
		$(this)
			.next()
				.slideDown(300)
				.siblings('dd')
					.slideUp(300);
	});
})();
```

注意我在 `on` 函数里又多传了一个参数，`'dt'` ，这叫做 选择器字串 (slector string)。

现在这整行代码的意思是，当用户鼠标进入 `dl` 时，选中 `dl` 的 `dt`：

```javascript
$('dl').on('mouseenter', 'dt', function()
```

仅仅重构了这一下，我们省去了给所有 `dt` 加上 event listener，只给特定的 `dt` 加上 event listener，尽量养成这样子的习惯，首先写一个能动的 jQuery，想想该怎么重构，并重构它。

打完收工。

