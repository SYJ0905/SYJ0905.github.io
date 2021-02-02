---
title: JavaScript 核心 (52) - ES6 章節：Let 及 Const - Let 有沒有 Hoisting？暫時性死區介紹
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 本篇來介紹 let 與 const 有沒有 Hoisting 特性
abbrlink: 2575331614
date: 2021-02-02 14:00:00
---
## let 與 const 的 Hoisting

``` JavaScript
/* 創造階段 */
/* 執行 */
console.log(Ming); /* Ming is not defined */
// 各瀏覽器錯誤訊息不同，這裡其實 let 有被提升
let Ming = '小明';
```

我們用另一個範例測試:

``` JavaScript
{
  let Ming; /* 暫時性死區 TDZ */
  
  console.log(Ming); /* Identifier 'Ming' has already been declared */
  let Ming = '小明';
}
```

* `let、const` 一樣會有創造階段
* 從創造階段到實際執行的階段會出現 `TDZ` 這個區域無法呼叫變數
* 有創造到執行的概念，但不會先出現 `undefined` 而是出現錯誤提示

## 驗證

``` JavaScript
console.log(typeof a); /* undefined */
console.log(typeof name); /* name is not defined */

let name = 'Cloud';
```

由此驗證無法在 `TDZ` 過程呼叫變數

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
