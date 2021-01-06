---
title: JavaScript 核心 (33) - 函式以及 This 的運作 - 工廠模式及私有方法
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 閉包進階技巧，善用工廠模式及私有方法，讓函式功能更加多元。
abbrlink: 546505187
date: 2021-01-06 15:30:00
---
## 工廠模式

可以理解成 `給不同材料數量，生產出相對應的產品數量`，類似工廠在生產產品的流程。

``` JavaScript
function storeMoney(initValue) {
  var money = initValue || 1000;
  return function(price) {
    money = money + price;
    return money;
  }
}

var CloudMoney = storeMoney(100);
console.log(CloudMoney(500)); /* 600 */
```

上面這個範例是回傳一個函式，在回傳一個值，那如果是包在一個回傳物件呢?

下面就來介紹閉包強大的私有方法。

## 私有方法

``` JavaScript
function storeMoney(initValue) {
  var money = initValue || 1000;
  return {
    increase: function(price) {
      return money += price;
    },
    decrease: function(price) {
      return money -= price;
    },
    value: function() {
      return money;
    }
  }
}
/* 第一位 */
var CloudMoney = storeMoney(100);
console.log(CloudMoney.increase(100)); /* 200 */
console.log(CloudMoney.decrease(25)); /* 175 */ 
console.log(CloudMoney.value());  /* 175 */

/* 第二位 */
var TestMoney = storeMoney(500);
console.log(TestMoney.increase(100)); /* 600 */
console.log(TestMoney.decrease(25)); /* 575 */
console.log(TestMoney.value());  /* 575 */
```

透過`回傳物件`的型式，可以讓函式增加許多功能，並且各自獨立呼叫閉包函式時，各自互不干擾。

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(39)-函式以及 This 的運作-閉包進階：工廠模式及私有方法](https://hsiangfeng.github.io/javascript/20201220/423870936/)
