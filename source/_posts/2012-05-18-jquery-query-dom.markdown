---
layout: post
title: "使用 jQuery 查询 DOM"
date: 2012-05-18 01:04
comments: true
categories: jQuery
tags: jQuery
---

哈罗，你又来看我文章了，谢谢，这篇讲的是巨基本的使用 jQuery 来查询 DOM。

给定一个 HTML：

```html
<!doctype html>
<html>
<head>
	<meta charset=utf-8>
	<title></title>
	<style>
	li { color: black }
	</style>
</head>
<body>

<div class="container">
	<h1>Welcome to My Website </h1>
	<p>
		Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
		tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
		quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
		consequat.
	</p>

	<ul class="emphasis">
		<li>item 1</li>
		<li>item 2</li>
		<li>item 3</li>
		<li>item 4</li>
		<li>item 5</li>
		<li>
			<ul>
				<li>hello from the nest.</li>
			</ul
		</li>
	</ul>
</div>

<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.js"></script>

<script>

</script>
</body>
</html>
```
<!--more-->

为了讲解方便，我直接使用 CDN 来引用 jQuery。之后讲述的代码请放在 `</body>` 前面的 `<script>` 标签内。

OK! 开始！

## children() find() next() prev() first()

假设今天我们想要选中类是 emphasis 的 `ul`：

```javascript
$('ul.emphasis');
```

上面这行：嘿，jQuery，帮我根据这个 CSS 选择器 `ul.emphasis` 去 DOM 把符合条件的找出来。

取出 `ul` 的第一个 `li` ，并添加绿色：

```javascript
$('ul.emphasis').children('li').css('color', 'green');
```

这等同于 CSS:

```javascript
ul.emphasis > li { color: green; }
```

**注意** 这个 `>` 在这边起的作用，这说明了我们只选中第一阶层的小孩，direct children。

试试看这个代码

你会发现嵌套的那个 ul li 是黑色，不是绿色。这样应该明白 direct children 了吧。

你也可以使用 jQuery 的 `find` 来找到：

```javascript
$('ul.emphasis').find('li').css('color', 'green');
```

但要注意的是，这会从 `ul.emphasis` 搜寻所有的 li (all descendent)，等同于 CSS 的：

```javascript
ul.emphasis li { color: green; }
```

好，现在我们在 `style` 标签内添加一个样式：

```javascript
.emphasis { color: green; }
```

并移除刚刚那行代码。

现在我们想替 `ul.emphasis` 的第一个 `li` 加上类名的办法来上色，该怎么做呢？

```javascript
$('ul.emphasis').children('li:nth-child(1)').addClass('emphasis');
// 或是
$('ul.emphasis').find('li:nth-child(1)').addClass('emphasis');
// 或是
$('ul.emphasis').children('li:first').addClass('emphasis');
```

你可能会说，干嘛不用 CSS 就好了，因为使用 jQuery 的话，这些新潮的 CSS3 选择器可以支援 IE6+。

都是万恶的 IE 害的，呜呜。。。

注意这行代码内的选择器：

```javascript
$('ul.emphasis').children('li:first').addClass('emphasis');
```

不是 CSS 的选择器，而是 jQuery 提供的 Helper。如果有自带的 CSS 选择器可用的话，就使用 CSS 选择器，再来才是使用 jQuery 提供的 Helper。因为这比使用 jQuery 提供的来得快一点点。

刚刚那行代码，使用 CSS 有的选择器：

```javascript
$('ul.emphasis').children('li:first-child').addClass('emphasis');
```

好，那 jQuery 还有别的方法可用吗，有：

```javascript
$('ul.emphasis').children('li').first().addClass('emphasis');
```

我们用了一个 jQuery 提供的 `first()`，作用一样。

那想选中第二个 `li` (item2)呢，并把文字改为 Hello from jQuery？

```javascript
$('ul.emphasis').children('li:nth-child(2)').text('Hello from jQuery');
// 或是
$('ul.emphasis').children('li').eq(1).text('Hello from jQuery');
```

注意到，`eq(1)`，因为 Javascript 跟大多数程序语言一样是 **零索引的** ，从零开始数。

好如果我想要先选中 item2，再往后一个，该怎么写呢：

```javascript
$('ul.emphasis').children('li').eq(1).next().text('Hello from jQuery');
```

这串长不拉机的东东有个术语叫做 *chaining* ，它能这么干的原因是每一个调用都返回一个 jQuery 对象。

但是别 chian 的太长了。

有 `next()` 也有 `prev()` 。

一个要写出 jQuery 的秘诀是写之前先念一遍，再直观地写出来，大部分都是对的哈哈。

不过这个贼长的 jQuery 你一般都会写成：

```javascript
$('ul.emphasis').children('li').eq(1).next().text('Hello from jQuery');
// better
$('ul.emphasis li:nth-child(2)').text('Hello from jQuery');
```

chaining 比较慢，代码也比较长，但你还是会需要动态地使用 chaining。

这么长的代码也可以这样缩排：

```javascript
$('ul.emphasis').children('li').eq(1).next().text('Hello from jQuery');

// 等同于
$('ul.emphasis')
		.children('li')
			.eq(1)
			.next().text('Hello from jQuery');
```

## parent() parents() closest()

HTML 实际上就是一个语法树，不懂语法树就想成家庭树，有爷爷奶奶老爸老妈儿子女儿孙子孙女。

好，看个例子，今天我们想要移除 `li` 的父节点的类别

```javascript
$(li).parent().removeClass('emphasis');
```

也可以显式指定要找的 parent 的类型：

```javascript
$(li).parent('ul').removeClass('emphasis');
```

你可以使用浏览器的开发工具查看源代码来检查是否移除成功。

现在让我们加入一个新样式：

```javascript
.container { color: green; }
```

刷新页面，整面绿油油。如果我不想要整片绿油油，我想要移除 parent 的类：container，

```javascript
$(li).parent('.container').removeClass('emphasis');
```

刷新页面，擦，没作用，这是因为这跟 direct children 一样，只会找到上一层的 parent，如果我把 parent 换成：

```javascript
$(li).parents('.container').removeClass('emphasis');
```

注意那个 **s** ，这样就会像 `find` 一样，一直往上找。

你也可以更具体的说，你要移除的是这个 `div.container` 元素:

```javascript
$(li).parents('div.container').removeClass('emphasis');
```

而这行代码等同于：

```javascript
$(li).closest('div.container').removeClass('emphasis');
```

让我们到 http://api.jquery.com/ 查查这个函数是干嘛使的。

## .closest()

> Get the first element that matches the selector, beginning at the current element and progressing up through the DOM tree.

我们这个例子是，从 `$(li)` 开始往上爬 DOM 树，寻找第一个匹配 `('div.container')` 的元素。

## .removeClass()

> Remove a single class, multiple classes, or all classes from each element in the set of matched elements.

移除匹配元素集合中的每一个元素的单一、多个或整个类别。

## parents() 与 closest() 的差异？

其实是一个微妙的差异，你可以研读一下 API，或是这次我直接跟你说了吧：

`parents()` 会根据选择器条件，往上爬树，找出所有符合的。

`closest()` 只会根据选择器条件，找到最近符合的那一个。

查询 API 与源代码是学习 jQuery 的不二法门。

本篇结束。