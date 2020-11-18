---
title: fatal unable to access XXX The requested URL returned error 403
tags:
  - Git
categories:
  - Git
description: 同一台電腦在 push 不同遠端資料庫時出現的問題，Git 經典問題，來記錄一下該如何解決。
abbrlink: 4277318126
date: 2019-09-09 00:00:00
---

## 前言
以下先說明一下情境:
Cloud 在公司第一天，就直接登入公司的 Github 並 clone 下一份專案，開啟分支進行他的第一份任務。完成後 push 上遠端也沒什麼問題。隔天，Cloud 想要紀錄一下昨天開發時遇到的問題，就登入自己的 Github clone 自己的部落格資料夾，一樣開始撰寫文章，等到要 push 上遠端時，git 出現了以下情形:
```
remote: Permission to SYJ0905/SYJ0905.github.io.git denied to XXX.
fatal: unable to access 'https://github.com/SYJ0905/SYJ0905.github.io.git/': The requested URL returned error: 403
```
究竟為什麼會發生無法上傳的問題呢?

## 找出問題
會發生第二個專案無法 push 是因為目前的使用者已經綁定了第一個專案的 repo，導致對應的 repo 對不上。這裡提供兩個解決方法
### 第一個 : 調整設定檔
進到專案料夾找尋 `.git` 檔，這需要開啟 "顯示隱藏的項目" 設定才會看到
![](https://i.imgur.com/rpO1WYl.png)
進到 `.git` 中打開 `config` 檔案，加入以下範例
```
[remote "origin"]
	url = https://github帳號:github密碼@github.com/xxx/xxx.git
	fetch = +refs/heads/*:refs/remotes/origin/*
```
修改完後就可以安心的 push 啦!!
### 第二個 : 調整 Windows 設定
搜尋 `Windows 認證` ，找到 github 相關資訊，編輯 github 帳號密碼後重新 push 即可。
![Windows 認證](https://i.imgur.com/El9VyEd.png)
![](https://i.imgur.com/GJJ8pzh.png)

### 結論
這方法也不算很完美，真正應該是用 SSH 的方法才對，但 ssh 在 Windows 上的路徑一直都很奇怪，網上的資源教學照著做了根本連第一步都無法達成，簡直是太難搞了!!
於是，找了很久才找到這兩種方法，真是一個屎坑啊QQ

## 參考文章
[解決多用戶時git push失敗，Permission denied返回403的問題](https://www.jianshu.com/p/93b8f3a794a0)
[Welcome.Web.World](https://hsiangfeng.github.io/git/20190614/391412804/)