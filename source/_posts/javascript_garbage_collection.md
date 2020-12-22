---
title: JavaScript 核心 (8) - 執行環境與作用域 - 回收機制
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 了解記憶體存放回收機制，將有助於撰寫更優良的程式碼
abbrlink: 3236158139
date: 2020-12-22 12:00:00
---

## 回收機制 Garbage Collection

又稱 `垃圾回收`，回收機制是一個自動化記憶體管理機制，舉凡宣告變數、執行函式這些都會占用記憶體空間，若沒有固定清理這些暫存記憶體，很快就會沒有空間可以繼續利用，進而導致網頁 lag 不順等等狀況。

## JS 的回收機制

回收機制是指 `「當物件不再被使用或是不再被其他物件參考時」，它才會被視為一個可回收的記憶體。`。
而在先前有說過 JS 有所謂的執行推疊，並且由後往前釋放，而當中就會將其函式所占用的記憶體一併回收。
以下舉例:

``` JavaScript
/* 隨機生成很長的字串來佔用記憶體 */
function randomString(length) {
  var result = '';
  var characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
  var charactersLength = characters.length;
  for (var i = 0; i < length; i++) {
    result += characters.charAt(Math.floor(Math.random() * charactersLength));
  }
  return result;
}


/* demoData 將持續占用記憶體空間 */
var demoData = [];
function getData() {
  for (let i = 0; i < 1000; i++) {
    demoData.push(randomString(5000));
  }
}
getData();
console.log(demoData);
```

在 `Memory` 中查看占用狀況
![記憶體占用](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/JavaScript%20%E6%A0%B8%E5%BF%83%20(8)%20-%20%E5%9F%B7%E8%A1%8C%E7%92%B0%E5%A2%83%E8%88%87%E4%BD%9C%E7%94%A8%E5%9F%9F%20-%20%E5%9B%9E%E6%94%B6%E6%A9%9F%E5%88%B6%2F%E8%A8%98%E6%86%B6%E9%AB%94%E5%8D%A0%E7%94%A8.jpg?alt=media&token=8713825c-2e7b-4a66-a0da-39c0a9f7ee8c)

即使是清掉 `console.log` 也依舊有很高的佔比。
將上面的函式修改成以下後再執行一次

``` JavaScript
function getData() {
  var demoData = [];
  for (var i = 0; i < 1000; i++) {
    demoData.push(randomString(5000))
  }
  // console.log(demoData);
}
getData()
```

![記憶體占用](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/JavaScript%20%E6%A0%B8%E5%BF%83%20(8)%20-%20%E5%9F%B7%E8%A1%8C%E7%92%B0%E5%A2%83%E8%88%87%E4%BD%9C%E7%94%A8%E5%9F%9F%20-%20%E5%9B%9E%E6%94%B6%E6%A9%9F%E5%88%B6%2F%E8%A8%98%E6%86%B6%E9%AB%94%E5%8D%A0%E7%94%A8(%E6%94%B9%E8%89%AF).jpg?alt=media&token=b517f893-651a-4a0e-be2a-35163fedfa60)

由此可知，在一開始時記憶體占用確實很高沒錯，但隨後因為`回收機制`的關係，`demoData`不再被參考或使用，就會釋放記憶體空間

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(8)-執行環境與作用域-記憶體存放與釋放](https://hsiangfeng.github.io/javascript/20200524/995184384/)
