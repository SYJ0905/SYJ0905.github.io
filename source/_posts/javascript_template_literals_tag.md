---
title: JavaScript 核心 (55) - ES6 章節：Let 及 Const - 標籤樣板字面值
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 本篇來介紹為何要在樣板字面值加入標籤
abbrlink: 3639878289
date: 2021-02-04 14:30:00
---
## 運作模式

可以使用函式傳入樣板字面值，並且會依照參數來區隔開字串與變數

``` JavaScript
function showConsole(strings, ...arg) {
  console.log(strings, arg); /* ["您好 ", " ，餐點已經準備好了!", raw: Array(2)]  ["小明"] */
};
const myName = '小明';
const sentence = showConsole`您好 ${myName} ，餐點已經準備好了!`;
```

## 加入標籤

``` JavaScript
const myName = '小明';
const highlight = (strings, ...arg) => strings.map((str, i) => `${ str }${ arg[i] ? `<span>${arg[i]}</span>` : '' }`).join('');
const sentence = highlight`您好 ${myName} ，餐點已經準備好了!`;
const sentence_2 = `您好 <span>${myName}</span> ，餐點已經準備好了!`;
console.log('sentence =>', sentence); /* sentence => 您好 <span>小明</span> ，餐點已經準備好了! */
console.log('sentence_2 =>', sentence_2); /* sentence_2 => 您好 <span>小明</span> ，餐點已經準備好了! */
```

上述這個例子雖然可以直接寫成 `sentence_2` 形式，但一旦字串中需要插入的變數很多，並且`都要套用相同方法`的時候，就可以考慮寫成 `標籤樣板字面值`的形式

## XSS 阻擋

`傳入的變數` 有`寫入 html 的時候(innerHTML)`，就要小心是否會傳入`非正常變數內容`，像是塞入惡意程式、call 外部 API 等。

``` JavaScript
const messageName = '小明';
document.querySelector('#message').innerHTML = `<p>${ messageName } 傳來一則訊息</p>`;

const xss_messageName = '<img onload="fetch(\'https://randomuser.me/api\')" src="https://images.unsplash.com/photo-1593642702749-b7d2a804fbcf?ixid=MXwxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=800&q=80"></img>';
document.querySelector('#message').innerHTML = `<p>${ xss_messageName } 傳來一則訊息</p>`;
```

![xss 範例](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/JavaScript%20%E6%A0%B8%E5%BF%83%20(55)%20-%20ES6%20%E7%AB%A0%E7%AF%80%EF%BC%9ALet%20%E5%8F%8A%20Const%20-%20%E6%A8%99%E7%B1%A4%E6%A8%A3%E6%9D%BF%E5%AD%97%E9%9D%A2%E5%80%BC%2F%E6%93%B7%E5%8F%96.JPG?alt=media&token=29daebfe-f265-41cb-85fd-5ba4748613a6)

解決方法也很好理解，只需將傳入的變數都先`轉成字串`再輸出即可

``` JavaScript
function convertHTML(strings, ...keys) {  
  return strings.map((str, i) =>
    `${str}${keys[i] ? `${keys[i]      
    .replace(/&/g, '&amp;')
    .replace(/</g, '&lt;')
    .replace(/>/g, '&gt;')}` : ''}`
  ).join('');
}
const xss_messageName = '<img onload="fetch(\'https://randomuser.me/api\')" src="https://images.unsplash.com/photo-1593642702749-b7d2a804fbcf?ixid=MXwxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=800&q=80"></img>';
document.querySelector('#message').innerHTML = convertHTML`<p>${ xss_messageName } 傳來一則訊息</p>`;
```

如此一來，就可以避免有 XSS 惡意攻擊行為。

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
