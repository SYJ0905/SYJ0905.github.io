---
title: JavaScript 核心 (37) - 函式以及 This 的運作 - this：DOM
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 來談談 this 與 DOM 的關係
abbrlink: 497532059
date: 2021-01-18 10:00:00
---
## DOM

試著在按鈕上綁定事件後看看 this 是誰?

``` HTML
<!-- addEventListener -->
<button type="button" id="btn">送出</button>
<!-- 直接綁在按鈕上 -->
<button type="button" onclick="console.log(this)">送出</button>
```

``` JavaScript
var btn = document.getElementById('btn');
btn.addEventListener('click', function() {
  console.log(this);
})
```

上述 `this 會指向 DOM`

## 搭配 bind()

如果希望 this 不是指向 DOM，而是由我們決定的話，可以使用 bind() 來賦予 this。

``` JavaScript
var obj = {
  name: 'Ray'
}
var btn = document.getElementById('btn');

function fn() {
  console.log(this);
}
btn.addEventListener('click', fn.bind(obj));
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(43)-函式以及 This 的運作-this：DOM](https://hsiangfeng.github.io/javascript/20210110/3064157407/)
