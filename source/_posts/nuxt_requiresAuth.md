---
title: Nuxt 中的驗證機制 requiresAuth
date: 2019-09-23
tags: nuxt
categories: nuxt
description: 來教大家如何在 Nuxt 中設置 requiresAuth 驗證
---
## 前言
在 Vue-cli 中可以在 `router` 中直接設定 `meta.requiresAuth` ，並且在進入點 `main.js` 中撰寫驗證代碼。
而在 Nuxt 則是使用 `middleware` 當作中介點，可以照不同頁面選擇要用哪個中介點，那該如何設定 `requiresAuth` 呢?
肯定有小夥伴從 Vue-cli 轉移至 Nuxt 會有這疑問，跟著我一起來了解吧!
## 設定導航守衛
首先在 `middleware` 資料夾底下建立一個 routerAuth.js
![](https://i.imgur.com/qERUcRi.png)
接著我們需要新增一個頁面，在 `pages` 底下新增一個 `user-profile.vue` 來當作測試。
必須在需要驗證的頁面加入剛剛建的 routerAuth.js
![](https://i.imgur.com/LYP2b6e.png)

## 驗證步驟
在 `index.vue` 中新增連結，並導入到 `user-profile.vue`
![](https://i.imgur.com/hlSLdfG.png)
接著在 `index.vue` 點擊 會員中心 會來到 `/user-profile.vue` ，並且可以在 console 看到 meta 中的 `requiresAuth`
![](https://i.imgur.com/SJct4dh.png)

## 測試
到目前為止，已經可以正確拿到 `requiresAuth` 了，那麼接下來就來實作類似登入機制的步驟。
在 index.vue 有寫登入函式，使用 localstorage 存取資料。
這邊要注意的一點是，必須要加入 `process.client` 的判斷，不然會在 `/user-profile` F5 後出現 `localstorage is not defined` 等錯誤。
接下來就能夠針對頁面是否含有 `meta.requiresAuth` 來進行驗證。
![](https://i.imgur.com/pWl6r5A.png)

## 結尾
依照以上步驟，應該就能正常撰寫驗證代碼了。針對這個問題，我查過很多資料，幾乎都會寫得相當複雜，是不能寫的簡單點嗎?QQ