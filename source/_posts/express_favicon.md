---
title: Express.js - 加入 favicon
tags:
  - Express
  - Nodejs
  - JavaScript
categories:
  - Nodejs
description: 除了在 ejs 直接引入外，還能透過後端 middleware 的方式加入 favicon 呦!!
abbrlink: 3431640210
date: 2020-01-10 00:00:00
---
## 安裝套件 
套件名稱: serve-favicon
[serve-favicon github](https://github.com/expressjs/serve-favicon)
[serve-favicon npm](https://www.npmjs.com/package/serve-favicon)
在專案內輸入
```
npm install serve-favicon -S
```

## 加入 favicon
在 `public` 目錄下，將網所需的 `favicon.ico` 檔加入
![favicon](https://i.imgur.com/2fwm2vE.png)

## Express 設定
加入以下程式碼即可
``` JavaScript
const favicon = require('serve-favicon');
app.use(favicon(path.join(__dirname, 'public', 'favicon.ico')));
```

## 結尾
都完成以上步驟後開啟服務，就能看見自定義的 favicon 囉!!