---
title: Cookie、LocalStorage、SessionStorage 差異
date: 2019-11-12
tags: 
  - HTML
  - Cookie
  - LocalStorage
  - SessionStorage
categories: HTML
description: 本篇會說明三個 HTML 所提供的儲存庫差異以及相關應用。
---
## Cookie
為伺服器傳送給使用者瀏覽器的一個小片段資料。瀏覽器可能儲存並在下一次請求回傳 cookie 至相同的伺服器。Cookie 通常被用來保持使用者的登入狀態，一般不能超過 20 個。
## LocalStorage / SessionStorage
兩者皆是 HTML5 標準中新加入的技術，彌補了 Cookie 儲存量小，不適用於大量資料本地儲存的問題。兩者在操作上的 API 都相同，差異在於時效性以及儲存的位置不同。
### LocalStorage
資料儲存於客戶端本地，不會過期，除非手動清除資料
### SessionStorage
資料儲存於 session 中，每次分頁或瀏覽器關掉後就會清除，而另開新分頁的話，又會是一個新的 SessionStorage。

## 三者差異比較
![Cookie、LocalStorage、SessionStorage 差異](https://i.imgur.com/IfuUsS3.png)

## 應用時機
### Cookie:
判斷用戶是否登入，並針對登入過的用戶在服務器端的 Cookies 中插入 token ，而下次只需取 token 就得知當前用戶是否登錄啦。
電商的購物車也能使用 Cookies 來儲存。

### LocalStorage:
有了 localStorage ，就能將 Cookie 的工作也交給它來辦了，此外，HTML5 遊戲也會產生很多數據，對於 Cookies 來說不是很友善(儲存量小)，則可使用 localStorage 來儲存資料。

### SessionStorage:
有時為了用戶體驗，不希望單一頁面有太多資訊或填寫步驟，則會採用多分頁的處理，這時 SessionStorage 就能夠派上用場啦!!

## 安全性問題
三者儲存庫都有 XSS 的風險，所以千萬不要用它們存儲系統中的敏感數據。