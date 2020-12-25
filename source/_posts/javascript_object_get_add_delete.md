---
title: JavaScript 核心 (20) - 物件 - 物件取值、新增、刪除
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 介紹物件屬性的取得、刪除、新增功能
abbrlink: 2096817927
date: 2020-12-25 18:30:00
---

## 取值

取值方式有兩種:

* 點運算子: 直接找尋物件底下屬性
* 中括號: 中括號內使用字串找尋物件屬性，此外也可以使用傳參數的方式
上範例:

``` JavaScript
var obj = {
  myName: 'Cloud',
  num: 1,
  family: {
    mon: '漂亮阿姨',
  },
  objFn: function() {
    console.log('漂亮阿姨回家囉');
  },
}

/* 點運算子 */
console.log(obj.myName); /* Cloud */
obj.objFn(); /* 漂亮阿姨回家囉 */

/* 中括號 */
var person = 'myName';
obj[person]; /* Cloud */
obj['objFn'](); /* 漂亮阿姨回家囉 */
```

另一個重要觀念是`物件屬性一律都會被轉換成字串`，即使用數字也是會被轉換的。

``` JavaScript
var obj = {
  1: '123',
}
/* 錯誤 */
obj.1; /* Uncaught SyntaxError: Unexpected number */

/* 正確 */
obj['1']; /* '123' */
obj[1]; /* '123' */
```

## 新增

直接用點運算子或是中括號建立屬性，並賦予值即可新增

``` JavaScript
var obj = {
  myName: 'Cloud',
}

obj.test = 'test';
obj['test2'] = 'test2';
console.log(obj); /* {myName: 'Cloud', test: 'test', test2: 'test2'} */
```

## 刪除

使用 `delete` 的方法刪除物件屬性

``` JavaScript
var obj = {
  myName: 'Cloud',
}

obj.test = 'test';
obj['test2'] = 'test2';
console.log(obj); /* {myName: 'Cloud', test: 'test', test2: 'test2'} */

delete obj.test
delete obj['test2']
console.log(obj); /* { myName: 'Cloud' } */
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(22)-物件-物件取值、新增、刪除](https://hsiangfeng.github.io/javascript/20200718/1499259613/)
