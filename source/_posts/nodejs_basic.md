---
title: Node.js - 基礎介紹
date: 2019-12-25
tags: 
  - Node.js
  - JavaScript
categories: Node.js
description: 介紹 Node.js 基礎
---
## Node.js 是什麼 ?
[Node.js wiki](https://zh.wikipedia.org/wiki/Node.js)
Node.js 是一個能在後端也使用 JavaScript 撰寫的開放原始碼，以往 JavaScript 主要負責前端程式的執行，而後端則使用 C#、PHP、Python等語言。
Node.js 的出現，讓前端得以使用 JavaScript 撰寫後端程式，並且使用 Node.js 內建模組開啟獨立伺服器，從而擺脫 Apache HTTP Server 或 IIS。

## V8 引擎
由 Google 所推出的 JavaScript 引擎，優勢就是快、快、還要更快。
[V8 引擎](https://zh.wikipedia.org/wiki/V8_(JavaScript%E5%BC%95%E6%93%8E))

## 優勢在哪?
* 採用 v8 引擎編譯
* 脫離 Apache HTTP Server 或 IIS
* 開放原始碼
* 有多款框架可以選擇(Express.js、Koa.js)

## 環境配置
到官網下載(選擇 LTS 版本)並安裝 Node.js
[Node.js](https://nodejs.org/en/)
安裝後在 `終端機` or `CMD` 查看版本號，有顯示的話就代表安裝成功囉!
```
node -v
```

## Node.js 起手式
首先創建一個資料夾，新建一支 `all.js` 寫個測試代碼
```
console.log('測試');
```
接下來打開 `CMD`，移到資料夾路徑並執行 `node all.js`，如果有看到 `測試` 就代表成功執行囉!