---
title: JavaScript 核心 (9) - 執行環境與作用域 - 執行緒與同步、非同步
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 同步、非同步是 JS 中相當重要的觀念，有助於日後與 API 打交道更順暢
abbrlink: 1607076329
date: 2020-12-22 12:30:00
---
## 單執行緒

一次只能執行一件事情行完後才會接續下一步驟
JavaScript 是屬於 `單執行緒`的程式語言

## 同步與非同步

執行緒 => 系統本身運作流程
同步與非同步 => 針對程式語言
這樣講有點似懂非懂的感覺，直接舉例說明會更清楚

以下是`同步`的範例:

``` JavaScript
function a() {
  console.log('a');
}
function b() {
  console.log('b');
}
function c() {
  console.log('c');
}
a();
b();
c();
```

上述執行順序肯定是 a() > b() > c()，不會在執行 a() 時，同時執行 b()。

以下是`非同步`範例:

``` JavaScript
function a() {
  console.log('a');
}
function b() {
  console.log('test')
  setTimeout(() => {
    console.log('b');
  }, 1000);
}
function c() {
  console.log('c');
}
a();
b();
c();

/* 結果 */
a
test
c
b
```

這裡多了一個 `setTimeout` 的非同步函式。
在 JS 中，`非同步函式` 會被放進 `事件佇列(Event queue)` 中，在其他函式都執行完後，才會執行

要注意的是，執行順序依舊是 a() > b() > c()，但是 b() 中的`非同步`會單獨移到`事件佇列`，而其他程式仍舊維持`同步`運作，所以 `test` 才會在 c() 前面呦

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(9)-執行環境與作用域-執行緒與同步、非同步](https://hsiangfeng.github.io/javascript/20200531/3571534372/)
