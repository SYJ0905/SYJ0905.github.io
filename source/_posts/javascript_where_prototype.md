---
title: JavaScript 核心 (41) - 繼承與原型鍊 - 原型在哪裡
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 本篇介紹原型觀念
abbrlink: 2810333641
date: 2021-01-22 14:30:00
---
## 原型的特性

* 一樣具有物件的特性
* 向上查找
* 原型可以共用方法及屬性
![向上查找](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/JavaScript%20%E6%A0%B8%E5%BF%83%20(41)%20-%20%E7%B9%BC%E6%89%BF%E8%88%87%E5%8E%9F%E5%9E%8B%E9%8D%8A%20-%20%E5%8E%9F%E5%9E%8B%E5%9C%A8%E5%93%AA%E8%A3%A1%2F%E6%93%B7%E5%8F%96.JPG?alt=media&token=23d4adb2-6b49-43b8-9e79-6fa064e0d35e)
![原型可以共用方法及屬性](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/JavaScript%20%E6%A0%B8%E5%BF%83%20(41)%20-%20%E7%B9%BC%E6%89%BF%E8%88%87%E5%8E%9F%E5%9E%8B%E9%8D%8A%20-%20%E5%8E%9F%E5%9E%8B%E5%9C%A8%E5%93%AA%E8%A3%A1%2F%E6%93%B7%E5%8F%962.JPG?alt=media&token=f8718d83-eeec-4368-aba4-c91b5e2720a9)

以下用範例操作看看:

``` JavaScript
var a = [1, 2, 3];
console.log(a[1], a.length); /* 2 3 */
a.forEach(function(i) {
  console.log(i);
  /* 1 */
  /* 2 */
  /* 3 */
})
```

`forEach()` 並不是 `a` 物件內方法，而是在 `array` 的原型方法
![__proto__](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/JavaScript%20%E6%A0%B8%E5%BF%83%20(41)%20-%20%E7%B9%BC%E6%89%BF%E8%88%87%E5%8E%9F%E5%9E%8B%E9%8D%8A%20-%20%E5%8E%9F%E5%9E%8B%E5%9C%A8%E5%93%AA%E8%A3%A1%2F__proto__.JPG?alt=media&token=580a91b1-1969-4d47-b36e-2e6922d8f31d)

``` JavaScript
var a = [1, 2, 3];
var b = [4, 5, 6];
a.__proto__.getLast = function() {
  return this[this.length - 1];
};

/* 此時 array 的原型中就有 getLast 函式 */
/* 所以 b 就可以使用 */
console.log(a.getLast()); /* 3 */
console.log(b.getLast()); /* 6 */
```

由上述範例可知 `原型可以共用方法及屬性`

``` JavaScript
var family = {
  name: '小明家',
};
family.__proto__.getName = function() {
  return this.name;
};

console.log(family.getName()); /* 小明家 */

var b = [4, 5, 6];
b.name = '陣列的屬性';
console.log(b.getName()); /* 陣列的屬性 */
```

`陣列原型` 的 `__proto__` 是 `物件原型`，也就是最頂層原型
由此可知 `原型有多個層級，可以不斷向上查找`

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
