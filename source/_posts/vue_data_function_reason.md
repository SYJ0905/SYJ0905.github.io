---
title: Vue - 為什麼 Vue 元件中的 data 必須是一個 Function 函數
tags:
  - Vue
categories:
  - Vue
description: 本篇介紹為什麼 Vue 元件中的 data 必須得是 Function ?
abbrlink: 146109072
date: 2021-05-22 01:00:00
---

## 元件與 data 用處

Vue 的元件是被拿來給其他頁面`複用`
假如 data 是一個對象，這也就表示作用域其實沒有分開，在使用時會互相影響。
因此，data 必須使用 Function 函數，來確保每個元件的 data 屬性值是不相影響的

## JS 特性 or Vue 設計?

如果使用 Object 的話，也會發生每個元件 data 會互相影響。
在 JS 中只有 Function 能構成作用域，當 data 是一個函數，意味著每個元件有自己的作用域，相互獨立。

* 當 data 是 Object 時:
兩個元件同時使用同一份 Object，修改其中一個屬性，也會同時修改到一個元件的。

``` JavaScript
const MyComponent = function() {}; 
MyComponent.prototype.data = {     
  a: 1,     
  b: 2, 
} 
const component1 = new MyComponent(); 
const component2 = new MyComponent(); 

component1.data.a === component2.data.a; // true;
 
component1.data.b = 5; 
component2.data.b // 5
```

* 當 data 是 Function:

``` JavaScript
const MyComponent = function() {     
  this.data = this.data(); 
}; 
MyComponent.prototype.data = function() {     
  return {         
    a: 1,        
    b: 2,     
  } 
};
```

## 結論

由以上範例可知， Vue 元件中的 data 必須是 Function 是因為受到 `JavaScript 本身特性` 所得的結果。

## 參考資料

[從原型鏈的角度看 -> 為什麼 Vue 組件中的 data 必須是一個 Function 函數](https://ichigoichie.medium.com/%E5%BE%9E%E5%8E%9F%E5%9E%8B%E9%8F%88%E7%9A%84%E8%A7%92%E5%BA%A6%E7%9C%8B-%E7%82%BA%E4%BB%80%E9%BA%BC-vue-%E7%B5%84%E4%BB%B6%E4%B8%AD%E7%9A%84-data-%E5%BF%85%E9%A0%88%E6%98%AF%E4%B8%80%E5%80%8B-function-%E5%87%BD%E6%95%B8-319d824655c8)
