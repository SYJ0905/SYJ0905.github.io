---
title: Vue - 部屬至 Google App Engine
date: 2020-04-19
tags:
  - Vue
  - w3HexSchool
categories: Vue
description: 本篇將介紹如何把 Vue Cli 打包後的專案部屬至 GAE(Google App Engine)
---
## 前言
請先建立好 `Google Cloud Platform` 服務，再開始以下內容。
## 資料夾結構配置
全部放在根目錄底下就對了。
```
-public
-src
-package.json
-app.yaml
-app.js
```
## 設定檔建置
由於 `Vue Cli` 在最後的 `build` 會產生 `index.html` 以及其他靜態資源，而部署到雲端主機時，必須讓雲端主機去執行這份打包檔案。所以，我們就必須在寫一份 `app.js` 腳本來跑這份靜態資源。
請參考以下範例:
``` JavaScript
const fs = require('fs');
const path = require('path');
const express = require('express');

const app = express();

app.use(express.static(path.resolve(__dirname, './dist')));
app.get('*', (req, res) => {
  const html = fs.readFileSync(path.resolve(__dirname, './dist/index.html'), 'utf-8');
  res.send(html);
});

app.listen(process.env.PORT || 9000);
```

## Google Cloud 設定檔建置
首先會建立一份 `app.yaml` 檔案，這是在部署時 `GAE` 所需要參考的設定，可以分為標準及彈性，標準設定會由 `GAE` 決定資源配置;若是彈性設定，則可以完全客製化資源(ex:`vcpu`、`記憶體`、`硬碟大小`等等)。
標準設定可以直接參考官方文件，以下連結
[app.yaml標準設定](https://cloud.google.com/appengine/docs/standard/nodejs/config/appref)
那麼就是彈性設定的寫法哩，請參考以下範例:
``` yaml
runtime: nodejs
env: flex

manual_scaling:
  instances: 1
resources:
  cpu: 1
  memory_gb: 1
  disk_size_gb: 10

handlers:
  # Serve all static files with urls ending with a file extension
- url: /(.*\..+)$ 
  static_files: dist/\1
  upload: dist/(.*\..+)$
  # catch all handler to index.html
- url: /.*
  static_files: dist/index.html
  upload: dist/index.html

env_variables:
  HOST: '0.0.0.0'
  NODE_ENV: 'production'
  VUE_APP_API_PATH: https://xxx.xxx.net
```
* resources: 可以調整主機資源，可以部署不同資源的版本，當流量過大時即可在 `GAE` 後台直接切換版本，馬上做出應對。
* runtime: 此處寫法與標準設定不同，請注意。
* env: 彈性設定必須寫 flex。
* env_variables: 若有相關變數必須在此設定。

## package.json 設定
將專案的 package.jsonㄊ調整成以下範例，
必須要寫 `npm run start` 的指令，因為這是 GAE 部署時會執行的，而指定的腳本就是剛剛寫的 `app.js`。
``` JSON
{
  "name": "demo",
  "version": "0.1.0",
  "private": true,
  "engines": {
    "node": ">=10.0.0"
  },
  "scripts": {
    "serve": "vue-cli-service serve",
    "build": "vue-cli-service build",
    "start": "node ./app.js",
  },
}
```
## 部署 GAE
這邊首先要安裝 `Google Cloud SDK`，這其實就類似 `CMD`，讓我們可以輸入部署指令用的。
完成後執行程式，並開始以下部署步驟:
1. 移到專案資料夾
```
cd 專案資料夾路徑
```
2. 初始化 `GAE`
```
gcloud init
```
此時會詢問一些問題，像是要用哪個帳號、連接的伺服器地區(台灣、香港)，最後是要部署到哪一份專案的 `app engine`。
3. 執行部署指令
```
gcloud app deploy app.yaml
```
輸入後有可能會出現 `python` 的錯誤代碼，不過沒關係，繼續讓他跑程式，若是沒有出現 `ERROR` 等字樣，並且完成所有程序，就代表已經部署至 `GAE` 囉。
## 結尾&驗證
回到 `GCP` 後台選好專案，來到 `GAE`的管理頁面，部署完成後會給一組網址，像是`www-專案名稱.appspot.com`，之後就可以將 `DNS` 全部轉到此處。
這樣用戶就可以正常執行 `SPA` 網站囉。

## 參考資料
[Vue + Vue-cli 建置與部署](https://medium.com/finn-programming-life/vue-vue-cli%E7%9A%84%E5%BB%BA%E7%BD%AE%E8%88%87%E9%83%A8%E7%BD%B2-8b996e1d2f6a)