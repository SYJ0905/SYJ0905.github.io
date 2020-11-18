---
title: Hexo 架站攻略 - 加入 Facebook 點讚與分享
tags:
  - Hexo
categories:
  - Hexo
description: 好文章就是要點讚與分享，怎麼可以少了這個功能呢?!!跟著我一起來加入 FB 的大拇指吧。
abbrlink: 2088167264
date: 2019-09-04 00:00:00
---

## 前言
好文章就是要點讚與分享，怎麼可以少了這個功能呢?!!跟著我一起來加入 FB 的大拇指吧。
<!-- more -->
## 建立 FB 應用程式
來到 FB 的開發人員模式，點選 "新增應用程式"，輸入網站名稱後即可。這邊要注意的是，FB 有時會改版畫面，但都大同小異，找到相同字樣幾乎就對啦!!
![](https://i.imgur.com/JBnCc7q.png)
![](https://i.imgur.com/3GwvhBS.png)
接著到基本設定中填寫 "網址" 後儲存，由於使用 FB 的功能會需要設定隱私權頁面，稍後會說明該如何設定
![](https://i.imgur.com/GlSv2TF.png)

## 設定 FB 隱私權政策
輸入以下建立指令
```
hexo new page 'Privacy Policy'
```
在 `source/Privacy-Policy` 中的 `index.md` 輸入以下隱私權政策內容
![](https://i.imgur.com/4gisExJ.png)

建立完頁面後回到 FB 將之前紅箭頭處所指的 `隱私權政策網址` 填入 `https://syj0905.github.io/Privacy-Policy`，前面記得改成自己的網站喔!!
![](https://i.imgur.com/9yzawFD.png)
輸入完成後開啟上方的服務即可

## 設置 FB 留言板
開啟 `主題配置文件` _config.yml 搜尋 `Facebook SDK Support`，修改設定檔配置，應用程式編號在 FB 控制台可以看到，貼上它吧。
![](https://i.imgur.com/f5vReIp.png)