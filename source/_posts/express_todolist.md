---
title: Express.js - 搭配 Firebase 實做 TodoList 代辦清單
date: 2019-12-30
tags: 
  - Express
  - Node.js
  - JavaScript
  - Firebase
categories: Express.js
description: 運用 Express 後端接收資料，並搭配 Firebase 資料庫，來完成一個超簡易的代辦清單吧!!
---
## 專案建立
首先直接輸入 `express --view=ejs` 快速產生資料夾結構
## 取得 Firebase 服務
建立一個新的 Firebase 資料庫後，進入資料庫設定點選 `服務帳戶` ，會看到下方有 `Admin SDK` 的使用方法，並且複製程式碼。
最重要的是點選最下方的 `產生新的私密金鑰` ，此檔案為一個 JSON 檔，內容稍後會用到。
![Firebase](https://i.imgur.com/GmE3U6s.png)

## 安裝套件
這裡除了要安裝 `Firebase admin` 的套件外，還需安裝 `dotenv` 這個環境變數套件。
先附上兩個套件的官方文件
[firebase-admin github](https://github.com/firebase/firebase-admin-node)
[firebase-admin npm](https://www.npmjs.com/package/firebase-admin)
[dotenv github](https://github.com/motdotla/dotenv)
[dotenv npm](https://www.npmjs.com/package/dotenv)
來說說為什麼要 `dotenv` 這個套件吧!
1. 上一部下載回來的金鑰是一個 `express-todolist-firebase-adminsdk-02zaz-3d9472adf6.json` 這種形式的檔案，其內容包含以下資訊:
``` JSON
{
  "type": "xxx",
  "project_id": "xxx",
  "private_key_id": "xxx",
  "private_key": "xxx",
  "client_email": "xxx",
  "client_id": "xxx",
  "auth_uri": "xxx",
  "token_uri": "xxx",
  "auth_provider_x509_cert_url": "xxx",
  "client_x509_cert_url": "xxx"
}
```
當然你可以將整個檔案重新命名並參考官方的引入方式，上一部複製程式碼區塊的地方
``` JavaScript
var serviceAccount = require("path/to/serviceAccountKey.json");
```
不過也能透過 `環境變數` 的方式引入，更為簡潔，畢竟一個專案可能會有很多服務，每個都一個一個引入不是很好。
2. 如果是一個服務就引入一個檔案的話，為了不上到版控，就必須不斷修改 `.gitignore` 的內容，而採用環境變數的方式就完全不需要在版控額外增加忽略的檔案

說明完理由就直接輸入指令吧
```
npm install --save dotenv firebase-admin
```
## 相關檔案建立
* 在 `根目錄` 新增 `.env` 檔案，並根據 `私密金鑰` 的內容填入。
注意: 這裡的的雙引號可加可不加，但 `FIREBASE_PRIVATE_KEY` 一定要加，不然 `100%` 報錯，因為內容含有 `特殊符號`，詳細規則可參照以下官方說明
[dotenv#rules](https://github.com/motdotla/dotenv#rules)
``` env
FIREBASE_DATABASEURL="xxx"
FIREBASE_TYPE="xxx"
FIREBASE_PROJECT_ID="xxx"
FIREBASE_PRIVATE_KEY_ID="xxx"
FIREBASE_PRIVATE_KEY="xxx"
FIREBASE_CLIENT_EMAIL="xxx"
FIREBASE_CLIENT_ID="xxx"
FIREBASE_AUTH_URL="xxx"
FIREBASE_TOKEN_URL="xxx"
FIREBASE_AUTH_PROVIDE_X509_CERT_URL="xxx"
FIREBASE_CLIENT_X509_CERT_URL="xxx"
```
* 在 `根目錄` 新增 `plugins` 資料夾並創建一支 `firebase-admin.js`，名稱隨你命名，只要最後路徑對就好
``` JavaScript
const firebaseAdmin = require('firebase-admin');
// 引入 dotenv 檔
// process.env.變數名稱 指向 .env 中的 變數名稱
require('dotenv').config();

// 跟官方引入是一樣的，不過我們使用變數的方式
firebaseAdmin.initializeApp({
  credential: firebaseAdmin.credential.cert({
    type: process.env.FIREBASE_TYPE,
    project_id: process.env.FIREBASE_PROJECT_ID,
    private_key_id: process.env.FIREBASE_PRIVATE_KEY_ID,
    private_key: process.env.FIREBASE_PRIVATE_KEY,
    client_email: process.env.FIREBASE_CLIENT_EMAIL,
    client_id: process.env.FIREBASE_CLIENT_ID,
    auth_uri: process.env.FIREBASE_AUTH_URL,
    token_uri: process.env.FIREBASE_TOKEN_URL,
    auth_provider_x509_cert_url: process.env.FIREBASE_AUTH_PROVIDE_X509_CERT_URL,
    client_x509_cert_url: process.env.FIREBASE_CLIENT_X509_CERT_URL,
  }),
  databaseURL: process.env.FIREBASE_DATABASEURL,
});

const db = firebaseAdmin.database();
// 輸出模組給外部 router 使用
module.exports = db;
```

## 引入服務
來到 `routes` 中的 `index.js` ，引入 Firebase 服務
``` JavaScript
const express = require('express');
const router = express.Router();
const firebaseAdmin = require('../plugins/firebase-admin');

/* GET home page. */
router.get('/', function(req, res, next) {
  res.render('index', { title: 'Express' });
  console.log(firebaseAdmin.ref());
});

module.exports = router;
```
開啟服務 `npm start` 後輸入 `http://localhost:3000/`，假使 `CMD` 有回傳以下物件陣列格式就以正確接上!!
![firebaseAdmin.ref()](https://i.imgur.com/Kbql7qk.png)

## 前端模版建立
來到 `public` 中的 `index.ejs`，並參考以下範例模版
註: 這裡我有引用 `axios` 的 CDN 服務，方便稍後撰寫 AJAX 更為簡潔，畢竟原生的 `xhr` 寫法在先前已經有提到過了，就不再贅述。
``` HTML
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title><%= title %></title>
    <link rel='stylesheet' href='/stylesheets/style.css' />
  </head>
  <body>
    <h1><%= title %></h1>
    <p>Welcome to <%= title %></p>

    <input type="text" name="todoContent" id="todoContent">
    <input type="button" id="send" value="送出">
    <ul class="todoList"></ul>

    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <script src="/javascripts/all.js"></script>
  </body>
</html>
```

## 後端製作 post API
利用 Express 快速建立 API，並搭配 Firebase 存儲前端傳過來的資料。
在 `routes` 中的 `index.js` 加入以下範例代碼段落:
``` JavaScript
router.post('/addTodo', function(req, res, next) {
  // 接收前端傳進來的資料
  console.log(req.body);
  const todo = {
    content: req.body.content,
  };
  firebaseAdmin.ref('todo').push(todo)
    .then(() => {
      // 顯示資料庫內容，並回傳前端 AJAX response 物件
      firebaseAdmin.ref('todo').once('value', (dataSnapshot) => {
        // 將物件形式的 dataSnapshot.val() 中的 key 加入到各自的物件內，並重組陣列回傳
        const listData = [];
        dataSnapshot.forEach((item) => {
          const itemInfo = item.val(); // item.val() 為一物件
          itemInfo.key = item.key; // item.key 取唯一值
          listData.push(itemInfo);
        });
        res.send({
          success: true,
          result: listData,
          message: '資料儲存成功',
        });
      });
    });
});
```
由於 Firebase 回傳的是物件格式，在迴圈上必須使用 `for in` 寫法，而不是 `forEach()`。
本人不是很喜歡 `for in` 在去組字串(ex:data[i])，所以使用 `forEach()` 將同一份資料包在物件內，並回傳前端一個 `陣列`格式。

## 前端串接資料
後端已經開好 API 了，接下來就在前端提取輸入內容再利用 AJAX 傳進後端
隨後，後端與資料庫將會寫入資料並回傳 `response` 給前端做渲染
在 `public/javascripts` 中建立 `all.js`，並可參考以下程式碼:
``` JavaScript
// DOM 宣告
const todoContent = document.querySelector('#todoContent');
const send = document.querySelector('#send');
const todoList = document.querySelector('.todoList');

send.addEventListener('click', sendTodo);

function sendTodo() {
  const todo = {
    content: todoContent.value,
  };
  // AJAX
  axios.post('/addTodo', todo)
    .then((res) => {
      console.log(res);
      renderTodo(res.data);
    })
    .catch((err) => {
      console.log(err);
    });
}

function renderTodo(data) {
  if (data.success) {
    const dataList = data.result;
    let str = '';
    dataList.forEach(item => {
      str += `<li data-key="${ item.key }">${ item.content }</li>`;
    });
    todoList.innerHTML = str;
  } else {
    return
  }
}
```
此處會使用 `data-key` 來保存唯一值，因為刪除功能時會需要這個唯一值跟 Firebase 刪除資料。
依照以上操作，已經可以開啟 `http://localhost:3000/` 輸入一些代辦事項，並渲染出來。
接下來會介紹如何在 `進頁面` 時就跟資料庫取得資料並渲染代辦事項以及刪除代辦事項。

## 後端修正 get API
進站時的路由是 `/`，所以就必須修改 `routes/index` 中的 `router.get('/')`。
修改範例請參照以下程式碼:
``` JavaScript
router.get('/', function(req, res, next) {
  firebaseAdmin.ref('todo').once('value', dataSnapshot => {
    const listData = [];
    dataSnapshot.forEach(item => {
      const itemInfo = item.val(); // item.val() 為一物件
      itemInfo.key = item.key; // item.key 取唯一值
      listData.push(itemInfo);
    });
    res.render('index', {
      title: 'Express',
      listData, // 省略寫法
    });
  });
});
```
## 模版修改
一開始進站就要渲染的話必須先將 DOM 結構寫出，在根據後端 GET 進來的資料做 `forEach()` 渲染資料列表。
修改位置 `index.ejs` 中的 `ul`，可參照以下範例:
``` HTML
<ul class="todoList">
  <% listData.forEach(function(item){ %>
    <li data-key="<%= item.key %>"><%= item.content %></li>
  <% }) %>;
</ul>
```
完成以上修正後，已經可以在進入首頁後看到資料顯示。
接下來就是最後的刪除部分囉，一起加油吧!!

## 後端新增 delete API
刪除 API 的路由是 `/deleteTodo`，在 `routes/index` 中新增 `router.delete('/deleteTodo')`。
修改範例請參照以下程式碼:
``` JavaScript
router.delete('/deleteTodo', function(req, res) {
  // 接收前端傳 todo 的 id 進來
  const todoId = req.body.id;
  firebaseAdmin.ref('todo').child(todoId).remove()
    .then(() => {
      firebaseAdmin.ref('todo').once('value', (dataSnapshot) => {
        const listData = [];
        dataSnapshot.forEach(item => {
          const itemInfo = item.val(); // item.val() 為一物件
          itemInfo.key = item.key; // item.key 取唯一值
          listData.push(itemInfo);
        });
        res.send({
          success: true,
          result: listData,
          message: '刪除成功',
        });
      });
    });
});
```

## 前端模版修正
多了刪除功能，代表也要有按鈕綁定事件。所以模版也需要一併修正
``` HTML
<ul class="todoList">
  <% listData.forEach(function(item){ %>
    <li data-key="<%= item.key %>"><%= item.content %> - 
      <a href="#" data-key="<%= item.key %>">刪除</a>
    </li>
  <% }) %>
</ul>
```

## 前端串接刪除資料
在 `all.js` 中加入刪除功能
``` JavaScript
todoList.addEventListener('click', deleteTodo);

function deleteTodo(e) {
  e.preventDefault();
  if (e.target.nodeName !== 'A') return;
  const data = {
    id: e.target.dataset.key,
  };
  axios.delete('/deleteTodo', {
    data,
  })
    .then((res) => {
      console.log(res);
      renderTodo(res.data);
    });
}
```
終於完成最簡易的前後端串接代辦清單啦!!