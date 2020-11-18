---
title: CSS - span 和 p 標籤的換行或者不換行問題
tags:
  - CSS
categories:
  - CSS
description: 本篇將介紹各種換行相關元素以及中英文換行時所發生的問題。
abbrlink: 1571711147
date: 2020-10-11 00:00:00
---
## 相關參數介紹
### word-break
  [MDN-word-break](https://developer.mozilla.org/zh-CN/docs/Web/CSS/word-break)
  決定單字内的斷句
  * noraml: 默認, 使用瀏覽器的換行規則。
  * break-all: 對於非 CJK(中/日/韓/文)文本，可在任意字符間斷行，中英文夾雜時不斷行。
  * break-word: CJK(中/日/韓)英文夾雜時，CJK 與 英文會斷行。
  * keep-all: CJK 文本不斷行。 Non-CJK 文本表现同 normal 設定
  參考程式碼，可以自己玩玩看
  ``` HTML
  <style>
    span {
      display: inline-block;
      width: 250px;
      word-break: break-all;
    }
  </style>
  <span>測試測試測試測試測試測試測試testtesttesttesttesttest</span>
  <span>測試測試測試測試測試測試測試測試測試測試測試測試測試測試</span>
  ```

### white-space
  [MDN-white-space](https://developer.mozilla.org/zh-TW/docs/Web/CSS/white-space)
  決定如何處理元素內的空白字元
  * normal: 連續的空白字元會被合併(collapse)，換行字元被視為空白字元。換行只在被文字空間限制時發生。
  * pre: 連續的空白字元都會被保留。換行在有換行字元以及 `<br>` 時發生。
  * nowrap: 對待空白字元的方式跟 normal 一樣，且會強制不換行。
  * pre-wrap: 連續的空白字元都會被保留。換行會在換行字元、有 `<br>` 元素以及被文字空間限制時發生。
  * pre-line: 連續的空白字元會被合併(collapse)。換行在換行字元、 `<br>`以及被文字空間限制時發生。
  * inherit: 從父元素繼承 `white-space` 這個属性。

### overflow-wrap(word-wrap)
  [MDN-overflow-wrap](https://developer.mozilla.org/zh-CN/docs/Web/CSS/word-wrap)
  說明當一个不能被分開的字符串太長而不能填充其容器時，為防止其溢出，瀏覽器是否允許這樣的單字中斷换行。
  * normal: 行只能在正常的單字斷點處中斷。（例如兩個單字之間的空格）。
  * break-word: 在實在找不到換行點的时候, 就斷單字換行。

### text-overflow
  [MDN-text-overflow](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-overflow)
  決定不換行時，超出文本該如何顯示
  * clip: 默認值，直接截斷文本。
  * ellipsis: 顯示省略符號来代表被修剪的文本。
  * string: 使用给定的字符串來代表被修剪的文本。
  
## 參考資料
[css里面的span和p标签的换行或者不换行问题](https://blog.csdn.net/icewst/article/details/105209423)
