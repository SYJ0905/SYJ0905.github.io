---
title: JavaScript 核心 (54) - ES6 章節：Let 及 Const - 巢狀結構
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 本篇來介紹樣板字面值的巢狀結構使用方法
abbrlink: 3146715217
date: 2021-02-04 11:00:00
---
## 傳入變數以外內容

由於樣板字面值是回傳表達式的值，所以除了變數外，還可寫入函式甚或是另一個樣板字面值

``` JavaScript
const person = {
  name: '小明',
  cash: 1000
};
const sentence = `我是${ person.name }，身上帶有${ person.cash || 2000 }元`;
const sentence_2 = `我是${ person.name }，身上帶有${ (function(c) { return c * 2 })(person.cash) }元`;
const sentence_3 = `我是${ person.name }，身上帶有${ ((c) => c * 2 )(person.cash) }元`;
console.log('sentence =>', sentence); /* sentence => 我是小明，身上帶有2000元 */
console.log('sentence_2 =>', sentence_2); /* sentence_2 => 我是小明，身上帶有2000元 */
console.log('sentence_3 =>', sentence_3); /* sentence_3 => 我是小明，身上帶有2000元 */

/* 巢狀插入 */
const sentence_4 = `我是${ person.name }，${ `身上帶有 ${ person.cash }` }元`;
console.log('sentence_4 =>', sentence_4); /* sentence_4 => 我是小明，身上帶有 1000元 */
```

## 樣板字面值與迴圈搭配

``` JavaScript
const people = [
  {
    name: '小明',
    cash: 50,
  },
  {
    name: '阿姨',
    cash: 100,
  },
  {
    name: 'Cloud',
    cash: 1000,
  },
];

const list_string = `<ul>
    ${ people.map((person) => `<li>我是${ person.name }，身上有 ${ person.cash } 元</li>`)}
  </ul>
`
console.log('list_string =>', list_string);
/* list_string => <ul>
    <li>我是小明，身上有 50 元</li>,<li>我是阿姨，身上有 100 元</li>,<li>我是Cloud，身上有 1000 元</li>
  </ul> */

/* 由於 map() 本身回傳的仍是陣列，所以會有 "逗號" 產生， 這時就得使用 .join() 來轉成字串值 */
const list_string_finish = `<ul>
    ${ people.map((person) => `<li>我是${ person.name }，身上有 ${ person.cash } 元</li>`).join('')}
  </ul>
`
console.log('list_string =>', list_string_finish);
/* list_string => <ul>
    <li>我是小明，身上有 50 元</li><li>我是阿姨，身上有 100 元</li><li>我是Cloud，身上有 1000 元</li>
  </ul> */
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
