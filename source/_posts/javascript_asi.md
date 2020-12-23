---
title: JavaScript 核心 (11) - 運算子、型別與文法 - ASI 自動插入分號
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 結尾分號加與不加究竟有何區別?
abbrlink: 1504038266
date: 2020-12-23 11:30:00
---

## ASI

[MDN ASI](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Automatic_semicolon_insertion)
Automatic Semicolon Insertion 自動插入分號
理論上 JS 是允許不寫分號的，但實際開發中除非很了解 JS 的斷行機制，不然不加分號會產生很多問題哩

``` JavaScript
var a = function() {
  return
  'ASI is Good!'
}

console.log(a())  /* return undefined */

var b = function() {
  return 'ASI is Good!';
}

console.log(b())  /* return ASI is Good! */
```

`return` 後面不加回傳值的話，ASI機制就會自動加入分號，所以在 `a()` 只會回傳 `undefined` 而不會回傳 `ASI is Good!`。

## 立即函式

``` JavaScript
(function() {
  console.log('one')
})();

;(function() {
  console.log('two')
})()
```

當有多個立即函式時，兩兩之間必須要有 `;` ，不論是在開頭還是結尾都可以，否則瀏覽器會報錯誤 `Uncaught TypeError: (intermediate value)(...) is not a function`

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(12)-運算子、型別與文法-ASI 自動插入分號](https://hsiangfeng.github.io/javascript/20200613/3587770435/)
