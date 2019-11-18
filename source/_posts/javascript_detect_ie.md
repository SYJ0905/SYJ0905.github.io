---
title: JavaScript - 判斷是否為ie瀏覽器的方法(含 IE 11)
date: 2019-11-19
tags: JavaScript
categories: JavaScript
description: 萬惡的 IE ，想不到之前 IE 10 以前的寫法已經不支援 IE11 了!!那就來更新一下最新的 IE 判斷法吧。
---
## 前言
原先 IE10 以前都是採用 `userAgent` 中的 `MSIE` 標誌來識別，但到了 IE11 卻把它給移除了QQ。當然也是有方法可以判斷的，並且還同時兼顧 IE6 以上呦!!

## IE 10 以前 (old)
還是附上一下以前的寫法好了。
```
function isIE() {
  if (window.navigator.userAgent.indexOf('MSIE') >= 1) {
    console.log('我是 IE');
  } else {
    console.log('我不是 IE');
  }
}
```

## IE11 (new for IE6 up)
```
function isIE() { //ie?
  if (!!window.ActiveXObject || 'ActiveXObject' in window) {
    console.log('我是 IE');
  } else {
    console.log('我不是 IE');
  }
}
```

## 結尾
接下來如果專案不須支援 IE 的話，可以試著把 IE 頁面導入到下載其他瀏覽器的頁面喔~~
避免使用者不知道如何是好，稍微提升點使用者體驗也是能拉回客人的www


