---
title: Webpack 架設 - 安裝 Webpack
date: 2019-09-10
tags: Webpack
categories: Webpack
description: 一起來研究現今最火的前端打包工具吧!!
---
## 前言
Webpack 是一個開源的前端打包工具。Webpack 提供了前端開發缺乏的模組化開發方式，將各種靜態資源視為模組，並從它生成最佳化過的程式碼。(Wiki)
![Webpack](https://i.imgur.com/5Z4PSWc.png)
## npm 初始化
首先進入專案目錄，執行 npm 初始化
```
npm init
```
## 安裝 Webpack
官方文件有提到不建議在全局安裝 `Webpack`，這會將你項目中的 webpack 鎖定到指定版本，並且在使用不同的 webpack 版本的項目中，可能會導致構建失敗。
在專案目錄下，採用本地安裝
```
npm install --save-dev webpack webpack-cli
```