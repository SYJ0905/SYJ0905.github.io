---
title: JavaScript 核心 (53) - ES6 章節：Let 及 Const - 樣板字面值（Template literals）基本介紹
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 本篇來介紹樣板字面值的基本用法
abbrlink: 3908712580
date: 2021-02-04 10:30:00
---
## Template literals

[MDN Template literals](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Template_literals)
允許嵌入運算式的字串字面值，解決傳統字串與變數組合時的不便性

``` JavaScript
/* 傳統寫法 */
const cash = 10;
const string = '氣氣氣氣';
const sentence = '我的 ' + cash + ' 元掉進水溝裡了，真是' + string;
console.log('sentence =>', sentence); /* sentence => 我的10掉進水溝裡了，真是氣氣氣氣 */


/* ES6 Template literals */
const cash = 10;
const string = '';
const sentence = `我的 ${ cash } 元掉進水溝裡了，真是${ string || '氣氣氣氣'}`;
console.log('sentence =>', sentence); /* sentence => 我的10掉進水溝裡了，真是氣氣氣氣 */
```

## 與模板搭配

當需要在 JS 中寫好 html 與變數後插入 Dom，傳統寫法比較麻煩一點
改成 `Template literals` 會清楚易懂

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
/* 傳統 */
const list_string = '<ul>\
  <li>我是 ' + people[0].name + '，身上有 ' + people[0].cash + ' 元</li>\
</ul>'

console.log('list_string =>', list_string);

/* ES6 Template literals */
const list_string = `<ul>
    <li>我是${ people[0].name }，身上有${ people[0].cash }元</li>
  </ul>
`
console.log('list_string =>', list_string);
```

如此一來，在組合字串與變數就變得相當清楚明瞭，並且還可以搭配判斷式來操作顯示內容。

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
