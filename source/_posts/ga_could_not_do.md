---
title: Google Analytics - GA分析無法做到的事
tags:
  - Analytics
  - w3HexSchool
categories:
  - Analytics
description: 來介紹一下 Google Analytics 無法分析的事
abbrlink: 3846114323
date: 2020-04-12 00:00:00
---
## GA 未提供以下功能
 * 無法永久刪除報表內資料，只能透過篩選條件來過濾資料。
 * 沒有即時通知功能
 * 無法查看使用者 IP
 * 沒有主機傳輸量統計
 * 沒有競爭分析比較

## GA 報表誤差來源
1. 客戶端環境影響
 * 防火牆或防毒的設定
 * 封鎖資訊的瀏覽器套件(AdBlock)
 * 瀏覽器 JS 功能被停用
 * GA 分析的 JS 載入速度過慢

2. 無法辨認新訪客正確度
 * 同一使用者使用不同網域進入
 * 多人共用裝置
 * 單一使用者使用多款裝置

## 結尾
本篇只著重說明 "GA 本身無法做到的事"，其他很多需求都可以透過 GA 所提供的 API 文件來達到分析功能。

## 參考連結
[https://blog.user.today/google-analytics-could-not-do/](https://blog.user.today/google-analytics-could-not-do/)


