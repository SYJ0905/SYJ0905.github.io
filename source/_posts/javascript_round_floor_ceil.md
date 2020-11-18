---
title: JavaScript - round()、floor()、ceil() 詳細介紹
tags:
  - JavaScript
  - w3HexSchool
categories:
  - JavaScript
description: 本篇將介紹 round()、floor()、ceil() 三種常見的小數值捨入為整數的方法
abbrlink: 3859167508
date: 2020-05-03 00:00:00
---
## 目標對象
參數型別可以是 `number`、`string` 的數字

## 功能說明
### round()
  如果小數位的部分值大於 0.5, 這個值將會進位. 如果小數位的部分值小於 0.5, 這個值將不會進位.
  ``` JavaScript
  // Returns the value 20
  x = Math.round(20.49);

  // Returns the value 21
  x = Math.round(20.5);

  // Returns the value -20
  x = Math.round(-20.5);

  // Returns the value -21
  x = Math.round(-20.51);
  ```

### floor()
  函式會回傳小於等於所給數字的最大整數。
  ``` JavaScript
  Math.floor( 45.95); //  45
  Math.floor( 45.05); //  45
  Math.floor(  4   ); //   4
  Math.floor(-45.05); // -46 
  Math.floor(-45.95); // -46
  ``` 

### ceil()
  函式會回傳大於等於所給數字的最小整數。
  ``` JavaScript
  console.log(Math.ceil(.95));
  // expected output: 1

  console.log(Math.ceil(4));
  // expected output: 4

  console.log(Math.ceil(7.004));
  // expected output: 8

  console.log(Math.ceil(-7.004));
  // expected output: -7
  ```


## 參考資料
[Math.round()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Math/round)
[Math.floor()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Math/floor)
[Math.ceil()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Math/ceil)