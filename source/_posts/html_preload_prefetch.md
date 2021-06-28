---
title: Preload vs Prefetch vs Preconnect 比較
tags:
  - HTML
  - Optimization
categories:
  - Optimization
description: 本篇介紹如何有效的提升前端效能
abbrlink: 1782034678
date: 2021-06-29 00:00:00
---
## Preload

告知瀏覽器這份資源對目前的頁面是必要的，請用最快的速度下載此資源。
`preload` 對瀏覽器有`強制作用`而非「建議」，所以必須很確定它是真正重要的資源。

``` HTML
<link rel="preload" as="script" href="main.js">
<link rel="preload" as="style" href="main.css">
<link rel="preload" as="font" crossorigin="anonymous" type="font/woff2" href="xxx.woff2">
```

* `as`: 必須，用來指定資源的類別。這個屬性需要指定，不然可能會重複下載同一份資源。
* `crossorigin`: 對字體作 preload，必須加上 crossorigin 這個 attribute，表示 anonymous mode CORS，否則字型會被重複下載兩次。crossorigin 也適用於其他支援 CORS 的資源。

<註>`Anonymous mode` 表示送這個 request 的時候不帶任何 user credential，包含 cookie、HTTP authentication 等

## Preconnect

告訴瀏覽器這個網頁將會在不久的將來下載某個 domain 的資源，請先幫我建立好連線。

``` HTML
<link rel="preconnect" href="https://example.com">
```

為什麼需要提前建立連線呢？

要理解這個功能的用途，我們必須先知道，瀏覽器在實際傳輸資源前，有以下步驟需要做：

1. 向DNS請求解析域名
2. TCP Handshake
3. (HTTPS連線) SSL Negotiation
4. 連線建立完成，等待拿到資料的第一個byte

[Eliminating Roundtrips with Preconnect](https://www.igvita.com/2015/08/17/eliminating-roundtrips-with-preconnect/)

上面四個步驟，每一步都會需要一個 RTT (Round Trip Time) 的來回時間。

所以在實際傳輸資料之前，已經花了 3 個RTT的時間。

如果是在 latency(延遲) 很高的情況下（例如手機網路），會大大拖慢取得資源的速度。

使用情境:

* `CDN`: 當有很多資源要從某個 CDN 去拿，可以提示 preconnect CDN的域名。
* `Streaming(影音串流)`: 如果頁面上有個串流媒體，但沒有要馬上播放，又希望按下播放的時候可以越快開始越好，那麼可以考慮先用 preconnect 建立連線，節省一段連線時間。

## Prefetch

告訴瀏覽器這資源我等等會用到，有空的話幫我先下載。
資源將會等頁面完全下載完以後，以 Lowest 優先度下載。

使用情境:

* `分頁的下一頁`: 如果確定使用者有很高的機率會點下一頁的話。

## 結論

* `preload` 告訴瀏覽器：「這份資源對目前的頁面是必要的，請用最快的速度下載此資源。」
* `preconnect` 告訴瀏覽器：「這個網頁將會在不久的將來下載某個 domain 的資源，請先幫我建立好連線。」
* `prefetch` 告訴瀏覽器：「這資源我等等會用到，有空的話幫我先下載」。

## 參考資料

[Preload vs Prefetch](https://cythilya.github.io/2018/07/31/preload-vs-prefetch/)
[深入淺出 Preload, Prefetch 和 Preconnect：三種加快網頁載入速度的 Resource Hint 技巧](https://shubo.io/preload-prefetch-preconnect/#preconnect)
