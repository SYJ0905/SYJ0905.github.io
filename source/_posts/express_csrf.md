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
