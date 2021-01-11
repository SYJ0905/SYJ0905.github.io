---
title: JavaScript 核心 (34) - 函式以及 This 的運作 - 最常見的 this：物件的方法調用
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 究竟 this 是什麼? 為什麼會讓眾多開發者頭痛呢?
abbrlink: 490625006
date: 2021-01-11 15:00:00
---
## this

先來介紹 this 是什麼?出現在什麼時候?

``` JavaScript
function fn() {}

fn();
```

執行上述範例後，可在 `F12 source` 中得知 this 會指向 `Window`
因此，`只要執行環境成立`，this 就會自動生成，不需要額外設定。
只是要知道這個 this 到底是指向什麼東西。

## this 基本觀念

以下三點是 this 觀念

* 每個執行環境都有屬於自己的 this 關鍵字
* this 與函式`如何宣告沒有關連性`，僅與 `呼叫方法` 有關
* `嚴格模式下`，簡易呼叫會有很大的改變
![this 觀念](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/JavaScript%20%E6%A0%B8%E5%BF%83%20(34)%20-%20%E5%87%BD%E5%BC%8F%E4%BB%A5%E5%8F%8A%20This%20%E7%9A%84%E9%81%8B%E4%BD%9C%20-%20%E6%9C%80%E5%B8%B8%E8%A6%8B%E7%9A%84%20this%EF%BC%9A%E7%89%A9%E4%BB%B6%E7%9A%84%E6%96%B9%E6%B3%95%E8%AA%BF%E7%94%A8%2F%E6%88%AA%E5%9C%96%202020-12-27%2022.50.01.png?alt=media&token=7688a1ec-71b4-4168-a246-fea5e366eee0)

## 影響 this 的呼叫方法

* 作為物件方法(最常運用 this 的方法)
* 簡易呼叫(絕大多數的呼叫方式)
* bind、apply、call 方法
* new
* DOM 事件處理器
* 箭頭函式(ES6)
![影響 this 的呼叫方法](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/JavaScript%20%E6%A0%B8%E5%BF%83%20(34)%20-%20%E5%87%BD%E5%BC%8F%E4%BB%A5%E5%8F%8A%20This%20%E7%9A%84%E9%81%8B%E4%BD%9C%20-%20%E6%9C%80%E5%B8%B8%E8%A6%8B%E7%9A%84%20this%EF%BC%9A%E7%89%A9%E4%BB%B6%E7%9A%84%E6%96%B9%E6%B3%95%E8%AA%BF%E7%94%A8%2F%E6%88%AA%E5%9C%96%202020-12-27%2022.53.28.png?alt=media&token=6ed466f4-d883-44a0-a5da-0d2237fe7386)

切記，看到 this 不要慌，找出這個 this 是依照上述`哪一個方法呼叫`的，就能知道這個 this 到底是指向誰?

## this 作為物件方法調用(最常見形式)

* 物件方法調用時，`僅須關注是在哪一個物件下`呼叫的

``` JavaScript
var data = {
  name: 'Cloud',
  callName() {
    console.log(this.name);
  },
}

data.callName(); /* Cloud */
```

由於 `callName()` 是在 `data` 底下呼叫的，所以 `callName` 中的 `this` 就會指向 `data` 這個物件。

一般不會將函式寫在物件內，而是獨立出來在用變數賦予物件內的屬性使用:

``` JavaScript
function fn () {
  console.log(this.name);
}
var data = {
  name: 'Cloud',
  callName: fn,
}

data.callName(); /* Cloud */
```

我們`不需要管 fn() 在哪裡`， 只需要知道 `fn()` 是怎麼呼叫的，上述範例依舊是回傳 `Cloud`。

在複雜一點的範例:

``` JavaScript
function fn () {
  console.log(this.name);
}
var data = {
  name: 'Cloud',
  callName: fn,
  ming: {
    name: 'Cloud2',
    callName: fn,
  }
}

data.callName(); /* Cloud */
data.ming.callName(); /* Cloud2 */
```

`data.callName()` 是在 `data` 底下呼叫，指向 `data`
`data.ming.callName()` 則是在 `data.ming` 底下呼叫，指向 `data.ming`

來看看以下錯誤示範:

``` JavaScript
function fn () {
  console.log(this.myName);
}
var data = {
  myName: 'Cloud',
  callName: fn,
  ming: {
    myName: 'Cloud2',
    callName: fn,
  }
}

var a = data.callName;
a(); /* undefined */
/* window.a(); */
```

為什麼是 `undefined` 呢?
`this.myName` 是由 a() 呼叫，而 `a()` 也等於 window.a()，所以這個 this 會指向 window，並且因為 window.myName 沒有值，所以是 undefined。

那該如何修正呢?

``` JavaScript
var myName = 'Cloud3'
function fn () {
  console.log(this.myName);
}
var data = {
  myName: 'Cloud',
  callName: fn,
  ming: {
    myName: 'Cloud2',
    callName: fn,
  }
}

var a = data.callName;
a(); /* Cloud3 */
```

只要在全域賦予一個變數 `myName` 即可。

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(40)-函式以及 This 的運作-最常見的 this：物件的方法調用](https://hsiangfeng.github.io/javascript/20201227/2207483464/)
