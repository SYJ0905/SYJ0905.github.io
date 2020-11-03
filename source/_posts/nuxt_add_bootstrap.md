---
title: Nuxt 中加入 Bootstrap
date: 2019-09-16
tags: nuxt
categories: nuxt
description: 來記錄一下該如何在 Nuxt 中加入 Bootstrap
---
## 前言
與 `Vue-cli` 加入 BS 稍有不同，由於 `Nuxt` 本身是沒有所謂的 `App.vue` 當作進入點，所以會在 `nuxt.config.js` 做些設定。

## 安裝 Bootstrap 及 相依套件
在專案目錄下輸入安裝指令
```
npm install bootstrap jquery popper.js webpack -S
```
另外，還需要在開發模式安裝 `sass-loader` 、 `node-sass` ，這樣才不會報錯。
```
npm install node-sass sass-loader -D
```

## 引入 Bootstrap scss
在 `assets` 底下新建一個 `scss` 資料夾，創建一個 `all.scss` 來當作所有 `scss` 的進入點。
並且新增一個 `vendors` 資料夾專門放置第三方資源。
有時我們會需要客製化 Bootstrap ，所以我會在創一個 `_bsvariables.scss` 來放置 Bootstrap 的變數，相關做法可以參考下圖方式。
![](https://i.imgur.com/3ZCcUry.png)

## 配置 CSS 設定檔
由於前面有提到 Nuxt 本身沒有 `App.vue` 可以當作進入點，所以會直接在設定檔做引入 scss 的設定。
來到 `nuxt.config.js` 搜尋 `Global CSS` 並修改配置
```
css: [
  '@/assets/scss/all.scss'
],
```

## 引入 Bootstrap JavaScript
在 Nuxt 中將第三方 JS 放在 `plgins` 內，並在設定檔中配置。
首先來到 `plugins` 資料夾，創建 `bootstrap.js`，加入以下代碼
```
if (process.client) {
  require('bootstrap')
}
```

## 配置 plugins 設定檔
來到 `nuxt.config.js` 最上方先加入 webpack(很重要!!)
```
import webpack from 'webpack'
```
搜尋 `plugins` 將剛剛創建的 `bootstrap.js` 引入，以及在 `build` 加入設定
![](https://i.imgur.com/cqsIxlz.png)

## 測試
回到 `index.vue` 中，這次我是使用 BS 內的 modal 彈窗做測試。
由於我有使用 eslint 的關係，在 `npm run dev` 會出現錯誤 `'$' is not defined  no-undef`，
只需要在 `eslintre.js` 中關掉此項設定就能正常運作了。
![](https://i.imgur.com/DIp1J41.png)


## 結尾
按照以上步驟，應該就能夠使用 Bootstrap 的樣式以及互動功能，如果各位小夥伴有任何問題都能夠在下方留言，我會盡快回覆!!
