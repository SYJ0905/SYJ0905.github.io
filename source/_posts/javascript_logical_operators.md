---
title: JavaScript 核心 (18) - 運算子、型別與文法 - 邏輯運算子及函式預設值
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
abbrlink: 79486610
date: 2020-12-24 16:00:00
description: 本篇將介紹邏輯運算子使用方法以及預設值細節
---

## 邏輯運算子

* `&&`: 運算式1 && 運算式2，假如 運算式1 可以被轉換成 `false` 的話，回傳 運算式1; 否則，回傳 運算式2。 因此，&&只有在 兩個運算元都是 true 時才會回傳 true，否則回傳 false。
* `||`: 運算式1 || 運算式2，假如 運算式1 可以被轉換成 `true` 的話，回傳 運算式1; 否則，回傳 運算式2。 因此，||在 兩個運算元有任一個是 true 時就會回傳 true，否則回傳 false。
* `!`: !運算式，假如單一個運算元能被轉換成 `true` 時，回傳 false，不然回傳 true。

上範例:

``` JavaScript
console.log(0 && 1); /* 0 */
console.log(1 && 0); /* 0 */

console.log(0 || 1); /* 1 */
console.log(1 || 0); /* 1 */

console.log(!0); /* true */
console.log(!1); /* false */
console.log(![]); /* false */
```

## 預設值問題

上範例說明:

``` JavaScript
var originCash = 500;
function updateEasyCard(cash) {
  cash = parseInt(cash);
  console.log(cash);
  
  /* 當 cash 是數值或為 0 時，使用 cash 的數值 */
  /* 如果 cash 是 NaN 時，則直接套用 500 */
  cash = (cash || cash === 0) ? cash : 500;
 
  var money = cash + originCash;
  console.log('我有 ' + money + ' 元');
}
updateEasyCard();  /* NaN 我有 1000 元 */
updateEasyCard(0); /* 0 我有 500 元 */
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(19)-運算子、型別與文法-邏輯運算子及函式預設值](https://hsiangfeng.github.io/javascript/20200705/3382481626/)
