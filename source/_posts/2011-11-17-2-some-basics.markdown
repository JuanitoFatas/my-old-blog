---
layout: post
title: "第2章 原子 x 表 x S-表達式"
date: 2011-11-17 11:17
comments: true
categories: [簡單學Scheme]
tags: Scheme
published: true
---

今天要講的是：

<strong>原子、表、還有S-表達式。</strong>

atom及list還有s-expression，這3個是Scheme最最最基礎的概念之一。

##那...什麼是原子(atom)？

恩，原子其實就是..."字串"。   

<!--more-->

###那...什麼是字串(String)？

字串就是用雙引號夾住的東西。
裡面可以塞數字、奇怪的符號、特殊符號、英文字母！     

還是不太懂，讓我們從例子下手吧...

"3456" 是不是原子呢？ -- 是，因為他是一個由數字3所組成的字串。

"Juanito" 是不是原子呢？ -- 是，因為他是一個由字母J開頭所組成的字串。

"julia" 是不是原子呢？ -- 是，因為他是一個由字母j開頭所組成的字串。

"html" 是不是原子呢？ -- 是，因為他是一個由字母h開頭所組成的字串。

有點感覺了吧？字串即原子...

> A string of characters/digits beginning with a letter/digit.

##那...什麼是表(List)？

List其實就是...包含在括弧內的原子集合。

(cake) 是不是表呢？ -- 是，因為他是一個包含原子cake所組成的表。

(cake chocolate) 是不是表呢？ -- 是，因為他是一個包含原子cake、chocolate所組成的表。

(today rains cats and dogs) 是不是表呢？ -- 是，因為他是一個包含原子today、rains、cats、and、dogs所組成的表。

((mama mia) mia mama) 是不是表呢？ 是，因為他是一個包含3個S-expression的表。

等等，什麼是S-expression? 除了開頭聽你講過以外，我聽都沒聽過。 

> A collection of atoms enclosed by parenthesis.

## 那...什麼是S-表達式(S-expression)？

所有的原子及表都是S-expression。

"hello" 是不是S-表達式？ 是，因為所有的原子都是S-表達式。

(hello world hi)  是不是S-表達式？ 是，因為所有的表都是S-表達式。

"css3" 是不是S-表達式？ 是，因為所有的原子都是S-表達式。

(((DrRacket) (rocks)) (REALLY)) 是不是S-表達式？ 是，因為所有的表都是S-表達式。

> All lists and atoms are S-expressions.

## 讓我們再複習一下表

剛剛我們說到，"表"其實就是...包含在括弧內的原子集合。

然而 S-表達式 是所有的原子及表。所以我們知道：

<strong> 表是包含在括弧內的S-表達式集合。 </strong>

> A collection of s-expressions enclosed by parenthesis.

## 更多問題

在這個表裡面有幾個S-表達式?

(((html5) css3) ((javascript) (ruby)) python ((lisp) (scheme)))

7個嗎？



不對，再想想。

10個嗎？



不對，再想想。

答案是：

((html5) css3)    
((javascript) (ruby))     
python     
((lisp) (scheme))     

<strong>共有4個S-表達式（3個表，1個原子）</strong>


()這是一個表嗎？

這題可能有點奸詐一點，答案是：

<strong>是。</strong>

為什麼呢？()是一個由一個特別的S-表達式所組成的表。

而這個特別的S-表達式我們稱它為<strong>零S-表達式、null、空表</strong>。

    
(() (()()()) () ()) 是一個表嗎？

<strong>是。</strong>

(() (()()()) () ()) 是由多個空表所組成的表。



呼，我希望你的頭腦還沒打結。

最後再重複一次，

<strong>原子就是字串，表就是括弧包起來的原子，而S-表達式就是原子與表。</strong>




##習題：


把這段代碼輸入到 DrRacket 編寫代碼的區域


{% gist 1379241 atom_s-exp.ss %}


然後存成 atom_s-exp.ss 或是 其他你喜歡的檔案名稱。

請記得左下角語言要選擇 R5RS，接著點選 Run 。

照著上面的範例 利用

atom?, list?, s-exp? 來自己檢驗上面我所問的問題。

測試方法比如：

####"3456"是不是原子？

在直譯器環境敲入

(atom? "3456") 

直譯器應該會告訴你 #t (true) 或是 #f (false)


####(cake chocolate)是不是表？

在直譯器環境敲入

(list? '(cake chocolate))

直譯器應該會告訴你 #t (true) 或是 #f (false)


####(((DrRacket) (rocks)) (REALLY))是不是S-表達式？

(s-exp? '(((DrRacket) (rocks)) (REALLY)))

直譯器應該會告訴你 #t (true) 或是 #f (false)


眼尖的同學應該注意到，我在 表 的前面加入了一個 單引號( ' )。
因為Scheme直譯器不知道你輸入的那些文字，要對應到記憶體的哪裡去，
加了一個單引號可以暫時騙過他，告訴他：這是一個外部常量哦。

Scheme直譯器（心想）：好吧，你開心就好。

開始練習吧！


