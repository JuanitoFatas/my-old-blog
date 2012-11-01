---
layout: post
title: "CL:LGISC 2/e 導讀"
date: 2012-02-05 03:01
comments: true
categories: Lisp
---


## Common Lisp: Lisp Gentle Introduction to Symbolic Computation 第二版

這本書出版於1990年，線上可[免費閱讀][lgisc]，本書用14章帶你入門 Common Lisp 。

[lgisc]: http://www.cs.cmu.edu/~dst/LispBook/

<!--more-->

本書目標讀者有三種：

* 第一次學寫程式的學生（只要懂算數就好）
* 打算研究 AI 領域的心理學家、語言學家、電腦科學家
* 電腦愛好者

初學者一開始都會被如何設定環境、怎麼除錯、特定的語法...等等議題給絆住並遭受挫折感。但初學者一開始只要先搞懂 Common Lisp 中，數字 (number)、符號 (symbol)及列表 (list)的差別就好了。

你或許聽過"程式就是資料"這個概念，但這是一般初學 Lisp 人主要感到困惑的來源。 本書使用了大量圖形化（箱子箭頭標示法）來表示程式及資料。讓你可以很輕鬆的分別它們。而電腦程式很難有這種表示法給你使用，所以在第一章及第二章，你只需要拿紙筆學習即可。這也讓初學者免去了設定環境那些瑣事而阻礙了你學 Lisp 。

要是學過別種程式語言的人可以花一分鐘讀讀第一章的總結就好，直接跳到第二章來學習基礎的列表操作。

第三章講標準的 EVAL 標示法。 Quote 的概念及如何命名變數。從本章起就可以開始使用電腦練習了。已經學了兩章，你應該不會感到那麼不安，甚至有很大的渴望想在電腦編程了。

另外三個，從第三章之後開始出現的特色是 Evaltrace 標示法、 Lisp Toolkit 小節以及為了 Lisp 的資料結構所設計的，易於理解的圖形表示法（包括了函數物件及符號的內部結構）。

Evaltrace給你演示一個Lisp表達式是如何求值的、函數是如何應用在引數 (argument)上及變數怎麼創建及綁定的、 EVAL 與 APPLY 的差別、變數的作用範圍，巢狀的變數作用域...這些都可以圖形化的解釋，讓你很簡單記起來並使用它們。

Lisp Toolkit 介紹了你編程的好幫手，像是 Common Lisp 內建的 DESCRIBE、INSPECT、TRACE、STEP及除錯器。還介紹了兩個獨特的工具（在Appendix A 跟 B 可以找到 source code）
* SDRAW 可以畫 cons cell 的圖，讓你理解 CONS、LIST、APPEND 的差別。
* DTRACE 是 TRACE 的加強版，讓你有更詳細的追蹤結果。

最後本章特別的介紹了符號的內部結構，包含了 name, function, value, plist, package cells。幫助你理解 Lisp 直譯器的本質，以及強調了符號、函數、變數與 print names 的區別。

應用的運算元 (Applicative operators)由第七章介紹，同時可以學到閉包 (lexcial closure)。

第八章講一個龍的故事介紹遞歸，也介紹了一個遞歸的模版。

而本書在前8章提倡了簡潔、無副作用程式設計風格。

第9章介紹了基本的輸入輸出。

第10章提供了一個一致的賦值方法，包含了普通的變數 (ordinary variable)、通用的變數 (generalized variable)以及破壞性的序列操作 (destructive sequence operations)。

第11章涉及到迭代 (iteration)，以及演示了如何不使用顯式賦值 (explicitly assignment)，用DO與DO*來創建可靠的迭代表達式。

第12章介紹了結構 (structures)。

第13章介紹了陣列 (array)、雜湊表 (hash table)以及屬性列表（property list）。

第14章，也是最後一章，獻給巨集 (macro) 與編譯 (compilation)。也解釋了 lexcial 與 dynamic scoping。 Evaltrace圖更闡明了macro與特殊變數 (special variable)的語義。

這本書強調簡單。像是排除掉使用 1+ 1- 這種令人困惑的函數，或是像 PUSHNEW 這種晦澀的函數。本書大部分使用了 EQUAL。而 EQ、EQL、EQUALP 放在進階的議題討論。

而多值跟包系統在本書不予討論。

有些人可能會說，為什麼不在入門課程使用比 Common Lisp 小巧精幹的 Scheme 來教學。但我們可以用 Common Lisp 的子集，與Scheme相同大小的子集來教，所以語言的大小不是問題。

另一個更使人信服的論調是，有一種應用程式設計的風格，大量使用到了詞法閉包，可以更優雅地在 Common Lisp 來表達。 

再舉幾個 Common Lisp 優於 Scheme 的地方來說，使用者可以自己定義巨集、序列型態有優雅且一致的列表、向量表示法、用關鍵字引數 (keyword argument)來大量擴充列表函數的功能...等等。

結合了驚人的威力、廣泛的軟體支援以及內建的物件導向程式設計讓 Common Lisp 是唯一具有工業級水準的 Lisp 方言。

這本時同時設計給菜鳥程式設計師，以及非資工專業的學生學習，但每章最後的進階議題也可滿足大三大四的求知慾比較高的學生。

大學生想更進一步學習的，可以學習 [Common Lisp The Language 2/e][cltl2] 。初學者想要參考資料的可以查閱由 Franz Inc 公司所寫的 [Common Lisp: The Reference][cltr]。

[cltl2]: http://www.cs.cmu.edu/Groups/AI/html/cltl/clm/clm.html
[cltr]: http://www.franz.com/support/documentation/8.2/ansicl/ansicl.htm
