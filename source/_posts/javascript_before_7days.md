---
title: JavaScript - 如何獲取前 7 天日期
tags:
  - JavaScript
categories:
  - JavaScript
description: 使用 new Date 與 getTime() 獲取前 7 天日期
abbrlink: 3564669203
date: 2021-02-22 21:00:00
---
## parseInt()

`parseInt(string, radix)`

* `string` : 待轉成數字的字串。若 string 參數類型不是字串的話，會先將其轉成字串
* `radix` : 從 2 到 36，能代表該進位系統的數字

## parseInt() vs parseFloat() vs Number()

在本範例中，使用這三個函式都是相同結果的，之後會寫一篇專門來介紹這三者的差異

## 參考程式碼

``` JavaScript
const now = new Date();
const nowMs = now.getTime();
const beforeMs = nowMs - (1000 * 60 * 60 * 24 * parseInt(7, 10));
// const beforeMs = nowMs - (1000 * 60 * 60 * 24 * parseFloat(7, 10));
// const beforeMs = nowMs - (1000 * 60 * 60 * 24 * Number(7, 10));

const test_1 = new Date(beforeMs).toISOString();

const test_2 = new Date().toISOString();

console.log('test_1 => ', test_1);
console.log('test_2 => ', test_2);
```

## 參考資料

[js获取前七天的日期](https://blog.csdn.net/liuguochao1024/article/details/79576365?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-1.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-1.control)
