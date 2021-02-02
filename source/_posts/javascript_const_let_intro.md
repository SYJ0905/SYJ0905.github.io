---
title: JavaScript 核心 (50) - ES6 章節：Let 及 Const - Let, Const 基本概念
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 本篇來介紹 ES6 新增的變數宣告 let、const 概念
abbrlink: 807133580
date: 2021-02-01 14:10:00
---
## var 盲點

記著 `var 作用域`是在`函式的區塊內`
來看看 `var` 在使用上會有那些問題吧

* 重複宣告，後者覆蓋前者
* 汙染全域變數

``` JavaScript
/* 重複宣告，後者覆蓋前者 */
var Cloud = '克勞德';
var Cloud = '克勞德_2'
console.log(Cloud); /* 克勞德_2 */  

/* 汙染全域變數 */
for (var i = 0; i < 10; i++) {
  console.log(i); /* 0 1 2 3 4 5 6 7 8 9 */
}
console.log(i); /* 10 */

var answer = true;
if (answer) {
  var myFeedback = '同意';
  console.log(myFeedback); /* 同意 */
}
console.log(myFeedback); /* 同意 */
```

## let const var 差異

* `let`: 變數，可重新賦值，`Block` 為作用域 ex: `{}` 大括號內
* `const`: 常數，不可重新賦值

``` JavaScript
let Cloud = 'Cloud';
let Cloud = '克勞德';
console.log(Cloud); /* Identifier 'Cloud' has already been declared */

let test_1 = '測試_1';
{
  let test_1 = '測試_括號';
}
console.log(test_1); /* 測試_1 */

for (let i = 0; i < 10; i++) {
  console.log(i); /* 0 1 2 3 4 5 6 7 8 9 */
}
console.log(i); /* i is not defined */

var answer = true;
if (answer) {
  let myFeedback = '同意';
  console.log(myFeedback); /* 同意 */
}
console.log(myFeedback); /* myFeedback is not defined */


for (let j = 0; j < 10; j++) {
  console.log(j); /* 0 1 2 3 4 5 6 7 8 9 */
}
console.log(j);
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
