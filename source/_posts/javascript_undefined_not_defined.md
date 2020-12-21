---
title: JavaScript 核心 (7) - 執行環境與作用域 - undefined VS not defined
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 了解 undefined 以及 not defined 的差異，在 debug 上是非常有幫助的
abbrlink: 212873177
date: 2020-12-21 19:00:00
---

## undefined

在宣告變數`之前`呼叫變數，則會是 `undefined`。

``` JavaScript
console.log(a);    /* undefined */
var a = 'Cloud'
```

### undefined 注意事項

在宣告變數時請不要使用 `undefined`或是給 `undefined` 當作值賦予變數，即使 JS 允許也一樣，這會導致在 debug 的困擾。

``` JavaScript
var a = undefined;
var undefined = '1';
undefined   /* undefined */
```

若想賦予變數`初始空值`，則可以使用 `null` 來代替。
<註>`null` 與 `''` 是不同的

``` JavaScript
typeof('');   /* return string */

typeof(null); /* return object */
```

而　`null`　為什麼會是　`object` 呢? 這是 JS 在一開始設計時產生的 Bug，但因為運行過久，導致現在若修正的話，會影響到全世界的網站，所以就一直維持這個 Bug。

## not defined

根本連宣告變數都沒有就呼叫變數，則會是 `not defined`
意即`變數或函式未定義`

``` JavaScript
console.log(a);    /* a is not defined */
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(7)-執行環境與作用域-not defined VS undefined](https://hsiangfeng.github.io/javascript/20200510/2581786882/)
