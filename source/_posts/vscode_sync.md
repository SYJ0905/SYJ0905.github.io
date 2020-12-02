---
title: Visual Studio Code 同步設定
tags:
  - VSCode
categories:
  - VSCode
description: 本篇介紹如何將 vscode 的設定檔上傳至 github gist，並在多個裝置中同步設定
abbrlink: 3486532201
date: 2020-12-03 00:00:00
---

## 介紹 Settings Sync

`Settings Sync` 主要有以下功能:

* 藉由 `Github` 帳號及 `Gist` 做為設定檔的儲存與下載使用。
* 可以將設定檔分享給其他人使用
* 有快捷鍵可以進行上傳及下載設定檔

`Settings Sync` 同步哪些設定:

* Settings File
* Keybinding File
* Launch File
* Snippets Folder
* VSCode Extensions & Extensions Configurations
* Workspaces Folder

## 建立 Github access token

步驟: Github > Settings > `Develop Settings` > Personal access token > `Generate New Token`
在 Token description 輸入設定檔敘述記憶，而在 scope 只需將 gist 打勾就好。
![Generate New Token](https://i.imgur.com/84jAjNy.png)
建立會有一組 Personal access tokens，將其記錄下，離開此頁面後是無查詢的。
![Personal access tokens](https://i.imgur.com/A3Inw8N.png)

## 上傳設定檔

首先請在 vscode 安裝 Settings Sync 套件，先按下 `Shift + Alt + U`，這裡會有兩種狀況:

1. 在有 .git 檔中已經有綁定 github 帳號，這樣就不用輸入 `Personal access tokens`，會自動抓到該帳號並上傳設定

2. 若沒有 .git 檔，則是會要求輸入 `Personal access tokens` 作為綁定帳號請求。

完成後右下角會出現通知
![Gist ID](https://i.imgur.com/UOfGIxr.png)

## 檢查 Gist

會到 github git 查看剛剛是否有正確上傳設定
![Gist ID](https://i.imgur.com/M3EqZMH.png)
點進 cloudSettings 會發現網址格式為
`https://gist.github.com/{YourAccount}/{Gist ID}`
而在其他裝置要同步的話，就必須要 `Gist ID` 即可

## 下載設定檔

到另一台電腦安裝 Settings Sync 並輸入 `Shift + Alt + D`，會要求輸入 `Gist ID`，但在此之前一樣會遇到兩個問題

1. 在有 .git 檔中已經有綁定 github 帳號，這樣就不用輸入 `Personal access tokens`，會自動下載設定。

2. 若沒有 .git 檔，則是會要求輸入 `Personal access tokens` 作為綁定帳號請求，假設剛剛沒記起來的話，這裡會有點麻煩哩。

如此一來，就完成兩台裝置都有共同的 Visual Studio Code 設定檔。

## 參考資料

[讓你的 Visual Studio Code 同步設定](https://medium.com/@kodofish/%E8%AE%93%E4%BD%A0%E7%9A%84-visual-studio-code-%E5%90%8C%E6%AD%A5%E8%A8%AD%E5%AE%9A-4c5fe6a4d882)
[vscode同步插件 sync](https://blog.csdn.net/weixin_42060896/article/details/105007965)
