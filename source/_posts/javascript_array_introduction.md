---
title: JavaScript 核心 (26) - 物件 - 陣列
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 接下來介紹 JavaScript 中陣列的寫法
abbrlink: 4202138340
date: 2021-01-04 16:00:00
---
## 陣列

陣列常被誤以為是 JavaScript 中的一個型別，但千萬要記得 JS 中只有兩種型別:

* 原始型別(七種)
* 物件型別
好了，試問陣列是哪一種呢?
反正只要`不是原始型別`，一律都屬於物件型別，想都不用想。

## 陣列實字

JavaScript 的陣列中可以加入任何型別，部分程式語言是無法像 JavaScript 這麼隨性的

``` JavaScript
var arr = [
  1,
  '1',
  true,
  undefined,
  {},
];
```

## 取值

陣列的順序是從 `0` 開始計算

``` JavaScript
var arr = [
  1,
  '1',
  true,
  undefined,
  {},
];

arr[2]; /* true */
```

## 新增

使用 `push()`，可在陣列最後新增內容

``` JavaScript
var arr = [
  1,
  '1',
  true,
  undefined,
  {},
];

arr.push('Cloud');
```

## 新增屬性!?

陣列還可新增屬性喔，並且這個屬性不會影響到陣列的長度。

``` JavaScript
var arr = [
  1,
  '1',
  true,
  undefined,
  {},
];
arr.name = 'Cloud';
console.log(arr.length); /* 5 */
```

## 空值

直接賦予值在指定順序的位置，若中間有空的順序，則以 `empty` 表示

``` JavaScript
var arr = [
  1,
  '1',
  true,
  undefined,
  {},
];
arr[10] = 'Cloud';
console.log(arr[6]); /* undefined */
console.log(arr); /* [1, "1", true, undefined, {…}, empty × 5, "Cloud"] */
```

## 迴圈找值

``` JavaScript
var arr = [
  1,
  '1',
  true,
  undefined,
  {},
];

var arrLen = arr.length

/* for　迴圈 */
for(var i = 0; i <= arrLen; i += 1) {
  console.log(arr[i]);
}

/* forEach　迴圈 */
arr.forEach(function (item){
  console.log(item);
})
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(31)-物件-陣列](https://hsiangfeng.github.io/javascript/20201108/33884/)
