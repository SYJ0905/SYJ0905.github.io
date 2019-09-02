---
title: Hexo 架站攻略-主題配置
date: 2019-09-02
tags: Hexo
categories: Hexo
---

## 前言
總是要來點跟別人不一樣的，Hexo 預先會有一個預設樣式，但我相信各位小夥伴或許都不是很滿意，這邊提供一個相當多用戶所使用的主題配置 
[NexT](https://theme-next.iissnan.com/)
[NexT Github](https://github.com/theme-next/hexo-theme-next)

![NexT](https://i.imgur.com/9GsDWAo.png "NexT 官網")

## 下載主題

按照官方文件 `git clone https://github.com/iissnan/hexo-theme-next themes/next` ，此版本有可能是 5.1.4，要注意的一點是該版本並不能透過 `git pull` 來進行更新。

![下載 NexT](https://i.imgur.com/svNOt9S.png "下載 NexT")

這邊來教各位如何取得 6.0 以上的版本，首先來到 [NexT Github](https://github.com/theme-next/hexo-theme-next)，找到 `Update` 並進入 `here`

![NexT Github](https://i.imgur.com/DNZcGEX.png)

中間有一段可以直接取得 6.0 以上的版本， `git clone https://github.com/theme-next/hexo-theme-next themes/next-reloaded` ，也不知道為什麼官網沒有更新到，還特地寫了一個說明文件，真的有點奇怪。

![download updated NexT version](https://i.imgur.com/WL483Ys.png)

## 更換主題

將 clone 下來的 themes 資料夾放入 Hexo 的 themes 內

![change themes](https://i.imgur.com/NIBPCA4.png)

接著到根目錄 _config.yml 將主題更換至 NexT，注意不要跑錯地方喔!

![change themes](https://i.imgur.com/BxRV2CJ.png)

更換後重啟服務即可看到 NexT 主題囉!!
