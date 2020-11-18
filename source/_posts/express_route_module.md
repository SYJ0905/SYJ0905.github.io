---
title: Express.js - Route 模組化
tags:
  - Express
  - Nodejs
  - JavaScript
categories:
  - Nodejs
description: 當網頁頁面來越多時，意味著 app.js 會撰寫更多路由設定，最後導致不易維護，本篇就來介紹如何將 Route 模組化吧!!
abbrlink: 447901249
date: 2019-12-30 00:00:00
---
## 建立模組化檔案
首先在 `根目錄` 新建一個 `routes` 資料夾，並建一支 `admin.js` 檔，
並在 `admin.js` 中撰寫以下範例程式碼:
`middleware` 的部分可以寫在 app.js 或是 模組內呦!
``` JavaScript
const express = require('express');
const router = express.Router();

const login = function(req, res, next) {
  console.log('已登入');
  next();
};

// 外層會設定父層路由 /admin
// 此路由就等於 /admin ， 因為指向 '/'
router.get('/', function(req, res) {
  res.send('Hello Admin');
});

// 外層會設定父層路由 /admin
// 此路由就等於 /admin/account
router.get('/account', function(req, res) {
  res.send('Hello Account');
});

module.exports = router;
```

## Express 設定
在 `app.js` 中引入 `routes` 內的模組化路由檔
``` JavaScript
const express = require('express');
const app = express();
const adminRoute = require('./routes/admin');

// middleware 設定，也可寫在核心 app.js 內呦
// const login = function (req, res, next) {
//   console.log('已登入');
//   next();
// }

app.use('/admin', adminRoute);
// 有需要在引入的模組化路由加入 middleware 則參考以下寫法
// app.use('/admin', login, adminRoute); 

// 首頁
app.get('/', function(req, res) {
  res.send('Hello Cloud');
});
// app.get('/', login, function(req, res) {
//   res.send('Hello Cloud');
// });

// 監聽 port
const port = process.env.PORT || 3000;
app.listen(port);
```
這裡會將 `routes` 資料夾內的 `admin.js` 引入，並且設定該路由模組的 `根目錄`，也就是 `/admin`，最後在將`middleware` 加入

## 測試
開啟 `Web Server` 後輸入以下兩個路徑
`http://localhost:3000/admin`
`http://localhost:3000/admin/account`
如果開啟後有顯示正常的字串就代表成功囉!!