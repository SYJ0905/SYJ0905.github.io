---
title: Hexo 架站攻略 - 加入 RSS 通知
date: 2019-09-05
tags: Hexo
categories: Hexo
description: 讓訂閱者第一時間收到通知吧!!
---
## 前言
RSS（簡易資訊聚合）是一種訊息來源格式規範，用以聚合經常發布更新資料的網站。訂閱 RSS 意味著當網站更新時，方便用戶獲取最新內容，可以時時關注最新文章。
<!-- more -->
## 安裝套件
參考來源: [hexo-generator-feed](https://github.com/hexojs/hexo-generator-feed)
輸入以下安裝指令
```
npm install hexo-generator-feed --save
```
## 設定 RSS 配置
到站點 _config.yml 中，加入以下範例
```
feed:
  type: atom
  path: atom.xml
  limit: 20
  hub:
  content:
  content_limit: 140
  content_limit_delim: ' '
  order_by: -date
  icon: icon.png
```
重啟服務後就能看到 RSS 圖像囉!!