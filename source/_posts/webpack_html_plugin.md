---
title: webpack 架設 - 自動生成 html
tags:
  - Webpack
categories:
  - Webpack
description: 在 webpack 加入自動生成 html 的插件
abbrlink: 3044919679
date: 2019-09-10 00:00:00
---
## 前言
在前一篇文章中，我們是手動新增 `index.html` 檔在 `dist` 資料夾內，確實是很不方便。本次的插件為 `html-webpack-plugin`，可以在打包後自動生成 html 檔。
## 安裝插件
在專案內輸入安裝指令
[html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin)
```
npm i --save-dev html-webpack-plugin
```
在 `webpack.config.js` 引入 `html-webpack-plugin`模塊，並在 `plugins` 加入，可參考下圖方式
![](https://i.imgur.com/imuY4p6.png)
`index.html` 的 head 相關設定可以參考官方文件，並直接在 plugin 內設定

## 開始編譯
手動把 dist 資料夾清空，執行 `npm run dev`，這時會自動生成 html 也會帶入相關設定。
這邊要注意的一點是，請不要把 dist 資料夾也刪除了，後續會教大家如何自動生成 dist 資料夾!!
![](https://i.imgur.com/isfVvRn.png)