---
title: JavaScript - 圖片放大鏡效果
date: 2020-05-17
tags: 
  - JavaScript
  - w3HexSchool
categories: JavaScript
description: 透過原生 JavaScript 或是各種函式庫實作圖片放大鏡效果。
---
## 前言
在網頁上逛購物平台時，會遇到這樣一種網頁特效：當滑鼠移到一張商品縮圖上時，旁邊就會顯示該商品局部放大的圖片。這就是所謂的放大鏡特效。本次會介紹如何使用`原生 JavaScript` 以及其他函式庫完成此效果。

## 設計想法
1. 當滑鼠移動到圖片區塊時，會觸發放大鏡效果。
2. 放大區塊使用背景圖片，並且利用滑鼠移動到原來圖片的位置來定位放大的部分。
3. 將放大區塊寫入 CSS 背景設定

## 原生 JavaScript 方式
``` HTML
<script src='https://cdnjs.cloudflare.com/ajax/libs/jquery/3.5.1/jquery.js'></script>
<div class='loupe'></div>
<div class='wrap'>
  <img src='./test_image.jpg' class='image'>
</div>
<script src='./all.js'></script>
```
``` CSS
* {
  margin: 0;
  padding: 0;
}
body {
  width: 100%;
  height: 100%;
  overflow: hidden;
}
.wrap {
  margin-left: auto;
  margin-right: auto;
  width: 600px;
}
.wrap img {
  display: block;
  max-width: 100%;
  height: auto;
  cursor: crosshair;
}
.loupe {
  position: absolute;
  pointer-events: none;
  visibility: hidden;
  z-index: 999;
  width: 200px;
  height: 200px;
  border: 3px solid #636363;
  border-radius: 50%;
}
```
``` JavaScript
$(document).ready(function () {
  var vh = $(window).height(); /* 獲取視窗高度 */
  var vw = $(window).width();  /* 獲取視窗寬度 */
  var imgh = $('.wrap img').height(); /* 獲取圖片高度 */
  var imgw = $('.wrap img').width();  /* 獲取圖片寬度 */
  var beginX = $('.wrap img').offset().left; /* 取得圖片最左邊的 x 值 */
  var endX = beginX + imgw; /* 取得圖片最右邊的 x 值 */
  var beginY = $('.wrap img').offset().top; /* 取得圖片最上方的 y 值 */
  var endY = beginY + imgh; /* 取得圖片最下邊的 y 值 */
  //滑鼠經過
  document.addEventListener('mousemove', loupe, false);
  function loupe(e) {
    var x, y;
    x = e.clientX;
    y = e.clientY;
    /* 判斷滑鼠或觸控點在圖片區域，是則顯示放大鏡div層 */
    if (x > beginX && x < endX && y > beginY && y < endY) {
      /* 使用 100 減去這個值，目的是將圖片懸浮的地方定位於圓形區域的中心。 */
      var mx = 100 - (x - beginX) / imgw * 1440; /* 1440為原圖片寬度 */
      var my = 100 - (y - beginY) / imgh * 1020; /* 1020為原圖片高度 */
      var bg = 'url(./test_image.jpg) ' + mx + 'px ' + my + 'px no-repeat #fff'
      $('.loupe').css('left', x - 100 + 'px').css('top', y - 100 + 'px').css('background', bg) /* 設定圓形區域中心及背景 */
      $('.loupe').css('visibility', 'visible')
    } else {
      $('.loupe').css('visibility', 'hidden')
    }
  }
})
```
基本概念就是利用圖片的寬高、所在的區域、滑鼠移動的位置，三者搭配並且設定放大鏡背景圖片即可達成此效果。

## Blowup.js 方法
[blowup.js](https://github.com/paulkr/blowup.js)
它是一個 `jQuery` 的插件，只需要一行代碼就可以生成超炫的放大鏡效果， 同樣擁有很多不同的特性和選項。
本身採用 `npm` 下載函式庫，沒有 `CDN` 可以使用
```
npm install blowup -S
```
``` HTML
<div class="wrap">
    <img src="./test_image.jpg" class="blowup_image">
  </div>
  <div class="wrap">
    <img src="./test_image.jpg" class="blowup_image">
  </div>
  <div class="wrap">
    <img src="./test_image.jpg" class="blowup_image">
  </div>
```
``` CSS
* {
  padding: 0;
  margin: 0;
}
body {
  width: 100%;
  height: 100%;
}
img {
  max-width: 100%;
  height: auto;
}
.wrap {
  width: 400px;
  margin: 0 auto;
  border-radius: 5px;
}
```
將需要使用放大鏡的圖片添加 `class`，並在 JS 加入以下代碼，即可擁有放大鏡效果囉!
``` JavaScript
$(document).ready(function () {
  $('.blowup_image').blowup({
    background: '#FCEBB6',
  });
})
```
Blowup.js 的原始碼也不算太難，有興趣的可以讀以下原始碼:
``` JavaScript
/**
 * blowup.js
 * Paul Krishnamurthy 2016
 *
 * https://paulkr.com
 * paul@paulkr.com
 */

$(function ($) {
  $.fn.blowup = function (attributes) {

    var $element = this;
    console.log($element.is("img"));

    // If the target element is not an image
    if (!$element.is("img")) {
      console.log("%c Blowup.js Error: " + "%cTarget element is not an image.",
        "background: #FCEBB6; color: #F07818; font-size: 17px; font-weight: bold;",
        "background: #FCEBB6; color: #F07818; font-size: 17px;");
      return;
    }

    // Constants
    var $IMAGE_URL = $element.attr("src");
    var NATIVE_IMG = new Image();
    NATIVE_IMG.src = $element.attr("src");

    // Default attributes
    var defaults = {
      round: true,
      width: 200,
      height: 200,
      background: "#FFF",
      shadow: "0 8px 17px 0 rgba(0, 0, 0, 0.2)",
      border: "6px solid #FFF",
      cursor: true,
      zIndex: 999999,
      scale: 1,
      customClasses: ""
    }

    // Update defaults with custom attributes
    var $options = $.extend(defaults, attributes);

    // Modify target image
    $element.on('dragstart', function (e) { e.preventDefault(); });
    $element.css("cursor", $options.cursor ? "crosshair" : "none");

    // Create magnification lens element
    var lens = document.createElement("div");
    lens.id = "BlowupLens";

    // Attack the element to the body
    $("body").append(lens);

    // Updates styles
    $blowupLens = $("#BlowupLens");

    $blowupLens.css({
      "position": "absolute",
      "display": "none",
      "pointer-events": "none",
      "zIndex": $options.zIndex,
      "width": $options.width,
      "height": $options.height,
      "border": $options.border,
      "background": $options.background,
      "border-radius": $options.round ? "50%" : "none",
      "box-shadow": $options.shadow,
      "background-repeat": "no-repeat",
    });

    // Add custom CSS classes
    $blowupLens.addClass($options.customClasses);

    // Show magnification lens
    $element.mouseenter(function () {
      $blowupLens.css("display", "block");
    })

    // Mouse motion on image
    $element.mousemove(function (e) {

      // Lens position coordinates
      var lensX = e.pageX - $options.width / 2;
      var lensY = e.pageY - $options.height / 2;

      // Relative coordinates of image
      var relX = e.pageX - $(this).offset().left;
      var relY = e.pageY - $(this).offset().top;

      // Zoomed image coordinates 
      var zoomX = -Math.floor(relX / $element.width() * (NATIVE_IMG.width * $options.scale) - $options.width / 2);
      var zoomY = -Math.floor(relY / $element.height() * (NATIVE_IMG.height * $options.scale) - $options.height / 2);

      var backPos = zoomX + "px " + zoomY + "px";
      var backgroundSize = NATIVE_IMG.width * $options.scale + "px" + NATIVE_IMG.height * $options.scale + "px";

      // Apply styles to lens
      $blowupLens.css({
        left: lensX,
        top: lensY,
        "background-image": "url(" + NATIVE_IMG.src + ")",
        "background-size": backgroundSize,
        "background-position": backPos
      });
    })

    // Hide magnification lens
    $element.mouseleave(function () {
      $blowupLens.css("display", "none");
    });
  }
})

```

## 其他函式庫
* `Magify JS`: 似乎需要有小圖跟放大圖才能使用。
* `jQuery Zoom`: 放大的效果有點像視窗滾動 + 大圖。
* `Leroy Zoom`: 一個只有 4k 的插件，能夠讓你放大任何網頁部分，包括圖片。
* `Magnifier.js`: 支持滑鼠滾輪放大縮小功能，還挺特別的。
* `Zoomple`: 支援多種放大樣式以及呈現的方式