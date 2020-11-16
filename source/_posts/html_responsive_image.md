---
title: HTML - 響應式圖片技巧
date: 2020-11-17
tags: 
  - HTML
  - Image
  - Picture
  - RWD
  - 圖片最佳化
  - 效能調校
  - 加載效能
  - Media Query
categories: HTML
description: 本篇將介紹在網頁中使用圖片時需要注意哪些事以及提高網頁加載效能。
---
## 前言
覺得圖片載入太慢嗎?覺得圖片在某些裝置模糊嗎?在網頁上使用適當的圖片格式、尺寸能有效的讓網站體驗更加，以下將介紹如何使用 `<picture> 、 <source> 、 <img>` 來讓瀏覽器根據自身環境決定最適當的圖檔。

## 圖片依據條件
* DPR(Device Pixel Ratio): 裝置像素密度，指每一英吋裡含有多少像素。
* Viewport: 網頁可視區域

## 圖片模糊
現在螢幕的 DPR 大多是 1，而貧果裝置就與別人不同，iPhone 的 DPR 是 2，iPad 則是 3，這也就導致圖片在蘋果裝置就會顯得模糊不少。解決辦法則是製作兩張不同解析度的圖片，並根據 DPR 來決定要載入哪張圖片。
參考代碼:
``` HTML
<img src="small.jpg"
  srcset="small.jpg 1x, small_2x.jpg 2x"
/>
```

## DPR 不清楚怎麼辦?
可以使用 `w` 依照 DPR 與 Viewport 兩者決定適當圖片。
以下是當螢幕寬度為 500px DPR 為 2，則選擇圖片尺寸為 500px*2 = 1000px，所以就會使用 cloud_m.jpg 。
``` HTML
<img src="small.jpg"
  srcset="small.jpg 500w, medium.jpg 1000w, large.jpg 1500w"
/>
```
而使用 `w` 就必須指定圖片大小，`size` 屬性只是選擇條件，不設定 `size` 就會當成 `100vw`。
以下是當 `Viewport` 小於or等於 `500px`，則圖片寬度為 `90% Viewport`，剩餘為 `60% Viewport`。當螢幕寬為 500px DPR 是 1，就會選擇 `small.jpg`(500 * 0.9 * 1=450px)
``` HTML
<img src="small.jpg"
  sizes="(max-width: 500px) 90vw, 60vw"
  srcset="small.jpg 500w, medium.jpg 1000w, large.jpg 1500w"
/>
```

## Viewport 選擇適當圖片
可使用 `media` 根據 `Viewport` 選擇適當圖片。
Viewport >= 1200px => 選擇 large.jpg
Viewport >= 768px => 選擇 medium.jpg
都不符合則選擇 small.jpg
``` HTML
<picture>
  <source media="(min-width: 1200px)" srcset="large.jpg" />
  <source media="(min-width: 768px)" srcset="medium.jpg" />
  <img src="small.jpg" alt="small" />
</picture>
```

## DPR 、 Viewport 兩者兼得
當 Viewport 為 700px 且 DPR 為 2 ，就會選擇 sample-large-2x.jpg 這張圖片
``` HTML
<picture>
  <source
    media="(min-width: 600px)"
    srcset="sample-large-1x.jpg 1x, sample-large-2x.jpg 2x"
  />
  <source
    media="(min-width: 400px)"
    srcset="sample-medium-1.jpg 1x, sample-medium-2.jpg 2x"
  />
  <img src="sample-small.jpg" alt="Sample" />
</picture>
```
## 加載效能
由於直接使用 `<picture>、<source>、<img>` 的關係，瀏覽器解析 HTML 時，就會依條件決定要`下載`哪一張圖片，與 css 中的 `Media Query` 使用 `display:none`不同(全部圖片都下載，再依 css 決定顯示與否)，後者會導致浪費過多網路資源，導致選染延遲等等。

## 參考資料
[響應式圖片（Responsive Images）](https://cythilya.github.io/2018/08/24/responsive-images/)
[使用picture tag來做到響應式圖片](https://hamisme.blogspot.com/2019/11/html5-picture-tag.html)
[用 img srcset 與 HTML5 picture，讓圖片也能RWD](https://shubo.io/responsive-image/#img-srcset-%E5%B1%AC%E6%80%A7)