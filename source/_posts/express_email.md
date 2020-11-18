---
title: Express.js - Gmail 發送信件實作 + OAuth 2.0
tags:
  - Express
  - Nodejs
  - JavaScript
  - OAuth
categories:
  - Nodejs
description: 使用 Google OAuth 2.0 + Express 製作更安全的寄信應用程式吧!!
abbrlink: 4047671532
date: 2020-01-06 00:00:00
---
## 前言
原本在 nodemailer 中輸入 Gmail 的帳號密碼就能夠發送信件，但 Google 基於安全性考量，在近幾年推出 OAuth 2.0 驗證機制。也就是必須跟 Google 取得 token 才能使用該帳號進行寄信功能

## 建立 OAuth
首先到 Google Cloud Platform 創建一個新專案
![Google Cloud Platform](https://i.imgur.com/X6tN1VT.png)
![新增專案](https://i.imgur.com/eBEGfdF.png)
創建完專案後，到左邊選單找到 <b>API 服務</b>，並點選啟用 API 服務
![API 服務](https://i.imgur.com/edSizp1.png)
搜尋 Gmail API，然後點選 <b>啟用</b>  
![Gmail API](https://i.imgur.com/jE3LrnH.png)
![Gmail API 啟用](https://i.imgur.com/a1Cq9aZ.png)
啟用之後會來到 Gmail API 頁面，接下來要建立憑證。
點擊左方 <b>憑證</b> 然後 <b>建立憑證</b> 選擇 <b>OAuth 用戶端ID</b>
接著會要求同意設定
![同意設定](https://i.imgur.com/3Nwgzsl.png)
User Type 選擇 <b>外部</b>
![User Type](https://i.imgur.com/Fvd5fgB.png)
接下來只需填寫名稱並儲存即可
![OAuth 同意畫面](https://i.imgur.com/LSjyfcY.png)
到左邊選 <b>憑證</b> <b>建立憑證</b> 選擇 <b>OAuth 用戶端ID</b>
![選擇憑證](https://i.imgur.com/qJPFu4m.png)
選擇 <b>網路應用程式</b>，並且在下方 <b>已授權的重新導向URL</b> 中填入 `https://developers.google.com/oauthplayground`。
![網路應用程式](https://i.imgur.com/VWE1NmV.png)
完成後會得到兩筆資料 <b>用戶端ID</b>、<b>用戶端密鑰</b> ，之後會用到。
![OAuth](https://i.imgur.com/kxSxWpz.png)

## 取得 Refrsh Token
開啟 [https://developers.google.com/oauthplayground](https://developers.google.com/oauthplayground) ，點選右上角齒輪，將 <b>Use your own OAuth credentials</b>打勾，並填入剛剛取得的 Client ID 以及 Client Secret
![Client ID 以及 Client Secret](https://i.imgur.com/X6ah8jN.png)
左邊的部分輸入 `https://mail.google.com/`後按下 Authorize APIs
![Authorize APIs](https://i.imgur.com/W6uhkwI.png)
選擇要使用的 Google 帳戶
![Google 帳戶](https://i.imgur.com/9E1kXA8.png)
這邊因為 Google 的安全機制會先擋一下，只需在 <b>進階</b> 裡面點選前往連結即可。
![未經驗證](https://i.imgur.com/jrkPl8x.png)
進入之後 Google 會再詢問一次是否允許。
![權限授予](https://i.imgur.com/urNqgzD.png)
再驗證一次是否允許應用程式
![應用程式權限](https://i.imgur.com/B3qQdx8.png)
接著畫面會回到原本的頁面，這時點選 <b>Exchange authorization code for tokens</b> 就可取得 Refresh Token
![Imgur](https://i.imgur.com/i2wying.png)

## 模版建立
開啟專案資料夾輸入
```
express --view=ejs
```
在 `views` 建立 `contact.ejs` 以及 `contactReview.ejs`，可以參考下範例:
* contact.ejs
``` HTML
<!DOCTYPE html>
<html>
<head>
  <title>傳送表單內容</title>
</head>
<body>
  <form action="/contact/post" method="post">
    <h1>聯絡我們</h1>
    <div>
      <label for="username">姓　　名：</label>
      <input type="text" name="username" id="username"/>
    </div>
    <div>
      <label for="email">電子郵件：</label>
      <input type="text" name="email" id="email"/>
    </div>
    <div>
      <label for="title">標　　題：</label>
      <input type="text" name="title" id="title"/>
    </div>
    <div>
      <label for="description">訊息內容：</label>
      <textarea name="description" id="description" cols="30" rows="10"></textarea>
    </div>
    <div>
      <input type="submit" value="送出訊息" />
    </div>
  </form>
</body>
</html>
```

* contactReview.ejs
``` HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <title>傳送成功</title>
</head>
<body>
  <h1>傳送成功</h1>
  <a href="/contact">回到 聯絡我們</a>
</body>
</html>
```

## Express 修正
到 `App.js` 中加入以下程式碼:
``` JavaScript
const contactRouter = require('./routes/contact');
app.use('/contact', contactRouter);
```

## nodemailer 設定
來到 `routes` 建立 `contact.js` 並加入範例:
``` JavaScript
const express = require('express');
const router = express.Router(); 
const nodemailer = require('nodemailer');

router.get('/', function(req, res) {
  res.render('contact');
});
router.get('/review', function(req, res) {
  res.render('contactReview');
});
router.post('/post', function(req, res) {
  const data = req.body;
  // 前端傳進資料，用傳統表單形式，也能用 AJAX 呦!
  console.log(data);
  const transporter = nodemailer.createTransport({
    service: 'Gmail',
    auth: {
      type: 'OAuth2',
      user: '要使用的 Gmail',
      clientId: '填入用戶端ID',
      clientSecret: '填入用戶端金鑰',
      refreshToken: '填入 Refresh Token',
    },
  });
  const mailOptions = {
    from: '"來自XXX"<xxx@gmail.com>',
    to: '收件人信箱',
    subject: `${req.body.username}寄了一封測試信`,
    text: req.body.description,
  };
  transporter.sendMail(mailOptions, (err, info) => {
    if (err) {
      return console.log(err);
    }
    res.redirect('/contact/review');
  });
});
module.exports = router;
```

## 測試
接著開啟服務，在 `http://localhost:3000/contact` 輸入一些內容並送出，並查看收件人信箱，如果有收到信件代表已經成功囉!!
