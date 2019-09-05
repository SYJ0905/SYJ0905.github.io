---
title: Hexo 架站攻略 - 加入 GA 及 Sitemap
date: 2019-09-05
tags: Hexo
categories: Hexo
---

## 前言
寫技術部落格不光是記錄自己的開發過程，也希望能讓其他開發者在踩坑時能夠幫助到他們，畢竟我到目前為止都還是會看其他人的踩坑紀錄和文章。在這個前端大坑裡，有太多東西要學了，總是希望有人能稍微提點一下，於是能讓爬蟲抓到，以便其他人搜尋時能更快找到解答。
<!-- more -->
## 加入 GA 追蹤碼
這部分網路上有很多教學，最後我們會得到一組 GA 追蹤碼
EX: `UA-XXXXXX-1`
來到主題配置 _config.yml 搜尋 `Google Analytics`，依據個人 GA 修改
```
google_analytics:
  tracking_id: UA-XXXXXX-1
  localhost_ignored: true
```

## 加入 Sitemap
首先要安裝插件
```
npm install hexo-generator-sitemap
```
到 [Google Search](https://search.google.com/search-console/about?hl=zh-tw)加入我們網站，並取得驗證碼
在主題配置 _config.yml 搜尋 `Google Webmaster`
```
# Google Webmaster tools verification.
See: https://www.google.com/webmasters
google_site_verification: // 驗證碼
```