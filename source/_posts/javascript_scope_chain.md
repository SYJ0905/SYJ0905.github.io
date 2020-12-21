---
title: JavaScript 核心 (5) - 執行環境與作用域 - 範圍鍊
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 釐清範圍練、執行推疊、執行環境關係
abbrlink: 1324601033
date: 2020-12-21 17:00:00
---

## 範圍練 Scope Chain

當函式的本身沒有相對應的變數或函式時，他就會向外層去尋找

``` JavaScript
var value = 1; /* 全域變數 */
function fu1 {
  console.log(value); /* 1 */
}
function fu2 {
  var value = 2; /* 區域變數 */
  fu1();
}
fu2();
```

在此範例中 `fu1` 不會去找 `fu2` 的 `value`，而是往本身函式 `fu1` 的外層尋找 `value`。
所以函式的`範圍鍊與執行推疊、執行環境是沒有關係的`。

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(5)-執行環境與作用域-範圍鍊](https://hsiangfeng.github.io/javascript/20200502/1231063032/)
