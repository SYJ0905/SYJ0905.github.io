---
title: HTML - 解決點擊輸入框時，畫面放大情況
tags:
  - HTML
categories:
  - HTML
description: 當使用行動裝置(iPhone、iPad)瀏覽網頁時，在預設的情況之下，點擊文字輸入框後，畫面會立即放大。如果不想要這個畫面放大的效果該怎麼做呢？
abbrlink: 2564304135
date: 2020-10-01 00:00:00
---
## meta tag 方法
在`<head>`輸入以下設定，會讓裝置的縮放功能給禁止，可謂相當暴力的解法之一。
``` HTML
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0" />
```

## CSS 設定
在 `input`、`textarea`等元素設定 `font-size`，可以保留畫面縮放功能，並且達到點及輸入框畫面放大問題勒。
``` CSS
input, textarea {
  font-size: initial;
}
```

## 參考資料
[如何在行動裝置上避免點擊輸入框時畫面放大](http://blog.shihshih.com/how-to-disable-zoom-in-when-focusing-on-the-input-box-on-mobile/)
