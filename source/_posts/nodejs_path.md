---
title: Node.js - Path 模組應用
date: 2019-12-25
tags: 
  - Node.js
  - JavaScript
categories: Node.js
description: 使用 Path 模組來取得並操作路徑
---
## 前言
由於模組化的關係，引入時必須指定路徑才能正確抓到相關檔案，這時 `Path` 模組提供了一些方法給我們使用，以下就來介紹幾種路徑使用方法吧!

## 相關範例
直接附上範例程式碼及資料夾結構
![path資料夾結構](https://i.imgur.com/WT8Vmhc.png)
``` JavaScript
var path = require('path');
// 抓目錄路徑
console.log(path.dirname('/xx/yy/zz.js')); // /xx/yy
// 路徑合併
console.log(path.join(__dirname, '/xx')); // C:\Users\gping\Downloads\nodejs_practice\node_path_demo\xx
// 抓檔名
console.log(path.basename('/xx/yy/zz.js')); // zz.js
// 抓副檔名
console.log(path.extname('/xx/yy/zz.js')); // .js
// 分析路徑
console.log(path.parse('/xx/yy/zz.js')); // { root: '/', dir: '/xx/yy', base: 'zz.js', ext: '.js', name: 'zz' }
```
執行 `node app.js` 有看到效果就成功囉!!