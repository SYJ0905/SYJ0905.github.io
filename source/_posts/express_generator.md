---
title: Express.js - generator 應用產生器
tags:
  - Express
  - Nodejs
  - JavaScript
categories:
  - Nodejs
description: 前面講了很多 Express 的設定，如果每個專案都要從頭設定肯定超白癡的，這時就能使用 Express 的應用產生器，直接幫我們產出一個應用程式的結構。
abbrlink: 2267746451
date: 2019-12-30 00:00:00
---
## 安裝套件
我們使用的是 `express-generator` 的套件，以下附上官方 github 及 npm 連結
[express-generator github](https://github.com/expressjs/generator)
[express-generator npm](https://www.npmjs.com/package/express-generator)
在專案內輸入
```
npm install -g express-generator
```
必須安裝在 `全域環境`才行哩。

## 產生應用程式
開啟專案資料夾，並且執行 `CMD` 到該目錄，
執行 `express --view=ejs`，接下來就會自動產生結構哩
![express-generator](https://i.imgur.com/GzulQ17.png)

## 個人設定
個人是使用 `ejs` 以及 `scss` 做開發，所以我的應用器產生代碼是
```
express --view=ejs --css=sass
```
相關參數設定都可在[官方文件](https://github.com/expressjs/generator)裡找到

設定 `scss` 後，還需在 `app.js` 調整，調整以紅色箭頭處設定，
即可在 `public/stylesheets` 中撰寫 `scss` 檔囉!!
![scss](https://i.imgur.com/XzeMus8.png)

## 測試
執行 `npm i` 後輸入
```
npm start
```
如果有正常出現畫面，並且有吃到 `scss` 的樣式就成功囉!!

