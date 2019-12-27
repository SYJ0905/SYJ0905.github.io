---
title: Express.js - 基礎介紹
date: 2019-12-26
tags: 
  - Express
  - Node.js
  - JavaScript
categories: Express.js
description: 學習 Express.js 前後端開發自己來，真牛逼!!
---
## Express
[Express.js Wiki](https://zh.wikipedia.org/wiki/Express.js)
Express.js 是以 Node.js 為核心開發的一套 Web 應用框架，具有非常簡潔又靈活的特性，可以快速製作出 RESTful API，有利於軟體開發的效率。

## Hello Express
首先要創建 preject 資料夾，開啟 `CMD`、`終端機` 進入資料夾目錄。
接著，執行 `npm init`，一路 enter 下去即可，此時會生成 `package.json`。
最後輸入 `npm i express -S`。
進入資料夾，新增 `app.js` 並參考以下範例程式碼:
``` JavaScript
const express = require('express');
const app = express();

app.get('/', function (req, res) {
  res.send('Hello Express');
});
app.get('/test', function (req, res) {
  res.send('測試');
});

// 監聽 port
const port = process.env.PORT || 3000;
app.listen(port, function () {
  console.log('Example app listening on port 3000!');
});
```
最後輸入 `node app.js` 並開啟 `localhost:3000` ， 如果有看到 `Hello Express` 的話就代表成功囉!!

## 細節講解
* 引入 `Express`，並宣告變數以便之後使用。
``` JavaScript
const express = require('express');
const app = express();
```
* 設定路由
使用 `get()` API 則可以新增一個路由，並當使用者進入此路由後回傳頁面內容給使用者。
路由規則: 
`/`: 代表網址列上輸入 `localhost:3000`
`/test`: test 可以更換成自定義名稱，並對應該路徑 `localhost:3000/test`
``` JavaScript
app.get('/', function (req, res) {
  res.send('Hello Express');
});
app.get('/test', function (req, res) {
  res.send('測試');
});
```
* 開啟 Web Server
使用 `listen()` API 指定 `port` 號
註: `process.env.PORT` 當部屬到正式主機時，由於主機商會有自定的 `port` 號，所以必須加這行，如果沒有的話才用自定義的 `port` 號
``` JavaScript
const port = process.env.PORT || 3000;
app.listen(port, function () {
  console.log('Example app listening on port 3000!');
});
```