---
title: JavaScript 核心 (36) - 函式以及 This 的運作 - this：call, apply, bind 與 嚴謹模式
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 來介紹 this 中的 apply、call、bind 三劍客，並且介紹 this 與 嚴謹模式關係
abbrlink: 2281332667
date: 2021-01-11 19:00:00
---
## call

[Function.prototype.call](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Function/call)

* 立刻執行
* 可以在 simalp call 中，使用 call() 來`指定 this`。
* 參數直接傳入

``` JavaScript
var family = {
  myName: 'Cloud',
};

function fn (para1, para2) {
  console.log(this, typeof this, para1, para2);
}
fn(1, 2); /* window object 1 2 */
fn.call(family, 1, 2); /* {myName: "Cloud"} "object" 1 2 */
```

## apply

[Function.prototype.apply](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)

* 立刻執行
* 可以在 simalp call 中，使用 call() 來`指定 this`。
* 參數使用 `陣列` 傳入

``` JavaScript
var family = {
  myName: 'Cloud',
};

function fn (para1, para2) {
  console.log(this, typeof this, para1, para2);
}
fn(3, 4); /* window object 3 4 */
fn.apply(family, [3, 4]); /* {myName: "Cloud"} "object" 3 4 */
```

## bind

[Function.prototype.bind](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)

* 不會立刻執行
* 可以在 simalp call 中，使用 call() 來`指定 this`。
* 參數直接傳入

``` JavaScript
var family = {
  myName: 'Cloud',
};

function fn (para1, para2) {
  console.log(this, typeof this, para1, para2);
}

var fn2 = fn.bind(family, '小明', '杰倫');
fn2(); /* {myName: "Cloud"} "object" "小明" "杰倫" */

/* 強制傳參數不會覆蓋原本已經設定的參數 */
fn2(1, 2); /* {myName: "Cloud"} "object" "小明" "杰倫" */

/* 部分寫入，參數依序傳入 */
var fn3 = fn.bind(family, '小明');
fn3(1,2); /* {myName: "Cloud"} "object" "小明" 1 */
```

bind() 很常跟 simple call 搞混，要記住，`在使用 bind() 的時後 this 就已經決定`了。

## 進階觀念

在`不使用嚴格模式下`，this 傳入純值竟然是建構式

```JavaScript
var family = {
  myName: 'Cloud',
};

function fn (para1, para2) {
  console.log(this, typeof this, para1, para2);
}

fn.call(1, '小明', '杰倫'); /* Number {1} "object" "小明" "杰倫" */
fn.call('文字', '小明', '杰倫'); /* String {"文字"} "object" "小明" "杰倫" */
fn.call(undefined, '小明', '杰倫'); /* window "object" "小明" "杰倫" */
```

傳入 undefined 回傳是 window
[Function.prototype.call](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Function/call)

在`非嚴格模式下`，使用 call() 傳入的純值如果是 `undefined`、`null`，將被置換成全域變數 window，原生型態則被封裝(建構式)

## 嚴格模式

[嚴格模式](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Strict_mode)

* 加入 `use strict` 即可運作
* 不會影響不支援嚴格模式的瀏覽器
* 可依據`執行環境設定 use strict`
* 透過拋出錯誤方式消除一些安靜的錯誤
* 禁止使用一些有可能被未來版本 ECMAScript 定義的語法

``` JavaScript
/* 不允許直接賦予值 */
(function() {
  'use strict';
  a = '小明'; /* a is not defined */
})();
```

回到先前範例:

``` JavaScript
var family = {
  myName: 'Cloud',
};

function callStrict(para1, para2) {
  'use strict';
  console.log(this, typeof this, para1, para2);
}

callStrict.call(1, '小明', '杰倫'); /* 1 "number" "小明" "杰倫" */
callStrict.call('文字', '小明', '杰倫'); /* 文字 string 小明 杰倫 */
callStrict.call(undefined, '小明', '杰倫'); /* undefined "undefined" "小明" "杰倫" */
callStrict('小明', '杰倫'); /* undefined "undefined" "小明" "杰倫" */
```

在`嚴格模式下`使用 `simple call`，`this` 會變成 `undefined`
`simple call` 等同於使用 `call()`，但`並不會傳 this` 進去
所以 this 會`預設是 undefined`
在 simple call 時盡量不要使用 this，因為此時 this 的本質是 undefined

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(42)-函式以及 This 的運作-this：call, apply, bind 與 嚴謹模式](https://hsiangfeng.github.io/javascript/20210110/1506036553/)
