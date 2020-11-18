---
title: Firebase - TodoList
tags:
  - Firebase
  - JavaScript
categories:
  - Firebase
description: 使用 Firebase 製作超簡易 TodoList
abbrlink: 4123263101
date: 2019-12-25 00:00:00
---
## 基本環境設置
請記得引入 Firebase 的初始化設定
``` HTML
<label for="todo_input">代辦事項:</label>
<input type="text" id="todo_input" placeholder="請輸入代辦事項">
<input type="button" value="送出" id="todo_send">
<ul id="todo_list"></ul>
```

## 範例程式碼
``` JavaScript
// DOM
var todo = document.querySelector('#todo_input');
var send = document.querySelector('#todo_send');
var todoList = document.querySelector('#todo_list');
var dataRef = firebase.database().ref('todos');

// 送出事項
send.addEventListener('click', function(e) {
  var todoContent = {
    content: todo.value,
  };
  dataRef.push(todoContent);
  todo.value = '';
});

// 監聽資料庫即時更新
dataRef.on('value', function(dataSnapshot) {
  var data = dataSnapshot.val();
  var str = ''
  for (const item in data) {
    str += `<li data-key="${item}">${data[item].content}</li>`;
  }
  todoList.innerHTML = str;
});

// 刪除邏輯
todo_list.addEventListener('click', function(e) {
  if (e.target.nodeName === 'LI') {
    var key = e.target.dataset.key;
    dataRef.child(key).remove();
  }
});
```
