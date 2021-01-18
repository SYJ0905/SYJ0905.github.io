---
title: JavaScript 核心 (38) - 函式以及 This 的運作 - this 課後練習
tags:
  - JavaScript
  - JavaScript 核心篇
categories:
  - JavaScript
description: 來複習一下是否真的學會 this 了
abbrlink: 3217853531
date: 2021-01-18 11:00:00
---
## 第一題

``` JavaScript
function callName() {
  console.log(this.name);
}
var auntie = {
  name: '漂亮阿姨',
  callName: callName,
  watch: {
    name: 'Magic Watch',
    callName: callName
  }
}
auntie.callName();
auntie.watch.callName();
/* Ans: 漂亮阿姨 / Magic Watch */
```

## 第二題

``` JavaScript
function callName() {
  console.log(this.name);
}
var auntie = {
  name: '漂亮阿姨',
  callName: callName,
  watch: {
    name: 'Magic Watch',
    callName: callName
  }
}
var callName1 = auntie;
var callName2 = auntie.watch;
var callName3 = callName1.callName();
var callName4 = callName2.callName;

callName3;
callName4;
/* Ans: 漂亮阿姨 / function callName() */
```

## 第三題

``` JavaScript
var name = '小明';
function namefu () {
  console.log(this.name);
};

var a =  {
  name: '小王',
  myname: namefu,
};

namefu.name='小美';

a.myname();
/* Ans: 小王 */
```

## 第四題

``` JavaScript
var name = '小明';
var obj = {
  x: function () {
  name = '小王';
  console.log(this.name);
  },
  y: '2',
}

obj.x();
/* Ans: undefined */
```

## 第五題

``` JavaScript
var name = '小明';
var obj = {
  x: {
    name: '小虎',
    myname: function () {
      console.log(this.name);
      setTimeout(function () {
      console.log(this.name);
      },500) 
    }
  },
  y: '2',
  name: '小王',
}

var a = obj.x.myname();
a;
/* Ans: 小虎 / 小明 */
```

## 第六題

``` JavaScript
function callName(name) {
  console.log(this.name, name);
}

var name = '全域阿婆';
var auntie = {
  name: '漂亮阿姨',
}
callName(undefined, '小明');
callName.call(auntie, '小明');
/* Ans: 全域阿婆 / undefined，漂亮阿姨 / 小明 */
```

## 第七題

``` JavaScript
var name = '全域';
var auntie = {
  name: '漂亮阿姨',
  callName: function () {
    console.log(this.name);
  }
};
(function() {
  var a = auntie.callName;
  a();
})();
/* Ans: 全域 */
```

## 第八題

``` JavaScript
var name = '全域';
(function () {
  var name = '區域';
  setTimeout(function() {
    console.log(this.name);
  },500)
})();
/* Ans: 全域 */
```

## 第九題

``` JavaScript
var name = '小明';

function callName(name) {
  console.log(this.name);
}

var obj = {
  name: '小美',
  family: {
    name: '小王',
  },
};

callName.name = '小光';

var a = callName.bind(obj, '小城');
a();
/* Ans: 小美 */
```

## 參考資料

[六角學院 - JavaScript 核心篇](https://www.hexschool.com/courses/js-core.html)
[JavaScript 核心觀念(44)-函式以及 This 的運作-this 課後練習](https://hsiangfeng.github.io/javascript/20210111/2101221515/)
