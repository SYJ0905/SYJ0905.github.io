---
title: axios - 解決 x-www-form-urlencoded 傳輸格式問題
date: 2020-03-08
tags: 
  - JavaScript
  - axios
  - w3HexSchool
categories: axios
description: 有些 API 是要使用 form-urlencoded 的格式傳輸資料，但 axios 所傳輸的是 json 格式，本篇將解說該如何轉換兩種格式。
---
## 前言
原先跟公司後端搭配都是使用 `JSON` 格式在傳遞資料，直到有一支 `API` 跟 `Google OAuth` 牽扯上。總而言之，就是要使用 `form-urlencoded` 來傳資料，也就會產生 `axios` 格式轉換問題哩。

## JSON 與 x-www-form-urlencoded
`form-urlencoded` 在表單傳輸是很常見的操作方式，通過 `&` 、 `=` 傳遞資訊。
`JSON` 是以陣列物件的形式在傳遞資訊
``` JavaScript
// x-www-form-urlencoded
Content-Type: application/json;charset=utf-8
firstName=Jeremy&lastName=&age=18

// JSON
Content-Type: application/x-www-form-urlencoded;charset=utf-8
var obj = {
  name : 'Cloud',
  age : 25,
};
```

## 使用套件
套件名稱 : qs (A querystring parser with nesting support)
[qs github](https://github.com/ljharb/qs)
[qs npm](https://www.npmjs.com/package/qs)
輸入安裝指令
```
npm install qs -S
```

## 引入套件
官方有提供 `require()` 引入方式，可參考官網作法。
本次是以 `Vue Cli` 來引入套件，在 `app.js` 加入以下程式碼:
``` JavaScript
import Qs from 'qs';

Vue.prototype.Qs = Qs;
```

## 使用方式
如果 `json` 格式只有一層的話就直接轉換即可，若是有多層的情況，則需要先使用 `JSON.stringify()` 轉換後再使用 `qs` 轉換。 
``` JavaScript
const obj_1 = {
  firstName: 'Cloud',
  lastName: 'Su',
  age: '25',
};
/* 正確方式 */
console.log(this.Qs.stringify(obj_1));

const obj_2 = {
  person: {
    firstName: 'Cloud',
    lastName: 'Su',
    age: '25',
  }
};
/* 正確方式 */
console.log(
  this.Qs.stringify({
    person: JSON.stringify(obj_2.person),
  })
);
```
轉換好之後，就可以使用 `axios` 送出這份 `x-www-form-urlencoded` 的資料囉。

## 結尾
我想應該會越來越多 API 都使用 `json` 格式傳送資料，`form-urlencoded` 格式也許會漸漸式微吧。

## 參考資料
[[axios] 處理 x-www-form-urlencoded 格式問題](https://jeremysu0131.github.io/axios-%E8%99%95%E7%90%86-x-www-form-urlencoded-%E6%A0%BC%E5%BC%8F%E5%95%8F%E9%A1%8C/)