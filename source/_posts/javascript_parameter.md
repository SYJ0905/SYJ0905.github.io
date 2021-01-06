---
title: JavaScript 核心 (29) - 函式以及 This 的運作 - 參數
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 參數與函式息息相關，有效運用可大幅提升程式效率
date: 2021-01-06 10:00:00
---
## 參數

[MDN 參數](https://developer.mozilla.org/zh-TW/docs/Glossary/Parameter)
參數 (parameter) 是個會傳進函式 (function) 的已命名變量，用來把引數 ((arguments)) 導入到函式中。

``` JavaScript
var globalName = 'Cloud';

var obj = {
  fn: function(name, bb) {
    var localName = 'CloudSu';
    console.log(name, localName, globalName, bb, arguments, this);
  }
}

obj.fn(globalName); /* Cloud CloudSu Cloud undefined */
```

此時的參數就是 `globalName`，，然後 function 的 `name` 來接收。
參數會依序載入，上述範例中有三個參數，但卻只有一個 `name` 參數接收者，所以也只有第一個參數 `globalName` 會被 `name` 接收到。

## arguments

[MDN Arguments 物件](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Functions/arguments)
arguments 物件是一個對應傳入函式之引數的類陣列（Array-like）物件。
由於不是陣列，自然就無法使用陣列中許多方法跟功能，但我們可以透過多種轉換方式，將 `arguments` 轉換成 `array`。
以下提供四種方法:

``` JavaScript
/* 轉換方法 - 1 效能最好 */
function test(...arguments) {
   console.log(arguments)
}
test(1,2,3); // [1,2,3]
/* 轉換方法 - 2 效能次之 */
function test() {
  var arr = Array.prototype.slice.call(arguments);
  // var arr = [].slice.call(arguments);
  console.log(arr);
}
test(1,2,3);
/* 轉換方法 - 3 效能最差 */
function test() {
  const arr = Array.from(arguments);
  console.log(arr);
}
test(1,2,3);
```

## 函式變數宣告

函式內的變數名稱與函式本身參數相同，不會因再次宣告而覆蓋原有內容。

``` JavaScript
var name = 'Cloud';

function fn(name) {
  console.log(name); /* Cloud */
  var name;
  console.log(name); /* Cloud */
}

fn(name);
```

若是用 `重新賦予值` 的話，是會更新的，這點不難理解。

``` JavaScript
var name = 'Cloud';

function fn(name) {
  console.log(name); /* Cloud */
  var name;
  console.log(name); /* Cloud */
  name = '我是誰';
  console.log(name); /* 我是誰 */
}

fn(name);
console.log(name); /* Cloud */
```

## 物件傳參考

傳入的參數若是一個物件的話，傳入的參數若是一個物件的話，依樣會有傳參考特性。
純值的話就不影響。

``` JavaScript
var obj = {
  name: 'Cloud',
};

function fn(a) {
  a.name = '測試';
}

fn(obj);

console.log(obj.name); /* 測試 */
```

## 傳函式 CallBack Function

參數還能是函式，想不到吧，因為函式也是一個物件喔。

* 匿名函式寫法:

``` JavaScript
function test(fn) {
  fn();
}

/* 傳入匿名函式 */
test(function() {
  console.log('Ray');
})
```

* 具名函式寫法:

``` JavaScript
function functionB(fn) {
  console.log('Ray');
}

function functionA(fn) {
  fn();
}

/* 傳入具名函式 */
functionA(functionB);
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(37)-函式以及 This 的運作-參數](https://hsiangfeng.github.io/javascript/20201129/3953962173/)
[前端Tips#2 - 将 arguments 转换成Array的最佳实践](https://zhuanlan.zhihu.com/p/100666855)
