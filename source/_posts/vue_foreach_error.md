---
title: Vue - v-for 常見錯誤
date: 2020-10-25
tags: 
  - Vue
categories: Vue
description: 本篇將介紹使用 v-for 語法時所需要注意的細節，避免出現錯誤渲染。
---
## 常見錯誤 1: Uncaught RangeError: Invalid array length
  ### 出現時機
  * 提供的 `data` 陣列長度`小於 0`
  * 提供的 `data` 陣列長度`不為整數`
  
此狀況只須避免上述兩種情況免錯誤產生。
## 常見錯誤 2: `v-for` 選單過多，造成渲染當機，導致畫面空白
  ### 出現時機
  * 用行動裝置瀏覽時，會發生畫面空白，連其他 DOM 元素都無法渲染
  
發生上述情形，請檢查 `data` 陣列長度是否過多(ex:99999)，太多會導致渲染當機。
可參考以下範例，避免此情況發生
  ``` HTML
  <template v-if="data.length > 50">
    <option v-for="(item, index) in 50" :key="index" :value="item">
      {{ item }}
    </option>
  </template>
  <template v-else>
    <option v-for="(item, index) in data.length" :key="index" :value="item">
      {{ item }}
    </option>
  </template>
  ```
  上述的 `select`、`option` 只是參考，也可套用在其他標籤的迴圈上哩。


## 參考資料
[Uncaught RangeError: Invalid array length 问题解决](https://blog.csdn.net/violetjack0808/article/details/54892889)
[RangeError: Invalid array length 问题解决](https://blog.csdn.net/qq_39400014/article/details/105558394)