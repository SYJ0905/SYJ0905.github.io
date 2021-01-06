---
title: JavaScript 核心 (25) - 物件 - Call by Reference 還是 Call by Sharing
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: JavaScript 的物件上是屬於 Call by Sharing，那與 Call by Reference 差異是什麼呢?
abbrlink: 833919043
date: 2020-12-30 16:30:00
---
## 傳參照呼叫 Call by reference

[傳參照呼叫](https://zh.wikipedia.org/zh-tw/%E6%B1%82%E5%80%BC%E7%AD%96%E7%95%A5#%E4%BC%A0%E5%BC%95%E7%94%A8%E8%B0%83%E7%94%A8%EF%BC%88-{Call_by_reference}-%EF%BC%89)
傳遞給函式的是它的實際參數的隱式參照而不是實參的拷貝。

``` JavaScript
function fn (a) {
  var temp = 100;
  a.x = temp;
  a['y'] = a.x;
}

var obj = {
  x: 10,
  y: 20,
}

fn(obj);

console.log(obj.x, obj.y); /* 100, 100 */
```

## 傳共享物件呼叫 Call by sharing

[傳共享物件呼叫](https://zh.wikipedia.org/zh-tw/%E6%B1%82%E5%80%BC%E7%AD%96%E7%95%A5#%E4%BC%A0%E5%85%B1%E4%BA%AB%E5%AF%B9%E8%B1%A1%E8%B0%83%E7%94%A8%EF%BC%88-{Call_by_sharing}-%EF%BC%89)
對於呼叫者而言在被呼叫函數裡修改參數是沒有影響的。如果要達成傳參照呼叫的效果就需要傳一個共享物件，一旦被呼叫者修改了物件，呼叫者就可以看到變化（因為物件是共享的，沒有拷貝）。

``` JavaScript
function fn (a) {
  a = {
    b: 100,
    c: 50
  }
}

var obj = {
  x: 10,
  y: 20,
}

fn(obj);

console.log(obj); /* { x: 10, y: 20, } */
```

由此可知兩點:

* 對傳入的參數進行`點運算、中括號`賦值等操作會是 `Call by reference`
* 對傳入的參數進行`物件實字宣告`賦值等操作會是 `Call by sharing`

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(29)-物件-Call by Reference 還是 Call by Sharing](https://hsiangfeng.github.io/javascript/20200904/1772972600/)
