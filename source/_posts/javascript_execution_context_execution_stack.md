---
title: JavaScript 核心 (4) - 執行環境與作用域 - 執行環境與執行堆疊
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
abbrlink: 1325020609
date: 2020-12-21 16:00:00
description: 搞懂執行環境與執行堆疊，可以更清楚變數及函式的運作哩
---

## 執行環境 Execution context

每一個函式都有 `自己的執行環境`，代表無法直接呼叫`函式內部的函式`。

``` JavaScript
function sayHi() {
  function sayName() {
    console.log('Cloud');
  }
}

sayName(); /* sayName is not defined; */
```

在瀏覽器開啟時或是 Node.js 執行時都會建立一個全域環境，分別是以下參數

* 瀏覽器: `window`
* Node.js: `global`

## 執行推疊 Execution stack

可以想像成是`函式一層一層執行下去，執行完後再一層一層退出`

``` JavaScript
function a() {
  b();
}

function b() {
  c();
}

function c() {
  console.log('Cloud');
}

a();
```

可以在 dev tools 中的 `sources` 查詢 `Call Stack`

`執行` 與 `釋放` 順序

* 執行: `a() > b() > c()`
* 釋放: `c() > b() > a()`

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(4)-執行環境與作用域-執行環境與執行堆疊](https://hsiangfeng.github.io/javascript/20200502/2917226562/)
