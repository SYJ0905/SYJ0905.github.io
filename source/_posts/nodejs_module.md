---
title: Node.js - 模組開發 module exports 
date: 2019-12-25
tags: 
  - Node.js
  - JavaScript
categories: Node.js
description: 學習模組化開發，有利於程式開發。
---
## module.exports 、 require
創建一個資料夾，分別建立 `app.js`、`data.js` 
在 `app.js` 撰寫以下程式碼:
``` JavaScript
var content = require('./data');
var a = 1
console.log(a);
console.log(content);
console.log(content.data);
console.log(content.bark());
```
在 `data.js` 撰寫以下程式碼:
``` JavaScript
var data = 2
// 兩種 exports 輸出寫法 (無法並存)
// 推薦 exports 寫法
module.exports = {
  data: data,
  title: '我是標題',
  bark: function () {
    return 'bark!!';
  },
};
// 另一種 exports 寫法
// exports.data = 2;
// exports.title = '我是標題';
// exports.bark = function () {
//   return 'bark!!';
// };
```
使用 `module.exports` 就代表要輸出一個物件模組，內容就跟撰寫 JS 物件是相同的，可以是 `物件`、`陣列`、`字串`、`函式`等等。
若要在其他支 js 引入的話，則宣告一個變數並且 `require('引入檔案的路徑')` ，這樣就能使用該檔案的內容了
參照以上範例，並在 `CMD` 執行 `node app.js` 就會看到效果囉!!
![模組開發](https://i.imgur.com/D85PcD2.png)