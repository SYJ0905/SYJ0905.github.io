---
title: Express.js - 取得表單內容及轉址
date: 2019-12-27
tags: 
  - Express
  - Node.js
  - JavaScript
categories: Express.js
description: 身為一個前端是絕對要掌握表單的傳送機制，本篇會介紹如何在前端送出表單並使用 Express 接收資料並導入正確路徑。
---
## 安裝套件
我們使用的是 `body-parser` 的套件，以下附上官方 github 及 npm 連結
[body-parser github](https://github.com/expressjs/body-parser)
[body-parser npm](https://www.npmjs.com/package/body-parser)
在專案內輸入
```
npm install body-parser --save
```
## Express 設定
在 `app.js` 中加入以下設定
``` JavaScript
const express = require('express');
const app = express();
const bodyParser = require('body-parser');

// 設定 EJS
const engine = require('ejs-locals');
app.engine('ejs', engine);
app.set('views', './views');
app.set('view engine', 'ejs');

app.use(bodyParser.json()); // 支援 json
app.use(bodyParser.urlencoded({ // 解析表單內容
  extended: false,
}));

app.get('/', function (req, res) {
  res.render('index', {
    documentTitle: '首頁',
  });
});

app.get('/search', function(req, res) {
  res.render('search', {
    documentTitle: '搜尋頁',
  });
});

// 有兩種寫法，需針對 action 修改路由
// action 為 /searchList
app.post('/searchList', function(req, res) {
  console.log('轉址');
  console.log(req.body);
  // 轉址
  res.redirect('/search');
});

// action 為 /search
// app.post('/search', function(req, res) {
//   console.log('渲染');
//   console.log(req.body);
//   // 渲染
//   res.render('/search', {
//     documentTitle: '搜尋頁',
//   });
// });

// 監聽 port
const port = process.env.PORT || 3000;
app.listen(port);
```
細節說明:
* `req.body`: 為物件格式，可紀錄前端表單 `name` 的屬性內容。
* `res.redirect('指定路由')`: 收到資料後，轉址到該路由，並渲染畫面。
註: 如果沒有 `轉址` 的話，會到導致網頁上方還在轉圈圈，也就是 loading 中，必須要正確轉址才算完成

## 建立搜尋頁面
由於有使用 `ejs` 當模版語言，還不清楚的可以看我之前的 `ejs` 的文章呦!
在 `views` 資料夾內新增 `search.ejs` 檔，並參考以下表單範例程式碼:
```
<% layout('layout') %>
  <h1><%= documentTitle %></h1>
  <form action="/searchList" method="post">
    <input type="text" name="inputText" placeholder="請輸入內容">
    <input type="submit" value="送出">
  </form>
```
## 測試
開啟 `Web Server` 後輸入 `http://localhost:3000/search`，在欄位輸入內容送出，此時觀察 `CMD`、`終端機` 是否有接收到一個物件資料 `req.body`，其內容有包含輸入的資料，如果有正確收到代表成功囉!!

## 結尾
這算是後端的表單驗證，在轉址前收到資料並進行一系列判斷，來決定要轉址到之後的網站內容。可想而知，如果驗證機制都交給後端的話，當計算量過大就會導致效能降低且網頁速度變慢。
以目前表單驗證來說，會在前端初步做驗證，由使用者的載具 cpu 來處理計算，畢竟平常用量就很低所以不用白不用，所以當使用者不斷輸入欄位內容時就判斷是否符合驗證規則之類的，這樣傳到後端時才不會導致伺服器計算量過大。