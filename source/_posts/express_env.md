---
title: Express.js - env 環境變數
tags:
  - Express
  - Nodejs
  - JavaScript
categories:
  - Nodejs
description: 將網站中的機密資料都使用環境變數來取代吧!
abbrlink: 3250754690
date: 2020-01-07 00:00:00
---
## 前言
前章節在使用 Google OAuth2.0 時有使用到 ID、金鑰以及 Token，這些資料雖然是寫在後端程式碼中，但在版控時還是要避免顯示。所以我們會新建一個環境變數檔，將往ˇ站的變數都放在此處，並且不會加入版控。到部屬到服務器時(ex:heroku)會有設定可以加入環境變數。

## 安裝套件
套件名稱: `dotenv`
[dotenv github](https://github.com/motdotla/dotenv)
[dotenv npm](https://www.npmjs.com/package/dotenv)
在專案內輸入
```
npm install dotenv -S
```

## 建立 .env 檔
在專案 `根目錄` 新建 `.env` 檔，其內容可參考以下寫法:
```
DB_HOST=localhost
DB_USER=root
DB_PASS=s1mpl3
```
## Express 引入設定
在 `app.js` 中加入以下程式碼:
``` JavaScript
require('dotenv').config();
```
## 使用 env 環境變數
將原先的機密資料使用 `process.env.環境變數名稱` 即可。
`XXX` 為 `.env` 檔中的名稱。
``` JavaScript
const user = process.env.XXX;
```