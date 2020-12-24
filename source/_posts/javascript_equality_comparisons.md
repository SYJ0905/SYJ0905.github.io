---
title: JavaScript 核心 (16) - 運算子、型別與文法 - 寬鬆相等、嚴格相等
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 由於 JavaScript 會自動轉換型別，所以在做相等對比時要特別小心
abbrlink: 514409429
date: 2020-12-24 12:30:00
---
## 寬鬆相等

又稱`一般相等`
先將比較值轉換成同型別後比較。接著進行的幾乎和嚴格相等（===）一樣。 寬鬆相等會對稱： A == B 等同 B == A ，無論 A 和 B 是什麼。

[MDN 相等比較](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Equality_comparisons_and_sameness)

``` JavaScript
console.log(1 == '1'); /* true */
/* 實際解析 */
console.log(1 == Number('1'));

console.log(17 == '0x11'); /* true */
/* 實際解析 */
console.log(17 == Number('0x11'));

console.log(true == 'true'); /* false */
/* 實際解析 */
console.log(true == Number('true')); /* Number('true') => NaN */
```

`布林與字串`會先轉換為`數值`在進行比對

至於 Object 與 Array 如何比對呢?
Array 是屬於 Object 的一種，並且在做寬鬆對比時，會被包裹物件轉換在進行比對

``` JavaScript
10 == [10]; /* true */
/* 實際解析 */
10 == Number([10]);
```

詳細範例:

``` JavaScript
var num = 0;
var obj = new String('0'); /* 此為物件型別 */
var str = '0';

console.log(num == num); /* true */
console.log(obj == obj); /* true */
console.log(str == str); /* true */

console.log(num == obj); /* true */
console.log(num == str); /* true */
console.log(obj == str); /* true */

/* 特別 */
console.log(null == undefined); /* true */

/* 特別 除了少數情況，這兩個應該是 false。 */
console.log(obj == null);
console.log(obj == undefined);
```

## 嚴格相等

嚴格相等比較兩個值，而被比較的兩個值`都不會轉換成其他型別`。如果值是不同型別，就會被視為不相等。如果兩值型別相同但不是數字，若值相同，則為相等。此外，如果兩個值皆為數字，只要他們是 NaN 以外的同一值，或者 +0 和 -0，則為相等。

NaN，用來表示某些定義不明確的數學問題的解， 例如：負無窮加正無窮，`嚴格比較認為 NaN 不等於任何值，包含他本身。`（(x !== x)只有在 x 是 NaN 時會是 true。）

``` JavaScript
var num = 0;
var obj = new String('0');
var str = '0';

console.log(num === num); /* true */
console.log(obj === obj); /* true */
console.log(str === str); /* true */

console.log(num === obj); /* false */
console.log(num === str); /* false */
console.log(obj === str); /* false */

/* 特別 */
console.log(null === undefined); /* false */

/* 特別 */
console.log(obj === null); /* false */
console.log(obj === undefined); /* false */

/* 特別 */
console.log(+0 === -0); /* true */
console.log(NaN === NaN); /* false */ 
console.log(NaN !== NaN); /* true */ 
console.log(null === NaN); /* false */ 
console.log(undefined === NaN); /* false */ 
```

## 實際開發

由上述介紹這兩個相等比較的差異，應該就知道在開發中基本上都會使用`嚴格比較`才不會出現問題。

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(17)-運算子、型別與文法-寬鬆相等、嚴格相等以及隱含轉型](https://hsiangfeng.github.io/javascript/20200628/4021116713/)
