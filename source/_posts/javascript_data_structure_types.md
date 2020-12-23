---
title: JavaScript 核心 (13) - 運算子、型別與文法 - 原始型別與物件型別
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 了解 JavaScript 的型別類型將有助於減少開發時出錯的機會
abbrlink: 4037866813
date: 2020-12-23 16:00:00
---

## 原始型別

[JavaScript 的資料型別與資料結構](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Data_structures)

JavaScript 的原始型別有以下六種:

* String     字串
* Boolean    布林
* Number     數值
* Undefined  未定義
* Null       空
* BigInt     整數數值
* Symbol     Symbol

而上述除了 `undefined` 、 `null` 以外，其他原始型別都有各自的`包裹物件`可以使用

``` JavaScript
new Boolean();
new String();
new Number();
BigInt();
Symbol();
```

而包裹物件會提供一些方法，ex: 改變大小寫、刪除空白等等函式可以使用

## 物件型別

只要不是上面那 7 種原始型別，就是物件型別，ex: `function() {}`

## 包裹物件是哪一種?

原始型別本身有各自的包裹物件，而如果宣告變數用包裹物件的話，會讓變數的型別是`物件型別`而不是原始型別。
上範例:

``` JavaScript
var a = new String('Hello');  /* 稱為 `建構式` */
var b = 'Hello';
console.log(typeof(a)); /* return object */
console.log(typeof(b)); /* return string */
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(14)-運算子、型別與文法-原始型別及物件型別](https://hsiangfeng.github.io/javascript/20200621/3684249269/)
