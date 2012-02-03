---
layout: post
title: "LISP的星號表示法"
date: 2011-12-12 23:25
comments: true
categories: ["Common Lisp"]
tags: lisp
---

## Lisp的星號表示法

詭譎的星號，` * `，英文叫做 asterisk

在Lisp當中只不過就是符號的名字中的一部分而已。

而Lisp程序員喜歡用星號來表示此名字有0個或著重複更多個。

<!--more-->

比如：`GA*` 表示 沒有GA 或 GA 或 GAGA

這種星號表示法又稱作 Kleene star notation （讀音 /ˈkleɪniː/ klay-nee.）

紀念20世紀數學家[Stephen Cole Kleene][SCK]。

另有Kleene plus notation。

`GA+` 表示 "至少"有一個 GA 或 GAGA 或 GAGAGA

## Lisp asterisk notation

The mysterious ` * `, called asterisk sign, appends to a symbol. It is just a part of the name of a symbol. Lisp programmers use this convention to denote 0 or more repetitions of the underlying name. E.g. `GA*` denotes no GA or GA or GAGA ... et cetera. This asterisk notation also called Kleene (pronounced: /ˈkleɪniː/ klay-nee) star notation for memories of [Stephen Cole Kleene][SCK].

Also there is a Kleene plus notation. wherein `GA+` denotes *one* or more repetition of GA. 

[SCK]: http://en.wikipedia.org/wiki/Stephen_Cole_Kleene

<blockquote>
Stephen Cole Kleene (January 5, 1909, Hartford, Connecticut, United States – January 25, 1994, Madison, Wisconsin) was an American mathematician who helped lay the foundations for theoretical computer science. 
</blockquote>

這位[Stephen Cole Kleene][SCK]可猛了，是[Alan Turing][AT]、[Alonzo Church][AC]（[John McCathy][JM]的導師）及[Emil Post][EP] 三大高手合力指導的學生阿...
 
[Alan Turing][AT] : 計算機科學之父，密碼破解高手，慢跑高手。    
[Alonzo Church][AC] : 是Lambda Calculus的發明人(Lisp與函數式編程的基礎)。    
[John McCarthy][JM] : Lisp的發明人阿!!!    
[Emil Post][EP] : 比較不有名，發表了一個什麼可計算性理論之類的。    

唉，這些往者怎麼都這麼猛，叫我們這些來者怎麼追呢？

[AT]:http://en.wikipedia.org/wiki/Alan_Turing
[AC]:http://en.wikipedia.org/wiki/Alonzo_Church
[JM]:http://en.wikipedia.org/wiki/John_McCarthy_(computer_scientist)
[EP]:http://en.wikipedia.org/wiki/Emil_Post