---
title: JavaScript - 使用 jQuery 來產生 QR CODE
tags:
  - JavaScript
  - jQuery
categories:
  - JavaScript
description: 本篇來介紹純前端生成 QR CODE 的方式
abbrlink: 3805875564
date: 2021-03-14 00:45:00
---
## jQuery.qrcode 介紹

[jQuery.qrcode 官網](https://larsjung.de/jquery-qrcode/)
[NPM jQuery.qrcode](https://www.npmjs.com/package/jquery.qrcode)

使用方式算挺簡單，幾個重要參數設定一下就能迅速產生 QR CODE

## 參考範例

``` HTML
<body>
  <div id="jquery-qrcode-canvas"></div>

  <div id="jquery-qrcode-image"></div>

  <div id="jquery-qrcode-div"></div>

  <!-- 引入 jQuery 引入 jQuery jquery.qrcode  -->
  <script src='https://cdnjs.cloudflare.com/ajax/libs/jquery/3.5.1/jquery.js'></script>
  <script src='https://cdnjs.cloudflare.com/ajax/libs/jquery.qrcode/1.0/jquery.qrcode.min.js'></script>
  <script>
    /* canvas */
    $("#jquery-qrcode-canvas").qrcode({
      render: 'canvas',
      size: 250,
      text: 'https://syj0905.github.io/'
    });

    /* image */
    $("#jquery-qrcode-image").qrcode({
      render: 'image',
      size: 250,
      text: 'https://syj0905.github.io/'
    });

    /* div */
    $("#jquery-qrcode-div").qrcode({
      render: 'div',
      size: 250,
      text: 'https://syj0905.github.io/'
    });
  </script>
</body>
```

## 參考資料

[jQuery.qrcode：純前端生成 QR Code](https://mnya.tw/cc/word/1467.html)
[10 Best Custom QR Code Generators In JavaScript (2021 Update)](https://www.jqueryscript.net/blog/best-custom-qr-code-generator.html)
