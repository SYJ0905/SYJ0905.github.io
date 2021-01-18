---
title: JavaScript 核心 (39) - 函式以及 This 的運作 - 函式的常見陷阱題
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 一起來分析函式的常見陷阱題
abbrlink: 180950825
date: 2021-01-18 12:00:00
---
##　第一題

``` JavaScript
var myName = '全域';
var person = {
  myName: '小明',
  getName: function() {
    return this.myName;
  },
};

var getName = person.getName;
console.log(getName();
/* Ans: 全域 */
```

## 第二題

``` JavaScript
var myName = '全域';

var obj = {
  myName: '奇怪的函式',
  fn: function(a, b, c) {
    return this.myName + ',' + a + ',' + b + ',' + c
  }
}
var fnA = obj.fn;
var fnB = fnA.bind(null, 0);

console.log(fnB(1, 2));
/* Ans: 全域,0,1,2 */
```

## 第三題

``` JavaScript
var value = 'Global';

var foo = {
  value: 'local',
  bar: function() {
    return this.value;
  }
}

// 直接執行
console.log(foo.bar());
//賦值
console.log((foo.bar = foo.bar)());
// or
console.log((false || foo.bar)());

/* Ans: local / Global / Global */
```

## 第四題

``` JavaScript
var arr = ['1', '2', '3'].map(parseInt);
console.log(arr);
/* Ans: [1, NaN, NaN] */


/* 解析 */
var arr = ['1', '2', '3'].map((item, index) => {
  return parseInt(item, index);
});
console.log(arr);
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(45)-函式以及 This 的運作-總結：函式的常見陷阱題](https://hsiangfeng.github.io/javascript/20210113/1357538756/)
