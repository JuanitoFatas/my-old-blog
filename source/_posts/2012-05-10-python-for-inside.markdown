---
layout: post
title: "Python For 循环的迭代器实现"
date: 2012-05-10 22:09
comments: true
categories: Python
tags: Python
---


给定一段 Python 代码：

	for x in items:
		print x


这个 items 可以是字串、列表、等等，这种可以迭代的集合称之为 iterable。

<!--more-->

这个 iter 就是创一个迭代器出来，相信有学过 Java 的人都不陌生。

然后用一个 `try .. except` 语句包住，迭代至停为止，停时会抛出 StopIteration。

实际上是这样实现的：

	it = iter(items)
	try:
		while True
			x = next(it)
			print x
	except StopIteration:
		pass
