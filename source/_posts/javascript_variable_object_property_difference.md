---
title: JavaScript 核心 (21) - 物件 - 變數及物件屬性的差異
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 介紹變數和物件屬性的區別
abbrlink: 4030024306
date: 2020-12-25 19:30:00
---
## 變數無法被刪除

直接宣告變數時，會是建立在`window`底下

``` JavaScript
var a = 1;
console.log(window.a); /* 1 */
```

而不使用 `var` 宣告呢?

``` JavaScript
var a = 1;
console.log(window.a); /* 1 */
b = 2;
console.log(window.b); /* 2 */
```

同樣都出現在 `window` 底下，那麼我們就來刪除看看吧!

``` JavaScript
var a = 1;
delete a; /* false */
```

``` JavaScript
b = 2;
delete b; /* false */
```

由此可知，變數是無法透過 `delete` 刪除的。

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(23)-物件-額外補充：變數及物件屬性的差異](https://hsiangfeng.github.io/javascript/20200726/2777973914/)
