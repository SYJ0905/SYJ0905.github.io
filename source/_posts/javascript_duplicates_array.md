---
title: JavaScript - 取出陣列重複/不重複值的方法
tags:
  - JavaScript
categories:
  - JavaScript
description: 本篇介紹如何取得陣列中重複與不重複值的方法
abbrlink: 865415262
date: 2021-05-21 18:00:00
---
## 狀況情境

有以下陣列，試著取出 重複/不重複 字串與數值

``` JavaScript
const array = [1, 2, 'a', 3, 1, 'b', 'a'];
```

## filter() 方法

搭配 `indexOf()` 方法會回傳給定元素於陣列中`第一個`被找到之索引，若不存在於陣列中則回傳 -1。

``` JavaScript
const array = [1, 2, 'a', 3, 1, 'b', 'a'];
const result = array.filter((element, index, arr) => arr.indexOf(element) === index);
const repeat = array.filter((element, index, arr) => arr.indexOf(element) !== index);
console.log(result);  // {1, 2, "a", 3, "b"}
console.log(repeat); // {1, "a"}
```

## Set()

Set 物件可讓儲存任何類型的唯一值（unique），並且有 `add`、`has` 等方法使用

``` JavaScript
const array = [1, 2, 'a', 3, 1, 'b', 'a'];
const result = new Set();
const repeat = new Set();
array.forEach((item) => {
  if (result.has(item)) {
    repeat.add(item);
  } else {
    result.add(item);
  }
});
console.log(result); // {1, 2, "a", 3, "b"}
console.log(repeat); // {1, "a"}
```

## Object + Object.keys()

``` JavaScript
const array = [1, 2, 'a', 3, 1, 'b', 'a'];
const result = {};
array.forEach((item) => {
  result[item] = result[item] ? result[item] + 1 : 1;
});
console.log(Object.keys(result)); // ["1", "2", "3", "a", "b"]
```

## reduce()

``` JavaScript
const array = [1, 2, 'a', 3, 1, 'b', 'a'];
const result = array.reduce((obj, item) => {
  const object = { ...obj };
  object[item] = 1;
  return object;
}, {});
console.log(Object.keys(result)); // ["1", "2", "3", "a", "b"]
```

## Set + Spread

``` JavaScript
const array = [1, 2, 'a', 3, 1, 'b', 'a'];
// const result = Array.from(new Set(array));
const result = [...(new Set(array))];
console.log(result); // [1, 2, "a", 3, "b"]
```

## 參考資料

[Set](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Set)
[Array.prototype.indexOf()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)
[JavaScript取出陣列重複/不重複值的方法](https://guahsu.io/2017/06/JavaScript-Duplicates-Array/)
