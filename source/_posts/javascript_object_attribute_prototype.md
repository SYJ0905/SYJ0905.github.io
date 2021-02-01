---
title: JavaScript 核心 (48) - 物件屬性延伸 - 屬性列舉與原型的關係
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 本篇會介紹屬性特徵是如何影響列舉的功能
abbrlink: 3829070841
date: 2021-02-01 11:00:00
---
## 原型屬性顏色判斷

``` JavaScript
function Person() {};
Person.prototype.name = '人類';
var Cloud = new Person();
Cloud.a = undefined;
console.log(Cloud);

console.log(Cloud.hasOwnProperty('a')); /* true */
console.log(Cloud.hasOwnProperty('b')); /* false */
console.log(Cloud.hasOwnProperty('name')); /* false */

for (var key in Cloud) {
  console.log(key);
  /* a */
  /* name */
}
```

使用 `hasOwnProperty()` 只針對當下物件是否有該屬性，但使用 `for in` 卻可以顯示出 `name`，究竟是為什麼呢?

由下圖可知，`Cloud 的 a` 跟 `name` 顏色都是相同的，而原型功能的顏色卻不一樣
![屬性顏色判斷](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/JavaScript%20%E6%A0%B8%E5%BF%83%20(48)%20-%20%E7%89%A9%E4%BB%B6%E5%B1%AC%E6%80%A7%E5%BB%B6%E4%BC%B8%20-%20%E5%B1%AC%E6%80%A7%E5%88%97%E8%88%89%E8%88%87%E5%8E%9F%E5%9E%8B%E7%9A%84%E9%97%9C%E4%BF%82%2F%E6%93%B7%E5%8F%96.JPG?alt=media&token=d96936c2-5427-40cb-92de-df4deb372bf9)

## 屬性列舉影響

新增原型的屬性預設其特徵都是會全開的`(configurable: true, enumerable: true, writable: true)`，而原型本身的功能其實是 `enumerable: false`　不可列舉

``` JavaScript
function Person() {};
Person.prototype.name = '人類';
var Cloud = new Person();
Cloud.a = undefined;

for (var key in Cloud) {
  console.log(key);
  /* a */
  /* name */
}

console.log(Object.getOwnPropertyDescriptor(Cloud.__proto__, 'name'));
console.log(Object.getOwnPropertyDescriptor(Cloud.__proto__.__proto__, 'toString'));
```

![enumerable 比對](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/JavaScript%20%E6%A0%B8%E5%BF%83%20(48)%20-%20%E7%89%A9%E4%BB%B6%E5%B1%AC%E6%80%A7%E5%BB%B6%E4%BC%B8%20-%20%E5%B1%AC%E6%80%A7%E5%88%97%E8%88%89%E8%88%87%E5%8E%9F%E5%9E%8B%E7%9A%84%E9%97%9C%E4%BF%82%2Fenumerable%20%E6%AA%A2%E6%9F%A5.JPG?alt=media&token=3f235090-483a-47f0-8455-4cd06bbadc28)

## 列舉正確做法

由上述可知，新增原型屬性若是沒有做好特徵定義，當依照建構式新增物件後使用迴圈時，就會有問題產生。
有兩種方法可以避免問題產生:

* 重新設定原型特徵(不推薦)

``` JavaScript
function Person() {};
Person.prototype.name = '人類';
Object.defineProperty(Person.prototype, 'name', {
  enumerable: false,
});
var Cloud = new Person();
Cloud.a = undefined;

for (var key in Cloud) {
  console.log(key);
  /* a */
}
```

* 迴圈判定(推薦)

``` JavaScript
function Person() {};
Person.prototype.name = '人類';
var Cloud = new Person();
Cloud.a = undefined;

for (var key in Cloud) {
  if (Cloud.hasOwnProperty(key)) {
    console.log(key);
    /* a */
  }
}
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
