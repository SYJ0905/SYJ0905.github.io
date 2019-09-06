---
title: Hexo 架站攻略 - NexT 分類與標籤頁不要有留言板
date: 2019-09-03
tags: Hexo
categories: Hexo
description: 標籤頁跟分類頁好像多了一些奇怪的東西呦
---

## 前言
來看看底下這張圖有沒有覺得哪裡奇怪了??
<!-- more -->
![](https://i.imgur.com/j6wj8bq.png)
有看出來不?沒錯，就是標籤頁多出了留言板，不只如此，在分類頁也有狀況，本篇就來解決這個問題。

## 修改模板
會出現留言板代表與文章內頁是套用同一個模板，所以就來找一下到底是用了哪一個模板，並加入判斷式來決定到底要不要出現留言板就行了。
首先來到 themes/layout/_layout.swig，搜尋 `comments.swig` 依照下圖紅箭頭處加入判斷式
![](https://i.imgur.com/CkhMfCH.png)
最後重啟服務就能看到標籤頁與分類頁已經沒有留言板囉!!

