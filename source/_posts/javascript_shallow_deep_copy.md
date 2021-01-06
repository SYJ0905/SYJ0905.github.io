---
title: JavaScript 核心 (26) - 物件 - 淺層複製及深層複製
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
abbrlink: 431199247
date: 2021-01-04 14:30:00
description: 操作物件時必須搞清楚什麼是淺層複製以及深層複製。
---
## 淺層複製 Shallow Copy

複製一個或多個物件自身所有可數的屬性到另一個目標物件。回傳的值為該目標物件。
上面不容易理解，直接上範例比較清楚:

``` JavaScript
/* 問題 */
var a = {
  name: 'Cloud',
};

var b = a;

b.name = '測試';
console.log(a.name); /* 測試 */
```

* Object.assign

``` JavaScript
var a = {
  name: 'Cloud',
};

var b = Object.assign({}, a);

b.name = '測試 Object.assign';
console.log(a.name); /* Cloud */
console.log(b.name); /* 測試 Object.assign */
```

`Object.assign` 也可改寫成 `ES6`:

``` JavaScript
var a = {
  name: 'Cloud',
};

var b = { ... a };

b.name = '測試 Object.assign';
console.log(a.name); /* Cloud */
console.log(b.name); /* 測試 Object.assign */
```

然後淺層複製只會複製第一層物件，若是修改到內層物件屬性，仍會改變原本物件的屬性值

``` JavaScript
var a = {
  name: 'Cloud',
  age: {
    number: 26,
  }
};

var b = { ... a };

b.age.number = '測試';
console.log(b.age.number); /* 測試 */
console.log(a.age.number); /* 測試 */
```

這是因為內層的 `age` 仍指向原本的參考，並不會一起複製勒。

## 深層複製 Deep Copy

只需要將物件轉換成純值，在轉換成物件即可

* JSON.parse() with JSON.stringify()

``` JavaScript
var a = {
  name: 'Cloud',
  age: {
    number: 26,
  }
};

var b = JSON.parse(JSON.stringify(a));

b.age.number = '測試';
console.log(b.age.number); /* 測試 */
console.log(a.age.number); /* 26 */
```

然而此方法`僅限用於 json 格式`，屬性值不能是`undefined`、`NaN`或是`function`，否則會無法轉換。

``` JavaScript
var a = {
  name: 'Cloud',
  age: {
    number: 26
  },
  fn: function() { /* 消失 */
    console.log('測試1');
  },
  un: undefined, /* 消失 */
  nan: NaN, /* 變成 null */
};

var b = JSON.parse(JSON.stringify(a)); /* {name: "Cloud", age: {…}, nan: null} */

console.log(b);
```

## 深層複製完美解法

一般會參考第三方工具的深層複製寫法，當然如果是高手等級，就乾脆自己寫一個插件也不是不行。

* Underscore — _.clone()
此方法只能算是半個深層複製，也就是說不會完全複製物件內的參考。

``` JavaScript
/* 請先引入 Underscore，否則會出錯 */
var a = {
  name: 'Cloud',
  age: {
    number: 26
  },
  fn: function() {
    console.log('1');
  },
  un: undefined,
  nan: NaN,
};

var b = _.clone(a);

console.log(b); /* {name: "Cloud", age: {…}, un: undefined, nan: NaN, fn: ƒ} */

/* 檢測是否為 深層複製 */
var x = {
  a: 1,
  b: { z: 0 }
};
var y = _.clone(x);
x.b.z = 100;
y.b.z         // 100
console.log(x === y); /* false */
console.log(x.b === y.b); /* true  物件內層屬性依然指向相同參考 */
```

* jQuery — $.extend()

``` JavaScript
/* 請先引入 jQuery，否則會出錯 */
var a = {
  name: 'Cloud',
  age: {
    number: 26
  },
  fn: function() {
    console.log('1');
  },
  un: undefined,
  nan: NaN,
};

var b = $.extend(true, {}, a);

console.log(b); /* {name: "Cloud", age: {…}, nan: NaN, fn: ƒ} */
```

注意，`undefined` 不會被複製到哩。

* lodash — _.clone() or_.cloneDeep()
`_.clone(obj, true)` 等於 `_.cloneDeep(obj)`
lodash 在深層複製上`更優於 jQuery、Underscore`，畢竟原始碼上就多了幾百行啊。

``` JavaScript
/* 請先引入 lodash，否則會出錯 */
var a = {
  name: 'Cloud',
  age: {
    number: 26
  },
  fn: function() {
    console.log('1');
  },
  un: undefined,
  nan: NaN,
};

var b = _.cloneDeep(a);

console.log(b); /* {name: "Cloud", age: {…}, un: undefined, nan: NaN, fn: ƒ} */
```

lodash的`_.cloneDeep()`幾乎完美複製原本的物件內容。

## 效能&功能比較

特性 | jQuery | lodash  | JSON.parse |
---------------------|:------:|:-------:|:----------:|
瀏覽器兼容性 | IE6+ (1.x) & IE9+ (2.x) | IE6+ (Compatibility) & IE9+ (Modern) | IE8+ |
能夠深複製內層所有屬性值 | 回傳異常 RangeError: Maximum call stack size exceeded  | 支持 | 回傳異常 TypeError: Converting circular structure to JSON |
對 Date, RegExp 的深層複製支持 | × | 支持 | × |
對 ES6 新引入的標準對象的深層複製支持 | × | 支持 | × |
複製陣列的属性 | × | [僅支持RegExp#exec返回的陣列结果](https://github.com/lodash/lodash/blob/5166064453ed6164b76fb20f8dd340d23dd334e5/lodash._baseclone/index.js#215) | × |
是否保留非原生對象的類型 | × | × | × |
複製不可枚舉元素 | × | × | × |
複製函數 | × | × | × |

方法 | jQuery | lodash | JSON.parse
----------|:------:|:-------:|:----------:|
平均 | 478 | 293 | 656

倘若需要使用到深層複製的話，還是會先以 `loadsh` 為優先哩。

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(30)-物件-淺層複製及深層複製](https://hsiangfeng.github.io/javascript/20200905/1375484447/)
[深入剖析 JavaScript 的深复制](https://jerryzou.com/posts/dive-into-deep-clone-in-javascript/)
