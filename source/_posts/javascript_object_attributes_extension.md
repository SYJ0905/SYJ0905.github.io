---
title: JavaScript 核心 (47) - 物件屬性延伸 - 物件屬性不可寫入？物件擴充的修改與調整
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 本篇會介紹物件的擴充、封裝、凍結等設定
abbrlink: 3280985594
date: 2021-01-28 18:00:00
---
## 延伸物件的方法

* `preventExtensions`: 防止擴充
* `seal`: 封裝
* `Freeze`: 凍結

## 防止擴充 preventExtensions

`Object.preventExtensions(obj)`
[MDN Object.preventExtensions](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Object/preventExtensions)
範例:

``` JavaScript
var person = {
  a: 1,
  b: 2,
  c: {},
};
Object.preventExtensions(person);
console.log('是否可被擴充 =>', Object.isExtensible(person)); /* 是否可被擴充 => false */
console.log('person a 的屬性特徵 =>', Object.getOwnPropertyDescriptor(person, 'a'));
/* { value: 1, writable: true, enumerable: true, configurable: true } */

/* 調整屬性 => 可行 */
person.a = 'a';
/* 新增屬性 => 不可行 */
person.d = 'd';
/* 巢狀屬性調整 => 可行 */
person.c.a = 'ca';
/* 刪除 => 可行 */
delete person.b;
/* 調整特徵 => 可行 */
Object.defineProperty(person, 'a', {
  configurable: false,
});

console.log('person 物件 =>', person); /* {a: "a", c: {a: "ca"}} */
console.log('person a 屬性特徵(修改後) =>', Object.getOwnPropertyDescriptor(person, 'a'));
/* {value: "a", writable: true, enumerable: true, configurable: false} */
```

## 防止封裝 seal

讓物件`屬性無法新增刪除`、也`無法重新配置`，但是可以`調整目前屬性的值`
預設物件會被加上 `preventExtensions`
`Object.seal(obj)`
[MDN Object.seal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/seal)
範例:

``` JavaScript
var person = {
  a: 1,
  b: 2,
  c: {},
};
Object.seal(person);
console.log('是否被封裝 =>', Object.isSealed(person)); /* 是否被封裝 => true */
console.log('person a 的屬性特徵 =>', Object.getOwnPropertyDescriptor(person, 'a'));
/* { value: 1, writable: true, enumerable: true, configurable: false } */

/* 調整屬性 => 可行 */
person.a = 'a';
/* 新增屬性 => 不可行 */
person.d = 'd';
/* 巢狀屬性調整 => 可行 */
person.c.a = 'ca';
/* 刪除 => 不可行 */
delete person.b;
/* 調整特徵 => 不可行 */
Object.defineProperty(person, 'a', {
  writable: false,
});

console.log('person 物件 =>', person); /* {a: "a", b: 2, c: {a: "ca"}} */
console.log('person a 屬性特徵(修改後) =>', Object.getOwnPropertyDescriptor(person, 'a'));
/* {value: "a", writable: true, enumerable: true, configurable: false} */
```

## 防止凍結 Freeze

物件會加上 `seal`，並且`無法調整值`
`Object.freeze(obj)`
[MDN Object.freeze](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)
範例:

``` JavaScript
var person = {
  a: 1,
  b: 2,
  c: {},
};
Object.freeze(person);
console.log('是否被凍結 =>', Object.isFrozen(person)); /* 是否被凍結=> true */
console.log('person a 的屬性特徵 =>', Object.getOwnPropertyDescriptor(person, 'a'));
/* { value: 1, writable: true, enumerable: true, configurable: false } */

/* 調整屬性 => 不可行 */
person.a = 'a';
/* 新增屬性 => 不可行 */
person.d = 'd';
/* 巢狀屬性調整 => 可行 */
person.c.a = 'ca';
/* 刪除 => 不可行 */
delete person.b;
/* 調整特徵 => 不可行 */
Object.defineProperty(person, 'a', {
  configurable: true,
});

console.log('person 物件 =>', person); /* {a: "a", b: 2, c: {a: "ca"}} */
console.log('person a 屬性特徵(修改後) =>', Object.getOwnPropertyDescriptor(person, 'a'));
/* {value: "a", writable: true, enumerable: true, configurable: false} */
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
