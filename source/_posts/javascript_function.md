---
title: JavaScript 核心 (29) - 函式以及 This 的運作 - 什麼是函式
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 在了解 this 之前，先來詳細認識函式吧
abbrlink: 962869145
date: 2021-01-04 17:30:00
---
## 函式特色

函式屬於物件一種，並且具有以下特性:

* 具有被呼叫的能力
* 可以撰寫程式碼的區塊
* 有屬於自己的 this
* 具有自己的執行環境
* 可回傳結果(return)
* 名稱（選用，匿名函式與具名函式）

## 函式陳述式

函式陳述式並不會主動回傳結果，而是必須等待呼叫後才會回傳結果

``` JavaScript
function fn() {
  ...
}
```

## 函式表達式

函式表達式在程式碼執行時，就會將函式回傳到 `fn` 中，可在細分為 `匿名函式`、`具名函式`

``` JavaScript
/* 匿名函式 */
var fn = function() {
  ...
}

/* 具名函式 */
var fnA = function fnB() {
  ...
}
console.log(fnA, fnB); /* fnB is not defined */
```

## 使用時機

專案上到底該使用 `函式陳述式` 還是 `函式表達式` 呢?
其實這沒有標準答案，一切還是看團隊一開始的規範文件而訂。
當然，像是 Airbnb 規範就希望都是用 `函式表達式`，而且還是`具名函式`，畢竟 `函式陳述式` 會有所謂的 `Hoisting`，有時候在 debug 上會需要先釐清運作流程，會增加除蟲時間。

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(35)-函式以及 This 的運作-什麼是函式](https://hsiangfeng.github.io/javascript/20201115/1294497105/)
