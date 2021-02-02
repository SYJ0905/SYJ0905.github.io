---
title: JavaScript - 移除字串中的表情符號 Emoji
tags:
  - JavaScript
categories:
  - JavaScript
description: 本篇來介紹如何使用正則表達式來移除表情符號
abbrlink: 2024888940
date: 2021-02-02 10:30:00
---
## 情境

使用者在前台輸入 Emoji 和一般文字，但後台進資料庫或是 ERP 時是無法分辨出 Emoji 的，而會是亂碼。

## 正則表達式

行動裝置上都有所謂的表情符號，那些有一定的規則存在，可以使用正則來把 Emoji 替換成空值。

## 範例

``` JavaScript
const emoji_range = [
  '[\u2764\uFE0F]',
  '[\u2694-\u2697]',
  '[\u2580-\u27BF]',
  '[\u2700-\u27BF]',
  '[\uE000-\uF8FF]',
  '[\u2011-\u26FF]',
  '\uD83E[\uDD10-\uDD5D]',
  '\uD83C[\uDF00-\uDFFF]',
  '\uD83D[\uDC00-\uDFFF]',
  '\uD83D[\uDC00-\uDE4F]',
  '\uD83D[\uDE80-\uDEFF]',
  '\uD83E[\uDD10-\uDDFF]',
];
const input = '輸入文本❤️🥺😂';
const output = input.replace(new RegExp(emoji_range.join('|'), 'g'), '');
console.log('output =>', output); /* output => 輸入文本 */
```

## 參考資料

[How to remove emoji code using javascript?](https://stackoverflow.com/questions/10992921/how-to-remove-emoji-code-using-javascript)
