---
title: parseFloat()、parseInt()、Number() 比較
tags:
  - JavaScript
categories:
  - JavaScript
description: 這三個函式都是在解析傳入的參數，並返回其值。而每個函式的解析規則又不盡相同，本篇就來介紹三者差異。
abbrlink: 4106383168
date: 2020-12-21 00:00:00
---

## parseFloat()

[MDN parseFloat](https:/*developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseFloat)
可解析一個字串，並返回一個浮點數。
`parseFloat(string)`

### 特性

* 若字串的第一個字符無法轉換為數字，則返回 `NaN`
* 只有字串中第一個字符會被返回
* 開頭、結尾的空格會被忽略

### parseFloat 範例

``` JavaScript
parseFloat('10')           /* 10 */
parseFloat('10.33')        /* 10.33 */
parseFloat('34 45 66')     /* 34 */
parseFloat(' 60 ')         /* 60 */
parseFloat('40 years')     /* 40 */
parseFloat('He was 40')    /* NaN */
parseFloat('010')          /* 10 */
```

## parseInt()

[MDN parseInt](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/parseInt)
能將輸入的字串轉成整數。
`parseInt(string, radix)`

### radix

必須，從 2 到 36，能代表該進位系統的數字。

* 如果 string 以 '0x' 開頭，parseInt() 會把 string 的其餘部分解析為十六進制的整數。
* 如果 string 由 0 開始，則 radix 會變成代表八進位的 8 或十進位的 10，但到底會變成 8 還是 10 則取決於各實做。ECMAScript 規定用代表十進位的 10，但也不是所有瀏覽器都支持。因此，使用 parseInt 時`一定`要指定 radix。
* 如果 string 以 1 ~ 9 的數字開頭，parseInt() 將把它解析為十進制的整數。

### parseInt 範例

``` JavaScript
parseInt('10')           /* 10 */
parseInt('10.33')        /* 10 */
parseInt('34 45 66')     /* 34 */
parseInt(' 60 ')         /* 60 */
parseInt('40 years')     /* 40 */
parseInt('He was 40')    /* NaN */
parseInt('010')          /* 10 */
parseInt(010)            /* 8 開頭為 0 的 Number 型別會被當作八進制帶入 (參考補充) */

parseInt('10', 10)       /* 10 */
parseInt('010')          /* 10 */
parseInt('10', 8)        /*  8 */
parseInt('0x10')         /* 16 */ 
parseInt('10', 16)       /* 16 */
```

## Number()

[MDN parseFloat](https:/*developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/parseInt)
函數把對象的值轉換為數字，如果對象的值無法轉換為數字，那麼 Number() 函數返回 NaN。
`Number(value);`

### Number 範例

``` JavaScript
Number(true);         /* 1 */
Number(false);        /* 0 */
Number('999');        /* 999 */
Number('010');        /* 10 */
Number(010);          /* 8 開頭為 0 的 Number 型別會被當作8進制帶入  */
Number('999 888');    /* NaN */
Number('lucky777');   /* NaN */
Number('777lucky')    /* NaN */
```

## 參考資料

[使用 parseFloat()、parseInt()、Number() 轉換型別](https://dylan237.github.io/js-parse-to-number.html)
