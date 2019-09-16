---
title: Nuxt 中加入 Bootstrap
date: 2019-09-16
tags: nuxt
categories: nuxt
description: 來記錄一下該如何在 Nuxt 中加入 Bootstrap
---
## 前言
與 `Vue-cli` 加入 BS 稍有不同，由於 `Nuxt` 本身是沒有所謂的 `App.vue` 當作進入點，所以會在 `nuxt.config.js` 做些設定。

## 安裝 Bootstrap
在專案目錄下輸入安裝指令
```
npm install bootstrap -S
```
另外，還需要在開發模式安裝 `sass-loader` 、 `node-sass` ，這樣才不會報錯。
```
npm install node-sass sass-loader -D
```

## 引入 Bootstrap
在 `assets` 底下新建一個 `scss` 資料夾，創建一個 `all.scss` 來當作所有 `scss` 的進入點。
並且新增一個 `vendors` 資料夾專門放置第三方資源。
有時我們會需要客製化 Bootstrap ，所以我會在創一個 `_bsvariables.scss` 來放置 Bootstrap 的變數，相關做法可以參考下圖方式。
![](https://i.imgur.com/3ZCcUry.png)

## 配置設定檔
由於前面有提到 Nuxt 本身沒有 `App.vue` 可以當作進入點，所以會直接在設定檔做引入 scss 的設定。
來到 `nuxt.config.js` 搜尋 `Global CSS` 並修改配置
```
css: [
  '@/assets/scss/all.scss'
],
```

## 結尾
最後可以試著在 `index.vue` 檔中加入一些 Bootstrap 原件來測試，這邊使用按鈕來測試是否有正確引入。
執行 `npm run dev`，有正確顯示就代表成功囉!!
![](https://i.imgur.com/nM2AAlv.png)
