---
title: Nuxt 加入 robots
date: 2019-10-24
tags: 
  - nuxt
  - seo
categories: nuxt
description: robots 限制爬蟲搜尋頁面
---
## 前言
robots.txt 是遵循機器人排除標準的純文字檔案，這個檔案包含一或多項規則，每項規則會分別禁止 (或允許) 特定檢索器存取網站中的某個檔案路徑。
參考資料:
* [google robors.txt 說明](https://support.google.com/webmasters/answer/6062596?hl=zh-Hant)

## 安裝套件
[@nuxtjs/robots](https://github.com/nuxt-community/robots-module)
```
npm install @nuxtjs/robots
```

## 配置設定檔
有關於 robots 的設定可以有很多寫法，像是 Object、 Array、Function，可以依據自己的需求做調整，下面附上範例段落。
```
export default {
  modules: [
    '@nuxtjs/robots'
  ],
  robots: {
    UserAgent: '*',
    Disallow: [
      '/xxx/admin',
      '/xxx/admin/**',
      '/xxx/create-order',
    ],
    Sitemap: 'https://www.xxx.com.tw/sitemap.xml',
  },
}
```
執行 `npm run dev` 後，開啟 `http://localhost:3000/robots.txt` 就可以看到 robots.txt 囉!!