---
title: JavaScript 核心 (43) - 繼承與原型鍊 - 原始型別的包裹物件與原型的關聯
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 運用原始型別包裹物件來新增 prototype 方法
abbrlink: 4216074588
date: 2021-01-25 12:30:00
---
## 包裹物件

先前有提過原始型別有各自的包裹物件，並且包裹物件有對應的 `prototype`，如此以來也就能新增包裹物件中的方法屬性哩

* 字串範例

``` JavaScript
var name = 'Cloud';
var b = new String('bcde');

console.log(b); /* String {"bcde"} */
console.dir(String); /* ƒ String() */

String.prototype.lastText = function() {
  return this[this.length - 1]
};

console.log(b.lastText()); /* e */
console.log(name.lastText()); /* d */
```

* 數值範例

``` JavaScript
Number.prototype.secondPower = function() {
  return this * this;
};

var num = 5;
console.log(num.secondPower()); /* 25 */
```

* 其他建構式

``` JavaScript
var date = new Date();
console.log(date); /* Mon Jan 25 2021 12:07:31 GMT+0800 (台北標準時間) */
console.dir(Date); /* 裡面的 prototype 有超多方法 */

Date.prototype.getFullDate = function() {
  var dd = String(this.getDate());
  var mm = String(this.getMonth() + 1);
  var yyyy = this.getFullYear();
  var today = `${yyyy}/${mm}/${dd}`;
  return today;
};
console.log(date.getFullDate()); /* 2021/1/25 */
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
