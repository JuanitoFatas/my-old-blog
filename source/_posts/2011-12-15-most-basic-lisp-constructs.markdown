---
layout: post
title: "COMMON LISP 基本函數"
date: 2011-12-15 01:45
comments: true
categories: ["Common Lisp"]
tags: lisp
---

粗略筆記僅供參考，如有錯誤請留言，感謝！
各種不同的Common Lisp的實現版本可能會有不同的結果產生。
想要深入了解請參考 [Common Lisp the Language, 2nd Edition][CLTL2]    
[CLTL2]: http://www.cs.cmu.edu/Groups/AI/html/cltl/clm/node1.html

<!--more-->

註記方式：
<strong> 表達式 => 回傳值 </strong> 
<strong> ; 分號後面為 註解 </strong> 

## 數值有關

### 加減乘除

` + - * / `

``` clojure

(* 1 2 3 4) => 24

(/ (+ 4 3) (- 2 1)) => 7

```

### 開根號

` sqrt `

``` clojure

(sqrt 9) => 3

```

### 指數

` expt `

``` clojure

; (expt Base Exponent)

(expt 10 2) => 100

```

### 最大值 最小值

` max min `

``` clojure

(max 1 2 3 4 5) => 5
(min 1 2 3 4 5) => 1

```

### 絕對值 餘數 取最近整數

` abs mod round `

``` clojure

(round (mod (abs -27) 5)) => 2

```

### rem與mod

語法一樣，都是：

``` clojure

mod number divisor
rem number divisor

```

mod 對 number跟divisor 做 floor 運算，並回傳floor運算結果的第二個。

> floor converts its argument by truncating toward negative infinity; that is, the result is the largest integer that is not larger than the argument.

``` clojure

; (mod -13 4) => 3 Equivalent to
(floor -13 4) => -4 3

```

rem 對 number跟divisor 做 truncate 運算，並回傳truncate運算結果的第二個。

>truncate converts its argument by truncating toward zero; that is, the result is the integer of the same sign as the argument and which has the greatest integral magnitude not greater than that of the argument.


``` clojure

; (mod -13 4) => -1 Equivalent to
(truncate -13 4) => -3 -1

```


### 正弦 餘弦 正切

` sin cos tan `

請代入 *radians* 而不是 degrees

``` clojure

(sin (/ pi 2)) => 1.0 ; PI = 3.14159...

```

## 跟List存取有關的函數

### 第一個 第一個之後的 最後一個 長度

` first rest last length `

``` clojure

(first '(a b c d)) => A
(rest '(a b c d)) => (B C D)
(last '(a b c d)) => D
(length '(a b c d)) => 4

```

### 第二個，第三個，第四個，...，第十個。

` second, third, fourth,..., tenth `

``` clojure

(third '(a b c d)) => C

```

### 第 N 個

` nth `

``` clojure

; (nth N List) 

(nth 2 '(a b c d)) => B

```

## List 建構函數

` cons append list`

``` clojure

; (cons Entry (List)) 

(cons 'a '(b c d)) => (A B C D)

; (append (List1) (List2) ... (listN))

(append '(a b) '(c d)) => (A B C D)

; (list Entry1 E2 ... EN) 

(list 'a '(b c) (+ 1 2 3 4)) => (A (B C) 10)

```

## 集合有關

### 交集、聯集、差集、成員、子集、加入

` intersection union set-difference member subsetp adjoin `

``` clojure

(setf r '(a b c d))
(setf s '(c d e))

(intersection r s)   => (c d)
(union r s) 		 => (a b c d e)
(set-difference r s) => (a b)
(member 'd 'r) 		 => (d)
(subsetp s r) 		 => NIL
(adjoin 'b s) 		 => (b c d e)
(adjoin 'c s) 		 => (c d e)

```


## 謂詞

Predicates 中文叫謂詞，真難懂，回傳 T 或 NIL 的判斷式。

### 型別檢查

` listp numberp integerp stringp atom `

atom 分別測試 引數 (arg) 是否是 list 或 number 或 integer 或 string 或 atom。

``` clojure

(listp '(a b)) => T
(numberp 3.14) => T
(integerp 3.14) => NIL
(stringp "hello") => T

```

### 奇數 偶數 數字比較

` evenp oddp = < > <= >= `

輸入非數字會有錯誤哦

``` clojure

(oddp 3) => T
(> 2 1) => T

```

### 邏輯比較 

` and or not `

``` clojure

(not (or (= 2 (1+1)) (evenp 3))) => NIL

```

### 一般比較 

` null equal eql `

eql 測試 兩個引數(args)是否有相同的值。
eql 不可以用在 list 或 string。

``` clojure

(null (rest '(a))) => T
(eql 'a 'a) => t
; (cons 'a '(b)) => (A B)
; (cons 'a 'b) => (A . B)
(equal '(a b) (cons 'a '(b))) => T
(eql '(a b) (cons 'a '(b))) => NIL
```

## 特殊形式

> Special froms are used for side effects, and don't follow the normal lisp rule of evaluating all the args before applying function to the results

### 給變數綁定一個值 

` setq (or setf) `

``` clojure

(setq foo 'lisp) => LISP

(list foo 'foo) => (LISP FOO)

```

### 回傳求值前的引數 

` ' (or quote) `

``` clojure

'(+ 2 3) => (+ 2 3)

(quote (+ 2 3)) => (+ 2 3)

```

### 定義函數 

` defun `

``` clojure

; (defun Function-Name (Arguments) Body)

(defun square (x) (* x x)) => SQUARE
(square 3) => 9

```

### 條件判斷 

` IF `

``` clojure

; (if Condition
;     Then-Result
;     Else-Result)

(if (= 2 (+ 1 1)) 
	'yes 
	'no) 

=> YES

```

### 條件判斷 cond

` COND `

Test1 是T 回傳 Result1
Test2 是T 回傳 Result2
...
TestN 是T 回傳 ResultN

``` clojure

; (cond (Test1 Result1)
;		(Test2 Result2)
;		(Test3 Result3)
;		...
;		(TestN ResultN))

(setq test 3) => 3

(cond ((not (numberp test)) "Not a number!")
      ((oddp test) "odd number")
      (t "even number")) 

=> odd number

```

### progn

語法： ` progn {form}* `

{form}* : 0或多個form。

Progn接受0或多個form輸入，用來組成compound statement。
回傳最後一個statement的求值當做回傳值。

當你在你的IF敘述式裡面想要做多件事情的時候，你可以用 progn 來達成。s

``` clojure

(progn) => NIL
(progn (+ 1 2)) => 3
(progn (+ 1 2) (+ 3 4)) => 7

```

> Group multiple commands into a single block, returning the value of the final one. Some constructs do this implicitly.



### loop

> The infamous all-in-one iteration construct.

網路上有好的範例請看：

[Common Lisp's Loop Macro Examples for Beginners][CLLMEB]
[CLLMEB]: http://www.unixuser.org/~euske/doc/cl/loop.html

## 其它

### 載入

` load `

載入指定的檔案，並對裡面所有Lisp代碼求值。

### 編譯檔案

` compile-file `

編譯 輸入的源代碼 `xxx.lisp` 產生出 `xxx.wfasl`

注意 此 `.wfasl` 不用 load

### 打印輸出

` print, format `

``` clojure

(print "Hello, World!") => Hello, World!
(format t "Hello, World!")

```

### defparameter VS defvar

defparameter, which defines a parameter , a variable that does not change over the course of a computation, but that might change when we think of new things to add (likethe FrenchMme or the military Lt.). 


The special forms defvar and defparameter both introduce special variables and assign a value to them; the difference is that a variable, like *grammar*, is routinely changed during the course of running the program.

### 尋找函數

` apropos ` 

(apropos 'concat 'user) 

回傳在 user package 內 含有 concat 字串的函數

``` clojure

CONCAT
MAKE-CONCATENATED-STREAM (defined)
CONCATENATED-STREAM-STREAMS (defined)
CONCATENATED-STREAM
CONCATENATE (defined)
CONCATENATE-SYSTEM (defined)

```

### 文檔索引

` documentation `

``` clojure

 (documentation 'concatenate 'function)

=> 

"Returns a new sequence of all the argument sequences concatenated together
which shares no structure with the original argument sequences of the
specified RESULT-TYPE."

```

### 除錯選項

``` 
:A Abort out of debugger
:B Backtrace (list previous calls)
:N Next entry on stack
:P Previous entry on stack
:? more debugger options

```




