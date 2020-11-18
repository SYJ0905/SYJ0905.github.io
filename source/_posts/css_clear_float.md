---
title: '什麼!! overflow:hidden 清除浮動'
tags:
  - CSS
categories:
  - CSS
description: '想不到清除浮動除了 clearboth 以外，還有 overflow:hidden !!'
abbrlink: 1889954039
date: 2019-11-06 00:00:00
---
## 前言
`overflow: hidden` 常用在隱藏溢出的範圍，也就是子層高度大於複層高度時會將超出部分隱藏。
然而，還有另一個用途就是清除包含子層的浮動。

## 示範模板
```
<body>
  <div class="parent">
    <div class="child1"></div>
    <div class="child2"></div>
  </div>
</body>
```
```
.parent {
  width: 300px; 
  background: #ddd; 
  border: 1px solid;
  /* overflow: hidden; // 試著加入看看，浮動是否會被清除 */
} 
.child1 { 
  width: 100px; 
  height: 100px; 
  background-color: pink;
  float: left;
}
.child2 { 
  width: 200px; 
  height: 50px; 
  background-color: red;
}
```
你沒看錯，當加了 `overflow: hidden` 後，竟然就可以清除浮動了!!這是什麼妖術阿?!

## 解析
### BFC
BFC (Block Formatting Context)，塊格式化上下文
[MDN-塊格式上下文](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)
塊格式化上下文包含創建它的元素內部的所有內容
浮動定位和清除浮動時只會應用於同一個 BFC 內的元素。浮動不會影響其它 BFC 中元素的佈局，而清除浮動只能清除同一 BFC 中在它前面的元素的浮動。
外邊距折疊（Margin collapsing）也只會發生在屬於同一 BFC 的塊級元素之間。
### BFC 創建
請參考 MDN 文件即可，這裡就不多寫了。
### 應用
EX: 遇到需要清除浮動的情況產生時，這時候只需要建立一個 BFC 來包含這個浮動即可。
EX: 外邊距塌陷，此情況常發生在同一層的兩元素都有 margin-top 及 margin-bottom 時，當重疊時則會發現 margin 發生合併，這是因為兩者都同屬一個 BFC，此時只需要將兩者分離，並創建一個 BFC，就可以解決問題囉!!

