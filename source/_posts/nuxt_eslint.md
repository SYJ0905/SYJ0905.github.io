---
title: Nuxt 中加入 ESLint
tags:
  - Vue
categories:
  - Vue
description: 團隊協作代碼規範必備工具 ESLint，本篇將說明如何正確安裝 ESLint 於 Nuxt
abbrlink: 410090658
date: 2019-09-19 00:00:00
---
## 前言
使用 ESLint 來讓我們代碼具有一致姓，看了就是舒服，維護起來沒煩惱!!

## 安裝套件
本篇將使用 ESLint 中的 `airbnb` 規範，先附上官網連結
[eslint-config-airbnb](https://github.com/airbnb/javascript/tree/master/packages/eslint-config-airbnb)
首先到 airbnb 的 github 找到安裝指令，但請別急著安裝，由於我們是使用 Nuxt 而不是 React ，所以這邊要點擊紅色箭頭處
![ESLint](https://i.imgur.com/k4C6Haw.png)
來到 npm eslint-config-airbnb-base 網站，一般來說現在安裝 node.js 本身就會是 npm 5+ 的環境了，所以安裝指令就是輸入紅色箭頭處即可
![eslint-config-airbnb-base](https://i.imgur.com/a7mGViT.png)

## 配置設定檔
到 `.eslintrc.js` 檔案，在 `extends` 加入 `airbnb-base` 。
除此之外，還需要加入以下設定
```
settings: {
  'import/core-modules': ['vue', 'vuex'] // these modules are included in nuxt.js
}
```
![](https://i.imgur.com/EOxZoXx.png)

## 測試
這邊提供 VSCODE 設定檔，這樣就可以在文件儲存之後直接修正 ESLint 錯誤
```
"eslint.validate": [
  "javascript",
  "javascriptreact",
  {
    "language": "vue",
    "autoFix": true
  },
],
"eslint.autoFixOnSave": true,
"vetur.validation.template": false,
```
註:  VSCODE 套件要先安裝 `ESLint`、`vue`、`Vetur` 避免出錯。