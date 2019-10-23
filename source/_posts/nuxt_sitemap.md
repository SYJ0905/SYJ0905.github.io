---
title: Nuxt 加入 sitemap
date: 2019-10-23
tags: 
  - nuxt
  - seo
categories: nuxt
description: 為了讓搜尋引擎能更有效爬蟲，快來加入 sitemap 吧!!
---
## 前言
前言越來越難寫了，直接附上 wiki 連結比較快XD
[seo](https://zh.wikipedia.org/wiki/%E6%90%9C%E5%B0%8B%E5%BC%95%E6%93%8E%E6%9C%80%E4%BD%B3%E5%8C%96) 

## 安裝套件
[@nuxtjs/sitemap](https://github.com/nuxt-community/sitemap-module)
[@nuxtjs/sitemap npm](https://www.npmjs.com/package/@nuxtjs/sitemap)
```
npm install @nuxtjs/sitemap
```
## 配置設定檔
首先在 `modules` 加入套件
```
// nuxt.config.js
{
  modules: [
    '@nuxtjs/sitemap'
  ],
  sitemap: {
    // custom configuration
  }
}
```
設定非動態的 sitemap ，正常來說是可以不用寫得，套件會自己將靜態頁面加入 sitemap ， 但會少一些屬性設定(日期、網址)
![nuxt config](https://i.imgur.com/eN6Dz4K.png)
加入後執行 `npm run dev` 將網址改成 `http://localhost:3000/sitemap.xml` ，前面的 port 如果不是 3000 記得要換成自己的呦!!
這時應該就會出現下圖了
![sitemap](https://i.imgur.com/Fc6upVl.png)

## 加入動態 sitemap
如果有些頁面的路由會有產品編號時，就需要設置動態 sitemap ，畢竟你不可能一筆一筆加入。
比如以下範例:
`https://www.xxx.com.tw/xxx/productdetail/A0801-010`
後面的 A0801-010 就是產品編號
那麼接下來就教大家如何動態加入 sitemap 吧。
註: 要先安裝 axios 套件
請參照以下圖片範例
![dynamic sitemap](https://i.imgur.com/dZRw7xY.png)
分成幾步驟來說明:
1. `nuxt.config.js` 最上方要先加入 `import axios from 'axios';`
2. routes 改成 function 形式
3. axios.all 搭配 axios.spread 處理多筆同步請求
4. 第一筆 api 的回傳會是 userList， 有多筆的話 api 就往下加，而 userList 後面繼續加回傳參數，記得要逗號喔!!
5. data.xxx 這個 xxx 請使用唯一值，類似產品 id 這樣，因為這就等於有這一頁面。
6. 針對每筆 sitemap 加入網址、日期等屬性
7. indexRoutes 將所有資料整合起來

最後，在執行 npm run dev 後，開啟 `http://localhost:3000/sitemap.xml`，如果有成功看到以下圖片就代表成功囉!!
![dynamic sitemap](https://i.imgur.com/ylnNKH3.png)