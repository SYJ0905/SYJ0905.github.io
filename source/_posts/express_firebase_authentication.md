---
title: Express.js - firebase 會員註冊登入功能
date: 2020-01-13
tags: 
  - Express
  - Node.js
  - JavaScript
  - Firebase
categories: Express.js
description: 利用 Firebase 建立會員及登入會員功能吧!!!
---
## 安裝套件
套件名稱: `firebase`
[firebase github](https://github.com/firebase/firebase-js-sdk)
[firebase npm](https://www.npmjs.com/package/firebase)
在專案內輸入
```
npm install firebase -S
```

## 取得 Firebase 環境變數
首先在 Firebase 新建專案，並新增 `網路應用程式` 
![網路應用程式](https://i.imgur.com/X7gEGGj.png)
完成後在設定區塊可以到環境變數
![環境變數](https://i.imgur.com/8RClT42.png)

## 引入環境變數
使用 `.env` 檔將 Firebase 資料引入，`.env` 相關作法可以參照 [Express.js - env 環境變數](https://syj0905.github.io/Express-js/20200107/express-env/)
在 `根目錄` 建立 `plugins` 資料夾，新增 `firebase.js` 並加入 Firebase 設定
``` JavaScript
const firebase = require('firebase');
require('dotenv').config();

firebase.initializeApp({
  apiKey: process.env.FIREBASE_APIKEY,
  authDomain: process.env.FIREBASE_AUTHDOMAIN,
  databaseURL: process.env.FIREBASE_DATABASEURL,
  projectId: process.env.FIREBASE_PROJECTID,
  storageBucket: process.env.FIREBASE_STORAGEBUCKET,
  messagingSenderId: process.env.FIREBASE_MESSAGINGSENDERID,
  appId: process.env.FIREBASE_APPID,
  measurementId: process.env.FIREBASE_MEASUREMENTID,
});

module.exports = firebase;
```

## 模板建立
在 `views` 中建立 `signup.ejs`，並參考以下範例:
``` HTML
<form action="/signup" method="post">
  <h2>註冊</h2>
  <div>
    <label for="">Email:</label>
    <input type="email" name="email">
  </div>
  <div>
    <label for="">Password:</label>
    <input type="password" name="passwd">
  </div>
  <div>
    <label for="">nickname:</label>
    <input type="text" name="nickname">
  </div>
  <div>
    <input type="submit" value="註冊">
  </div>
  <%- errorMsg %>
</form>
```
在 `views` 中建立 `login.ejs`，並參考以下範例:
``` HTML
<form action="/login" method="post">
  <h1>登入</h1>
  <div>
    <label for="">Email:</label>
    <input type="text" name="email">
  </div>
  <div>
    <label for="">Password:</label>
    <input type="password" name="passwd">
  </div>
  <div>
    <input type="submit" value="Log In">
  </div>
  <%- errorMsg %>
</form>
```


## 路由設定
在 `app.js` 加入以下範例:
``` JavaScript
const signup = require('./routes/signup');
app.use('/signup', signup);
```
接著在 `routes` 新增 `signup.js` 檔，最後就是撰寫註冊功能囉!!

## 註冊邏輯
除了 Firebase 註冊的 `API` 有區別外，其餘都是先前已會的程式碼，不會太過艱深，可參照以下範例:
``` JavaScript
const express = require('express');

const router = express.Router();
const firebase = require('../plugins/firebase');
const firebaseAdmin = require('../plugins/firebase-admin');

const firebaseAuth = firebase.auth();

// route: /signup
router.get('/', (req, res) => {
  res.render('signup', {
    title: '註冊',
    errorMsg: req.flash('errorMsg'),
  });
});

// route: /signup
router.post('/', (req, res) => {
  const email = req.body.email;
  const password = req.body.passwd;
  const nickname = req.body.nickname;
  firebaseAuth.createUserWithEmailAndPassword(email, password)
    .then((user) => {
      const userInfo = {
        uid: user.user.uid,
        email: user.user.email,
        nickname,
      };
      firebaseAdmin.ref(`/user/${user.user.uid}`).set(userInfo);
      res.redirect('/signup/success');
    })
    .catch((error) => {
      const errorMsg = error.message;
      req.flash('errorMsg', errorMsg);
      res.redirect('/signup');
    });
});

router.get('/success', (req, res) => {
  res.render('success', {
    title: '註冊成功',
  });
});

module.exports = router;
```
## 登入邏輯
``` JavaScript
const express = require('express');

const router = express.Router();
const firebase = require('../plugins/firebase');

const firebaseAuth = firebase.auth();

// route: /login
router.get('/', (req, res) => {
  res.render('login', {
    title: '登入',
    errorMsg: req.flash('errorMsg'),
  });
});

router.post('/', (req, res) => {
  const email = req.body.email;
  const password = req.body.passwd;
  firebaseAuth.signInWithEmailAndPassword(email, password)
    .then((user) => {
      req.session.uid = user.user.uid;
      res.redirect('/');
    })
    .catch((error) => {
      const errorMsg = error.message;
      req.flash('errorMsg', errorMsg);
      res.redirect('/login');
    });
});
module.exports = router;
```
避免篇幅太冗長，以上範例請搭配 `完整 Demo` 服用，以免出現錯誤!! 

## Demo
[Express - 會員留言板](https://github.com/SYJ0905/Express-Admin)