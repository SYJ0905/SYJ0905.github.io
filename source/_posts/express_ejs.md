---
title: Express.js - EJS template
date: 2019-12-27
tags: 
  - Express
  - Node.js
  - JavaScript
categories: Express.js
description: 使用 template 模版語言不但提高了可維護性還降低程式碼重複性呢!!
---
## 前言
以前在撰寫 HTML 檔時是不是每支檔案都必須要有 `!DOCTYPE html`、`head`、`header`、`footer` 等標籤，而當網站頁數一多起來，在維護上就變得不容易了。
最簡單的例子就是當 `header` 有變更時，所有頁面的 `header` 必須修正，這就得一頁一頁的修改，效率極為慘烈。
於是 `template` 模版語言就是因此而被開發出來，不僅能夠讓所有頁面共用同一份 `layout` ，還能使用 `迴圈`、`判定參數`、`傳入資料`等行為，將開發效率提升了一個檔次，其實很多前端開發者到後來都不再寫 `HTML` 了，而轉成寫 `ejs`、`pug`等模版語言，只需要搭配編譯工具轉成 `HTML` 即可達到 `具有簡潔的架構`、`易維護` 的成效。

## 安裝套件
我們使用的是 `ejs-locals` 的套件，以下附上官方 github 及 npm 連結
[ejs-locals github](https://github.com/randometc/ejs-locals)
[ejs-locals npm](https://www.npmjs.com/package/ejs-locals)
在專案內輸入
```
npm install ejs-locals --save
```
## Express 設定
在 `app.js` 中加入以下引入設定
``` JavaScript
const express = require('express');
const app = express();

// 設定 EJS template
const engine = require('ejs-locals');
app.engine('ejs', engine);
app.set('views', './views');
app.set('view engine', 'ejs');

// 指定路由 > 渲染特定 ejs 檔 > 傳入參數(物件格式)
app.get('/', function (req, res) {
  res.render('index', { // 指定 index.ejs
    show: true,
    documentTitle: '首頁',
    title: '<h1>部落格名稱: Cloud F2E Blog</h1>',
    boss: 'Cloud',
    course: ['html', 'js', 'bootstrap', 'vue'],
  });
});

app.get('/user', function(req, res) {
  res.render('user', { // 指定 user.ejs
    documentTitle: '使用者頁',
  });
});

// 監聽 port
const port = process.env.PORT || 3000;
app.listen(port);
```

## template 建立
來到根目錄，建立 `views` 資料夾，名稱可以隨便取，但必須跟上方 `./views` 一樣才行呦。
![views](https://i.imgur.com/k8SZMkx.png)
在底下建立 `layout.ejs`、`index.ejs`、`header.ejs`
* layout.ejs 內容
``` HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title><%= documentTitle %></title>
</head>
<body>
  <header>
    <% include header %>
  </header>
  
  <%- body %>

  <footer>
    <% include header %>
  </footer>
</body>
</html>
```
* index.ejs 內容
``` HTML
<% layout('layout') %>
  <h1>Index</h1>

  <% if (show) { %>
    <span>顯示資料: show = true</span>
  <% } else { %>
    <span>不顯示資料: show = false</span>
  <% } %>

  <%- title %> 

  <h1>主辦人: <%= boss %></h1>

  <ul>
    <% for(i = 0;i < course.length; i++) { %>
      <li><%= course[i] %></li>
    <% } %>
  </ul>
```
* header.ejs 內容
``` HTML
<p>I'm in the header.</p>
```
輸出及引入 template 的方法:
* `<% layout('layout') %>`: 找到 `layout.ejs` 並搭配 `layout.ejs` 中的 `<%- body %>` 渲染內容
* `<% include header %>`: 找到 `header.ejs` 並搭配 `HTML` 渲染內容

此範例中有寫入 `if`、`for迴圈` 的方法，其實跟寫 JavaScript 很雷同，差在要顯示時需要加入 ejs 的引入寫法而已
在 ejs 內顯示傳入參數的方法:
* `<%= 傳入參數的屬性 %>`: 此方法會將傳入資料以 `字串` 形式渲染出來
* `<%- 傳入參數的屬性 %>`: 此方法會將傳入資料以 `HTML` 形式渲染出來
