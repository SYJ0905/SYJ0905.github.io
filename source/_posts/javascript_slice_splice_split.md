---
title: JavaScript - slice()、splice()、split() 詳細介紹
date: 2020-03-22
tags: 
  - JavaScript
  - w3HexSchool
categories: JavaScript
description: 本篇將介紹 slice()、splice()、split() 三種常見的 Array、String 處理方法。
---
## 目標對象
* slice(): `Array` 及 `String`
* splice(): `Array`
* split(): `String`

## 功能說明
### slice()
  複製開始與結束點（結束點不算）中的內容
  ``` JavaScript
  arr.slice()
  arr.slice(begin) /* 含 end 項 */
  arr.slice(begin, end) /* 包含 begin項 但不包含 end 項 */
  ```
  `begin` 為開始的索引值，若為 `負數` 則從後面算起。
  `end` 為結束的索引值，若無填寫則直接預設為最後一項。
  以下是參考用法:
  ``` JavaScript
  const game = ['PS4', 'Xbox', 'Switch', 'N3DS'];
  const game_1 = game.slice(1);
  const game_2 = game.slice(1, 2);
  const game_3 = game.slice(-3);

  // game contains ['PS4', 'Xbox', 'Switch', 'N3DS']
  // game_1 contains ['Xbox', 'Switch', 'N3DS']
  // game_2 contains ['Xbox', 'Switch']
  // game_3 contains ['Xbox', 'Switch', 'N3DS']

  const game_string = 'PS4XboxSwitch';
  const game_string_1 = game_string.slice(1);
  const game_string_2 = game_string.slice(1, 2);
  const game_string_3 = game_string.slice(-3);

  // game_string_1 contains S4XboxSwitch
  // game_string_2 contains S
  // game_string_3 contains tch
  ```

### splice()
  將原 `Array` 置換項目，並回傳被置換的項目。
  ``` JavaScript
  array.splice(start)
  array.splice(start, deleteCount)
  array.splice(start, deleteCount, item1, item2, ...)
  ```
  `start` 置換項目的位置，負數代表從後方算起。
  `deleteCount` 置換的個數，如為 0 則不會置換。
  `item` 添加的新項目。
  以下是參考用法:
  ``` JavaScript
  var game_1 = ['PS4', 'Xbox', 'Switch', 'N3DS'];
  var game_removed_1 = game_1.splice(2, 1, 'PC');

  // game_1 = ['PS4', 'Xbox', 'PC', 'N3DS'];
  // game_removed_1 is ['Switch']

  var game_2 = ['PS4', 'Xbox', 'Switch', 'N3DS'];
  var game_removed_2 = game_2.splice(-2, 2, 'PC');

  // game_2 = ['PS4', 'Xbox', 'PC'];
  // game_removed_2 is ['Switch', 'N3DS']

  var game_3 = ['PS4', 'Xbox', 'Switch', 'N3DS'];
  var game_removed_3 = game_3.splice(2, 1);

  // game_3 = ['PS4', 'Xbox', 'N3DS'];
  // game_removed_3 is ['Switch']
  ``` 

### split()
  將 `String` 依照規則區分，並放入 `Array` 內
  ``` JavaScript
  stringObject.split(separator,howmany)
  ```
  `separator` 自訂字串符或正則表達式，從該參數指定的地方分割 `String`。
  `howmany` 返回值的最大長度，超過該長度則不顯示。
  以下是參考用法:
  ``` JavaScript
  var str = "How are you ?"
  var splits_1 = str.split(" ");
  var splits_2 = str.split("");
  var splits_3 = str.split(" ",3);

  //splits1 contains ["How", "are", "you", "?"]
  //splits2 contains ["H", "o", "w", " ", "a", "r", "e", " ", "y", "o", "u", " ", "?"]
  //splits3 contains ["How", "are", "you"]
  ```


## 參考資料
[Array.prototype.slice()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)
[Array.prototype.splice()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)
[String.prototype.split()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/split)