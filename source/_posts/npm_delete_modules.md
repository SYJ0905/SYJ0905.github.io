---
title: 刪除 node_modules
date: 2019-09-09
tags: npm
categories: npm
description: 快速刪除 node_modules 資料
---
## 前言
會想刪除 node_modules 的情況有很多種，有時單純是強迫症發作(我)，在部屬之前一定會清乾淨重裝。但總是為了刪除資料而費了不少時間，本篇就來教大家該怎麼一個指令刪除 node_modules 。

## 安裝 rimraf 刪除套件
開啟 CMD (終端機)，執行 `npm install rimraf -g`

## 一鍵刪除
使用 VSCode or CMD 到你想要刪除 node_modules 的專案內，執行以下刪除指令
```
rimraf node_modules
```

## 結尾
這才是效率嘛!!