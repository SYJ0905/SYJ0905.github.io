---
title: Express.js - 路由 Route 介紹
tags:
  - Express
  - Nodejs
  - JavaScript
categories:
  - Nodejs
description: 使用 Express 自定網站路由以及參數。
abbrlink: 1852101665
date: 2019-12-26 00:00:00
---
## 網址組成
首先要介紹網址的組成，這裡選擇 Google 搜尋 `express` 當例子。
以下是範例網址，實際操作時網址可能很長一串，不過是可以簡化成這樣子的，其他多餘的都是 Google 的設定
`https://www.google.com/search?q=exprss`
* `https`: 傳輸協定，有兩種類型，對應的 port 也不同
  * http: port 80，有安全性問題
  * htpps: port 443，代表安全傳輸協定，又稱 `SSL`
* `www`: 子網域，掛在主網域底下，也就是說一個主網域底下可能有多個子網域，並提供服務(ex: mail.google.com、drive.google.com)
* `google.com`: 主網域，透過網域供應商購買
* `search`: 路由 route
* `?q=exprss`: 網址參數 query

## Express Route
參考之前的範例，我們可以在根目錄 `/` 下新建一個 `/user` 的路由
``` JavaScript
const express = require('express');
const app = express();

app.get('/', function (req, res) {
  res.send('Hello Express');
});
app.get('/user', function (req, res) {
  res.send('測試');
});

// 監聽 port
const port = process.env.PORT || 3000;
app.listen(port, function () {
  console.log('Example app listening on port 3000!');
});
```
如果要在 `/user` 底下在建一個路由呢 ? 只需在建一個 `get()` 並再 `/user/欲加入的路由名稱` 即可
``` JavaScript
const express = require('express');
const app = express();

app.get('/', function (req, res) {
  res.send('Hello Express');
});
app.get('/user', function (req, res) {
  res.send('測試');
});
app.get('/user/test2', function (req, res) {
  res.send('測試2');
});

// 監聽 port
const port = process.env.PORT || 3000;
app.listen(port, function () {
  console.log('Example app listening on port 3000!');
});
```

## 網址參數
如同前面 google 的搜尋參數 `?q=exprss`，如何在進入到 `http://localhost:8080/user?search=express` 這個網址時，後端 express 也能收到我的參數呢?

在 Express 中是使用了 `req.query` 來紀錄資料
註: `query` 中文應該是詢問的意思，不確定為什麼會被翻成參數
``` JavaScript
const express = require('express');
const app = express();

app.get('/', function (req, res) {
  res.send('Hello Express');
});
app.get('/user', function (req, res) {
  console.log(req.query);
  const query = req.query.search; // search 必須跟網址對應到的 ?search 要是相同的呦
  res.send(`測試 ${query}`);
});

// 監聽 port
const port = process.env.PORT || 3000;
app.listen(port, function () {
  console.log('Example app listening on port 3000!');
});
```
這時進入到 `http://localhost:8080/user?search=express` 時，頁面就會有 `測試 express` 的字樣囉，並且在 `CMD` or `終端機` 會有 `req.query` 的物件。
如果參數有很多個的話，就在 `?search=express` 後面加個 `&` 再繼續寫 `?search=express&name=Cloud`， 就可以囉。

## 網址路由
先前提到的路由都是預先設定好的，像是 `/`、`/user` 等等，假設有一個路徑是 `/user/Cloud` 指定到個人頁面的話，該怎麼再 Express 設定呢?
Express 使用 `req.params` 來接收動態的路徑資料
參考以下範例:
``` JavaScript
const express = require('express');
const app = express();

app.get('/', function (req, res) {
  res.send('Hello Express');
});
app.get('/user/:name', function (req, res) {
  console.log(req.params);
  const name = req.params.name;
  res.send(`測試 ${name}`);
});

// 監聽 port
const port = process.env.PORT || 3000;
app.listen(port, function () {
  console.log('Example app listening on port 3000!');
});
```

## 總結
以下是本篇路徑所講的所有內容統整，可以執行 `http://localhost:3000/user/Cloud/0905?limit=10&q=hello` 來看觀察資料結構
範例程式碼:
``` JavaScript
const express = require('express');
const app = express();

app.get('/', function (req, res) {
  res.send(`
    <html>
      <head></head>
      <body>
        <h1>Hello Express</h1>
      </body>
    </html>
  `);
});

// http://localhost:3000/user/Cloud/0905?limit=10&q=hello
app.get('/user/:name/:date', function (req, res) {
  console.log(req.params);
  console.log(req.query);
  const myName = req.params.name;
  const date = req.params.date;
  const limit = req.query.limit;
  const q = req.query.q;
  res.send(`
    <html>
      <head></head>
      <body>
        <h1>我的名字:${ myName }</h1>
        <p>日期: ${ date }</p>
        <P>筆數: ${ limit }</P>
        <p>尋找關鍵字: ${ q }</p>
      </body>
    </html>
  `);
});

// 監聽 port
const port = process.env.PORT || 3000;
app.listen(port, function () {
  console.log('Example app listening on port 3000!');
});
```