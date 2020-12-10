---
title: JavaScript - 實現 input file 圖片預覽功能
tags:
  - JavaScript
  - w3HexSchool
categories:
  - JavaScript
description: 本篇將介紹如何將 input file 的圖片檔案顯示出來。
abbrlink: 4258008084
date: 2020-04-26 00:00:00
---
## 前言

最近在負責公司後台的管理系統，有一個需求是需要上傳本地端圖片，但同時也必須在加入圖片時就顯示出來讓管理者預覽，以下就跟我一起來時做看看吧。

## 模板設定

基本的 HTML、CSS 請參考以下範例

``` HTML
<input type='file' onchange="readURL(this);" />
<img id="blah" src="http://placehold.it/180" alt="your image" />
```

``` CSS
img{
  max-width:180px;
}
input[type=file] {
  padding:10px;
  background:#2d2d2d;
}
```

## FileReader 使用

藉由 `FileReader` 物件，瀏覽器能以非同步的方式讀取再用戶端的檔案內容，可以使用 File、Blob 物件指定要讀取的資料
[FileReader MDN](https://developer.mozilla.org/zh-TW/docs/Web/API/FileReader)
以下就是如何透過 `onchange` 是觸發預覽功能範例

``` JavaScript
function readURL(input) {
  console.log(input);
  if (input.files && input.files[0]) {
    var reader = new FileReader();
    console.log(reader);

    reader.onload = function (e) {
      console.log(e);
      $('#blah').attr('src', e.target.result);
    };

    reader.readAsDataURL(input.files[0]);
  }
}
```

理論上這時候就可以測試將圖片加入，若有正常預覽代表成功囉!!
`FileReader` 本身有其他 API 功能，就看各位的需求是什麼在調整即可。

## 參考資料

[FileReader MDN](https://developer.mozilla.org/zh-TW/docs/Web/API/FileReader)
[How To Display Uploaded Image In Html Using Javascript ?](https://www.webtrickshome.com/faq/how-to-display-uploaded-image-in-html-using-javascript)
