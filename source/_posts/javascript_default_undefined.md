---
title: JavaScript 核心 (23) - 物件 - 未定義的物件屬性預設值
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 呼叫未定義屬性會出現什麼呢? undeinfed 還是 not defined?
abbrlink: 1663111178
date: 2020-12-28 17:00:00
---
## 呼叫未定義屬性

``` JavaScript
var obj = {
  name: 'Cloud',
}
console.log(obj.age); /* undefined */
console.log(obj.age.year); /* Uncaught TypeError: Cannot read property 'year' of undefined */
```

上述範例出現兩個錯誤:

* 第一個是因為物件沒有該屬性，所以呼叫是回傳 undefined。
* 第二個錯誤是因為運算子的相依性 `obj.age` 會是 `undefined`，並且會變成 `undefined.year`，而原始型別的 `undefined` 是不能新增屬性的，所以才會報錯。

然而不是所以有原始型別都不能操作屬性，有幾個還是可以的。

``` JavaScript
/* Number */
Number.test = 100;
console.log('Number.test => ', Number.test); /* Number.test =>  100 */
var a = 123;
console.log('a.test => ', a.test); /* a.test =>  undefined */
a.test = 'Cloud';
console.log('a.test => ', a.test); /* a.test =>  undefined */
console.log('a.test.test_2 => ', a.test.test_2); /* Uncaught TypeError: Cannot read property 'test_2' of undefined */

/* String */
String.test = 'Cloud';
console.log('String.test => ', String.test); /* String.test =>  Cloud */
var a = '123';
console.log('a.test => ', a.test); /* a.test =>  undefined */
a.test = 'Cloud';
console.log('a.test => ', a.test); /* a.test =>  undefined */
console.log('a.test.test_2 => ', a.test.test_2); /* Uncaught TypeError: Cannot read property 'test_2' of undefined */

/* Boolean */
Boolean.test  = 'Cloud';
console.log('Boolean.test => ', Boolean.test); /* Boolean.test =>  Cloud */
var a = true;
console.log('a.test => ', a.test ); /* a.test =>  undefined */
a.test = 'Cloud';
console.log('a.test => ', a.test); /* a.test =>  undefined */
console.log('a.test.test_2 => ', a.test.test_2 ); /* Uncaught TypeError: Cannot read property 'test_2' of undefined */

/* null */
null.test  = 'Cloud'; /* Uncaught TypeError: Cannot set property 'test' of null */
var a = null;
console.log('a.test => ', a.test ); /* Uncaught TypeError: Cannot read property 'test' of null*/
a.test = 'Cloud'; /* Uncaught TypeError: Cannot set property 'test' of null*/
console.log('a.test.test_2 => ', a.test.test_2 ); /* Uncaught TypeError: Cannot read property 'test' of null*/

/* undefined*/
undefined.test  = 'Cloud'; /* Uncaught TypeError: Cannot set property 'test' of undefined */
var a = undefined;
console.log('a.test => ', a.test ); /* Uncaught TypeError: Cannot read property 'test' of undefined*/
a.test = 'Cloud'; /* Uncaught TypeError: Cannot set property 'test' of undefined*/
console.log('a.test.test_2 => ', a.test.test_2 ); /* Uncaught TypeError: Cannot read property 'test' of undefined*/
```

## 解決預設值

* 預先定義物件屬性

``` JavaScript
var obj = {
  name: 'Cloud',
  status: {},
}
obj.status.id = 26; /* 26 */
```

* 賦予屬性

``` JavaScript
var obj = {
  name: 'Ray',
}

obj.status = {};

obj.status.id = 26; /* 26 */
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(25)-物件-未定義的物件屬性預設值](https://hsiangfeng.github.io/javascript/20200808/2097513019/)
