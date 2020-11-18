---
title: JavaScript - 如何偵測使用者的裝置是否為行動裝置
tags:
  - JavaScript
categories:
  - JavaScript
description: CSS 有了 media query 處理多裝置的樣式，那麼 JavaScript 該如何解決多裝置的判定呢?
abbrlink: 1159365328
date: 2019-11-18 00:00:00
---
## 前言
實務上有時會根據使用者的裝置來決定部分功能是否開啟或關閉，單純使用 CSS 的 media query 斷點有個缺點是手機有功能要開啟但桌面、平板是關閉的，而使用者縮放視窗到手機尺寸時則會變成能使用該功能。
有鑑於此，我們必須要使用 JavaScript 來判定使用者的裝置，而不是依據 media query 斷點。

## 判斷依據
偵測瀏覽器的 userAgent 有沒有包含行動裝置的關鍵字，若有包含則回傳 true，沒有則 false。

## ES5 寫法
```
function isMobileDevice(){
  var mobileDevices = ['Android', 'webOS', 'iPhone', 'iPad', 'iPod', 'BlackBerry', 'Windows Phone'];
  var isMobileDevice = false;
  var length = mobileDevice.length;
  for(var i = 0; i < length; i++) {
    if(navigator.userAgent.match(mobileDevice[i])){
      isMobileDevice = true;
    }
  }
  return isMobileDevice;
}
```

## ES6 寫法
```
function isMobileDevice() {
  const mobileDevice = ['Android', 'webOS', 'iPhone', 'iPad', 'iPod', 'BlackBerry', 'Windows Phone'];
  let isMobileDevice = mobileDevice.some(e => navigator.userAgent.match(e));
  return isMobileDevice;
}
```