---
title: Vue - 我們為什麼要使用 Vue，Vue 究竟解決了哪些問題?
tags:
  - Vue
categories:
  - Vue
description: 本篇介紹為什麼要使用 Vue，以及 Vue 究竟解決了哪些問題?
abbrlink: 1916550834
date: 2021-06-28 22:00:00
---
## 為什麼要學框架?

框架作為一個工具，是用來幫助我們更好的處理網頁複雜度問題

## 三大框架之選擇

* Angular：Angular 期望做的事情非常多，比如說它會包含著自己的路由，這讓我們決定去使用 Angular 的時候，就必須要接受它的全部，也讓學習成本提高，與此同時選擇會變得更少，不過這同時也是 Angular 的優點
* React & Vue: 基本上兩者都專注在視圖層(可以理解成 UI 畫面)，而其他的所有一切都會有各種配套的工具，比如說路由、狀態管理工具，所以說他們可以依照各自的需求來使用配套工具，此方式也會讓學習曲線相對平緩

## Vue 的特點

### MVVM 框架

  所謂 MVVM 框架就是 `Model-View-ViewModel` 的設計模式
  Vue 正是使用了 MVVM 的框架形式，並且通過 `聲明式渲染(或稱宣告式渲染)` 和 `響應式數據綁定(或稱雙向綁定)` 的方式來幫助我们完全避免了對 DOM 的操作。
  <註>原生 JS 操作 DOM 為 `指令式渲染`

### 單頁面應用程序(SPA)

  整個網站應用就只有一個頁面，當這一個單頁面被加載進來之後，就不會在進行關於頁面的網路請求。Vue 配合生態圈中的 Vue-Router 就可以非常方便的開發複雜的單頁應用。

### 輕量化與易學習

  我们知道網頁中引入的 JS 體積越大，那麼加載所需要耗費的時間就越長，反之體積越小，則越節省時間。所以我们會更傾向使用體積更小的 JS 文件。
  目前 Vue 的最新穩定版本为 2.6.14，生產版本只有 33.46KB 的大小，幾乎不會對我們的的網頁加載速度產生影響。同時因為 Vue 只關注視圖層，單獨的 Vue 就像一個 library，所以使我們的學習成本變得非常低

### 漸進式與兼容性

  漸進式意味著 Vue 只做份內的事，不會要求太多。
  前面提到 Vue 只關注視圖層，不僅易於上手，還便於與其生態系工具(Vue-Router)及第三方 library 做整合，這就讓 Vue 擁有很大程度的兼容性。

### 視圖組件化(元件化)

  將網頁元素拆分成元件，Vue 利用元件來去拼裝成一個頁面，每個元件都是一個可複用的 Vue 實例，元件內有自身的數據、視圖、以及程式碼邏輯。

### Virtual DOM

  Virtual DOM 也就是虛擬 DOM，大家知道瀏覽器去處理 DOM 操作時，是存在效能問題的，這也是我们在使用 jQuery 或者原生 JavaScript 來去頻繁操作 DOM 進行數據渲染的时候，我们的頁面經常出現卡頓的原因。
  而 Virtual DOM 則是預先通過 JS 的 Diff 運算，把最終生成的 DOM 計算出來，並進行優化，在計算出來之後才會將 DOM 放到我們的 DOM 樹中。由於這種操作並沒有進行真實的 DOM 操作，所以才會稱為虛擬 DOM。

## 參考資料

[重新認識 Vue.js | Kuro Hsu](https://book.vue.tw/CH1/1-1-introduction.html)

[Why Vue.js? 我能不要用他嗎？](https://ithelp.ithome.com.tw/articles/10213438)

[为什么要用vue.js？](https://www.html.cn/qa/vue-js/16084.html)

[我們為什麼要用vue，他解決了什麼問題，如何使用它？](https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/535450/#outline__1_4)

[深入現代前端開發](https://f2e.kalan.dev/frontend-ui-development/10.html#%E5%85%B6%E4%BB%96%E9%81%B8%E6%93%87)

[为什么那么多前端都选择用 Vue.js框架？](https://segmentfault.com/a/1190000023459214)

[Vue 的 Virtual Dom](https://medium.com/@paulyang1234/vue-%E7%9A%84-virtual-dom-af44f4394120)
