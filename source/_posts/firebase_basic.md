---
title: Firebase - 基礎介紹
tags:
  - Firebase
  - JavaScript
categories:
  - Firebase
description: 本篇將介紹如何使用 Firebase 讀寫資料庫內容。
abbrlink: 2037953785
date: 2019-12-25 00:00:00
---
## 基本環境建立
首先請到 Firebase 建立一份新的專案，並依照下圖紅色箭頭新建一個網路應用程式。
![Firebase](https://i.imgur.com/E6nUBkN.png)
新建完成後會給一段 `script` ，這是之後要在 HTML 中引入的。
![新建應用程式](https://i.imgur.com/DS1e33O.png)
註:由於新版的 Firebase 將核心程式碼獨立出來，其他功能拆分成各個模組。
會使用到 Firebase 中的 Database 功能，所以必須額外引入套件，請參照以下 `script`。
版本號的部分請跟 `firebase-app.js` 核心模組相同即可。
``` HTML
<script src="https://www.gstatic.com/firebasejs/7.6.1/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/7.6.1/firebase-database.js"></script>
```

## 引入檔案
開啟一份專案資料夾，並創建 `index.html`，將 Firebase 的 script 加入到 body 的最後面。
``` HTML
<body>
  <script src="https://www.gstatic.com/firebasejs/7.5.2/firebase-app.js"></script>
  <script src="https://www.gstatic.com/firebasejs/7.5.2/firebase-database.js"></script>
  <script src="https://www.gstatic.com/firebasejs/7.5.2/firebase-analytics.js"></script>
  <script>
    // Your web app's Firebase configuration
    var firebaseConfig = {
      apiKey: "不給你看",
      authDomain: "不給你看",
      databaseURL: "不給你看",
      projectId: "不給你看",
      storageBucket: "不給你看",
      messagingSenderId: "不給你看",
      appId: "不給你看",
      measurementId: "不給你看"
    };
    // Initialize Firebase
    firebase.initializeApp(firebaseConfig);
    firebase.analytics();
  </script>
</body>
```
接下來就開始介紹 Firebase 中 Database 的各種操作囉!!

## ref()、set()
* `ref()`: 尋找資料庫路徑
* `set()`: 新增資料
在 Firebase 中，資料全部都是物件格式，不能是陣列格式

參考範例程式碼:
``` JavaScript
var data = null;
data = {
  food: {
    coke: {
      price: 30,
      num: 1,
    },
    fries: {
      price: 35,
      num: 50,
    },
  },
  order: {
    1: {
      coke: 2,
    },
    2: {
      coke: 2,
      fries: 50,
    },
  },
};
firebase.database().ref().set(data);
firebase.database().ref('stu1/name').set('Cloud');
```
之後打開 `Web Server`，再切到 Firebase 後台就可以看到資料已經寫入囉!!
![資料寫入Firebase](https://i.imgur.com/zWihB4c.png)

## once()、on()
* `once()`: 讀取一次資料庫的資料
* `on()`: 隨時監聽資料庫
註: 回傳的參數 snapshot 等於 dataSnapshot，兩者在官方文件都有出現過

參考範例:
``` HTML
<h1 id="title"></h1>
<h1 id="subtitle"></h1>
<h1 id="number"></h1>
<h1 id="subnumber"></h1>
```
``` JavaScript
var myNameRef = firebase.database().ref('myName');
myNameRef.set('Cloud');
// callback 寫法
myNameRef.once('value', function (snapshot) {
  document.getElementById('title').textContent = snapshot.val();
});
// Promise 寫法
myNameRef.once('value')
  .then((dataSnapshot) => {
    document.getElementById('subtitle').textContent = dataSnapshot.val();
  });

var numberRef = firebase.database().ref('myNumber');
numberRef.set('7');
numberRef.on('value', function (snapshot) {
  document.getElementById('number').textContent = snapshot.val();
});

// 測試 once() 與 on() 差異
setTimeout(() => {
  firebase.database().ref('myName').set('Tom');
  firebase.database().ref('myNumber').set('20');
}, 5000);
```
同樣開啟 `Web Server` 會發現 `5` 秒前的顯示內容與資料庫相同，但 `5` 秒後的數字已經變成 `20`，確實與資料庫相同，但 `title` 卻依舊是 `Cloud`，此時資料庫已經更換成 `Tom`，這就是 `once()` 與 `on()` 的差異。
5秒前 Firebase
![5秒前 Firebase](https://i.imgur.com/1OiMzxB.png)
5秒後 Firebase
![5秒後 Firebase](https://i.imgur.com/WWckntp.png)

## push()、remove()
* `push()`: 傳入資料，必須是物件格式
* `key`: push 之後 firebase 給的唯一值
* `remove()`: 刪除資料
* `child()`: 子路徑

參考範例:
``` JavaScript
var dataArray = [
  {
    content: '今天要記得刷牙',
  },
  {
    content: '今天要記得看牙醫',
  }
]
var todos = firebase.database().ref('todos');
dataArray.forEach((item) => {
  todos.push(item);
});
var todosChild = firebase.database().ref().child('todos');
// id 請填入 key
// todosChild.child('id').remove();
```
開啟 `Web Server`，Firebase 就會寫入資料並將每一筆資料都帶有 `key`，如果要刪除特定一筆資料就在 `child('key')` 填入 `key` 接著 `remove()` 就能刪除資料庫資料了
![Firebase](https://i.imgur.com/bwqvUYt.png)

## orderByChild()
路徑 > 排序('屬性') > 過濾 > 限制筆數 > 讀取 > forEach 依序撈出
必需搭配 `forEach()` 取出資料才行，
是對 `dataSnapshot` 做 `forEach()`，不是對 `dataSnapshot.val()`

* `orderByChild()`: 排序('屬性')
* `startAt()`: 過濾多少以上的資料
* `endAt()`: 過濾多少以下的資料
* `equalTo()`: 過濾特定數值的資料
* `limitToFirst()`: 限制比數，從頭開始算
* `limitToLast()`: 限制比數，從尾開始算


參考範例:
``` JavaScript
var people = {
  mike: {
    length: 12.5,
    weight: 5000,
    height: 50,
  },
  casper: {
    length: 9,
    weight: 4500,
    height: 25,
  },
  bob: {
    length: false,
    weight: 2500,
    height: 55,
  },
  john: {
    length: 9,
    weight: 3500,
    height: 10,
  }
  ,
  josh: {
    length: 9,
    weight: 2500,
    height: 30,
  },
};

var peopleRef = firebase.database().ref('people');
peopleRef.set(people);
peopleRef.orderByChild('height').once('value', function(dataSnapshot) {
  // 注意 是對 dataSnapshot 做 forEach，不是對 dataSnapshot.val()
  dataSnapshot.forEach(item => {
    console.log('orderByChild', item.val());
  });
});

// startAt() 過濾多少以上的資料
// endAt() 過濾多少以下的資料
peopleRef.orderByChild('weight').startAt(3500).endAt(4500).once('value', function (dataSnapshot) {
  dataSnapshot.forEach(item => {
    console.log('startAt endAt', item.val());
  });
});

// equalTo() 過濾特定數值的資料
peopleRef.orderByChild('weight').equalTo(2500).once('value', function (dataSnapshot) {
  dataSnapshot.forEach(item => {
    console.log('equalTo', item.val());
  });
});

// limit
peopleRef.orderByChild('weight').startAt(2500).limitToLast(1).once('value', function (dataSnapshot) {
  dataSnapshot.forEach(item => {
    console.log('limitTofirst', item.val());
  });
});
```