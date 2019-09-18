---
title: Nuxt 中加入 axios
date: 2019-09-18
tags: nuxt
categories: nuxt
description: 如何在 Nuxt 中加入 Axios
---
## 前言
串接資料從最早的 XHR 到 jQuery 的 `$.ajax()` 在到現在最火的 axios，不外乎都是為了更有效的解決開發問題，今天就帶著大家在 Nuxt 中加入 Axios 吧!

## 安裝套件
在專案目錄下輸入安裝指令
```
npm install axios vue-axios -S
```
在 `plugins` 資料夾新增 `axios.js` 檔案，加入以下程式碼
```
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'

Vue.use(VueAxios, axios)
```
## 配置設定檔
來到 `nuxt.config.js` 搜尋 `plugins` 將 `axios.js` 加入配置
![](https://i.imgur.com/IMEbu6Q.png)

## 測試
在 `index.vue` 當中來取得資料，參考以下範例
[RandomAPI](https://randomuser.me)
![](https://i.imgur.com/XNfWLMo.png)
執行 `npm run dev` ，查看 console 是否有正確拿到資料
![](https://i.imgur.com/aa7wNZ0.png)

## 結尾
看到有資料是不是很興奮呢!!趕快在 Nuxt 加入 Axios 吧!!