---
title: JavaScript 核心 (12) - 運算子、型別與文法 - 動態型別
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: JavaScript 不用先宣告變數的型別也能運作!!
abbrlink: 2319355199
date: 2020-12-23 14:30:00
---

## 動態型別 Dynamic typing

JavaScript 是弱型別，也說是動態的程式語言。
代表不必特別宣告變數的型別。程式在運作時，型別會`自動轉換`。這也代表可以`以不同的型別使用同一個變數`。

``` JavaScript
var foo = 42;    /* foo 目前是數字 */
foo = 'bar';     /* foo 目前是字串 */
foo = true;      /* foo 目前是布林值 */
```

## 顯性轉換與隱性轉換

雖說 JavaScript 沒有要預先定義型別，，但實際撰寫時仍會希望一開始先搞清楚變數型別，不然當無法確定型別的變數在做運算時會因為 JavaScript的規則導致問題產生。

顯性轉換(Explicit conversion)範例:

``` JavaScript
var foo = 42;
foo = 'bar';
```

隱性轉換(Implicit conversion)範例:

``` JavaScript
var num = 1;
console.log(num, typeof(num));    /* return 1 "number" */
num = num + '1';
console.log(num, typeof(num));   /* return 11 string */
```

上述的隱性轉換範例說明了除非真的很清楚運算時的型別轉換規則，否則，在做運算時都必需要清楚知道變數的型別才行，這樣可以減低 Bug 產生。

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(13)-運算子、型別與文法-動態型別](https://hsiangfeng.github.io/javascript/20200621/3160672433/)
