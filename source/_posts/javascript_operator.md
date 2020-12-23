---
title: JavaScript 核心 (14) - 運算子、型別與文法 - 運算子
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 了解 JavaScript 提供的運算子函式吧!
abbrlink: 1000884306
date: 2020-12-23 17:00:00
---

## 運算子

[MDN 運算式與運算子](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Guide/Expressions_and_Operators)
是 JavaScript 提供的函式，基本上運算子都屬於表達式，必定回傳一個值。
運算子的左右兩側稱為 `運算元`，依照運算子的數量，可分為 `一元`、`二元`、`三元`運算子。

``` JavaScript
1 + 1 /* 2 */

name = 'Cloud'; /* Cloud */
```

運算子類型:

* 賦值運算子
* 比較運算子
* 算數運算子
* 位元運算子
* 邏輯運算子
* 字串運算子
* 條件(三元)運算子
* 逗點運算子
* 一元運算子
* 關係運算子

## 特殊寫法

由於運算子本身是一個函式，所以我們可以將運算子視為一個函式名稱，就有下面這種寫法:

``` JavaScript
var a = +(1, 2);
console.log(a); /* return 2 */
```

大概就類似下方的函式宣告

``` JavaScript
function +(a, b){
 return a + b;
}
```

實際開發時請不要使用這種寫法，除非預計明天就要離開公司了。

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(15)-運算子、型別與文法-運算子](https://hsiangfeng.github.io/javascript/20200628/192115648/)
