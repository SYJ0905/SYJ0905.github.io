---
title: JavaScript 核心 (15) - 運算子、型別與文法 - 優先性及相依性
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
abbrlink: 2401760990
date: 2020-12-23 18:00:00
description:
---
## 優先性 Precedence

決定運算子彼此之間被語法解析的方式，優先序較高的運算子會成為優先序較低的運算元

## 相依性 Associativity

決定運算方向

用以下範例解釋比較清楚

``` JavaScript
var a = 2 + 2 * 2 / 2; /* return 2 */
```

由於 `*`、`/` 的優先序高於 `+`、`=` 所以會`先乘除後加減`的賦值過程。
相同的優先性會以相依性決定運算方向，所以 `*` `/` 都是 `從左至右`。
詳細的運算子可參考 MDN 說明
[MDN 運算子優先序](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)

相依性常見考題

``` JavaScript
/* 範例一 */
console.log(1 < 2 < 3); /* true */

/* 解析過程 */
console.log(1 < 2);     /* true */
console.log(true < 3);  /* true 會受到型別轉換，true = 1， 所以其實是 1 < 3 */
console.log(1 < 2 < 3); /* true */

/* 範例二 */
console.log(3 > 2 > 1); /* false */

/* 解析過程 */
console.log(3 > 2);     /* true */
console.log(true > 1);  /* true 會受到型別轉換，true = 1， 所以其實是 1 > 1 */
console.log(3 > 2 > 1); /* false */
```

由上述範例可知，運算過程是一次執行一個運算子`並回傳`，在接著跟下一個運算元運算，才決定其值。

下面這個範例將更清楚瞭解運算過程

``` JavaScript
var a = {};

Object.defineProperty(a, 'b', {
  value: 0,
  writable: false,
})

var b = {};

Object.defineProperty(b, 'b', {
  value: 99,
  writable: false,
})

Object.defineProperty(b, 'c', {
  value: 123,
  writable: false,
})

var c = b.c = b.b = a.b = 10;
console.log(b.c);  /* return 123 */
console.log(b.b);  /* return 99 */
console.log(a.b);  /* return 0 */
console.log(c);    /* return 10 */
```

因為 `a.b = 10` 的回傳值是 `10`，但因為 `a.b`是不可寫入的所以不會改變其值。
同理可知 `c = b.c = b.b = a.b = 10` 等於 `c = 10`。

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(16)-運算子、型別與文法-優先性及相依性](https://hsiangfeng.github.io/javascript/20200628/713590185/)
