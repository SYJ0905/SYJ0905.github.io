---
title: Hexo 架站攻略 - 加入搜尋功能
date: 2019-09-05
tags: Hexo
categories: Hexo
---
## 前言
平常找資源時都會下關鍵字找資料，當然在部落格也希望能夠快速地找到符合自己需求的文章，正所謂時間就是金錢，跟著以下操作為部落格加入搜尋功能吧!!

## 安裝搜尋套件
NexT 有提供本身的搜尋功能，輸入以下指令即可
[hexo-generator-searchdb](https://github.com/theme-next/hexo-generator-searchdb)
```
npm install hexo-generator-searchdb --save
```
進到站點(根目錄)下的 _config.yml 複製以下搜尋功能代碼
```
# 搜尋功能
search:
  path: search.json
  field: post
  format: html
  limit: 10000
```
相關參數可參考官方 Github 說明

## 開啟搜尋功能
在主題配置 _config.yml 中搜尋 `Local Search`，將底下的 `enable` 修改為 `true`，重啟服務後就可以看到搜尋功能囉!!