---
title: Express.js - AJAX 傳送表單資料
date: 2019-12-27
tags: 
  - Express
  - Node.js
  - JavaScript
categories: Express.js
description: 使用 AJAX 非同步傳遞資料更快速也提高使用者體驗!!
---
## 前言
傳統的表單與 AJAX 的差異可以先自行 Google ，本篇就不再多贅述了。

## 建立 template
在 `views` 資料夾內新增 `search.ejs` 檔，並參考以下範例程式碼:
```
<% layout('layout') %>
  <form action="" method="">
    <input type="text" name="inputText" id="inputText" placeholder="請輸入內容">
    <input type="submit" id="inputSend" value="送出">
  </form>
  <script src="/all.js"></script>
```
這裡的 `action` 跟 `method` 都不需要填入呦!!

## 建立 js 檔
在 `public` 資料夾內新增 `all.js` 檔，並參考以下範例程式碼:
``` JavaScript
;(function() {
  const content = document.querySelector('#inputText');
  const send = document.querySelector('#inputSend');
  send.addEventListener('click', function(e) {
    e.preventDefault();
    const value = content.value;
    const xhr = new XMLHttpRequest();
    xhr.open('post', '/search'); // 搭配 app.js 中的 post 路由

    // x-www-form-urlencoded 格式
    // xhr.setRequestHeader('Content-type', 'application/x-www-form-urlencoded');
    // const data = `content=${value}`;
    // xhr.send(data);
    // xhr.onload = function() {
    //   console.log(JSON.parse(xhr.responseText));
    // }

    // json 格式
    xhr.setRequestHeader('Content-type', 'application/json');
    const data = JSON.stringify(
      {
        content: value,
        list: [1, 2, 3],
      },
    );
    xhr.send(data);
    xhr.onload = function() {
      console.log(JSON.parse(xhr.responseText));
    }
  });
})();
```

## Express 設定
在 `app.js` 中加入以下設定
``` JavaScript
const express = require('express');
const app = express();
const bodyParser = require('body-parser');

// 增加靜態檔案路徑 ， 必須寫在最前面
app.use(express.static('public'));

// 設定 EJS
const engine = require('ejs-locals');
app.engine('ejs', engine);
app.set('views', './views');
app.set('view engine', 'ejs');

app.use(bodyParser.json());
app.use(bodyParser.urlencoded({
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

// 重點 post
app.post('/search', function(req, res) {
  console.log('post');
  console.log(req.body);
  res.send(req.body);
});

// 監聽 port
const port = process.env.PORT || 3000;
app.listen(port);
```
`app.post()` 中的 `/search` 就是前端所稱的 `API`。

## 測試
開啟 `Web Server` 後輸入 `http://localhost:3000/search`，在欄位輸入內容送出，此時觀察瀏覽器是否有 loading 狀態以及 `CMD`、`終端機` 有沒有收到資料，如果有收到資料，但瀏覽器沒有跳轉，代表已經透過 Ajax 達成非同步傳輸資料囉!!