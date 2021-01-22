---
title: JavaScript 核心 (40) - 繼承與原型鍊 - 原型鍊的概念 - 為什麼有原型
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 本篇介紹 JS 中相當底層的原型起源
abbrlink: 1980326624
date: 2021-01-22 12:00:00
---
## 原型

諸多 `OOP` 物件導向的程式語言中常會有這種原型功能
可以理解成 創建一個 `類別`，並賦予這個類別有哪些功能、屬性等等
而利用這個 `類別` 則可以創造出多種相似的實體出來
![物件導向](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/JavaScript%20%E6%A0%B8%E5%BF%83%20(40)%20-%20%E7%B9%BC%E6%89%BF%E8%88%87%E5%8E%9F%E5%9E%8B%E9%8D%8A%20-%20%E5%8E%9F%E5%9E%8B%E9%8D%8A%E7%9A%84%E6%A6%82%E5%BF%B5%20-%20%E7%82%BA%E4%BB%80%E9%BA%BC%E6%9C%89%E5%8E%9F%E5%9E%8B%2F%E6%88%AA%E5%9C%96%202021-01-17%2021.21.51.png?alt=media&token=4dac17f6-3c42-4c1d-a7ba-9cb97d085a85)

![創建實體](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/JavaScript%20%E6%A0%B8%E5%BF%83%20(40)%20-%20%E7%B9%BC%E6%89%BF%E8%88%87%E5%8E%9F%E5%9E%8B%E9%8D%8A%20-%20%E5%8E%9F%E5%9E%8B%E9%8D%8A%E7%9A%84%E6%A6%82%E5%BF%B5%20-%20%E7%82%BA%E4%BB%80%E9%BA%BC%E6%9C%89%E5%8E%9F%E5%9E%8B%2F%E6%88%AA%E5%9C%96%202021-01-17%2021.32.14.png?alt=media&token=f67eca50-21dd-461f-b350-7864ce8060f0)

## JavaScript 原型

JavaScript 根本上是一個物件，任何內容均是以物件方式建立，就沒有所謂的 `class 類別`概念，所以是採用 `原型繼承` 的方式做出類似 class 的功能。
ES6 中有 `class 語法糖`可以使用，但根本上與其他語言的 `class` 是不一樣的

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(47)-繼承與原型鍊-原型鍊的概念 - 為什麼有原型](https://hsiangfeng.github.io/javascript/20210117/3096588885/)
