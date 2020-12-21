---
title: JavaScript 核心 (6) - 執行環境與作用域 - 提升
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 釐清 JavaScript 函式與變數運作原理
abbrlink: 3533353387
date: 2020-12-21 18:30:00
---

## 提升 Hoisting

Hoisting 一詞僅僅只是要釐清 JavaScript 的運作原理而出現的觀念說明。
在 JavaScript 運作過程中可分為兩階段，`創造階段` 以及 `執行階段`

``` JavaScript
/* 一般撰寫流程 */
var a = 'Cloud';
console.log(a); /* return 'Cloud' */

/* JavaScript 實際運作 */

/* 創造階段 */
var a;          /* 記憶體給出空間 */

/* 執行階段 */
a = 'Cloud';    /* 賦予其值 */
console.log(a); /* return 'Cloud' */
```

當 console.log 移到宣告變數前則會出現 `undefined` 錯誤，這是因為在 `創造階段` 時，僅僅是準備記憶體空間而已，並未賦予其值，所以才出現 `undefined`。

``` JavaScript
console.log(a)  /* return undefined */
var a = 'Cloud';
```

## 函式、變數優先順序

`函式`的 Hoisting 會比 `變數` 更高，但其中僅限於 `函式陳述式`，因為 `函式表達式` 實際上是屬於變數一種，所以並不會高過其他變數宣告順序

``` JavaScript
var a = 'Cloud';
function a() {
  console.log('Hello');
}
console.log(a); /* Cloud */

/* 創造階段 */
function a() {
  console.log('Hello');
}
var a;

/* 執行階段 */
a = 'Cloud';
console.log(a); /* Cloud */
```

由於函式會被優先建立的關係，所以其實是可以在函式之前呼叫該函式的

``` JavaScript
sayHi();        /* Hello Cloud */
function sayHi() {
  console.log('Hello Cloud');
}
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(6)-執行環境與作用域-提升](https://hsiangfeng.github.io/javascript/20200503/1924910570/)
