---
title: Nuxt 加入 JSON-LD 結構化資料
tags:
  - Vue
  - SEO
categories:
  - Vue
description: 加入 JSON-LD 讓電腦更看懂你的網站資訊吧!!
abbrlink: 2360505463
date: 2019-10-24 00:00:00
---
## 前言
一切都是為了站上搜尋排行榜的龍頭，反正 SEO 的前言已經懶的想了@@
參考資料:
[google 說明](https://developers.google.com/search/docs/data-types/product)
[schema.org](https://schema.org/) : 共用詞彙庫
[Structured Data Testing Tool](https://search.google.com/structured-data/testing-tool/u/0/) : 測試網頁結構

## 安裝套件
[nuxt-jsonld](https://github.com/ymmooot/nuxt-jsonld)
```
npm install nuxt-jsonld
```
在 `plugins` 底下新增一個 `jsonld.js` 檔案，並引入套件
```
import Vue from 'vue';
import NuxtJsonld from 'nuxt-jsonld';

Vue.use(NuxtJsonld);
```

## 配置設定檔
在 `nuxt.conig.js` 的 `plugins` 加入上一步建立的 `jsonld.js` 檔
```
export default {
  plugins: [
    {
      src: '@/plugins/jsonld.js',
      ssr: true,
    },
  ],
}
```

## 新增 JSON-LD 檔案
在 `static` 中建立 `jsonld.json` 內容要搭配 [schema.org](https://schema.org/) 來寫，看個幾遍就應該可以知道該怎麼撰寫網站的 JSON-LD 囉!!
參考範例:
```
{
  "organization": {
    "@context": "http://schema.org",
    "@id": "公司網址/#organization",
    "@type": "Organization",
    "name": "公司名稱",
    "description": "公司描述",
    "url": "公司網址",
    "contactPoint": [
      {
        "@type": "ContactPoint",
        "telephone": "+886-02-xxxx-xxxx",
        "areaServed": "TW",
        "contactType": "Customer Service",
        "availableLanguage": "Chinese"
      }
    ],
    "address": {
      "@type": "PostalAddress",
      "streetAddress": "公司地址",
      "addressLocality": "台北市xx區",
      "addressRegion": "台灣",
      "addressCountry": "TW"
    }
  },
  "webpage": {
    "@context": "http://schema.org",
    "@id": "公司網址/#webpage",
    "@type": "WebPage",
    "name": "頁面名稱",
    "description": "頁面敘述",
    "url": "網址",
    "publisher": {
      "@type": "Organization",
      "name": "xxx公司"
    }
  },
  "website": {
    "@context": "http://schema.org",
    "@id": "公司網址/#website",
    "@type": "WebSite",
    "name": "頁面名稱",
    "description": "頁面敘述",
    "url": "公司網址"
  }
}
```

## 各頁面引入
1. 在 .vue 檔中 `import` jsonLd
註: eslint 可能會報錯，把 rules 加入 `'import/no-unresolved': 'off'` 就可以解決囉，雖然不是很優雅。
2. 使用 `asyncData` 取出 JSONLD 資料，必須是 return 物件喔。
3. 使用 jsonld(){} 來製作該頁專屬的 JSONLD 資料，ex: 產品詳細頁的麵包屑就需要這麼做，這邊要 return 陣列，才不會結構出錯。
![JSONLD](https://i.imgur.com/3r20Rtb.png)

## 測試
執行 `npm run dev` 後，檢視原始碼就可以看到以下畫面囉!!
![JSONLD](https://i.imgur.com/W2GjE71.png)
也可以將 JSONLD 的 `script` 段落複製下來，貼到 [Structured Data Testing Tool](https://search.google.com/structured-data/testing-tool/u/0/) ，就可以看到結構是否有誤或是缺少一些屬性囉!!