---
title: JavaScript 核心 (19) - 物件 - 物件結構
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
abbrlink: 79486610
date: 2020-12-25 11:30:00
description: 本篇介紹什麼是物件?
---

## 物件的宣告方式

在 JavaScript 中，宣告物件的方式有兩種，一是`物件實字`，二是`包裹物件`，至於兩種以何不同?哪一種宣告方式比較好呢?以下一一介紹。

## 物件實字 Object Literals

以下是物件實字的宣告範例

``` JavaScript
var object = {
  property: 'value',
};
```

物件是由 `屬性: 值` 搭配而成的，而 `值` 可以是 `純值`、`物件`甚至是 `函式` 都是可以的。

``` JavaScript
var obj = {
  name: 'Cloud', /* String */
  money: 10,     /* Number */
  sleep: true,   /* Boolean */
  familyObj: {}, /* Object */
  arr: [],       /* Array */
  fn: function() {}, /* function */
};
```

## 包裹物件

使用`建構式`建立物件

``` JavaScript
var obj = new Object();
obj.name = 'Cloud';
```

這種宣告方式除了可讀性很差以外，也會有傳值上的問題，所以開發上不要使用這種方式。

``` JavaScript
var obj1 = new Object('123');
var obj2 = new Object(123);

console.log(obj1); /* String {"123"} */
console.log(obj2); /* Number {123} */
```

這兩種實際上是不一樣的哩。

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(21)-物件-物件結構](https://hsiangfeng.github.io/javascript/20200712/753837712/)
