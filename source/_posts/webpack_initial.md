---
title: webpack 架設 - 安裝 webpack
date: 2019-09-10
tags: webpack
categories: webpack
description: 一起來研究現今最火的前端打包工具吧!!
---
## 前言
webpack 是一個開源的前端打包工具。webpack 提供了前端開發缺乏的模組化開發方式，將各種靜態資源視為模組，並從它生成最佳化過的程式碼。(Wiki)
![webpack](https://i.imgur.com/5Z4PSWc.png)
## npm 初始化
首先進入專案目錄，執行 npm 初始化
```
npm init
```
## 安裝 webpack
官方文件有提到不建議在全局安裝 `webpack`，這會將你項目中的 webpack 鎖定到指定版本，並且在使用不同的 webpack 版本的項目中，可能會導致構建失敗。
在專案目錄下，採用本地安裝
```
npm install --save-dev webpack webpack-cli
```
## 配置 webpack
在專案目錄下新增 `src` 資料夾，創建一個 webpack 進入點 `main.js`，先寫個測試代碼
```
console.log('webpack test');
```
接著在根目錄新增 webpack 設定檔 `webpack.config.js`，寫個最基本的設定
```
const path = require('path');

module.exports = {
  entry: './src/main.js', // 進入點
  output: { // 輸出點
    filename: 'main.bundle.js', // 輸出的檔案
    path: path.resolve(__dirname, 'dist') // 路徑
  },
};
```
![](https://i.imgur.com/wcCuNP1.png)
設定 `package.json` 則可以使用 npm 指令來執行編譯
在 `package.json` 的 `script` 新增自定義名稱，後面帶上 `webpack`，之後輸入以下範例即可打包
```
npm run dev
```

## 引入打包後的檔案
在 `dist` 資料夾內新增一個 `index.html` 檔，並引入 webpack 打包後的檔案
![](https://i.imgur.com/jvVy0as.png)
重新開一個新的 vscode ，打開 dist 資料夾，用 web server 開啟就能在 `console` 看到 `main.js`　中寫的代碼了。
![](https://i.imgur.com/1ucYvXW.png)