---
title: JavaScript - 瀏覽器中常見的高度介紹
date: 2020-02-23
tags: 
  - JavaScript
  - HTML
  - w3HexSchool
categories: JavaScript
description: 避免每次都忘記高度設定，就來記錄一下瀏覽器中的常見高度吧。
---
## 名詞解釋
* window.outerHeight
  獲取`整個瀏覽器`的高度、包含側邊欄、、書籤、網頁標題。此處在縮放瀏覽器時，也會有所變化，並非指電腦螢幕的高度。
* window.innerHeight
  瀏覽器的顯示內容（viewport）高度；如果有水平滾動條，也包括滾動條高度。
  ![outerHeight 與 innerHeight](https://i.imgur.com/8aX8jea.png)

* document.body.clientHeight
  為內容文檔 `body` 的高度，當高度超過 `window.innerHeight`，則會出現滾動條。
  如果在 `body` 設定高度為 100vh 或是在 `html` 設定高度 100vh 而 body 的高度為 100% 的話(隨父層 `html` 高度)，此時 `clientHeight`、`height()` 都只會給出 `window.innerHeight` 的高度數值，這點在設定高度上比需要注意。
* window.screen.height
  電腦解析度的高，如果電腦解析度文 1920*1080，那此數值就會是 1080。
* screen.availHeight
  為螢幕可用工作的高度，此數值不會變動，畢竟螢幕的大小只有在換螢幕時才會變換啊。
* HTMLElement.offsetHeight
  為該 `element`or`DOM`元素的高度，此高度包含 padding、border，不包含 margin 數值
  ![offsetHeight](https://i.imgur.com/YSLtn7C.png)
* Element.scrollHeight
  當該 `element` 有設定 overflow 屬性，而沒顯示在螢幕上的高度可使用 `scrollHeight` 取得該 `element` 全部高度
  ![scrollHeight](https://i.imgur.com/cTcb7VR.png)

## 滾動應用
* Element.scrollTop: 獲取元素被向上滾動的高度，此項常被用來監聽 `window` 的滾動事件
ex: 
``` JavaScript
window.onscroll = function() {
  //為了保證相容性，這裡取兩個值，哪個有值取哪一個
  //scrollTop就是觸發滾輪事件時滾輪的高度
  var scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
  console.log(scrollTop);
}
```

## 結尾
基本上使用 `HTMLElement.offsetHeight` 以及 `Element.scrollTop` 加上監聽事件，就能做出像是 `錨點動畫`、`回頂部動畫`、`滾動特定區塊後增加 DOM 元素的 class 配合 transform 屬性`等等，
本篇著重基本觀念解說，監聽事件的範例之後會在寫篇文章記錄。

## 參考資料
[javascript的offset、client、scroll使用方法詳解](https://codertw.com/%E5%89%8D%E7%AB%AF%E9%96%8B%E7%99%BC/292151/)