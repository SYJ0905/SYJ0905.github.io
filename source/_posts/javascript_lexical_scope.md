---
title: JavaScript 核心 (3) - 執行環境與作用域 - 語法作用域
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: JavaScript 是採用語法作用域，宣告時就決定作用域
abbrlink: 1972639133
date: 2020-12-21 15:00:00
---

## 語法作用域 Lexical scope

又稱 `靜態作用域`
當宣告語法時，就已經決定其作用域
而常見作用域有 `全域環境`、`區域環境`

``` JavaScript
function test() {
  var name = 'Cloud';
}
console.log(name); /* name is not defined; */
```

此時 `name` 的作用域是在函式內，全域環境並沒有 `name` 參數

``` JavaScript
function sayHi() {
  function sayName() {
    console.log('Cloud');
  }
}

sayName(); /* sayName is not defined; */
```

除了變數以外，`函式`也會受到語法作用域影響

## 動態作用域

變數的作用域在`函式調用時`才決定

## 綜合說明

以下範例

``` JavaScript
var value = 1; /* 全域變數 */
function fu1 {
  console.log(value);
}
function fu2 {
  var value = 2; /* 區域變數 */
  fu1();
}
fu2();
```

* 靜態作用域: `value = 1`
* 動態作用域: `value = 2`

## 參考資料
