---
title: JavaScript 核心 (23) - 物件 - 物件的參考特性
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 純值傳值 ? 物件傳參考 ?
abbrlink: 3340933473
date: 2020-12-28 18:30:00
---
## 純值傳值 Call by value

純值就是 JavaScript 的7個原始型別，以下用 `String` 當賦值:

``` JavaScript
var a = 'Cloud';
var b = a;
console.log(a, b); /* Cloud, Cloud */
b = 'Test';
console.log(a, b); /* Cloud, Test */
```

由此可知，`a、b兩者互不相干`。

## 物件傳參考 Call by reference

接下來用物件試試，看與上面有何差異吧。

``` JavaScript
var a = {
  name: 'Cloud',
}

var b = a;

b.name = 'Test';

console.log(a.name, b.name); /* Test, Test */
```

結果 a、b 都為 Test，也就是說 a、b 兩者是`相同的`

``` JavaScript
console.log(a === b); /* true */
```

之所以兩者相同是因為 `物件傳參考` 特性
那什麼是`參考`?
可以理解成是宣告物件時(a)建立記憶體空間，而此變數是`指向記憶體空間`，而不是`值`。
而後新變數(b)又用 a 當變數宣告，此時指向的依舊是物件。
用以下圖片更好理解:
![物件傳參考](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/JavaScript%20%E6%A0%B8%E5%BF%83%20(23)%20-%20%E7%89%A9%E4%BB%B6%20-%20%E7%89%A9%E4%BB%B6%E7%9A%84%E5%8F%83%E8%80%83%E7%89%B9%E6%80%A7%2F%E7%89%A9%E4%BB%B6%E5%82%B3%E5%8F%83%E8%80%83.png?alt=media&token=54cb7e93-14b2-4d6c-ae38-3e260e21fb04)

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(26)-物件-物件的參考特性](https://hsiangfeng.github.io/javascript/20200808/2652400322/)
