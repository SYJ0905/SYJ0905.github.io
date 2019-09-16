---
title: 建立 Nuxt 專案
date: 2019-09-16
tags: nuxt
categories: nuxt
description: 當 SPA 需要有 SEO 時， Nuxt 是你的好選擇!!
---
## 前言
原先使用 Vue-cli 開發的 SPA 網站會因為內容都是由 JS 動態生成，所以對於爬蟲、搜尋引擎而言都是找不到資料的。就如下圖所見，連個 `title` 都不會有，是要怎麼讓搜尋引擎爬呢?
而 Nuxt 可以想像成在 SPA 渲染頁面前先在 Web 伺服器產生內容，最後在一併渲染，這樣就能夠讓爬蟲找到我們的網站囉!!
![SPA](https://i.imgur.com/FE9aQT7.png)

## 安裝 Nuxt
首先到專案資料夾目錄下，輸入安裝指令
[Nuxt](https://zh.nuxtjs.org/guide/installation)
```
npx create-nuxt-app
```
安裝過程中有提供多種 UI 框架，可依自己喜好選擇，本身習慣自己引入 BS ，這裡就選 `None`
![UI](https://i.imgur.com/RqFrO0u.png)
之後會問你要不要選擇伺服器，一樣選 `None` 預設的就可以了。
![Server](https://i.imgur.com/vZ9VhvM.png)
最後幾個會問要不要加入 `modules` 、 `linting` 、 `test` 以及最重要的 `mode`，直接附上我的配置
![](https://i.imgur.com/DMOZGMm.png)

## 執行 Nuxt 
安裝完成後輸入
```
npm run dev
```
預設是 `localhost:3000`，有看到 Nuxt 開啟的話代表已經建立成功囉!!
![Nuxt](https://i.imgur.com/s1bEesk.png)
這時我們在開啟 `檢視原始碼` 會看到與最上方第一張圖的 `檢視原始碼` 不太一樣，多了一些 SEO 的配置，像是 `title` 、 `description` 等等，後續會教各位小夥伴如何設定這些 `meta` 值。
![](https://i.imgur.com/5jvRn7K.png)

## 結尾
其實在 SPA 開發後會需要 SEO 這點會顯得有些矛盾，為什麼這樣說哩?
SPA 適合運用在大型的網站應用程式，而應用程式是不會在意 SEO 的，著重的是效能與使用者體驗。
而 SEO 其實是很深的議題，但卻有很大的誤解，對於行銷層面來說，是必須先有流量才會關注 SEO ，而不是花大筆成本規劃 SEO 卻沒有流量。
註: 花大成本 => 上頭說要加 SEO ，卻搞死工程師!! 成本其實是來自於工程師，對上面來說不就是一句話而已Orz