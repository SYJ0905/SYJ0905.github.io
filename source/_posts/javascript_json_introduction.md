---
title: JavaScript 核心 (27) - 物件 - JSON
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 接下來介紹常見資料格式 JSON
abbrlink: 2776902226
date: 2021-01-04 16:45:00
---
## 物件 VS JSON

[MDN JSON](https://zh.wikipedia.org/wiki/JSON)
JSON 與物件寫法類似，定義上是屬於資料格式。
實際上與 JavaScript 並沒有關係。

``` JavaScript
const a = {
  name: 'Ray',
  fn: 'SayHello',
};
```

``` JSON
{
  "name":"Ray",
  "fn":"SayHello"
}
```

JSON 主要特性:

* 必定為字串格式
* 最後一個不可有逗號
* 採用雙引號而非單引號

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(32)-物件-JSON](https://hsiangfeng.github.io/javascript/20201112/8535/)
