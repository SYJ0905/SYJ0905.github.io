---
title: Hexo 架站攻略-NexT 相關設定
date: 2019-09-02
tags: Hexo
categories: Hexo
---

## 前言
NexT 提供很多設定可以讓每位使用者依據個人喜好來做修改，建立專屬於你的個人配置。本身有點強迫症的我來說，文章必須要井然有序的分類整齊，而不單單只是紀錄而已，畢竟之後開發時如果忘記一些資訊也比較好找。
有關 NexT 的設置均在 themes 中的 `_config.yml` 來做修改，而不是在跟目錄的 `_config.yml` 喔!!

## 選擇 Scheme
![選擇 Scheme](https://i.imgur.com/omz7nSs.png "選擇 Scheme")
* Muse - 默認Scheme
* Mist - Muse 的緊湊版本
* Pisces - 雙欄Scheme
* Gemini - 雙欄Scheme(跟 Pisces 好像一樣 ??)

## 選單分類
在 _config.yml 搜尋 `Menu Settings` 即可找到
![選單分類](https://i.imgur.com/9ZUfXUm.png "選單分類")
依據個人喜好選擇即可
另外，在 source 底下要根據你的設定新增資料夾與頁面
```
hexo new page tags
hexo new page categories
```
![設定](https://i.imgur.com/G6xrCDr.png)

## 側欄設定

### 修改選單位置
在 _config.yml 搜尋 `Sidebar Position` ，將位置更改為左或右(你爽就好)

### 修改頭像
在 _config.yml 搜尋 `avatar`，可參考以下範例
```
avatar:
  url: /images/avatar.png
  rounded: true
  opacity: 1
  rotated: false
```
至於頭像檔案可以放在 themes 底下的 source `img` 資料夾內

![修改頭像](https://i.imgur.com/QzI3bCh.png "修改頭像")

### 修改滾動效果
在 _config.yml 搜尋 `scrollpercent` ，並將 `scrollpercent: false` 改為 `scrollpercent: true`，可以看到滾動時的百分比呦!!

### 社群連結
在 _config.yml 搜尋 `Social Links`，可以看到很多社群連結的設定
![社群連結](https://i.imgur.com/7HhII0s.png "社群連結")
想顯示哪個就取消註解並更改連結就能使用了。

## 版權設置
在 _config.yml 搜尋 `copyright`，不輸入則顯示網站作者名稱
其他有 Hexo 預設的字也能清除，可參考底下圖片及紅箭頭處
![版權設置](https://i.imgur.com/k9MhWH2.png "版權設置")
版權文字前有個小圖示，可以增加動畫效果，須將 `animated` 改為 `true` ，但不是很明顯，斟酌使用。

## 美化效果

### 程式碼區塊
在 _config.yml 搜尋 `codeblock`，可調整樣式
![程式碼區塊](https://i.imgur.com/B4Sr5Dm.png "程式碼區塊")

### Github follow me 右上角圖示
在 _config.yml 搜尋 `github_banner`，照以下範例即可享有右上角圖示
```
github_banner:
  enable: true
  permalink: https://github.com/SYJ0905
  title: Follow me on GitHub
```

### 頁面切換時動畫
在 _config.yml 搜尋 `motion`
![loading動畫](https://i.imgur.com/iUDYoaz.png "loading動畫")
有很多效果可以套用，任君挑選!!

### lightbox 效果
直接照著官方文件就可以運行起來了，工程師不要連英文都懶得看喔~~
[theme-next-fancybox3](https://github.com/theme-next/theme-next-fancybox3)
![](https://i.imgur.com/oidfcis.png)

### 背景效果
效果有分 "粒子" 與 "3D" 兩種，我來教大家怎麼找這些資源，首先來到 _config.yml ， 接著搜尋 `Animation Settings`，這部分以下都是插件，並且都有附網址可直接參照文件來進行配置。
![](https://i.imgur.com/GG8hYGA.png)

## 進度條效果
直接照著官方文件就可以運行起來了。
[theme-next-pace](https://github.com/theme-next/theme-next-pace)
![](https://i.imgur.com/so2TEoY.png)

## 增加留言板
先到 [Disqus](https://disqus.com) 點選 GET STARTED
![Disqus](https://i.imgur.com/z147laC.png)
選擇  I want to install Disqus on my site
![](https://i.imgur.com/CfAtRjw.png)
創建一個 new site
* Websit Name 是自訂名稱(不要填寫部落格網址)，位置會在下圖紅箭頭處
![](https://i.imgur.com/mU0KmVq.png)
接下來到右上角的控制台選擇 `Settings`，進畫面後再次到右上角齒輪選擇 `Admin`，點選紅色箭頭處的連結
![](https://i.imgur.com/cAAeIEI.png)
點擊右方 `Edit Setting`
![](https://i.imgur.com/6kDruMS.png)
會看到你剛剛所建立的 `short name`
![](https://i.imgur.com/Ugj7UPe.png)
在 themes 的 _config.yml 中搜尋 `Disqus`，修改相關設定
```
disqus:
  enable: true
  shortname: clouds-blog // 填入您專屬的 short name
  count: true
  lazyload: false
  #post_meta_order: 0
```
我也不知道為什麼我的會多一個 s 在那邊 = = 

## 結尾
Hexo 跟 NexT 有很多有趣的設定跟各式各樣的插件可以玩，本篇文章在後續也會繼續更新，目前寫的配置跟我的網站配置是一樣的，所以各位小夥伴如果還不知道怎麼配置，不仿先看看整個網頁是不是你喜歡的，如果是就一步一步照著做吧!!