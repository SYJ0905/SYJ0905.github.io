---
title: CSS - 響應式圖片在 Retina 螢幕使用技巧
tags:
  - CSS
  - Image
  - RWD
  - 圖片最佳化
  - Media Query
categories:
  - CSS
description: 紀錄響應式圖片在 Retina 螢幕上不失真的小技巧
abbrlink: 1810131633
date: 2020-11-23 00:00:00
---
## 檢查裝置

一般螢幕下 `pixel-ratio` 是 1，也就代表在桌機顯示 1920*1080 圖片是不會失真的。然而 Retina 顯示器的 `pixel-ratio` 卻不一樣，有的是 2(iphoe5 ~ iphoe8)，也有些新出的是 3(iphoe6+ ~ iphoeX) 以上這些類型的裝置，在設計師出圖時就必須要同時給出適當倍率的圖片。
ex:
舉例 pixel-ratio = 2
在 iphoe5 ~ iphoe8 上就要顯示 2x 倍的圖
在 iphoe6+ ~ iphoeX 上就要顯示 3x 倍的圖
那要如何知道各裝置的 `舉例 pixel-ratio` 呢?

使用以下連結，可查詢目前裝置的 `CSS pixel-ratio` 跟 `Resolution (dpi)`
[mydevice](https://www.mydevice.io/)
並且搭配 CSS 的 `min-device-pixel-ratio` 即可依據裝置的 `pixel-ratio` 來決定到底該套用哪一張倍率的圖片。

## Retina Display Media Query

``` css
@media
(-webkit-min-device-pixel-ratio: 2),
(min-resolution: 192dpi) {
    /* Retina-specific stuff here */
}
```

## 使用時機

注意:在出 2x、3x 圖時，不是將 1 倍圖片等比放大 2 倍或是 3 倍，而是反過來用 3 倍圖片等比縮小成 2 倍 跟 1倍圖片，這樣才不會產出模糊圖片

* 375px up : 在手機時該圖片最大尺寸的 1x、2x、3x圖
* 768px up : 在平板時該圖片最大尺寸的 1x、2x、3x圖
* 1200px up : 在筆電、桌機時該圖片最大尺寸的 1x、2x 圖

## 參考資料

[網頁前端優化 — 響應式圖片實作](https://medium.com/nick-%E5%B7%A5%E7%A8%8B%E5%B8%AB%E5%AD%B8%E7%BF%92%E8%A8%98/%E7%B6%B2%E9%A0%81%E5%89%8D%E7%AB%AF%E5%84%AA%E5%8C%96-%E9%9F%BF%E6%87%89%E5%BC%8F%E5%9C%96%E7%89%87%E5%AF%A6%E4%BD%9C-3ab1989b9d9c)
[[CSS] Media Query](https://pjchender.github.io/2018/06/09/css-media-query/)
[Retina Display Media Query](https://css-tricks.com/snippets/css/retina-display-media-query/)
[Mydevice.io](https://www.mydevice.io/)
