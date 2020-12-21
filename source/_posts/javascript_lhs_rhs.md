---
title: JavaScript 核心 (2) - 執行環境與作用域 - LHS、RHS差異
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 什麼是 LHS ? 什麼是 RHS ? 一起了解吧!!
abbrlink: 3916322912
date: 2020-12-21 14:00:00
---

## LHS (Left-Hand Side)

賦予值到左側的變數上

``` JavaScript
var a = 1; /* 將 1 賦予到變數 a 上 */
```

錯誤的 LHS 範例

``` JavaScript
'小傑' = 1;
```

輸入以上範例時，瀏覽器的 console 則會報錯 `Uncaught SyntaxError: Invalid left-hand side in assignment`

另一種錯誤範例

``` JavaScript
var '小明' = 1;
```

此時回報不是 LHS 錯誤，而是 `Uncaught SyntaxError: Unexpected string`

## RHS (Right-Hand Side)

指取值是來自右側的變數上

``` JavaScript
var a = '小傑';
console.log(a);
```

RHS 也可以視為 `變數重新賦予到新的變數上`。

錯誤的 RHS 範例

``` JavaScript
console.log(b);
```

輸入以上範例時，瀏覽器的 console 則會報錯 `Uncaught ReferenceError: b is not defined`
不同瀏覽器有些微差異，但都是以 `XXX is not defined` 為主

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(2)-執行環境與作用域-執行的錯誤情境 LHS, RHS](https://hsiangfeng.github.io/javascript/20200405/949633773/)
