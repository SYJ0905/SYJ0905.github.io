---
title: JavaScript 核心 (22) - 物件 - 物件與純值
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 介紹物件與純值區別
abbrlink: 1953779625
date: 2020-12-28 16:00:00
---
## 純值不允許新增屬性

前面介紹到物件可以操作屬性，然而這種操作僅有物件可以達成，一般的純值型別是無法新增屬性的。
上範例:

``` JavaScript

/* 物件 */
var family = {};
family.name = 'Cloud';
console.log(family, family.name); /* {name: "Cloud"} "Cloud" */

/* 純值 */
var num = 'Cloud';
num.age = 26;
console.log(num, num.age); /* Cloud undefined */
```

可以看到 `num.age` 是 `undefined`。

## 繼承原始物件型別

那究竟為什麼物件可以有操作屬性的方法呢?
是因為 `prototype` 在運作，你可以把 `prototype` 想成是 `該型別可以使用的功能or方法`。
好比人類只能在陸地上呼吸空氣，而不能在水中呼吸空氣一樣，會出事的。
此外，即使能硬是操作 `prototype`，也依舊是`無法讓純值有操作屬性的功能`。

``` JavaScript
var num = 10;
console.log(num); /* 10 */
num.name = 'Cloud';
console.log(num.name); /* undefined */

Number.prototype.qq123 = 'Cloud';
console.log(num.qq123); /* Cloud */
num.qq123 = 'Hello';
console.log(num.qq123); /* Cloud */
```

## 建構式是物件

使用建構式宣告純值的話，是可以有操作屬性的功能哩。
因為建構式本身就是物件型別，即使傳入的參數是純值也一樣

``` JavaScript
var test = new Number('26');
console.log(test, typeof(test)); /* Number {26} "object" */
test.name = 'Cloud';
console.log(test.name); /* Cloud */
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(24)-物件-物件與純值](https://hsiangfeng.github.io/javascript/20200802/848840847/)
