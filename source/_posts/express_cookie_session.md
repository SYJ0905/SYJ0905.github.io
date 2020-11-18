---
title: Express.js - Cookie 和 session 應用
tags:
  - Express
  - Nodejs
  - JavaScript
  - Storage
categories:
  - Nodejs
description: 本篇會介紹如何在後端 Express.js 中使用 Cookie 和 Session 存儲資料
abbrlink: 1975209315
date: 2020-01-02 00:00:00
---
## 前言
有一點必須先釐清，這邊所以提 Session 是屬於後端儲存庫，而跟 HTML5 中的 SessionStorage 是不一樣的。

## Cookie
通常用來儲存登入狀態、造訪紀錄，具備以下特性:
* 儲存空間僅 4KB
* 由 key/value 寫入
* 可設置失效時間
* 可在 Client 與 Server 讀取與寫入資料
* 每次請求都會攜帶在 header 中，保存過多數據會導致效能降低

## Session
Session 具備以下特點:
* 儲存在 Server 的暫存資料，可依開發設計放置記憶體或是資料庫上
* Session 可以在 Cookie 中儲存 UUID，並透過驗證確認使用者

## Cookie 語法
* 寫入 Cookie 資料

``` JavaScript
document.cookie = 'myname=Cloud';
```
即可在 `application` 的 Cookie 看見資料
![Cookie](https://i.imgur.com/IJ2OyJg.png)

* 設定失效時間
`expires`: 失效時間，使用 GMT 時間
`path`: 路徑

```
document.cookie = 'myname=Cloud;expires=Thu, 02 Jan 2020 07:48:48 GMT;path=/';
```
但我們總不能去手寫時間吧，有方法可以直接取得
``` JavaScript
new Date().toGMTString();
```

* 設定時效
`max-age`: 幾秒後 Cookie 失效，如此一來就不用設定時間

``` JavaScript
document.cookie = 'myname=Cloud;max-age=10;path=/';
```

## Express Cookie
可以使用 `req.cookies` 取得 cookie 資料，當然如果要回傳並寫入 cookie 也是可行的。
``` JavaScript
res.cookie('myname', 'Cloud', {
  maxAge: 5000,
});
```
安全性寫法:
為了避免駭客或其他不肖開發人員使用 JS 抓取 Cookie 資料，可加入安全性參數
``` JavaScript
res.cookie('myname', 'Cloud', {
  maxAge: 5000,
  httpOnly: true,
})
```
但即便如此，還是可以在 `application` 中清楚看見資料，所以會建議採用 Session 給一組 UUID 來綁定資料。

## Express Session
要在 Expres 中使用 Session 必須安裝 `express-session` 套件
[express-session github](https://github.com/expressjs/session)
[express-session npm](https://www.npmjs.com/package/express-session)
```
npm i express-session -S
```
並在 `app.js` 中加入設定
``` JavaScript
const session = require('express-session');
app.use(session({
  secret: 'keyboard cat', // 安全方式，會依照裡面的字串去做加密邏輯
  resave: true, // 是否要每次進入網頁時重新設置 seesion cookie，如果有設置失效，例如 5 分鐘，重新整理後又有 5 分鐘，但是必須要改成 ture 才有效，但是建議改成 true
  saveUninitialized: true,
  cookie: { 
    maxAge: 5000 // 可以設置 cookie 過期時間，例如 5 秒後過期
  }
}))
```
* Express 接收前端 `表單` or `AJAX` 資料並寫入 Session

``` JavaScript
req.session.XXX = req.body.XXX;
```
註: 不論顯示或寫入，都是使用 `req` 而不會用到 `res` 呦!! 