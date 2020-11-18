---
title: JavaScript - Google sheet 表單串接 API
tags:
  - JavaScript
  - Google App Script
  - w3HexSchool
categories:
  - JavaScript
description: 本文將介紹如何使用 Google sheet 表單 API 來當我們的後端表單資料庫吧。
abbrlink: 430374326
date: 2020-02-29 00:00:00
---
## 前言
`Google form` 表單服務應該是目前最多人拿來建立表單的一種方式，然而，有優點自然也有缺點，在表單中無法製作`相對複雜的內容`、`需外連到表單網頁`、`無法追蹤表單行為`、`無法使用 GA 轉換追蹤`，此問題 Google 也聽到了，開發出 API 服務，使得開發者可以透過此 API 來與 `Google sheet` 讀寫資料。

## 建立 Google Sheet 表單
[Google Sheet method](https://developers.google.com/apps-script/reference/spreadsheet/sheet)
打開雲端硬碟，建立 Google 試算表，取得表單 `ID`。
表單 ID 就是網址中間那串亂碼 ex: https://docs.google.com/spreadsheets/d/表單ID/edit#gid=0。
![Google Sheet](https://i.imgur.com/VdFfBAw.png)

## 撰寫 API 執行內容
在表單選單中找到 `工具` => `指令碼編輯器`
![](https://i.imgur.com/ltULzLL.png)
接著會出現以下頁面
![指令碼編輯器](https://i.imgur.com/8dhhpMc.png)
中間 Function 參考範例，並有附上說明
``` JavaScript
/* doGet => API method 爲 get */
/* doPost => API method 爲 post */
function doGet(e) {
  //取得參數 e.parameter
  var params = e.parameter;
  var name = params.name; /* 屬性名稱必須跟前端相符合 */
  var phone = params.phone; /* 屬性名稱必須跟前端相符合 */
 
  //sheet資訊
  var SpreadSheet = SpreadsheetApp.openById("表單ID");
  var Sheet = SpreadSheet.getSheets()[0]; /* 取得要存入的試算表的第一張試算表 */
  var LastRow = Sheet.getLastRow(); /* 取得該張試算表中，最後一列有值的列數。 */

  //存入資訊 /* 將資料存入最後有值的下一列 */
  Sheet.getRange(LastRow+1, 1).setValue(name);
  Sheet.getRange(LastRow+1, 2).setValue(phone);
  
  //回傳資訊
  return ContentService.createTextOutput("成功");
}
```

## 部屬應用程式
選擇`發布` => `部屬為網路應用程式`
![部屬應用程式](https://i.imgur.com/pCizGPu.png)
選擇要允許讀寫的的對象，這裡一定要選 `任何人，包含匿名使用者`，不能選`所有人`，否則會出現 `CORS` 問題。
![部屬應用程式](https://i.imgur.com/kVzlKYq.png)
都選好就下一步，就會取得該 `API` 囉。
![API](https://i.imgur.com/u8IJUeq.png)

## 範例模板
以下直接附上 HTML 、 JavaScript 範例程式碼，基本上就單純的 `AJAX` 行為，可依照自己的專案使用像是 `jQuery` 取值、`Vue` 雙向綁定取值等方式。
``` HTML
<body>
  <div class="container">
    <div>
      <span>您的大名：</span><input id="nameValue" type="text">
    </div>
    <div>
      <span>您的電話：</span><input id="phoneValue" type="text">
    </div>
    <button>送出</button>
  </div>
  <script type="text/javascript" src="index.js"></script>
</body>
```

``` JavaScript
let sendButton = document.querySelector('button');

function send() {
  let name = document.querySelector('#nameValue').value;
  let phone = document.querySelector('#phoneValue').value;
  $.ajax({
    type: "get",
    url: "剛剛取得的 API，請直接貼上",
    data: {
      "name": name, /* 屬性名稱需與 Google Sheet 相同 */
      "phone": phone, /* 屬性名稱需與 Google Sheet 相同 */
    },
    dataType: "JSON",
    success: function(response) {
      console.log(response);
      if(response == "成功"){
        alert("成功");
      }
    },
  });
};

sendButton.addEventListener('click', send);
```

## 結尾
依照上述操作，就可以執行寫入表單的服務囉。

## 參考資料
[寫給純前端，讓 Google Sheets 當你的後端完成寫入功能](https://medium.com/unalai/%E5%AF%AB%E7%B5%A6%E7%B4%94%E5%89%8D%E7%AB%AF-%E8%AE%93-google-sheets-%E7%95%B6%E4%BD%A0%E7%9A%84%E5%BE%8C%E7%AB%AF%E5%AE%8C%E6%88%90%E5%AF%AB%E5%85%A5%E5%8A%9F%E8%83%BD-715799e5e013)
[Google sheet 試算表表單串接api](https://iandays.com/2018/02/08/googleformapi/)
