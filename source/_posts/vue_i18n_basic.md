---
title: Vue - 使用 Vue I18n 打造多國語系網站環境
date: 2020-02-14
tags: 
  - Vue
  - JavaScript
categories: Vue
description: 本文將介紹純前端網站該如何使用 Vue I18n 引入自訂語言包，並達到切換語系的功能。
---
## 前言
當網站的用戶有外籍人士時，客戶本身可以透過 Google 自動翻譯來閱讀，但翻譯過後的內容極有可能不完整、不正確。所以必須由公司內部製作特定語系的版本，讓客戶可以在網站中做語言切換的功能。過往可能會搭配後端 + 網址參數來回傳特定版本的 `HTML`，類似這種有參數的網址出現，才能達成多語系切換。而 Vue I18n 則可以在完全不動到網址的前提下，做語系的切換，以下就來介紹使用方法吧!

## 引入套件
[Vue](https://vuejs.org/)
[Vue I18n](https://kazupon.github.io/vue-i18n/)
``` HTML
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script src="https://unpkg.com/vue-i18n/dist/vue-i18n.js"></script>
```

## 建立專案內容
本次專案結構相當簡易，只需 `HTML`、`CSS`、`JS` 三支檔案就好。
會不使用 Vue-Cli 引入的原因是 `Vue I18n` 會在一開始就先引入並使用，而其他套件(ex:`Swper.js`)在其後引入也不會出現問題，所以沒有雷點就直接按照官方文件即可。
HTML 直接使用官方模板，跟簡單做一下切換按。
``` HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>vue-i18n-sample</title>
  <link rel="stylesheet" href="https://unpkg.com/swiper/css/swiper.min.css">
  <link rel="stylesheet" href="./all.css">
  <script src="https://unpkg.com/swiper/js/swiper.min.js"></script>
</head>

<body>
  <div id="app">
    <!-- Swiper -->
    <div class="swiper-container">
      <div class="swiper-wrapper">
        <div class="swiper-slide">Slide 1</div>
        <div class="swiper-slide">Slide 2</div>
        <div class="swiper-slide">Slide 3</div>
      </div>
    
      <div class="swiper-button-prev"></div>
      <div class="swiper-button-next"></div>
    
      <div class="swiper-scrollbar"></div>
    </div>
    <!-- Swiper -->

    <!-- 切換語言 -->
    <input type="button" value="tw" class="switchLan">
    <input type="button" value="en" class="switchLan">
    <input type="button" value="ja" class="switchLan">
    <!-- 切換語言 -->

    <p>{{ $t("message.hello") }}</p>

  </div>
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script src="https://unpkg.com/vue-i18n/dist/vue-i18n.js"></script>
  <script src="./all.js"></script>
</body>
</html>
```

JS 的部分就要注意囉!
1. 引入語言包，可以使用 `JSON` 檔來製作，並搭配其他編譯打包工具 `import` 進來。
2. `new Vue({ i18n }).$mount('#app')` 必須比其他 `new XXX()` 寫法更早執行。
3. 第2點就是本次不使用 Vue-Cli 的原因，畢竟會在 `main.js` 最先引入，而其他套件則會在元件內引入，所以就不會有問題勒。
``` JavaScript
/* 不能比 new Vue({ i18n }).$mount('#app') 還先執行 */
/* 否則會無法輪播呦，但會切換語系 */
// var mySwiper = new Swiper('.swiper-container', {
//   direction: 'horizontal',
//   loop: true,
//   navigation: {
//     nextEl: '.swiper-button-next',
//     prevEl: '.swiper-button-prev',
//   },
// }) 

/* 定義語言包物件 */
const messages = {
  tw: {
    message: {
      hello: '您好'
    }
  },
  en: {
    message: {
      hello: 'hello world'
    }
  },
  ja: {
    message: {
      hello: 'こんにちは、世界'
    }
  }
}
/* 預設語系 */
let locale = localStorage.getItem('locale') || 'tw'

/* 建立 VueI18n 實體 */
const i18n = new VueI18n({
  locale,
  messages,
})

/* 必須比其他 JS 套件更前面就執行 */
new Vue({ i18n }).$mount('#app')

/* 切換網switchLang站語系 */
function switchLang () {
  locale = this.value;
  i18n.locale = locale
  localStorage.setItem('locale', locale)
}

const buttons = Array.from(document.querySelectorAll('.switchLan'));
buttons.forEach((button) => {
  button.addEventListener('click', switchLang);
});

var mySwiper = new Swiper('.swiper-container', {
  direction: 'horizontal',
  loop: true,
  navigation: {
    nextEl: '.swiper-button-next',
    prevEl: '.swiper-button-prev',
  },
})
```
``` CSS
.swiper-container {
  width: 600px;
  height: 300px;
  background-color: skyblue;
}  
```

## 結尾 Demo
依照上面參考範例打開 `Web server` 就可以同時執行輪播以及切換語系囉。
[Vue - 使用 Vue I18n 打造多國語系網站環境](https://syj0905.github.io/vue-i18n-sample)

## 參考資料
[VUE+VUE i18n 讓HTML靜態網頁，也支援多國語言](https://www.minwt.com/webdesign-dev/js/20464.html)
[使用 vue-i18n 打造多國語系網站環境](https://dotblogs.com.tw/wasichris/2018/05/12/012517)