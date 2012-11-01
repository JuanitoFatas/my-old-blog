---
layout: post
title: "Python 解决 Zebra 谜题"
date: 2012-05-10 22:35
comments: true
categories: Python
tags: Python
---

爱因斯坦养鱼问题的学名就叫 Zebra Puzzle。之所以叫爱因斯坦养鱼问题是为了刊登在杂志上吸引读者的注意，其实这个问题不是爱因斯坦搞的...

问题可以到这里看：[Zebra Puzzle](http://en.wikipedia.org/wiki/Zebra_Puzzle)

<!--more-->

首先实现了 2 个 小函数，`imright` 跟 `nextto`

确定某房是不是在某房右边、或是两个房挨著。

接下来给每个房子编上号，12345，

然后使用了 Python 自带的排列工具 `itertools.permutations` 给出房子可能的排列。

接著用了一个 Python 的奇技淫巧，叫做 Generator Expression，

语法是：`(term for-子句 (选择性) for-if-子句)`

这个 generator expression 会返回一个 Generator 对象。

恩，给个例子好了：

先定义一个算平方的函数，然后用 Generator Expression：


	def sqr(x): print '调用 sqr, 参数 ', x; return x*x

	g = (sq(x) for x in range(10) if x%2==0)

这个时候如果调用 g ：

	>>> g
	<GeneratorObject ....>

不会去调用函数，只返回一个 Generator 对象、然而

	>>> next(g)
	调用 sqr, 参数 0
	0

才会调用这个 Generator 所绑定的函数。。。汗。。。

这个问题要找，水在哪个房子被喝的，哪个房子养斑马。

藉由把 Constraint 移到对的地方，减少需要的计算，再搭配 Generator-exp 的特性，最后大概 0.00028 秒之类的就算好了，
本来用 嵌套 For-loop 要算 1 小时。

至于那个 c 函数 是拿来显示统计数据跟除错用的。

完整代码：

{% gist 2653290 %}