---
title: JavaScript 核心 (44) - 繼承與原型鍊 - 使用 Object.create 建立多層繼承
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 本篇介紹如何製作更完善的原型鍊
abbrlink: 2757333667
date: 2021-01-25 18:30:00
---
## 多層繼承

先前介紹都類似 `Object > Dog > 實體` 這樣的繼承鍊。
若想在 `Dog` 前面在多加一層原型變成 `Object > Animal > Dog > 實體` 呢?
這時就要用到 `Object.create()`
[MDN Object.create()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Object/create)
`Object.create(proto[, propertiesObject])`

* proto: 指定新物件的原型 (prototype) 物件。
* propertiesObject: 選用，為一物件(細節參考文檔)。

範例說明:

1. 在 Animal 上新增原型方法`move()`
2. `Dog()` 繼承 Animal的原型 `prototype`，並新增 `bark()` 原型方法

``` JavaScript
function Animal(family) {
  this.kingdom = '動物界';
  this.family = family || '人界';
  console.log('this', this); /* 指向 Dog Cat 物件 */
};

Animal.prototype.move = function () {
  console.log(this.name + '移動');
};

function Dog(name, color, size) {
  /* 目前只有繼承動物界原型，還需要繼承 動物界 建構函式 */
  /* 繼承動物界建構函式 start */
  Animal.call(this, '犬科'); /* 此時的 this 可以看成是 Dog 的一個空物件 */
  /* 繼承動物界建構函式 end */
  this.name = name;
  this.color = color || '白色';
  this.size = size || '小';
  /* 沒有 return 物件的話，會默認 return this */
  // return this;
};
Dog.prototype = Object.create(Animal.prototype);
/* 補回原本 Dog 的建構函式 */
Dog.prototype.constructor = Dog;
Dog.prototype.bark = function() {
  console.log(this.name + '吠叫');
};

var Bibi = new Dog('比比', '棕色', '小');
console.log(Bibi);/* Dog {kingdom: "動物界", family: "犬科", name: "比比", color: "棕色", size: "小"} */
Bibi.bark(); /* 比比吠叫 */
Bibi.move(); /* 比比移動 */


function Cat(name, color, size) {
  Animal.call(this, '貓科');
  this.name = name;
  this.color = color || '白色';
  this.size = size || '小';
};

Cat.prototype = Object.create(Animal.prototype);
Cat.prototype.constructor = Cat;
Cat.prototype.meow = function() {
  console.log(this.name + '喵喵叫');
};

var Kity = new Cat('凱蒂', '', '大');
console.log(Kity); /* Cat {kingdom: "動物界", family: "貓科", name: "凱蒂", color: "白色", size: "小"} */
Kity.meow(); /* 凱蒂喵喵叫 */
Kity.move(); /* 凱蒂移動 */
Kity.bark(); /* Kity.bark is not a function */
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
