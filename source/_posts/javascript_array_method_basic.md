---
title: JavaScript - 常見陣列方法(基礎篇)
date: 2020-05-10
tags: 
  - JavaScript
  - w3HexSchool
categories: JavaScript
description: 本篇會介紹幾種比較常用的陣列方法，不再只是用迴圈加判定的方式來操作陣列，可以大幅的減少程式碼以及整體效能。
---
## 前言
JavaScript 陣列方法有十幾種操作，我會依照使用次數以及難易程度分成三篇來介紹。
## 陣列分類方法
此表格會在後續的陣列介紹中陸續加入，此處只標註本篇會介紹的方法
<table>
  <thead>
    <tr>
        <th style="width:150px">分類</th>
        <th>操作方法</th>
    </tr>
  </div>
  <tbody>
    <tr>
        <td>改變原始陣列</td>
        <td></td>
    </tr>
    <tr>
        <td>回傳特定資訊</td>
        <td>
          <a href="#filter">filter()</a>、
          <a href="#find">find()</a>
        </td>
    </tr>
    <tr>
        <td>處理每個元素</td>
        <td>
          <a href="#forEach">forEach()</a>
        </td>
    </tr>
    <tr>
        <td>產生新陣列or值</td>
        <td>
          <a href="#map">map()</a>、
          <a href="#reduce">reduce()</a>
        </td>
    </tr>
    <tr>
        <td>回傳布林值</td>
        <td>
          <a href="#every">every()</a>、
          <a href="#some">some()</a>
        </td>
    </tr>
    <tr>
        <td>其餘用法</td>
        <td></td>
    </tr>
  </div>
</table>

## forEach()
會將陣列中每個元素套用到指定的函式裡進行運算，函式有三個參數，第一個參數表示每個元素的值(必填)，第二個參數為該元素的索引值(選填)，第三個參數則表示原本的陣列(選填)。
其實很多方法都可以透過 `forEach()`與 `if else` 等判斷方法來達成。，但程式碼就很冗長以及效能較低。
``` JavaScript
let a = [1,2,3,4,5];
let b = 0;
a.forEach((item, index, array) => {
    b = b + item;
});
console.log(b); /* 15 ( 1+2+3+4+5 ) */
```
## find()
會將陣列中的「每一個」元素帶入指定的函式內做`判斷`，並會回傳`第一個`符合判斷條件的元素，如果沒有元素符合則會回傳 `undefined`。
注意，`find()` 只會回傳一次值，且是第一次為 `true` 的`值`。
``` JavaScript
let a = [1,2,3,4,5,6,7,8];
console.log(a.find((item, index, array) => {
  return item > 3;
})); /* 4 只回傳第一個為 ture 的值 */
console.log(a.find((item, index, array) => {
  return item < 0;
})); /* undefined */
```
## filter()
會將陣列中的「每一個」元素帶入指定的函式內做判斷，如果元素符合判斷條件則會傳出，成為一個`新的陣列元素`。
應用: 很適合用在搜尋符合條件的資料。
``` JavaScript
let a = [1,2,3,4,5,6,7,8];
console.log(a.filter((item, index, array) => {
  return item > 3;
}));  /* [4, 5, 6, 7, 8] */
console.log(a.filter((item, index, array) => {
  return item%2 == 0
})); /* [2, 4, 6, 8] */
```
## map()
處理陣列中每個元素，透過函式內所回傳的值組合成一個陣列。
註:回傳陣列的長度`等於`原始陣列長度，若是不回傳則會預設填入 `undefined`。
應用: 將原始的變數運算後重新組合一個新的陣列。
``` JavaScript
let a = [1,2,3,4,5,6,7,8];
let b = a.map((item, index, array) => {
    return item + 10;
});
console.log(b); /* [11, 12, 13, 14, 15, 16, 17, 18] */
```
## every()
可以檢查所有的元素是否符合條件，只要有任何一個元素`不符合判斷條件`，會回傳 `false`，如果全部符合，就會回傳 `true`。
``` JavaScript
let a = [1,2,3,4,5,6];
console.log(a.every((item, index, array) => {
  return item > 3;
})); /* fasle */
console.log(a.every((item, index, array) => {
  return item > 0;
})); /* true */
```
## some()
可以檢查所有的元素是否符合條件，只要有任何一個元素`符合判斷條件`，就會回傳 `true`，如果全都不符合，就會回傳 `false`。
``` JavaScript
let a = [1,2,3,4,5,6];
console.log(a.some((item, index, array) => {
  return item > 3;
})); /* true 4 5 6 大於 3 */
console.log(a.some((item, index, array) => {
  return item > 6;
})); /* false 沒有元素大於 6 */
```
## reduce()
可以將陣列中每個元素進行計算，每次計算的結果會再與下個元素作計算，直到結束為止。
``` JavaScript
let a = [1,2,3,4,5,6,7,8];
let b = a.reduce((accumulator, currentValue, currentIndex, array) => {
  console.log(accumulator, currentValue);
  return accumulator + currentValue;
});
console.log(b); /* 36 ( 1+2+3+4+5+6+7+8=36 ) */
```
## 結尾
基礎篇的陣列操作技巧對於中、小型專案而言其實就足以應付，下篇開始會介紹進階一點的方法，一起來學習更多陣列技巧吧。
## 參考資料
[JavaScript 陣列處理方法 [filter(), find(), forEach(), map(), every(), some(), reduce()]](https://wcc723.github.io/javascript/2017/06/29/es6-native-array/#Array-prototype-every)
[JavaScript Array 陣列操作方法大全 ( 含 ES6 )](https://www.oxxostudio.tw/articles/201908/js-array.html#array_reduce)
[Array MDN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array)