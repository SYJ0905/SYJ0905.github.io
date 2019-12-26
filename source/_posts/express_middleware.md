---
title: Express.js - middleware
date: 2019-12-26
tags: 
  - Express
  - Node.js
  - JavaScript
categories: Node.js
description: 以為輸入網址就能隨便進入任何網頁嗎?有了 middleware 就能夠阻擋較為隱私的網頁不讓使用者輕鬆輸入網址進入呦!! 
---
## 前言
舉凡電商網站、CMS後台管理系統等含有個人隱私資料或會員系統這類的網站就會需要在特定的隱私頁面做使用者驗證，避免其他人透過任何手法取得網址就直接進入個人頁面竄改資料等行為

## middleware
* `middleware`: 又稱中界軟體、中間組件等。常用於導航守衛(登入驗整等)功能

在 Express 中使用 `app.use()` 來建立導航守衛，需要注意幾點:
* `middleware` 有先後順序問題
* `next()` 必須設定，不加入無法進入到下一步驟
* `res.status(404)` 頁面不存在，不代表程式出錯
* `res.status(500)` 程式錯誤，頁面可能存在，網頁會出現錯誤訊息，為了避免給使用者看到天書，會導入其他自定頁面

參考範例:
``` JavaScript
const express = require('express');
const app = express();

app.use(function (req, res, next) {
  console.log('有人造訪網頁');
  next();
});

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

app.use(function (req, res, next) {
  console.log('有人進來特定頁面');
  // kk(); // 測試 500 時請開啟
  next();
});

app.get('/user', function (req, res) {
  res.send(`
    <html>
      <head></head>
      <body>
        <h1>Hello Cloud</h1>
      </body>
    </html>
  `);
});

app.use(function (req, res, next) {
  res.status(404).send('抱歉，您的頁面找不到');
});

app.use(function (err, req, res, next) {
  console.error(err.status);
  res.status(500).send('程式有點問題，請稍後嘗試');
});

// 監聽 port
const port = process.env.PORT || 3000;
app.listen(port);
```

## 進階 middleware
由於上述寫法必須在每個路由前面都寫入 middleware 的函式，會造成多餘的程式碼。
Express 提供另一種寫法，可以在每個路由的參數中添加 middleware 在接著後面的 `callback function` or `promise` 
參考範例:
``` JavaScript
const express = require('express');
const app = express();

const login = function (req, res, next) {
  const _url = req.url;
  console.log('有人進來首頁');
  console.log(_url);
  if (_url !== '/') {
    next();
  } else {
    res.send('您的登入資料有錯');
  }
}

app.get('/', login, function (req, res) {
  res.send(`
    <html>
      <head></head>
      <body>
        <h1>Hello Express</h1>
      </body>
    </html>
  `);
});

app.use(function (req, res, next) {
  console.log('有人進來特定頁面');
  // kk(); // 測試 500 時請開啟
  next();
});

app.use(function (req, res, next) {
  res.status(404).send('抱歉，您的頁面找不到');
});

app.use(function (err, req, res, next) {
  console.error(err.status);
  res.status(500).send('程式有點問題，請稍後嘗試');
});

// 監聽 port
const port = process.env.PORT || 3000;
app.listen(port);
```