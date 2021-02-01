---
title: JavaScript 核心 (49) - 物件屬性延伸 - Getter 與 Setter，賦值運算不使用函式
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 本篇會介紹如何使用物件中的 get 和 set 功能
abbrlink: 3056751174
date: 2021-02-01 12:00:00
---
## 物件賦值

一開始學的物件賦值都是使用直接賦值的方式，然而物件有提供 `取值`、`賦值` 的功能，可以做出類似物件內函式的操作呦

``` JavaScript
var wallet = {
  total: 100,
};

wallet.total = 300;

console.log(wallet.total);
```

## get、set

設定物件 `get`、`set` 有兩種方法

* 物件內定義

``` JavaScript
var wallet = {
  total: 100,
  set save(price) {
    this.total = this.total + price;
  },
  get save() {
    return this.total / 2;
  },
};
console.log(wallet.save); /* 50 */

/* 使用 = 號賦值 */
wallet.save = 300;

console.log(wallet.save); /* 400 */
console.log(wallet);
console.log(Object.getOwnPropertyDescriptor(wallet, 'save'));
/* { enumerable: true, configurable: true, get: ƒ, set: ƒ } */
```

此時的 `save` 是可以被列舉、可被刪除的設定
![屬性特徵](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/JavaScript%20%E6%A0%B8%E5%BF%83%20(49)%20-%20%E7%89%A9%E4%BB%B6%E5%B1%AC%E6%80%A7%E5%BB%B6%E4%BC%B8%20-%20Getter%20%E8%88%87%20Setter%EF%BC%8C%E8%B3%A6%E5%80%BC%E9%81%8B%E7%AE%97%E4%B8%8D%E4%BD%BF%E7%94%A8%E5%87%BD%E5%BC%8F%2F%E6%93%B7%E5%8F%961.JPG?alt=media&token=210f423b-c0fd-42c4-a06a-5b0f9eb68be1)

* definedProperty 法

``` JavaScript
var wallet = {
  total: 100,
};

Object.defineProperty(wallet, 'save', {
  set: function(price) {
    this.total = this.total + price;
  },
  get: function() {
    return this.total / 2;
  },
});

/* 使用 = 號賦值 */
wallet.save = 300;

console.log(wallet.save); /* 400 */
console.log(wallet);
console.log(Object.getOwnPropertyDescriptor(wallet, 'save'));
/* { enumerable: false, configurable: false, get: ƒ, set: ƒ } */
```

由於此方法會讓 `save` 視為原型屬性，所以是不可列舉的、不可被刪除的設定，除非有再額外調整特徵。
![屬性特徵](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/JavaScript%20%E6%A0%B8%E5%BF%83%20(49)%20-%20%E7%89%A9%E4%BB%B6%E5%B1%AC%E6%80%A7%E5%BB%B6%E4%BC%B8%20-%20Getter%20%E8%88%87%20Setter%EF%BC%8C%E8%B3%A6%E5%80%BC%E9%81%8B%E7%AE%97%E4%B8%8D%E4%BD%BF%E7%94%A8%E5%87%BD%E5%BC%8F%2F%E6%93%B7%E5%8F%962.JPG?alt=media&token=3d0c52d1-2718-4765-ac9b-9ec4c790caa3)

修正後:

``` JavaScript
var wallet = {
  total: 100,
};

Object.defineProperty(wallet, 'save', {
  configurable: true,
  enumerable: true,
  set: function(price) {
    this.total = this.total + price;
  },
  get: function() {
    return this.total / 2;
  },
});

/* 使用 = 號賦值 */
wallet.save = 300;

console.log(wallet.save); /* 400 */
console.log(wallet);
console.log(Object.getOwnPropertyDescriptor(wallet, 'save'));
/* { enumerable: true, configurable: true, get: ƒ, set: ƒ } */
```

## 陣列也適用

由於陣列也是物件的一種，所以也能使用 `get`、`set`，但只能用 `defineProperty` 設定哩

``` JavaScript
var a = [1, 2, 3];
var b = [4, 5, 6];
var c = [7, 8, 9];
Object.defineProperty(a, 'latest', {
  get: function() {
    return this[this.length - 1];
  },
});

console.log(a.latest); /* 3 */
console.log(b.latest); /* undefined */  

Object.defineProperty(Array.prototype, 'latest', {
  get: function() {
    return this[this.length - 1];
  },
});

console.log(c.latest); /* 9 */
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
