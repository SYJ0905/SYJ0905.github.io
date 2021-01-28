---
title: JavaScript 核心 (46) - 物件屬性延伸 - 屬性特徵是什麼?
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 本篇將深入了解物件屬性的其他用法
abbrlink: 616745406
date: 2021-01-28 10:15:00
---
## 屬性的參數

我們可以透過 `Object.defineProperty()` 來個別設定屬性的特徵，以下是四點是屬性的特徵，都是可以調整設定的:

* `value`: 值
* `writable`: 可否寫入
* `configurable`: 可否被刪除
* `enumerable`: 可否列舉，使用 `for in` 時會列舉的

示範如何使用:

``` JavaScript
var person = {
  a: 1,
  b: 2,
  c: 3,
};
console.log(person); /* {a: 1, b: 2, c: 3} */

/* 改變值 */
Object.defineProperty(person, 'a', {
  value: 4,
  writable: true,
  configurable: true,
  enumerable: true,
});
console.log(person);  /* {a: 4, b: 2, c: 3} */

/* 可否寫入 */
Object.defineProperty(person, 'a', {
  value: 4,
  writable: false,
  configurable: true,
  enumerable: true,
});
person.a = 8;
console.log(person);  /* {a: 4, b: 2, c: 3} */

/* 可否刪除 */
Object.defineProperty(person, 'b', {
  configurable: false,
});

delete person.a;
delete person.b;
console.log(person);   /* {b: 2, c: 3} */

/* 可否列舉 */
Object.defineProperty(person, 'c', {
  enumerable: false,
});

for (var key in person) {
  console.log('列舉 =>', key); /* 列舉 => b */
}
```

## 淺層保護

屬性特徵只針對`指定的該屬性有效`，不會連帶影響內部的屬性特徵

``` JavaScript
var person = {
  a: 1,
  b: 2,
  c: 3,
};
Object.defineProperty(person, 'd', {
  value: {},
  writable: false,
});

person.d.name = 'Cloud';

console.log(person); /* {a: 1, b: 2, c: 3, d: { name: "Cloud" } */
```

## 多屬性一次設定

使用 `Object.defineProperties()`，可以直接將物件內多個屬性進行修改

``` JavaScript
var person = {};
console.log(person); /* {} */
Object.defineProperties(person,{
  a: {
    value: 1,
    writable: true,
    configurable: true,
    enumerable: true,
  },
  b: {
    value: 2,
    writable: true,
    configurable: true,
    enumerable: true,
  },
  c: {
    value: 3,
    writable: true,
    configurable: true,
    enumerable: true,
  },
});
console.log(person); /* {a: 1, b: 2, c: 3} */
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
