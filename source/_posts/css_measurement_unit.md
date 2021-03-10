---
title: CSS - 解析網頁尺寸單位
tags:
  - CSS
categories:
  - CSS
description: 本篇來介紹各種網頁尺寸的區別跟使用方法
abbrlink: 745685236
date: 2021-03-10 15:00:00
---
## 尺寸種類

### PX

絕對單位，是一般最常見的網頁設計單位，他是「絕對數值」，也就是設定多少就顯示多少。

### em

相對單位，每個 **<font color=#FF0000>子元素</font>** 透過「倍數」乘以 **<font color=#FF0000>父元素</font>** 的 px 值。

``` HTML
<style>
  html {
    font-size: 16px;
  }
  .wrap1 {
    font-size: 20px;
  }
  .wrap2 {
    font-size: 2em;
  }
  .wrap3 {
    font-size: 3em;
  }
</style>

<div class="wrap1">
  wrap1 => 20px
  <div class="wrap2">
    wrap2 => 40px
    <div class="wrap3">
      wrap3 => 120px
    </div>
  </div>
</div>
```

### rem

相對單位，每個 **<font color=#FF0000>元素</font>** 透過「倍數」乘以 **<font color=#FF0000>根元素(html)</font>** 的 px 值

``` HTML
<style>
  html {
    font-size: 16px;
  }
  .wrap1 {
    font-size: 20px;
  }
  .wrap2 {
    font-size: 2rem;
  }
  .wrap3 {
    font-size: 1rem;
  }
</style>

<div class="wrap1">
  wrap1 => 20px
  <div class="wrap2">
    wrap2 => 32px
    <div class="wrap3">
      wrap3 => 16px
    </div>
  </div>
</div>
```

### 百分比 %

每個 **<font color=#FF0000>子元素</font>** 透過「百分比」乘以 **<font color=#FF0000>父元素</font>** 的 px 值。

``` HTML
<style>
  html {
    font-size: 16px;
  }
  .wrap1 {
    font-size: 20px;
  }
  .wrap2 {
    font-size: 110%;
  }
  .wrap3 {
    font-size: 120%;
  }
</style>

<div class="wrap1">
  wrap1 => 20px
  <div class="wrap2">
    wrap2 => 22px
    <div class="wrap3">
      wrap3 => 26.4px = wrap2 * 120%
    </div>
  </div>
</div>
```

## 參考資料

[一次搞懂 CSS 字體單位：px、em、rem 和 %](https://www.oxxostudio.tw/articles/201809/css-font-size.html)
[PX、EM、REM](https://medium.com/neptune-coding/html-css%E6%95%99%E5%AD%B8-15-px-em-rem-12a1ba517c12)
[網頁用的尺寸單位:PX 跟 EM 怎麼區分呀？等等，還有一個 REM…](https://medium.com/@5min.reading/css-%E7%B6%B2%E9%A0%81%E7%94%A8%E7%9A%84%E5%B0%BA%E5%AF%B8%E5%96%AE%E4%BD%8D-px-%E8%B7%9F-em-%E6%80%8E%E9%BA%BC%E5%8D%80%E5%88%86%E5%91%80-%E7%AD%89%E7%AD%89-%E9%82%84%E6%9C%89%E4%B8%80%E5%80%8B-rem-4ee3911f1307)
[對於頁面適配，你應該使用px還是rem](https://kknews.cc/zh-tw/code/q5v2azr.html)
