---
title: JavaScript 套件 - 客製化捲軸 OverlayScrollbars
tags:
  - JavaScript
  - Vue
categories:
  - JavaScript
abbrlink: 3061888294
date: 2021-01-29 23:59:00
description: 本篇來介紹超好用的客製化捲軸套件
---
## OverlayScrollbars

[OverlayScrollbars](https://github.com/KingSora/OverlayScrollbars)
一款純 Javascript 或依賴 jQuery 所開發的近原生捲軸套件，並且也有開發支援三大框架。

## 範例

本篇會使用 Vue 製作範例

``` NPM
npm install overlayscrollbars-vue
```

在 `main.js` 加入以下內容：

``` JavaScript
import OverlayScrollbars from 'overlayscrollbars';
import { OverlayScrollbarsPlugin } from 'overlayscrollbars-vue';
import 'overlayscrollbars/css/OverlayScrollbars.css';
Vue.use(OverlayScrollbarsPlugin);

OverlayScrollbars(document.body, {
  nativeScrollbarsOverlaid: {
    initialize: false,
  },
});
```

Template:

``` HTML
<overlay-scrollbars :options="{ scrollbars: { autoHide: 'scroll' } }"></overlay-scrollbars>
```

假設有設定高度，加上內容過多溢出，正常來說按照上面範例就會出現`滾動條`囉。
官方提供很多參數可以設定，有興趣的人可以在玩玩看，這邊只做最簡單的範例。
