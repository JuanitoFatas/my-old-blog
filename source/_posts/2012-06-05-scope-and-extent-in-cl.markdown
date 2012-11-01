---
layout: post
title: "Common Lisp 的 Scope 与 Extent"
date: 2012-06-05 00:24
comments: true
categories: Lisp
tags: lisp
---

## 为什么要理解 Scope 与 Extent?

这两个概念在理解许多 Common Lisp 语言的特色时是很有用的，这两个概念出现在某个对象 (object)或建构子 (construct)需要被一个程序的某个部分参照时。

## Scope

Scope 在一个程序中或是一个程序中特定的范围里，参照可能发生的地方。

## Extent

Extent 参照可能发生的时间区间。

一个简单的例子：

```scheme
	(defun copy-cell (x)
		(cons (car x) (cdr x)))
```

在这个例子里，我们只能在 `copy-cell` 函数主体中来参照到 `x` 参数，这个就是参数 `x` 的 scope。而参数 `x` 的 extent 是当函数 `copy-cell` 被调用至离开的这段时间区间。但是参数的 extent 是有可能在离开函数后仍存在的，但上面这个简单的例子是不可能发生的。

数种描述 Common Lisp 特别有用的 scope 与 extent:

* Lexical scope 由某个特殊建构子所建立的程序區塊（通常是一個主體 body）。可以想想 Common Lisp 的 let、defun 所設立的參數。

例子1:

```scheme
(let ((x 1)
			(y 2))
	(+ x y))
```

x 与 y 的 scope 就是由 let 建构子所建构的主体。

例子2:

```scheme
(defun foo (x)
	(+ x 1))
```

`x` 的 scope 在 defun 建构子所建构的主体。

* Indefinite scope. 在程序任何地方都可以參照的叫做 Indefinite scope。

* Dynamic extent 参照可以发生在配置 (established)与释放 (disestablished) entity 时发生。 Entity 通常可以想成是对象 (如 cons 核、符號）、变量绑定或是 go 可以到的地方。什么时候释放呢？在配置的 entity 执行完毕或是终止时。因此有 dynamic extent 的 entity 遵循著一种类似栈的规范，同时有著平行执行嵌套的建构。

例子：`with-open-file` 建构子开启了一个与文件 (file)的连接并构造了一个流对象来表示这个连接。流对象有著 `indefinite extent` ，但开启文件的连接有著 dynamic extent: 当 `with-open-file` 建构子交出控制权时，流会自动关闭。

例子2: 一个“特殊”变量的绑定是 dynamic extent。

* Indefinite extent Entity 在离开建构子所设立的区块时，仍有参照的可能性存在。

例子：大多数的 Common Lisp 数据对象 (data objecs) 是 indefinite extent 的。
例子：绑定一个函数 lexcially scoped 的参数是 indefinite extent 的。

考虑以下函数定义：

```scheme
(defun compose (f g)
  #'(lambda (x)
      (funcall f (funcall g x))))
```

当给定两个参数时，返回一个函数作为返回值。参数 `f` 与 `g` 的绑定由于返回的函数存在，所以并没有消失。当我们调用这个返回的函数时，我们仍可以参照到 `f` 与 `g` 。因此

```scheme
(funcall (compose #'sqrt #'abs) -9.0)
```

会返回 `3.0` 。

除了上面这些术语之外，通常我们把 dynamic scope 定义成表示 indefinite scope 与 dynamic extent。所以我们说特殊的变数有著 dynamic scope，或是被 dynamically scoped 了，因为它们有 indefinite scope 与 dynamic extent: 一个特别变数可以在任何地方被参照，只要它的绑定 (binding)仍有效。

## Shadowing

以上的定义没有考虑到 Shadowing，当我们定义两个同样名称的 entities 时，第二个会遮蔽了第一个，在这个情况下，我们就无法参照到第一个了。

在 lexcial scope 的情况，如果两个建构子设置了同名的 entities 时，会做嵌套的动作。内部的会遮蔽外部的。举个例子：

```scheme
(defun foo (x z)
  (let ((z (* x 2)))
  	(print z))
  z)
```

内部的 `z` 会是 `(* x 2)`，而外部的 z 会是传入的参数 `z` 。

在 dynamic extent 的情况，如果两个 entities 的发生时间区间重叠时，一个会被嵌套在另一个里面。

一个有著 dynamic extent 的 entity 透过名字来参照时，总是参照到最近一次尚未被释放的 (disestablished) entity。比如：

```scheme
(defun fun1 (x)
  (catch 'trap (+ 3 (fun2 x))))

(defun fun2 (y)
  (catch 'trap (* 5 (fun3 y))))

(defun fun3 (z)
  (throw 'trap z))
```

调用 `(fun1 7)` 的结果会是 `10`。在 `throw` 执行时，同时有两个 `catch` 在监看 `trap` : 一个由 `fun1` 配置的，另一个是 `fun2` 。第二个 `fun2` 是最新的那个，所以 `7` 会在 `fun2` 里返回。从 `fun3` 内部来看， `fun2` 遮蔽了 `fun1` 。


若是 `fun2` 是这样定义的话：

```scheme
(defun fun2 (y)
  (catch 'snare (* 5 (fun3 y))))
```

那么两个 `catch` 会有不同的名称，因此 `fun1` 不会被遮蔽。`(fun1 7)` 结果会是 `7`。