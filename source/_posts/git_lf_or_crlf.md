---
title: Git 多平台換行符問題
tags:
  - Git
categories:
  - Git
description: 到底該用 LF 還是 CRLF 呢?
abbrlink: 4060533944
date: 2019-09-09 00:00:00
---

## 前言
目前開發者使用的作業系統大多分為兩類，Mac 以及 Windows 。
前者是使用 LF 當作換行符，後者使用的是 CRLF，這兩者差異這邊就不多說明。
在 Github 上做版本控管時，都是採用 LF 在紀錄的，此時 Windows 用戶就必須調整成 LF 格式才行提交，`git` 有提供相關配置制來解決這問題。

## 配置指令
可參考以下配置命令，在 git bash 環境執行就行
```
# 提交時轉換為 LF，檢出時轉換為CRLF
git config --global core.autocrlf true

# 提交時轉換為 LF，檢出時不转换
git config --global core.autocrlf input

# 提交檢出均不轉換
git config --global core.autocrlf false
```
調整 `autocrlf` 後，也要再調整 `safecrlf` 設定
```
# 拒絕提交包含混合换行符的文件
git config --global core.safecrlf true

# 允許提交包含混合換行符的文件
git config --global core.safecrlf false

# 提交包含混合換行符的文件時给出警告
git config --global core.safecrlf warn
```

## 多平台配置(推薦)
目前我也是使用以下配置:
```
git config --global core.autocrlf input
git config --global core.safecrlf true
```
說明: 此配置在代碼中若有 CRLF 文件將無法提交，可使用 `dos2unix` 方法來完成，若文件都為 LF 格式則可以提交，在檢出時也都會是 LF 格式