---
title: Node.js - 開啟 Web Server
tags:
  - Nodejs
  - JavaScript
categories:
  - Nodejs
description: 使用 Nodo.js 內建模組來建立一個 Web Server 吧!
abbrlink: 3369199661
date: 2019-12-25 00:00:00
---
## 創建一個 Web Server
1. 建立專案資料夾與 `all.js`
2. require `http` 模組
3. 撰寫 `creatServer` 的 function

何謂 `request` 與 `response` ?
* request 請求: 當使用者讀取網站時會向伺服器發送請求，伺服器接收到使用者的相關資料
* response 回傳 : 收到 request 後回傳的資料

以下是範例程式碼:
``` JavaScript
const http = require('http');
const port = 8080;
http.createServer(function (request, response) {
  // request 請求 : 當使用者讀取網站時會向伺服器發送請求，伺服器接收到使用者相關資料
  // response 回傳 : 收到 request 後回傳的資料
  console.log(request.url);
  response.writeHead(200, {
    'Content-Type': 'text/plain', // 回傳格式 text/plain or text/html
  })
  response.write('hello'); // 一般文字 or html 標籤形式
  response.end();
}).listen(port); // 監聽通訊阜
```
執行 `node app.js` 後開啟 `http://localhost:8080`就會看到 `hello` 囉!