---
title: Hexo 架站攻略-建立與部署
date: 2019-09-01
tags: Hexo
categories: Hexo
---

## 前言

為了避免其他架站教學的文章遺失，乾脆就自己架站紀錄一下，順便來跟各位小夥伴說明會遇到那些意想不到的坑喔!!

![Hexo](https://i.imgur.com/SmnCmdV.png "Hexo 官網")

## 建立 Github Repo

![建立 Github Repo](https://i.imgur.com/zEkAKDf.png "建立 Github Repo")

Repository name 必須依照以下格式輸入:

```
帳戶名稱.github.io
```

## 安裝 Hexo

依照官網安裝方式，開啟 CMD 輸入安裝指令

```
npm install hexo-cli -g
```

## 建立 Hexo 資料夾環境

請先到想要建立資料夾的目錄，並輸入建立指令

```
hexo init projectname
```

註: projectname 若已在資料夾內可不用加

接著，安裝 npm 相依套件，輸入以下指令

```
npm install
```

## 運行 Hexo

安裝套件後，來運行你的第一個部落格吧!!

```
hexo s
```

註: hexo s => hexo server 簡寫

## Hexo 基本設定

在 _config.yml 找到 `Site`，並設定您的內容
```
# Site
title: 小克的前端技術 Blog # 網站標題
subtitle: Cloud's Blog - 前端無底洞，一起來挖洞 # 網站副標題
description: Cloud's Blog - 前端無底洞，一起來挖洞 # 網站敘述
keywords: # 關鍵字
author: Cloud Su # 網站作者
language: zh-TW # 網站語系
timezone:

# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: https://syj0905.github.io # 網址
root: /
permalink: :category/:year:month:day/:title/
permalink_defaults:
```

## 加入版控，所有操作皆在 dev 環境

撰寫文章時使用 dev 分支，會有指令直接部屬到 master ，此時遠端資料庫的 master 資料夾結構會變。
此做法是為了在兩地(家裡、公司)，皆能寫部落格的方法。
如果只在 master 撰寫文章並部屬後，在另一地 `git  clone` 時，會發生沒有 Hexo 的原始碼，因為遠端 master 只會存在部屬的結構。
此舉相當重要!!

在部落格資料夾路徑內開啟 git bash，依照以下方法加入版控

```
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/SYJ0905/SYJ0905.github.io.git
git push -u origin master
```

接下來開啟分支吧!!

```
git branch dev
git checkout dev
git push origin dev (先推送一次版本)
```

## 部屬 GitHub

這裡必須先安裝部屬套件，Hexo本身不會預設呦(人家哪知道你要部屬 Github 啦!!)

`npm install hexo-deployer-git --save`

此外，設定檔 _config.yml 內也需要設定

```
deploy:
  type: git
  repo: https://github.com/SYJ0905/SYJ0905.github.io.git
  branch: master
```

可以部屬囉!!

`hexo d g`

註: d g => 部屬靜態頁面(不要寫反了!!)

### 其他指令

`hexo clean`

註: 刪除已生成的靜態頁面及快取檔案

## 結尾

現在應該就能在 Github 專屬的網址上看到部落格囉!!接下來會開始針對部落格進行優化跟主題配置，有興趣的小夥伴還請多多關注，我將帶著大家一起踩雷!!