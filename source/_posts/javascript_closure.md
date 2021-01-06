---
title: JavaScript 核心 (32) - 函式以及 This 的運作 - 閉包 Closure
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 除了垃圾回收機制以外，閉包的使用也與記憶體有很大關係。
abbrlink: 1355597142
date: 2021-01-06 11:30:00
---
## 閉包 Closure

[MDN 閉包 Closure](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Closures)
前面在介紹記憶體的垃圾回收機制有提到，假使參數或函式不再被使用實，就會釋放其記憶體空間。
不清楚的可以回去看這一篇文章[JavaScript 核心 (8) - 執行環境與作用域 - 回收機制](https://syj0905.github.io/javascript/20201222/3236158139/)
閉包（Closure）是函式以及該函式被宣告時所在的作用域環境（lexical environment）的組合。

``` JavaScript
function randomString(length) {
  var result = '';
  var characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
  var charactersLength = characters.length;
  for (var i = 0; i < length; i++) {
    result += characters.charAt(Math.floor(Math.random() * charactersLength));
  }
  return result;
}
function getData() {
  var demoData = [];
  for (let i = 0; i < 1000; i++) {
    demoData.push(randomString(1000))
  }
  setTimeout(function() {
    demoData;
  }, 10000);
}
getData();
```

由於 `setTimeout` 有需要參考 `demoData` 參數，所以在10秒鐘前記憶體會占用，10秒後就釋放掉了。

## 實用的閉包

閉包實用之處，在於能讓你把一些資料（透過作用域環境）與操控這些資料的函式相關聯。很明顯地，這與把一些資料（物件屬性）與一些方法的相關聯的物件導向程式設計（object-oriented programming）相似。

來寫一個真正的閉包範例:

``` JavaScript
function fn() {
  var money = 100;
  return function(num) {
    money = money + num;
    return money;
  }
}

var a = fn();

console.log(a); /* ƒ (num) {money = money + num; return money;} */
console.log(a(100)); /* 200 */
console.log(a(100)); /* 300 */
console.log(a(100)); /* 400 */
console.log(a(100)); /* 500 */
```

肯定會有人想問:為什麼傳入都是 `100`，但金額會不斷累加呢?
以下按步驟解析:

1. `fn()` 本身會回傳一個匿名函式，而此匿名函示又會回傳一個數值 `money`。
2. 將 a 賦予 fn()，此時 a 釋回傳一個函式，而不是一個數值。
3. 要回傳數值必須要使用 `a(傳入的數值)`，而不是單純呼叫 `a` 而已。
4. 第一次執行 `a(100)` 後，函式內部的 money 因為重新被賦予成 `100 + 100 = 200`。
5. 第二次執行 `a(100)` 後，注意，由於這個函式 `fn()` 又再次被調用參考，所以上一步的 money 仍會維持 200，最後回傳 200 + 100 = 300。
6. 同上5.步驟，只要有一直參考到函式，這個函式內的 money 就不會被釋放掉。

實際上閉包用單一個函式表現不出它的強大之處，來看看以下範例:

``` JavaScript
function fn() {
  var money = 100;
  return function(num) {
    money = money + num;
    return money;
  }
}

var a = fn();

console.log(a(100)); // 200
console.log(a(100)); // 300
console.log(a(100)); // 400
console.log(a(100)); // 500

var b = fn();

console.log(b(500)); // 600
console.log(b(500)); // 1100
console.log(b(500)); // 1600
console.log(b(500)); // 2100
```

上述範例僅僅使用一個閉包，就能建立 `a`、`b` 兩個獨立的函式，但只需要寫一個閉包即可。

## 實際應用範例

來寫一個實際應用的閉包吧。

``` HTML
  <p>Some paragraph text</p>
  <h1>some heading 1 text</h1>
  <h2>some heading 2 text</h2>

  <a href="#" id="size-12">12</a>
  <a href="#" id="size-14">14</a>
  <a href="#" id="size-16">16</a>
```

``` CSS
body {
  font-family: Helvetica, Arial, sans-serif;
  font-size: 12px;
}
h1 {
  font-size: 1.5em;
}
h2 {
  font-size: 1.2em;
}
```

``` JavaScript
function makeSizer(size) {
  return function() {
    document.body.style.fontSize = size + 'px';
  };
}

var size12 = makeSizer(12);
var size14 = makeSizer(14);
var size16 = makeSizer(16);

document.getElementById('size-12').onclick = size12; /* 為按鈕綁訂特定的函式 */
document.getElementById('size-14').onclick = size14; /* 為按鈕綁訂特定的函式 */
document.getElementById('size-16').onclick = size16; /* 為按鈕綁訂特定的函式 */
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(38)-函式以及 This 的運作-閉包 Closure](https://hsiangfeng.github.io/javascript/20201220/3559993634/)
