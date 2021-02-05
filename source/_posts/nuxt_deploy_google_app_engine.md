---
title: Nuxt 部署策略 - 部署 Google App Engine
tags:
  - Vue
  - Nuxt
  - SEO
categories:
  - Vue
description: 本篇將介紹如何把 Nuxt 專案部屬至 GAE(Google App Engine)
abbrlink: 3352502083
date: 2021-02-05 01:30:00
---
## app.yaml 配置

``` yaml
# 標準環境
runtime: nodejs10
# 彈性環境
# runtime: nodejs
# env: flex

# manual_scaling:
#   instances: 1
# resources:
#   cpu: 1
#   memory_gb: 1
#   disk_size_gb: 10

handlers:
  - url: /_nuxt
    static_dir: .nuxt/dist/client
    secure: always

  - url: /(.*\.(gif|png|jpg|ico|txt))$
    static_files: static/\1
    upload: static/.*\.(gif|png|jpg|ico|txt)$
    secure: always

  - url: /.*
    script: auto
    secure: always

env_variables:
  HOST: '0.0.0.0'
  NODE_ENV: 'production'
  API_PATH: https://xxx.xxx.xxx
```

* resources: 可以調整主機資源，可以部署不同資源的版本，當流量過大時，可在 `GAE` 後台直接切換版本，馬上做出應對。
* runtime: 此處寫法與標準設定不同，請注意。
* env: 彈性設定必須寫 flex。
* env_variables: 若有相關變數必須在此設定。

## package.json 設定

將專案的 package.json 調整成以下範例，
必須要寫 `npm run start` 的指令，因為這是 GAE 部署時會執行的

``` JSON
{
  "name": "demo",
  "version": "0.1.0",
  "private": true,
  "engines": {
    "node": ">=10.0.0"
  },
  "scripts": {
    "dev": "cross-env NODE_ENV=dev nuxt",
    "prod": "cross-env NODE_ENV=production nuxt",
    "build": "nuxt build",
    "start": "nuxt start"
  },
}
```

## 部署 GAE

這邊首先要安裝 `Google Cloud SDK`，這其實就類似 `CMD`，讓我們可以輸入部署指令用的。
完成後執行程式，並開始以下部署步驟:

1. 移到專案資料夾

``` CMD
cd 專案資料夾路徑
```

2. 初始化 `GAE`

``` CMD
gcloud init
```

此時會詢問一些問題，像是要用哪個帳號、連接的伺服器地區(台灣、香港)，最後是要部署到哪一份專案的 `app engine`。

3. 執行部署指令

``` CMD
gcloud app deploy app.yaml
```

輸入後有可能會出現 `python` 的錯誤代碼，不過沒關係，繼續讓他跑程式，若是沒有出現 `ERROR` 等字樣，並且完成所有程序，就代表已經部署至 `GAE` 囉。

## 結尾&驗證

回到 `GCP` 後台選好專案，來到 `GAE`的管理頁面，部署完成後會給一組網址，像是`www-專案名稱.appspot.com`，之後就可以將 `DNS` 全部轉到此處。
這樣用戶就可以正常執行 `Nuxt` 網站囉。

## 參考資料

[Vue - 部署至 Google App Engine](https://syj0905.github.io/vue/20200419/4265981960/)
