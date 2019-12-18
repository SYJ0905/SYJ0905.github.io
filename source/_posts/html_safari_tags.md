---
title: HTML - Mobile Safari Meta Tags
date: 2019-12-19
tags: HTML
categories: HTML
description: 善用 Safari Meta Tags ，可讓 iphone 在瀏覽網站時有更多變化。一起學習有哪些 Meta Tags 吧!!
---
## Apple 特有的 Meta Tag Keys
* apple-mobile-web-app-capable
* apple-mobile-web-app-status-bar-style
* format-detection

### apple-mobile-web-app-capable
範例程式碼
``` HTML
<meta name="apple-mobile-web-app-capable" content="yes">
```
參數設定:
`content` : `yes` or `no` ，決定是否以全螢幕模式顯示，不會顯示 navigation bar (網址那條)。
註:選擇 `yes`時，狀態列的字都會是黑色的，導致看不見最上方的 status bar(wifi、4G、時間)等等的資訊，如果只想不顯示 navigation bar 但能看到這些資訊該如何呢?
   那就要搭配 `apple-mobile-web-app-status-bar-style`

### apple-mobile-web-app-status-bar-style
這個屬性只有在 `apple-mobile-web-app-capable` 設定為不是全螢幕的狀態下，也就是 `apple-mobile-web-app-capable` 為 `no` 時是不會有效果的。
範例程式碼
``` HTML
<meta name="apple-mobile-web-app-status-bar-style" content="black">
```
參數設定:
`default` : 不會顯示出 status bar 的資訊。
`black` : 會在 status bar 加上黑色背景，讓 status bar 的內容以白色顯示。
`black-translucent` : 這個效果會讓 status bar fiexd 在最上端，而網頁內容則是在下層。

### format-detection
範例程式碼
``` HTML
<meta name="format-detection" content="telephone=no">
```
Mobile Safari 在預設中會解析網頁的數字，有可能會解析成超連結點擊。
設定成 `telephone=no` 後，則會不解析網頁數字，避免出現問題。

## 參考資料
[Safari HTML Reference](https://developer.apple.com/library/archive/documentation/AppleApplications/Reference/SafariHTMLRef/Articles/MetaTags.html#//apple_ref/doc/uid/TP40008193-SW1)
