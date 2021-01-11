---
title: JavaScript 核心 (30) - 函式以及 This 的運作 - 立即函式
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 本篇介紹立即函式 IIFE
abbrlink: 1134069126
date: 2021-01-04 18:30:00
---
## 立即函式 IIFE

[MDN IIFE](https://developer.mozilla.org/zh-TW/docs/Glossary/IIFE)

全名 「immediately-invoked function expression」，意即 `立即呼叫函式表達式`。
可依照 `具名與否`以及`()位置`分成四種寫法。
此外，多個 IIFE 中間必須要有`;`斷行，才不會違法 JavaScript 規範。

``` JavaScript
(function IIFE_1() {
  console.log('具名、括號在內');
}());
(function IIFE_2() {
  console.log('具名、括號在外');
})();
(function() {
  console.log('IIFE_3 匿名、括號在內');
}());
(function() {
  console.log('IIFE_4 匿名、括號在外');
})();
```

## 侷限作用域

IIFE 有一個特點是 `無法在函式外再次被執行`

``` JavaScript
(function IIFE() {
  var test = 'Cloud';
})();
console.log(test); /* test is not defined */
```

``` JavaScript
(function IIFE() {
  var test = 'Cloud';
})();
IIFE(); /* IIFE is not defined */
```

## 傳遞參數

IIFE 是利用後面的 `()` 傳遞參數，並在前面的`()`接收參數。

``` JavaScript
(function(name) {
  console.log(name); /* Cloud */
})('Cloud');
```

## 表達式

不要忘記 IIFE 也是表達式，所以也能賦予值給變數使用。

``` JavaScript
var myName = (function(name) {
  return name;
})('Cloud');
console.log(myName);
```

## 為何要使用 IIFE

主要是避免污染到全域環境並導致污染與衝突。
在許多框架中，會將框架運作的程式碼包在 IIFE 之中，最後在回傳掛載在 `全域環境變數上` 做使用。

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(36)-函式以及 This 的運作-立即函式](https://hsiangfeng.github.io/javascript/20201118/707576253/)
