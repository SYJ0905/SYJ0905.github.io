---
title: JavaScript 核心 (42) - 繼承與原型鍊 - 使用建構式自定義原型
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 利用建構式有效的新增原型內容
abbrlink: 1855392321
date: 2021-01-25 10:30:00
---
## 建構式

[MDN new operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new)
利用建構式創建多種物件，再利用 `prototype` 新增原型功能，即可讓所有藉此原型創建的物件都具備該`方法or屬性`。
這種方法可以有效地降低記憶體空間，因為若替每個物件都加上`相同方法or屬性`，會大幅增加記憶體的使用空間，而運用原型新增一次即可讓所有新物件都具備功能屬性，而只會使用到一個記憶體空間。

``` JavaScript
function Dog(name, color, size) {
  this.name = name;
  this.color = color;
  this.size = size;
  /* 沒有 return 物件的話，會默認 return this */
  // return this;
}

var Bibi = new Dog('比比', '棕色', '小');
var Pupu = new Dog('噗噗', '白色', '大');
console.log(Bibi); /* Dog {name: "比比", color: "棕色", size: "小"} */
console.log(Pupu); /* Dog {name: "噗噗", color: "白色", size: "大"} */
console.log(Dog);


Dog.prototype.bark = function() {
  console.log(this.name + `吠叫`);
}
Dog.prototype.test = '測試';

console.log(Bibi.bark()); /* 比比吠叫 */
console.log(Pupu.bark());  /* 噗噗吠叫 */
console.log(Bibi.test); /* 測試 */
console.log(Pupu.test); /* 測試 */
```

## __proto__ vs prototype

* `__proto__` : 物件連結原型的屬性，並非正式屬性，會造成原型來源不明，造成維護困難。
* `prototype` : 函式原型屬性
雖然這兩個是相同的，但操作原型都還是使用 `prototype` 為主

``` JavaScript
function Dog(name, color, size) {
  this.name = name;
  this.color = color;
  this.size = size;
}
var Bibi = new Dog('比比', '棕色', '小');
console.log(Dog.prototype === Bibi.__proto__); /* true */
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
