---
layout: post
title: "CSS 一个常见 nth-child 的误区"
date: 2012-05-12 23:04
comments: true
categories: css
tags: css
---

给定有如下的 HTML 代码片段：

<!--more-->

``` html
<html>
...
<style>
	dt {
		boder-top: 1px solid white;
		boder-bottom: 1px solid gray;
	}
</style>
<body>
	<dl>
		<dt>How to install</dt>
		<dd>Check ...</dd>
		<dt>How to install</dt>
		<dd>Check ...</dd>
		<dt>How to install</dt>
		<dd>Check ...</dd>
		<dt>How to install</dt>
		<dd>Check ...</dd>
		<dt>How to install</dt>
		<dd>last ...</dd>
	</dl>
</body>
</html>
```

假设这是一个 FAQ，我们有一个 Definition list (`dl`)，并有五个 item (`dt`)，五个 item 描述 (`dd`)，

每个 `dt` 的上下有边界，分别是白色、黑色。

今天假如我们想要第一个 `dt` 上方没有 boder，以及最后一个 `dt` 下方没有 boder，这时候 CSS 该怎么写呢？

我们可以使用 CSS3 的 `first-child`：

	dt:first-child { boder-top: none; }

现在你可能会想要使用 `last-child` 来把 最后一个 dd 的 boder-bottom 拿掉：

	dt:last-child { boder-bottom: none; }

而这样不行，因为 `last-child` 是选择 parent 的最后一个 child，这个例子里会选中：

	<dd>last ...</dd>

那该怎么办呢？可以使用 `nth-last-child` ：

	dt:nth-last-child(2) { boder-bottom: none; }

这样子会从 `dl` 的最后一个 child 开始往上 2 个，也就是我们想要的最后一个 `dt`。

That's it!!!

