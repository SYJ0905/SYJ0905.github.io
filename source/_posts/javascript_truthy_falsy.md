---
title: JavaScript 核心 (17) - 運算子、型別與文法 -  Truthy 與 Falsy
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 真假值常用於判斷式中，與前面提到的型別轉換沒有關聯
abbrlink: 309252186
date: 2020-12-24 15:00:00
---
## Truthy 與 Falsy

`truthy`（真值）指的是在布林值上下文中，轉換後的值為真的值。所有值都是真值，除非它们被定義為`假值`（即除 false、0、""、null、undefined 和 NaN 以外皆為真值）。

可參考[真假值表](https://dorey.github.io/JavaScript-Equality-Table/)

``` JavaScript
if(10) {
  console.log('執行程式'); /* 會出現這一行字 */
}

10 == true; /* false */
```

![真假值表](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/JavaScript%20%E6%A0%B8%E5%BF%83%20(17)%20-%20%E9%81%8B%E7%AE%97%E5%AD%90%E3%80%81%E5%9E%8B%E5%88%A5%E8%88%87%E6%96%87%E6%B3%95%20-%20%20Truthy%20%E8%88%87%20Falsy%2F%E7%9C%9F%E5%81%87%E5%80%BC%E8%A1%A8.jpg?alt=media&token=90d92b5f-1779-4500-bacb-e8e612e3261f)

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(18)-運算子、型別與文法-Truthy 與 Falsy](https://hsiangfeng.github.io/javascript/20200628/2353666308/)
