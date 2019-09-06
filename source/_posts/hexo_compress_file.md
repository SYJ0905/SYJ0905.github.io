---
title: Hexo 架站攻略 - 壓縮檔案，榨出更多效能
date: 2019-09-03
tags: Hexo
categories: Hexo
description: 效能是網站很重要的一個指標，使用者的時間都是寶貴的，那怕是 1~2 秒的等待時間都有可能關掉分頁並另外尋找其他資訊。為了讓大家願意停留在我的網站上，咱們就來壓縮吧，榨出更多的效能。
---

## 前言
效能是網站很重要的一個指標，使用者的時間都是寶貴的，那怕是 1~2 秒的等待時間都有可能關掉分頁並另外尋找其他資訊。
為了讓大家願意停留在我的網站上，咱們就來壓縮吧，榨出更多的效能。
<!-- more -->
## 安裝壓縮套件
輸入安裝指令
```
npm install hexo-neat --save
```

## 加入設定
在根目錄上的 _config.yml 加入以下程式碼
```
## hexo-neat
# 壓縮
neat_enable: true
# 壓縮HTML
neat_html:
  enable: true
  exclude:
# 壓縮CSS
neat_css:
  enable: true
  exclude:
    - '**/*.min.css'
# 壓縮JS
neat_js:
  enable: false
  mangle: true
  output:
  compress:
  exclude:
```
JS 壓縮暫時沒有做，容易出問題，等測試過後會在更新文章。
