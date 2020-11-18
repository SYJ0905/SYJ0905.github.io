---
title: Hexo 架站攻略 - SEO 優化
tags:
  - Hexo
categories:
  - Hexo
description: 本篇文章會記錄該如何進一步優化網站 SEO，優化方法有很多種，會陸續更新內容。
abbrlink: 285599935
date: 2019-09-06 00:00:00
---

## 前言
本篇文章會記錄該如何進一步優化網站 SEO，優化方法有很多種，會陸續更新內容。

## 建立 sitemap
安裝站點地圖套件
```
npm install hexo-generator-sitemap --save
```
在 [Google Search Console](https://search.google.com/search-console/about) 提交 sitemap.xml
![Google Search Console](https://i.imgur.com/FqRYG8P.png)

## 加入 robots.txt
`Robots.txt` 主要行為就是在搜尋引擎檢索網站時，告訴它網站哪些內容可以被檢索，哪些內容可以不用被檢索。
在 `source` 下新增 `robots.txt` 檔案，並加入以下範例說明即可
![robots.txt](https://i.imgur.com/jeqORKI.png)
### 相關參數介紹 :
  * User-agent => 定義下述規則對哪些搜尋引擎生效，即是對象。
  * Disallow => 指定哪些目錄或檔案類型不想被檢索，需指名路徑，否則將會被忽略。
  * Allow => 指定哪些目錄或檔案類型可能被檢索，需指名路徑，否則將會被忽略。
  * Sitemap => 指定網站內的sitemap檔案放置位置，需使用絕對路徑。

### 常見應用方式與環境 :
  * 允許所有搜尋引擎檢索所有內容(通常建議使用)
    * User-agent: *
    * Disallow:
  * 拒絕所有搜尋引擎檢索所有內容(正式環境請避免使用)
    * User-agent: *
    * Disallow: /
  * 拒絕所有搜尋引擎檢索 /members/ 底下所有內容。
    * User-agent: *
    * Disallow: /members/
  * 拒絕 Google 爬蟲檢索 /images/ 底下所有內容。
    * User-agent: Googlebot-image
    * Disallow:/images/
  * [萬用字元]拒絕所有搜尋引擎檢索網站內png為副檔名的圖檔。
    * User-agent: *
    * Disallow: *.png$
  * [萬用字元]拒絕 Bing 搜尋引擎檢索網站內 /wp-admin 目錄底下所有內容及網站內開頭為 test 的所有檔名。
    * User-agent: bingbot
    * Disallow: /wp-admin/
    * Disallow: ^test*

## 開啟 NexT 內建 SEO 優化功能
在主題配置 _config.yml 搜尋 `SEO Settings`，將 `seo` 改為 `true` 即可
```
# Change headers hierarchy on site-subtitle (will be main site description) and on all post / page titles for better SEO-optimization.
seo: true
```

## 修改連結設定
使用 `nofollow` 技巧避免爬蟲遇到連結後進去回不來的情況產生，目前 NexT 模板有兩處連結需要修正。
找到 在 themes 文件中的 `themes/next-reloaded/layout/_partials/footer.swig`

1. 搜尋 `theme-next.org`，修改成以下範例
```
#}{{ __('footer.theme') }} – <a href='https://theme-next.org' class='theme-link' rel='external nofoolow'> NexT.Pisces </a>{#
```
2. 搜尋 `hexo.io`，將原本的程式碼修改成以下範例
```
<a href='https://hexo.io' class='theme-link' rel='external nofollow'> Hexo </a>
```

### 另一種方法 hexo-autonofollow
覺得看不懂上方的改寫嗎?又或者是擔心下次改版後又得重新設定嫌麻煩嗎?
那就用套件來幫我們自動為非友情連結加上 `nofollow` 吧!!
安裝自動加入連結套件
[hexo-autonofollow](https://github.com/liuzc/hexo-autonofollow)
```
npm install hexo-autonofollow --save
```
在站點配置 _config.yml 加入設定
```
nofollow:
	enable: true
	exclude:
    - // 可以加入友情連結，會讓連結不加上 nofollow
```
