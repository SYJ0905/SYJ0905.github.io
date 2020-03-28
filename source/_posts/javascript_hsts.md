---
title: JavaScript - 解決網站 HSTS 問題
date: 2020-03-28
tags: 
  - JavaScript
  - w3HexSchool
  - HTTP
categories: JavaScript
description: 本將介紹如何將網站強制使用 HTTPS 傳遞機制，避免網站被惡意人士攻擊，竊取用戶資料。
---
## 前言
不知道各位將自己的網站部屬到某些主機後，使用 `http` 依舊可以開啟而不會自動轉址到 `https` 呢?
其實各個主機服務的後台都有對應的 `強制使用 https` 的設定，不過，也是有辦法在原始碼中直接設定 `強制使用 https` 的方法就是了。

## 直接寫入 HTML
此方法則是在渲染頁面時強制改寫網址 `HTTPS`
``` HTML
<html>
  <head>
    <title>Redirecting...</title>
  </head>
  <script language="JavaScript">
  function redirectHttpToHttps()
  {
      var httpURL= window.location.hostname + window.location.pathname + window.location.search;
      var httpsURL= "https://" + httpURL;
      window.location = httpsURL;
  }
  redirectHttpToHttps();
  </script>
  <body></body>
</html>
```

## redirect-ssl
套件名稱: redirect-ssl
[redirect-ssl github](https://github.com/nuxt-community/redirect-ssl)
輸入安裝指令 
```
npm install redirect-ssl -S
```
此套件是使用在 Nuxt.js，一般專案形式採用上面的方法即可。
在 `nuxt.config.js ` 中加入以下的 `serverMiddleware` 設定
``` JavaScript
export default {
  serverMiddleware: [
    // Will register redirect-ssl npm package
    'redirect-ssl'
  ]
}
```
有一點要特別小心，此方法在本地端執行 `npm run dev` 時會無法開啟，請記得在開發階段不要開啟此設定。

## 結尾
最保險的方法還是根據主機服務商提供的設定來使用，以上方法只是因為小弟還不太會設定 `GCP` 的 `HTTPS`，之後有機會在介紹如何使用 `GCP` 設定 `HTTPS`。

## 參考資料
[automatic redirection to https?](https://stackoverflow.com/questions/4954768/automatic-redirection-to-https)