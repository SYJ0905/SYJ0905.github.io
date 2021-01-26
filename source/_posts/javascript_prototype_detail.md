---
title: JavaScript 核心 (45) - 繼承與原型鍊 - 原型鏈、建構函式整體結構概念
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 本篇將完整解析原型鍊、建構函式到底是怎麼運作的。
abbrlink: 579374325
date: 2021-01-26 16:00:00
---
## 範例程式碼

我們會以下列程式碼來分別介紹 `__proto__` 、 `prototype`跟物件以及函式的關係:

1. 物件的 __proto__ 是誰?

2. 建構函式 `prototype` 與 `__proto__` 關係

3. Function Object 的 `__proto__` 、 `prototype` 關係

``` JavaScript
function Animal(family) {
  this.kingdom = '動物界';
  this.family = family || '人界';
};
Animal.prototype.move = function () {
  console.log(this.name + '移動');
};
function Dog(name, color, size) {
  Animal.call(this, '犬科');
  this.name = name;
  this.color = color || '白色';
  this.size = size || '小';
};
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;
Dog.prototype.bark = function() {
  console.log(this.name + '吠叫');
};
var Bibi = new Dog('比比', '棕色', '小');
Bibi.bark();
Bibi.move();
```

* 物件的 `__proto__` 是誰?
Bibi `透過（重點) __proto__` 會向上找到 `Dog.prototype`，這個 `Dog.prototype`是依照 `constructor` 而建立。
`Dog.prototype` 的 `constructor` 則會指向 `Dog 建構函式`
![__proto__](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/JavaScript%20%E6%A0%B8%E5%BF%83%20(45)%20-%20%E7%B9%BC%E6%89%BF%E8%88%87%E5%8E%9F%E5%9E%8B%E9%8D%8A%20-%20%E5%8E%9F%E5%9E%8B%E9%8F%88%E3%80%81%E5%BB%BA%E6%A7%8B%E5%87%BD%E5%BC%8F%E6%95%B4%E9%AB%94%E7%B5%90%E6%A7%8B%E6%A6%82%E5%BF%B5%2F1.JPG?alt=media&token=b67202d1-a935-4c9e-af55-94038569fbc0)

* 建構函式 `prototype` 與 `__proto__`
使用 `Dog.prototype` 來產生相對應的原型，而之所以能這樣使用是因為 `Dog.__proto__` 也繼承於 `Function.prototype`
![建構函式 prototype](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/JavaScript%20%E6%A0%B8%E5%BF%83%20(45)%20-%20%E7%B9%BC%E6%89%BF%E8%88%87%E5%8E%9F%E5%9E%8B%E9%8D%8A%20-%20%E5%8E%9F%E5%9E%8B%E9%8F%88%E3%80%81%E5%BB%BA%E6%A7%8B%E5%87%BD%E5%BC%8F%E6%95%B4%E9%AB%94%E7%B5%90%E6%A7%8B%E6%A6%82%E5%BF%B5%2F2.JPG?alt=media&token=5a0210dc-2942-4d64-a04f-ff5a7f09315d)

* Function Object 的 `__proto__` 、 `prototype`
`Function.constructor` 則回指向 `Function` 本身
而 `Function.__proto__` 又會指向 `Function.prototype`
`Function.prototype.__proto__` 又會指向 `Object.prototype`
![Function Object prototype](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/JavaScript%20%E6%A0%B8%E5%BF%83%20(45)%20-%20%E7%B9%BC%E6%89%BF%E8%88%87%E5%8E%9F%E5%9E%8B%E9%8D%8A%20-%20%E5%8E%9F%E5%9E%8B%E9%8F%88%E3%80%81%E5%BB%BA%E6%A7%8B%E5%87%BD%E5%BC%8F%E6%95%B4%E9%AB%94%E7%B5%90%E6%A7%8B%E6%A6%82%E5%BF%B5%2F3.JPG?alt=media&token=31b81b32-cf1a-44c4-aebe-fdae281fe0fc)

## 驗證

``` JavaScript
function Animal(family) {
  this.kingdom = '動物界';
  this.family = family || '人界';
};
Animal.prototype.move = function () {
  console.log(this.name + '移動');
};
function Dog(name, color, size) {
  Animal.call(this, '犬科');
  this.name = name;
  this.color = color || '白色';
  this.size = size || '小';
};
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;
Dog.prototype.bark = function() {
  console.log(this.name + '吠叫');
};
var Bibi = new Dog('比比', '棕色', '小');

console.log(Bibi); /* true */

console.log(Bibi.__proto__ === Dog.prototype); /* true */
console.log(Bibi.__proto__.__proto__ === Animal.prototype); /* true */
console.log(Bibi.__proto__.__proto__.constructor === Animal); /* true */
console.log(Bibi.__proto__.__proto__.__proto__.__proto__ === null);  /* true */

console.log(Dog.__proto__ === Function.prototype);  /* true */
console.log(Animal.__proto__ === Function.prototype);  /* true */
console.log(Object.__proto__ === Function.prototype);  /* true */

console.log(Function.__proto__ === Function.prototype);  /* true */
console.log(Function.__proto__.__proto__ === Object.prototype);  /* true */
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
