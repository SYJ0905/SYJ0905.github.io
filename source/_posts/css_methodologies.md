---
title: CSS - 模組化的方法 OOCSS、SMASS、BEM
tags:
  - CSS
categories:
  - CSS
description: 這麼多種規範或是方法存在的目的都是為了讓程式碼易懂、可重複用，有效增加開發效率和後續維護
abbrlink: 2160383962
date: 2019-11-21 00:00:00
---
## OOCSS (Object Oriented CSS)
* 分離結構與樣式 Separation of Structure from Skin : 結構像是元素的大小，樣式則是顏色等。
* 分離 HTML 與 CSS : 盡量將可共用的樣式提取到單獨的 Class 以供使用。
範例:
```
<button class="btn btn-small btn-primary"></button>
```
來說明一下這當中使用了那些 OOCSS 概念
* `btn` : 規範按鈕的預設樣式。
* `btn-small` : 規範按鈕的大小，ex: `btn-large`、`btn-medium`。
* `btn-primary` : 規範按鈕的顏色，ex: `btn-default`、`btn-danger`。

優點: 架構清楚，可經由組合而產生多種樣式結構，使程式碼更精簡與方便管理
缺點: 有可能會出現為了區別樣式而產生不意懂得 Class 名稱，ex: `mt-3`。
個人觀點: 身為 Bootstrap 用戶，真心覺得這種寫法挺棒的。

## SMACSS
* 結構分類 : Base、Layout、Module、State、Theme。
* 明明規則 : id 與 class 受限制使用、並使用 dash 分隔。
結構:
* Base : 網頁基本樣式，包含 CSS Reset。
* Layout : 將網頁切割成不同區塊，若區塊是唯一則使用 id 命名 ex: `#tab`;重複區塊則使用 class 命名 ex: `.tab-default`。
* Module : 同 Layout ，但屬於區塊的內容，只能使用 class 命名，並使用 dash 分隔 ex: `.tab-item`。
* State : 描述元件狀態，ex: `.tab-item active`。
* Theme : 針對主視覺而定義的樣式，ex: `.tab-dark`。

優點: 與 OOCSS 相同
缺點: 結構分類存在模糊界線，就跟我上面自己寫了啥都不是很明白ww
個人觀點: 除了 Base 、 Layout 以外，使用機率幾乎為 0。

## BEM
BEM 是以區塊(Block)、元素(Element)、修飾子(Modifier)來命名
範例: 
```
<ul class="menu">
  <li class="menu__item">首頁</li>
  <li class="menu__item menu__item--active">關於我</li>
  <li class="menu__item">分類</li>
</ul>
```
* Element 使用雙底線分隔，Modifier 使用雙 dash 做分隔
* `menu` 是區塊(Block)
* `menu__item` 是 `menu` 的元件
* `menu__item--active` 是 `menu__item` 的其中一種狀態

優點: 以元件觀念進行開發，具有重用性。沒有 SMACSS 複雜的部分，同時有著 OOCSS 清楚的架構。
缺點: 命名方式過長
個人觀點: BEM 相對其他兩種方式更清楚簡單，並且達到模組化的效果。

## 結尾
任何一種模式都有其優缺點以及適用的時機，並且可以互相搭配使用，達到 1+1 > 2 的效果，後續的維護也更方便，畢竟一開始如果沒有一定規範，那麼之後就是一直還技術債啦www