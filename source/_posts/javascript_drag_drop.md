---
title: JavaScript - 拖曳功能(一) - 拖曳
date: 2019-12-09
tags: 
  - HTML5
  - JavaScript
categories: JavaScript
description: 在 HTML5 中使用 Drag & Drop API，在瀏覽器中做到拖曳、排序元素等功能。
---
## 名詞解釋
* `Drag Source` : 被點擊要拖曳的物件
* `Drop Target` : 拖曳物件要被放置的區域
兩者分別有對應的事件可以使用，請見下圖:
![Drag Drop Event](https://i.imgur.com/tpQ8Koe.png)
### 有關 Drag Source 事件
* `dragstart` : 當滑鼠點擊 Drag Source 時，並且拖曳的時間瞬間觸發。
* `drag` : 在 Drag Source 被拖曳持續觸發。
* `dragend` : 當滑鼠鬆開 Drag Source 時觸發。
### 有關 Drop Target 事件
* `dragenter` : 當拖曳的 Drag Source 首次進入 Drop Target 範圍內時觸發。
* `dragover` : 當拖曳的 Drag Source 進入 Drop Target 範圍內時，持續觸發。
* `dragleave` : 當拖曳的 Drag Source 離開可放置區塊時觸發。
* `drop` : 當拖曳 Drag Source 在 Drop Target 的範圍內被釋放時所觸發

## 相關元素的前置作業
### HTML Attribute
針對要拖曳的元素，在其 HTML 標籤添加屬性 `draggable="true"`
``` HTML
<div id="drag_source" draggable="true"></div>
```
### SCSS 設定
為了避免使用者在拖曳元素時選取到元素內的內容，可以在 CSS 添加以下程式碼
``` CSS
[draggable="true"] {
  /*
   To prevent user selecting inside the drag source
  */
  user-select: none;
  -moz-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
}
#drag_drop_basic,
#drag_drop_multiple {
  display: flex;
  justify-content: space-between;
  .soruce_container,
  .target_container {
    height: 200px;
    border: 2px solid #ccc;
    flex: 0 0 calc(50% - 1rem);
  }
  #drag_source_basic,
  #drag_source_multiple {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100px;
    height: 100px;
    border-radius: 50%;
    background-color: skyblue;
    font-size: 50px;
    line-height: 1.0;
  }
}
.dragging {
  opacity: .25;
}
.hover {
  background-color: rgba(red, 0.4);
}
```
## 基本範例說明
直接按照以下程式碼就能做出單一元素拖曳效果囉!!(僅限一次拖曳)
### HTML
``` HTML
<div id="drag_drop_basic">
  <div class="soruce_container">
    <div id="drag_source_basic" draggable="true"></div>
  </div>
  <div class="target_container" class="target_container"></div>
</div>
```
### JavaScript
* `Drag Source` :
將要被拖曳的元素設置 `dragstart` 事件。
``` JavaScript
let dragSource = document.querySelector('#drag_drop_basic #drag_source_basic');
dragSource.addEventListener('dragstart', dragStart);
dragSource.addEventListener('dragend', dragEnd);
function dragStart(e) {
  e.dataTransfer.setData('text/plain', e.target.id);
  this.classList.add('dragging'); // 加入 dragging 自定義樣式
}
function dragEnd(e) {
  this.classList.remove('dragging'); // 移除 dragging 自定義樣式
}
```
* `Drop Target` :
對要放置的容器設置 `dragenter`、`dragover`、`drop` 三個事件。
``` JavaScript
let dropTarget = document.querySelector('#drag_drop_basic .target_container');
dropTarget.addEventListener('drop', droped);
dropTarget.addEventListener('dragenter', cancelDefault);
dropTarget.addEventListener('dragover', dragover);
dropTarget.addEventListener('dragleave', dragLeave);
function droped(e) {
  cancelDefault(e);
  let id = e.dataTransfer.getData('text/plain');
  e.target.appendChild(document.querySelector(`#${id}`));
  this.classList.remove('hover'); // 移除 hover 自定義樣式
}
function dragover(e) {
  cancelDefault(e);
  this.classList.add('hover'); // 加入 hover 自定義樣式
}
function dragLeave(e) {
  this.classList.remove('hover'); // 移除 hover 自定義樣式
}
// 元素預設行為是不能被放置拖曳物的，因此在拖曳對象出現在放置目標上時，取消預設行為，讓放置目標可以被放置
function cancelDefault(e) {
  e.preventDefault();
  e.stopPropagation();
  return false; // 可加可不加
}
```
## 進階範例說明
以下是針對多個元素進行多次拖曳的範例
### HTML
``` HTML
<div id="drag_drop_multiple">
  <div class="soruce_container" data-role="drag_drop_container">
    <div id="drag_source_multiple" draggable="true"></div>
  </div>
  <div class="target_container" data-role="drag_drop_container"></div>
</div>
```
### JavaScript
* `Drag Source` :
``` JavaScript
let dragSources_multiple = document.querySelectorAll('#drag_drop_multiple #drag_source_multiple');
dragSources_multiple.forEach(item => {
  item.addEventListener('dragstart', dragStart);
  item.addEventListener('dragend', dragEnd);
});
function dragStart(e) {
  e.dataTransfer.setData('text/plain', e.target.id);
  this.classList.add('dragging'); // 加入 dragging 自定義樣式
}
function dragEnd(e) {
  this.classList.remove('dragging'); // 移除 dragging 自定義樣式
}
```
* `Drop Target` :
``` JavaScript
let dropTargets_multiple = document.querySelectorAll('[data-role="drag_drop_container"]');
dropTargets_multiple.forEach(item => {
  item.addEventListener('drop', droped);
  item.addEventListener('dragenter', cancelDefault);
  item.addEventListener('dragover', dragover);
  item.addEventListener('dragleave', dragLeave);
});
function droped(e) {
  cancelDefault(e);
  let id = e.dataTransfer.getData('text/plain');
  e.target.appendChild(document.querySelector(`#${id}`));
  this.classList.remove('hover'); // 移除 hover 自定義樣式
}
function dragover(e) {
  cancelDefault(e);
  this.classList.add('hover'); // 加入 hover 自定義樣式
}
function dragLeave(e) {
  this.classList.remove('hover'); // 移除 hover 自定義樣式
}
// 元素預設行為是不能被放置拖曳物的，因此在拖曳對象出現在放置目標上時，取消預設行為，讓放置目標可以被放置
function cancelDefault(e) {
  e.preventDefault();
  e.stopPropagation();
  return false; // 可加可不加
}
```
## 完整 DEMO
[DEMO](https://syj0905.github.io/drag-drop-demo/)
## 參考資料:
[HTML 拖放 API](https://developer.mozilla.org/zh-TW/docs/Web/API/HTML_Drag_and_Drop_API)
[HTML 5 拖放](https://www.w3school.com.cn/html5/html_5_draganddrop.asp)
[使用拖曳效果，進化寶可夢吧！](https://w3c.hexschool.com/blog/2f2c7c6e)
[製作可拖曳的元素](https://pjchender.blogspot.com/2017/08/html5-drag-and-drop-api.html)
