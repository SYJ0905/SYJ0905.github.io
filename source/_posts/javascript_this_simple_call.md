---
title: JavaScript 核心 (35) - 函式以及 This 的運作 - this：簡易呼叫
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 來介紹 this 第二常見的呼叫方式 simple call
abbrlink: 3970152447
date: 2021-01-11 17:00:00
---
## Sample Call

簡易呼叫，此方式呼叫的 this 基本上會`指向 window`。
以下範例:

``` JavaScript
function fn() {
  console.log(this);
}

fn(); /* window */

/* 驗證 this 是否指向 window  */
function fn1() {
  return this;
}

fn1() === window; /* true */
```

## simple call 常見類型

* IIFE 立即函式

``` JavaScript
var myName = 'Cloud';
(function() {
  var myName = 'Cloud2'
  console.log(this.myName); /* Cloud */
  function callSomeone() {
    var myName = 'Cloud3';
    console.log(this.myName); /* Cloud */
  }

  callSomeone();
})();
```

* closure 閉包

``` JavaScript
var myName = 'Cloud';
function fn() {
  var a = 1;
  return function(update) {
    a = a + update;
    console.log('a=>',a);
    console.log(this.myName, this.a);
  }
}

var qq = fn();
qq(10); /* Cloud undefined */
```

* Callback 回呼函式

``` JavaScript
var myName = 'Cloud';
function fn(callback) {
  var money = 100;
  callback(money); /* Cloud 200 */
};

fn(function(money) {
  console.log(this.myName, money + 100);
});
```

其他 callback 類型

``` JavaScript
var myName = 'Cloud';
var a = [1, 2, 3];
a.forEach(function(i) {
  console.log(this.myName, i);
});
/*
Cloud 1
Cloud 2
Cloud 3
*/
```

## callback 中使用 this

``` JavaScript
var myName = 'Cloud';
var family = {
  myName: '小明家',
  callName: function() {
    setTimeout(function() {
      console.log(this.myName);
    });
  },
};
family.callName(); /* Cloud */
```

因為 `setTimeout()` 是 `simaple call`，即便是用 `family.callName()` 呼叫函式，但實際上內部的 `setTimeout()` 仍是直接執行的緣故，所以 this 依舊指向 window。

那如果我們想要取得 `小明家` 這個 myName 呢?

* 撰寫方式一: 匿名函式

``` JavaScript
var myName = 'Cloud';
var family = {
  myName: '小明家',
  callName: function() {
    const vm = this;
    setTimeout(function() {
      console.log(vm.myName);
    });
  },
};
family.callName(); /* 小明家 */
```

* 撰寫方式二: 具名函式

``` JavaScript
var myName = 'Cloud';
function fn() {
  const vm = this;
  setTimeout(function() {
    console.log(vm.myName);
  });
}
var family = {
  myName: '小明家',
  callName: fn,
};
family.callName(); /* 小明家 */
```

至於 `vm` 這個存取 this 的變數名稱則是依照團隊制定，沒有一定形式。
常見的有 `vm`、`that`、`_this`、`self`。
<註>不推薦使用 `self`
因為 `self` 其實就是 `window 本身`

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(41)-函式以及 This 的運作-this：簡易呼叫](https://hsiangfeng.github.io/javascript/20210103/2997707827/)
