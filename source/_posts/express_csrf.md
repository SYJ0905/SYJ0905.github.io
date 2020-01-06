---
title: Express.js - CSRF 驗證機制
date: 2020-01-07
tags: 
  - Express
  - Node.js
  - JavaScript
categories: Express.js
description: 使用 CSRF 驗證讓網站不會受到攻擊吧!!
---
## 前言
根據上一篇 `Express.js - Gmail 發送信件實作 + OAuth 2.0` 做的寄信程式，只要知道 POST 位址就能使用 postman 填入相關參數並讓該應用程式寄信。
這會讓網站變得很不安全，一不小心就會被駭客攻擊到應用程式崩潰，而 Node.js 也將 CSRF 驗證機制加入其中，一起 CSRF 的攻擊吧!!

## 安裝套件
本次使用的套件為 `csurf` 不是 `csrf` 喔。
[csurf github](https://github.com/expressjs/csurf)
[csurf npm](https://www.npmjs.com/package/csurf)
輸入安裝指令
```
npm install csurf -S
```

## Express 設定
專案資料夾則是採用 Express.js - Gmail 這篇建立的。
來到 `routes/contact.js`中，引入 `csurf` 服務。
一開始就加入下設定
``` JavaScript
const csrf = require('csurf');
// setup route middlewares
var csrfProtection = csrf({ cookie: true })
```
路由修改範例:
``` JavaScript
router.get('/', csrfProtection, function(req, res) {
  res.render('contact', { csrfToken: req.csrfToken() });
});
router.post('/post', csrfProtection, function(req, res) {
  // 中間省略
});
```
分別在兩個路由都加入 `middlewares`，接下來是修改模版

## 模版修改
位置: `views/contact.ejs`
在 form 表單加入 `csurf` 設定
``` HTML
<!DOCTYPE html>
<html>
<head>
  <title>傳送表單內容</title>
</head>
<body>
  <form action="/contact/post" method="post">
    // name 、 value 必填
    <input type="hidden" name="_csrf" value="<%= csrfToken %>">
    // 中間省略
  </form>
</body>

</html>
```

## 測試
開啟服務，進入 `http://localhost:3000/contact` 看一下 F12 中的 `cookie` 是否有 `_csurf` 的值，以及 `input` 元素有沒有寫入 `csrfToken` 變數，如果都有的話就成功囉!!
這時使用 postman 即使知道路由也是無法傳送資訊到後端並寄發信件的喔!!