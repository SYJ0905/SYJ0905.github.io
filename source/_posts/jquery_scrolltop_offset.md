---
title: jQuery - scrollTop 與 offset 運用
tags:
  - JavaScript
  - jQuery
categories:
  - jQuery
description: 本篇將介紹使用 jQuery 製作"滑動到指定區塊"以及"回到頂部功能"
abbrlink: 1559860955
date: 2020-12-10 00:00:00
---

## 語法介紹

### animate()

`.animate( properties [, duration ] [, easing ] [, complete ] )`

* properties: Object 型別，屬性可以設定 CSS 或者是 滾動參數 scrollTop

* duration: 為動畫完成的速度，以毫秒為單位

* easing: 設定動畫速度函數，有 `swing`、`linear` 可選
  
* complete:動畫執行完後要執行的函式

### offset()

回傳該 DOM 元素頂部與 document 的距離，與 position() 的關係有些差異。

``` javascript
const x = $(selector).offset().left;
const y = $(selector).offset().top;


/* 設定 DOM 元素新的座標偏移 */
$(selector).offset(function(index,oldoffset){
  const newPos = new Object();
  newPos.left = oldoffset.left + 50;
  newPos.top = oldoffset.top + 50;
  return newPos;
});

```

## 參考範例

``` javascript
/* go top 的按鈕 */
$('.go_top').on('click', function (e) {
  e.preventDefault();
  $('html, body').animate({
    scrollTop: 0,
  }, 700)
});



$('navbar').on('click','a', function (e) {/* 監聽 navbar 下的每個 a */
  e.preventDefault();
  const target_href = $(this).attr('href');
  const linkScroll = $(target_href).offset().top;
  $('html,body').stop().animate({
      scrollTop: linkScroll,
  }, 700)
});
```

## 參考資料

[jQuery 取得Dom 元素座標- Offset() 與Position() | 一群棒子](https://bonze.tw/jquery-%E5%8F%96%E5%BE%97-dom-%E5%85%83%E7%B4%A0%E5%BA%A7%E6%A8%99-offset-%E8%88%87-position/)
[JQuery — scrollTop, offset 運用](https://medium.com/chloelo925/jquery-scrolltop-offset-%E9%81%8B%E7%94%A8-f7bbe93b77c4)
