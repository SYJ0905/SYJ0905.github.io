---
title: Vue - Chart.js 視覺化圖表
tags:
  - Vue
  - Nuxt
  - Chart.js
  - RWD
categories:
  - Vue
description: 如何在 Vue、Nuxt專案中使用 Chart.js 將各式資料圖表化
abbrlink: 1205289835
date: 2020-12-01 00:00:00
---

## 前言

`vue-chart.js` 是一款輕量級的視覺化圖表 library，本篇紀錄如何在 Vue、Nuxt 專案中使用。

## 套件安裝

[vue-chartjs 官方網站](https://vue-chartjs.org/)
安裝指令

``` node
npm install vue-chartjs chart.js --save
```

## Vue 專案引入(Nuxt相同)

### Chart 模組建立

* 首先到 `components` 建立 `Chart.vue`，並引入所需要用到的套件
* `vue-chart.js` 有提供 mixins 使用，並且藉由 `reactiveProp` 自動建立的 `chartData` 參數作為 `prop` 父子間的傳遞參數，同時也將 `watch` 添加在個 `prop` 上。意味著只要父層 `data` 有更新，圖表會自動更新，若不使用的話得寫以下的 `watch` 監視內容

``` Javascript
watch: { /* 只要 chartData 改變，就要重新渲染圖表 */
  chartData() {
    this.$data._chart.destroy();  /* 官方文件 api 提供的 destroy() 方法 */
    this.renderChart(this.chartData, this.options); /* 重新渲染圖表的 function */
  },
  deep: true,
},
```

`Chart.vue` 元件範例:
注意:不要在 `Chart.vue` 引入 `<template>`標籤，否則 Vue 將會以此作為模板渲染，而不是從 `extend` 中獲取模板，將導致圖表生成錯誤。

``` html
<script>
/* Line 為引入的圖表種類（可以參考官方文件) */
import {
  Line, mixins,
} from 'vue-chartjs';

const { reactiveProp } = mixins;

export default {
  extends: Line,
  mixins: [reactiveProp],
  data() {
    return {
      options: { /* 圖表選項，各類圖表的 options 可能不盡相圖，可參照官方文件 */
        responsive: true,
        maintainAspectRatio: false,
        scales: {
          yAxes: [
            {
              ticks: {
                beginAtZero: true,
              },
              gridLines: {
                display: true,
              },
            },
          ],
          xAxes: [{
            gridLines: {
              display: true,
            },
          }],
        },
      },
    };
  },
  async mounted() {
    this.renderChart(this.chartData, this.options);
  },
};
</script>
```

### 引入 Chart 模組

在要引入 `Chart.vue` 在 .vue 檔中撰寫以下內容
在 `<select>` 綁定 `v-model="chartdataloaded"`，並利用下拉選單切換各種圖表內容。

``` html
<template>
  <div id="app">
    <!-- 父元件切換資料內容，並重新渲染圖表 -->
    <select
      v-model="chartdataloaded"
    >
      <option
        v-for="(item, index) in test"
        :key="index"
        :value="item"
      >
        測試 {{ index }}
      </option>
    </select>
    <!-- 
      Chart.vue 模組
      chart_loaded 是當圖表資料為 API 非同步行為時，增加的"讀取後顯示判斷"
    -->
    <div id="Chart">
      <Chart
        v-if="chart_loaded"
        :chart-data="chartdataloaded"
      />
    </div>
  </div>
</template>

<script>
import Chart from '@/components/Chart.vue';

export default {
  components: {
    Chart,
  },
  data() {
    return {
      chart_loaded: true, /* 圖表讀取 */
      chartdataloaded: {
        labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
        datasets: [
          {
            label: '測試1',
            borderColor: 'red',
            pointBackgroundColor: 'red',
            borderWidth: 1,
            pointBorderColor: 'white',
            data: [40, 35, 10, 40, 39, 80, 40],
          },
        ],
      },
      test: [
        {
          labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
          datasets: [
            {
              label: '測試1',
              borderColor: 'red',
              pointBackgroundColor: 'red',
              borderWidth: 1,
              pointBorderColor: 'white',
              data: [40, 35, 10, 40, 39, 80, 40],
            },
          ],
        },
        {
          labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
          datasets: [
            {
              label: '測試2',
              borderColor: 'skyblue',
              pointBackgroundColor: 'skyblue',
              borderWidth: 1,
              pointBorderColor: 'white',
              data: [50, 45, 20, 50, 35, 70, 50],
            },
          ],
        },
      ],
    };
  },
};
</script>
```

## 結語

以上僅介紹如何快速引入 Chart.js 圖表，`options` 還有很多東西可以設定，像是 `背景色`、`漸層色`、`互動模式`等等，這些在官方文件都有寫到，也不會太複雜，大概詳讀個一兩天就可以輕鬆上手了。

## 參考資料

[在 Nuxt.js 專案中使用 vue-chartjs](https://medium.com/@tiahi5914/%E5%89%8D%E7%AB%AF%E7%AD%86%E8%A8%98-%E5%9C%A8-nuxt-js-%E5%B0%88%E6%A1%88%E4%B8%AD%E4%BD%BF%E7%94%A8-vue-chartjs-ca799560ba44)
[使用Vue.js和Chart.js製作絢麗多彩的圖表](https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/648100/)
