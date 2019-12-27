---
title: Express.js - 載入靜態 static 檔
date: 2019-12-27
tags: 
  - Express
  - Node.js
  - JavaScript
categories: Express.js
description: 靜態檔案是用來存放 CSS、JS、圖片檔等等，後續 template 在引入這些檔案時才會找到正確路徑。
---
## 前言
截至目前為止，都只會有一支 `app.js` 在撰寫程式碼，如果我們希望使用者進網頁時有看到一些畫面或圖片的話，該怎麼渲染呢?
又該在哪裡存放靜態檔案，最後是該如何正確的引入，以下就會介紹 Express 中引入 static 檔的方法吧!!

## 建立 public 資料夾
首先在 `根目錄` 創建一個 `public` 資料夾，之後存放檔案用的。
並可以依分類建立子資料夾 css、js、images 做區隔，之後引入只要路徑沒錯是沒有問題的。
![public](https://i.imgur.com/r2udHZC.png)

## Express 設定
此設定必須要寫在路由最前面，這樣所有路由才能正確引入。
在 `app.js` 添加以下程式碼:
``` JavaScript
app.use(express.static('public'));
```

## 引入 static 檔
這邊會先示範使用 `res.send()` 來渲染畫面，後續會使用 template 引入。
`/`: 指向 public 當根目錄開始找檔案
參考範例程式碼:
``` JavaScript
app.get('/', function (req, res) {
  res.send(
    `
      <html>
        <head></head>
        <body>
          <img src="/image/logo.png" alt=""/>
        </body>
      </html>
    `
  );
});
```

## 完整範例程式碼
``` JavaScript
const express = require('express');
const app = express();

// 增加靜態檔案路徑 ， 必須寫在最前面
app.use(express.static('public'));

app.get('/', function (req, res) {
  res.send(
    `
      <html>
        <head></head>
        <body>
          <img src="/image/logo.png" alt=""/>
        </body>
      </html>
    `
  );
});

// 監聽 port
const port = process.env.PORT || 3000;
app.listen(port);
```