---
layout: post
title: "ANSI COMMON LISP CH2 練習"
date: 2011-12-25 01:05
comments: true
categories: ["Common Lisp"]
tags: lisp
---

新手學習LISP，有錯請指正，謝謝！

下文書寫風格：

<!--more-->

一些術語：

函數 function

表達式 expression

列表 list

引數 argument

符號 symbol


`>` prompt(LISP 等候輸入提示符)    
`;` 註解    
`=>` 被求值為
    
求值後字母一律大寫。    

## 1. 下列表達式求值結果？


``` clojure
; (a) 
; (+ (- 5 1) (+ 3 7))
=> 14

; (b) 
; (list 1 (+ 2 3))
=> (1 5)

; (c) 
; (if (listp 1) (+ 1 2) (+ 3 4))
=> 7

; (d) 
; (list (and (listp 3) t) (+ 1 2))
=> (NIL 3)

```

## 2. 使用三種不同的cons方式回傳(a b c)

``` clojure
> (cons 'a '(b c))
=> (A B C)

> (cons 'a (cons 'b '(c)))
=> (A B C)

> (cons 'a (cons 'b (cons 'c nil)))
=> (A B C)

```

## 3. 定義一函數

使用car與cdr，定義一函數，接受一個引數，列表，回傳此列表的第四個元素

``` clojure

 (defun our-fourth (lst)
    (car (cdr (cdr (cdr lst)))))

; better
(defun our-fourth (lst)
	(first (rest (rest (rest lst)))))

; built-in Common Lisp
; (fourth list)
(fourth '(1 2 3 4 5))
=> 4

```

## 4. 定義一函數

定義一個接受兩個引數的函數，並回傳大的那個。

``` clojure

(defun two-greater (x y)
  (if (>= x y)
      x
      y))

```

## 5. 這些函數的作用？

``` clojure

; (a)

(defun enigma (x)
    (and (not (null x))
         (or (null (car x))
             (enigma (cdr x)))))

``` 

### 解：檢查一個列表是否有NIL元素。

``` clojure

; (b)

(defun mystery (x y)
    (if (null y)
      nil
      (if (eql (car y) x)
        0
        (let ((z (mystery x (cdr y))))
          (and z (+ z 1))))))

``` 

### 解：找出x在y列表的位置。

## 6. 填空題

輸入適合的x滿足以下的表達式及其求值的結果

``` clojure
; a
> (car (x (cdr '(a (b c) d))))
=> B

```

### 解：x 為 car 可取出 列表 '(a (b c) d) 的第二個元素之中的 b 元素

``` clojure
; b
> (x 13 (/ 1 0))
=> 13

```

### 解：x 為 or，因為or會依序對引數求值（由左往右），一旦求值為真就回傳此數值。


``` clojure
; c
> (x #'list 1 nil)
=> (1)

```

### 解：x 為 apply 可創建 列表 (1)
如 x 為 funcall 則創建出 列表 (1 NIL)

> Apply takes a function and a list of arguments, returns the result of applying the function to the arguments

因為 apply 的最後一個引數必須是列表    
而funcall則不需要引數為列表形式傳入（故把NIL考慮成一個列表的元素）

## 7. 定義一函數

只能用本章所介紹的運算元來定義一個函數，此函數接受一個引數，列表。    
如果此列表內有一個元素為列表，則回傳 真。

``` clojure

(defun find-list (lst)
      (if (null lst)
        nil
        (if (listp (car lst))
          t
          (find-list (cdr lst)))))

```
 
## 8. 寫出函數的迭代及遞迴定義 

(a) 此函數接受一個引數，如果此引數為正數時，印出多少個點。
如輸入7 輸出 7個點 "......."
輸入 -2 輸出 nil

``` clojure

; iterate

(defun print-dots-itr (n)
    (if (and (numberp n) (> n 0))
      (do ((i n (- i 1)))
          ((= i 0) (format t "~%"))
        (format t "."))))

; recursion

(defun print-dots-rec (n)
    (if (and (numberp n) (> n 0))
      (if (= n 0)
        (format t "~%")
        (progn 
          (format t ".")
          (print-dots-rec (- n 1))))))


```


(b) 接受一個列表，回傳符號a在此列表所出現的次數

``` clojure

; iterate

(defun count-a-itr (lst)
      (let ((len 0))
        (dolist (obj lst)
          (if (eql obj 'a)
            (setf len (+ len 1))))
        len))

; recursion

 (defun count-a-rec (lst)
      (if (null lst)
        0
        (if (eql (car lst) 'a)
          (+ (count-a-rec (cdr lst)) 1)
          (count-a-rec (cdr lst)))))

```

## 9. 解釋並改正

你有一個朋友正在寫出一個函數，可以加總一個列表內所有的非nil元素。
他寫了兩個版本，你來幫他看看哪裡出錯了？並改寫成正確的版本。

``` clojure

; a
 (defun summit (lst)
    (remove nil lst)
    (apply #'+ lst))

; (remove nil lst) 不影響本來的列表lst
; correct version

(defun summit (lst)
    (apply #'+ (remove nil lst)))


; b
(defun summit (lst)
    (let ((x (car lst)))
      (if (null x)
        (summit (cdr lst))
        (+ x (summit (cdr lst))))))

;(let ((x (car lst))) 會讓code陷入死胡同
; '(nil 1 2 nil)
; 走訪到第四個元素nil時還是會繼續一直判斷下去...

;correct version
(defun summit (lst)
        (if (null lst)
          0
          (if (null (car lst))
            (+ (summit (cdr lst)) 0)
            (+ (summit (cdr lst)) (car lst)))))

```