---
title: JavaScript 核心 (1) - 執行環境與作用域 - JavaScript 運作方式
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 重新了解 JavaScript 的運作模式
abbrlink: 2070232557
date: 2020-12-21 12:16:00
---
## 直譯語言 Interperted language

直接編譯的語言。
直譯式語言必須先一條一條將程式碼讀取出來並透過`直譯器`轉換成`機器碼`才能夠被運作，所以通常來講直譯式語言的錯誤訊息都是直接呈現於開發環境上，舉例來講 JavaScript 就是直接呈現在瀏覽器的 console Tools 中。

直譯語言列表:

* BASIC
* LISP
* Perl
* Python
* Ruby
* JavaScript
* PHP
* R

![運作流程](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/JavaScript%20%E6%A0%B8%E5%BF%83%20(1)%20-%20%E5%9F%B7%E8%A1%8C%E7%92%B0%E5%A2%83%E8%88%87%E4%BD%9C%E7%94%A8%E5%9F%9F%20-%20JavaScript%20%E9%81%8B%E4%BD%9C%E6%96%B9%E5%BC%8F%2F%E7%9B%B4%E8%AD%AF%E8%AA%9E%E8%A8%80%E9%81%8B%E4%BD%9C.jpg?alt=media&token=29b8f72f-42f4-458a-9c97-031c4752818d)

## 編譯式語言 Compiled language

是以編譯器，先將程式碼編譯為機器碼，再加以執行。由於已經在預先編譯，當遇到問題時就可以預先除錯，這就是編譯式語言的好處，通常來講效能也會比較好。

![運作過程](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/JavaScript%20%E6%A0%B8%E5%BF%83%20(1)%20-%20%E5%9F%B7%E8%A1%8C%E7%92%B0%E5%A2%83%E8%88%87%E4%BD%9C%E7%94%A8%E5%9F%9F%20-%20JavaScript%20%E9%81%8B%E4%BD%9C%E6%96%B9%E5%BC%8F%2F%E7%B7%A8%E8%AD%AF%E8%AA%9E%E8%A8%80%E9%81%8B%E4%BD%9C.jpg?alt=media&token=7b51be80-95e5-4558-93fb-02ea6eba55a5)

編譯語言列表:

* C++
* Objective-C
* C#

## JavaScript 運作過程

前面提到 JS 是屬於直譯式語言，需透過直譯器`轉譯`成機器碼才能夠執行，而這個轉換過程分成以下三個階段:

![JavaScript 轉換過程](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/JavaScript%20%E6%A0%B8%E5%BF%83%20(1)%20-%20%E5%9F%B7%E8%A1%8C%E7%92%B0%E5%A2%83%E8%88%87%E4%BD%9C%E7%94%A8%E5%9F%9F%20-%20JavaScript%20%E9%81%8B%E4%BD%9C%E6%96%B9%E5%BC%8F%2FJS%20%E8%BD%89%E8%AD%AF%E9%81%8E%E7%A8%8B.jpg?alt=media&token=b7c9e0cf-cabe-4d8c-9eb5-2c483f208edd)

[Esprima](https://esprima.org/demo/parse.html) 這是用來了解語法基本單元化以及抽象結構樹的小工具

* 語法基本單元化: 透過逐行逐字的分析程式碼，`尚未定義完成`
* 抽象結構樹: 將原始碼定義完成，`尚未運行`
* 代碼生成: 生成機器碼，`運行程式碼`

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(1)-執行環境與作用域-JavaScript 運作方式](https://hsiangfeng.github.io/javascript/20200307/1405700237/)
