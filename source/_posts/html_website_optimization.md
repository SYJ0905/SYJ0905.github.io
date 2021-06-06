---
title: 網站前端效能優化總整理
tags:
  - HTML
categories:
  - HTML
description: 本篇介紹如何有效的提升前端效能
abbrlink: 1197578805
date: 2021-06-07 15:00:00
---
## 影響效能的幾種因素

接下來會個別針對以下幾點做詳細優化方式。

* 圖片使用
* 程式語言
* 網路技術
* 字型使用

## 圖片使用

### 能不用圖片就不用圖片

* `程式製圖` : 能用程式就用程式來製作圖片。
* `特效修正` : 圖片的陰影( box-shadow )、圓角( box-radius)、漸層( background-gradient)，皆可使用 CSS 製作

### 使用 CDN 載入

將圖片這種靜態資源放到離使用者更近、更快的伺服器節點來獲取網頁檔案，讓圖片快速載入、提高效能。

* `第三方 library` : 圖片可以使用現成的 icon font library 作為 icon 圖片，如 FontAwesome，透過這種方法載入的圖片也具有彈性可以自由縮放圖片大小、改變顏色。
* `CDN 分流` : 利用 CDN 圖片分流加速服務來加速載入自己製作的圖片，如 AWS CloudFront ，設定後在載入網站時，會幫助使用者指向至最近節點獲取圖片、同時進行快取，除了能加速外亦有節省流量的效果。

### 最佳化圖片

* `使用合適的圖片大小` : 網頁上要呈現的長、寬多少像素，就將上傳的圖片裁切成同樣的大小，可以減少網路數據使用量、縮短載入時間。
* `新的圖片壓縮技術` : 如JPEG 2000、JPEG XR 或 WebP 等圖片格式，這類技術的圖片壓縮效率會比傳統的 PNG 或 JPEG 好，能夠更快下載完成圖片、減少網路數據使用量，但需考慮`兼容性`。
* `延遲載入圖片` : 使用如 lazyload.js、lozad.js 套件，讓使用者一開始載入網頁時，不會將全部網頁圖片一起載入(`未寫入src`)，而是網頁卷軸滾動到時才會載入(`寫入src`)。或是先載入圖片小圖，再載入圖片大圖。
* `優先使用 SVG 圖片` : 不受解析度和圖片縮放影響

### 程式語言優化

* `壓縮(minify)程式檔案` : 將 CSS、Javascript 檔案中的空白、註解去除，最小化程式語言檔案。
* `禁止轉譯的資源` : 減少在HTML `<link>`載入外部的 CSS、JavaScript，將網頁中首次載入網頁必要使用的 CSS、JavaScript，直接嵌入HTML`<head>`；延後載入之後需要的 CSS 樣式，如之後需要使用時，再用 JavaScript 載入。
* `減少 JavaScript 的執行時間` : 優化 JavaScript 的演算法運算的時間空間複雜度。
* `避免 DOM 節點數量過多` : Google建議應少於 1,500 個左右。理想的網頁樹狀層級應包含少於 32 個元素，以及少於 60 個下層/上層元素。過多的 DOM 會使用過多的記憶體。
* `使用 SPA 網站設計` :避免重復重新導向網頁，會導致網頁頁面延遲載入。
* `規劃良好 HTML 的輪廓` : 使用區塊語意標籤(ex: `<header>`)來取代區塊標籤(ex: `<div>`)，使 HTML 的上下層級是有階層的，更易載入，同時也強化網站的SEO。
* `CSS的Reflow 及 Repaint` : 當 CSS 檔解析出 CSS DOM Tree 後會和 HTML 解析出來的 DOM Tree，合作疊加產生 Render Tree，才開始計算畫面的 Layout，如 Box Model 的位置大小，以及可不可見(visible)，最後轉化成像素畫(Paint)到瀏覽器上。
  1. CSS 屬性替換 : 選擇用 translate 取代 Box Model 屬性與 定位(Position)屬性如top,left等

  2. 使用精確的 class : 在使用 JS 修改樣式時，明確指定到某區塊(div)的 CSS 來做修改，避免多餘的區塊修改時的計算。
  3. 減少觸發 : 節點數量不要過多與過深，減少渲染觸發影響的範圍。

### 網路技術優化

* `使用快取(Cache)` : 將部分需要載入的資源暫時存在使用者電腦的本地端。
* `預先連上必要來源(preload)` : 新增預先連線或預先擷取使用者的 DNS 的資源提示，及早連線至重要的第三方資源，不過關閉瀏覽器時會結束請求資源的請求。在HTML的`<head>`連結 JS、CSS 檔案時，使用 `<link rel="preload">`。
* `延遲載入必要來源(prefetch)` : 新增未來才會使用到的資源， 這些資源可以結合 catch 機制有更好的效能，先暫存在 HTTP Cache 中加快未來載入時的速度，關閉瀏覽器時，不會立即結束請求，而是等待資源是否可以取得再決定是否要取消請求，使用 `<link rel="prefetch">`。
* `網站伺服器升級到 HTTP/2` : 更新 HTTP 通訊協定到HTTP/2， 這個新一代的協定可以向下完全兼容，不用修改任何程式碼，它主要修改的底層通訊封包的傳輸，它具有連線多工（Multiplexing）的特性，在單一次網路的連線，就可以同時傳輸多個 HTTP Request 和 Response，一次請求多個 CSS、JavsScript和圖片等等的網路資源。

### 字型優化

* 優先使用本機端 : 先從使用者端的電腦載入字型，如使用者未有該字型，再從網路上下載。

``` CSS
@font-face {
  font-family: 'Noto Sans TC', sans-serif;
  src: local('Noto Sans TC Regular'),
       url(Noto Sans TC Regular'.woff2);
}
```

* 壓縮 : 將未使用到的字剔除，只擷取所需要的字。
* 適量使用 : 減少使用過多的網路字型，減少載入字型所造成的網頁載入延遲。

## 參考資料

[dom_performance_reflow_repaint.md](https://gist.github.com/faressoft/36cdd64faae21ed22948b458e6bf04d5)
[網站前端效能優化 (performance optimize)的方法](https://tcssh611503.medium.com/%E7%B6%B2%E7%AB%99%E5%89%8D%E7%AB%AF%E6%95%88%E8%83%BD%E5%84%AA%E5%8C%96-performance-optimize-%E7%9A%84%E6%96%B9%E6%B3%95-ec9b05804547)
[網頁前端效能優化學習筆記](https://medium.com/@chihsuan/%E7%B6%B2%E9%A0%81%E5%89%8D%E7%AB%AF%E6%95%88%E8%83%BD%E5%84%AA%E5%8C%96%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98-5993ccdb6f0d)
[三小招提升網頁 PageSpeed 分數，優化網頁開啟速度與 Web Vitals 指標](https://blog.user.today/2-ways-to-make-pagespeed-score-higher/)
