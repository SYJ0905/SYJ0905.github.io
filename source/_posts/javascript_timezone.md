---
title: JavaScript - 取得各國日期與時間
tags:
  - JavaScript
categories:
  - JavaScript
description: 使用原生 JS 取得各國時間製作相關應用
abbrlink: 3751349744
date: 2019-12-02 00:00:00
---
## 取得本地日期與時間
* `Date.prototype.toLocaleString()` : 取得本地的日期與時間
```
// 建立 Date 物件再使用 toLocaleString 方法
var date = new Date().toLocaleString();
console.log(date);  // "2019/12/2 上午9:38:59"
```
* `Date.prototype.toLocaleDateString()` : 取得本地的日期
```
// 建立 Date 物件再使用 toLocaleDateString 方法
var date = new Date().toLocaleDateString();
console.log(date);  // "2019/12/2"
```
* `Date.prototype.toLocaleTimeString()` : 取得本地的時間
```
// 建立 Date 物件再使用 toLocaleTimeString() 方法

var date = new Date().toLocaleTimeString();
console.log(date);  // "上午9:57:13"
```

## 取得其他國家的日期和時間
### 加入 locales, options 參數
`Date.prototype.toLocaleString([locales[, options]])`
```
var options = {
  // day: 'numeric',    // 十位數有 0 不顯示 
  // month: 'long',     // 完整月份
  // year: 'numeric',   // (e.g., 2019)
  // hour: '2-digit',   // (e.g., 02)
  // minute: '2-digit', // (e.g., 02)          
  hour12: false,     // 24 小時制
  timeZone: 'America/New_York' // 美國/紐約
};
var date = new Date().toLocaleString('zh-TW', options);
console.log(date); // 2019/12/1 21:29:13
```
* 註: options 前五項如果有加入的話會顯示 xxxx年xx月xx日，如果之後有需要個別拆分的話用 `split()` 會有點麻煩，所以一般我都只開顯示 24 小時制跟時區就好，畢竟 `split('/')` 就可以將年、月、日拆出來使用，相當簡潔有力呢!!
```
var options = {       
  hour12: false,     // 24 小時制
  timeZone: 'America/New_York' // 美國/紐約
};
var date = new Date().toLocaleString('zh-TW', options);
var dateStr = date.split(' ')[0];
var timeStr = date.split(' ')[1];
var yaer = dateStr.split('/')[0];
var month = dateStr.split('/')[1];
var day = dateStr.split('/')[2];
console.log(date);    // 2019/12/1 21:39:48
console.log(dateStr); // 2019/12/1
console.log(timeStr); // 21:39:48
console.log(yaer, month, day); // 2019 12 1
```

## 參考資料
* [[MDN] Date.prototype.toLocaleString()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleString)
* [List of Time Zones](https://timezonedb.com/time-zones)