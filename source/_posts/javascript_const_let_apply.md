---
title: 'JavaScript 核心 (51) - ES6 章節：Let 及 Const - Let, Const 實戰運用技巧'
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 本篇來介紹 var const let 應用上差異
abbrlink: 542658997
date: 2021-02-02 12:00:00
---
## 作用域

由下圖可知，`var` 會互相汙染，導致 `console.log` 出錯

``` JavaScript
for (var i = 0; i < 10; i++) {
  setTimeout(function() {
    console.log('這執行第' + i + '次'); /* 10 */
  }, 10);
}
console.log(i); /* (10) 這執行第10次 */
```

來看看替換成 let 會有什麼差異
上篇提到 `let` 的作用域是在 `Block` 內

``` JavaScript
for (let i = 0; i < 10; i++) {
  setTimeout(function() {
    console.log('這執行第' + i + '次'); 
    /* 這執行第0次 */
    /* 這執行第1次 */
    /* 這執行第2次 */
    /* 這執行第3次 */
    /* 這執行第4次 */
    /* 這執行第5次 */
    /* 這執行第6次 */
    /* 這執行第7次 */
    /* 這執行第8次 */
    /* 這執行第9次 */
  }, 10);
}
console.log(i); /* i is not defined */
```

再換成 `const` 試試
`const` 是常數不能變更，且作用域也是再 `Block` 內
所以在執行`第一次 i++`時就會報錯

``` JavaScript
for (const i = 0; i < 10; i++) { /* Assignment to constant variable. 不能變更 */
  console.log(i); /* 0 */
  setTimeout(function() {
    console.log('這執行第' + i + '次'); /* 這執行第0次 */
  }, 10);
}
console.log('測試', i); /* 無回應 */
```

## 物件屬性差異

雖然說 `const` 是常數不能變更，但如果不是純值的話，就都會依照物件傳參考的特性，變成可以修改內部屬性

``` JavaScript
const person = {
  name: 'Cloud',
  money: 500,
}
person.name = 'Cloud_2';
console.log('person =>', person); /* person => { name: "Cloud_2", money: 500 } */

const name = 'Cloud';
name = 'Cloud_3';
console.log('name =>', name); /* Assignment to constant variable. */
```

使用 `Object.freeze()` 凍結時，`const` 跟 `var` 也會有所不同

``` JavaScript
var person = {
  name: 'Cloud',
  money: 500,
};
person.name = 'Cloud_2';
Object.freeze(person); /* freeze() 只針對物件內屬性 */
person.money = 1000;
console.log('person =>', person); /* person => { name: "Cloud_2", money: 500 } */

person = {};
console.log('person =>', person); /* person => {} */

const person_const = {
  name: 'Cloud',
  money: 500,
};
person_const.name = 'Cloud_2';
Object.freeze(person_const); /* freeze() 只針對物件內屬性 */
person_const.money = 1000;
console.log('person_const =>', person_const); /* person_const => { name: "Cloud_2", money: 500 } */

person_const = {};
console.log('person_const =>', person_const); /* Assignment to constant variable. */
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
