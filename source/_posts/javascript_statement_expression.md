---
title: JavaScript 核心 (10) - 運算子、型別與文法 - 陳述式與表達式
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
abbrlink: 63010062
date: 2020-12-22 15:15:00
description: 摸透 JavaScript 中的兩大語句類型
---

## 陳述式 Statement

[MDN 陳述式與宣告](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Statements)
用於命令執行指定的一系列操作，最大特徵是`不會回傳結果`。
由於不會回傳結果的關係，所以陳述式不能賦予值給變數。

舉例:

* if...else
* var、let、const
* function
* for

``` JavaScript
if(true) {}               /* return undefined */

function fu() {}          /* return undefined */

for(var i; i< 10;i++) {}  /* return undefined */
```

這裡回傳 `undefined` 並`不是回傳結果`，只是瀏覽器告訴我們已經準備好記憶體空間而已

## 表達式 Expression

[MDN 運算式與運算子](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Guide/Expressions_and_Operators)
又稱`表示式`、`運算式`，經常透過符號結合上下語句並運算及`回傳結果`

JavaScript 運算式有下列幾種種類:

* 算術: 解析出數字， 例如 3.14159. (通常使用 算術運算子.)
* 字串: 解析出字串， 例如 "Fred" or "234"。 (通常使用 字串運算子.)
* 邏輯: 解析出 True 或 False (通常與 邏輯運算子 相關。)
* 主流運算式: JavaScript 基本的關鍵字及運算式。
* 左側運算式: 左側是指定值的對象。

``` JavaScript
aa = 'Cloud';       /* return "Cloud" */
1+1;                /* return 2 */
a = true;           /* return true */
b = function () {}  /* return ƒ () {} */
```

## 函式陳述式

又稱`具名函式`，與陳述式相同，`不會回傳結果`且`具有 hoisting 效果`

``` JavaScript
function test() {}
```

## 函式表達式

又稱`匿名函式`，會宣告一個變數並搭配等號運算子以及函式組合，`不具有 hoisting 效果`

``` JavaScript
var test = function() {}
```

## 物件實字 VS Block

Block => 陳述式
物件實字 => 表達式

``` JavaScript
/* Block */
{
  var a = 'Cloud'; /* return undefined */
}

/* 物件實字 */
{
  a: 'Cloud',     /* {a: "Cloud"} */
}
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(11)-運算子、型別與文法-陳述式與表達式](https://hsiangfeng.github.io/javascript/20200607/196651152/)
