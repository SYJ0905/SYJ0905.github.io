---
title: npm - 緩存指令
date: 2019-09-09
tags: npm
categories: npm
description: 編譯時出錯了嗎? 可能是你的緩存沒清呢!!
---

## 前言
有時當專案在切換時，重新啟動 `npm run dev` or `npm run serve` 時會出現一些錯誤，第一時間點我會先來清除緩存來解決，不行的話那就繼續看是不是哪邊又出現問題，不過大多都是緩存沒清呢!!

## NPM 緩存命令
先來看看一般情況下 npm 的相關路徑
`C:\Users\使用者\AppData\Roaming\npm` => 這裡會放全域安裝的套件
`C:\Users\gping\AppData\Roaming\npm-cache` => npm 快取資訊，待會要清除的資料
開啟 CMD 終端機，輸入清除緩存指令
`npm cache verify` 
接下來，重新編譯你的專案吧!!