---
title: Vue - props.sync 使用方式
tags:
  - Vue
categories:
  - Vue
description: 本篇介紹該如何使用 .sync 來達成原先的 props emit 父子元件 data 綁定問題
abbrlink: 2943028405
date: 2021-05-22 15:00:00
---
## props 、 emit 操作

`index.vue`

``` HTML
<p>{{ city }}</p>
<PropsEmit
  :city="city"
  :city-list="cityList"
  @handle_city="update_city"
/>
```

``` JavaScript
  import PropsEmit from '@/components/PropsEmit.vue';
  export default {
    components: {
      PropsEmit,
    },
    data() {
      return {
        city: '台北市',
        cityList: [
          {
            id: 1,
            name: '台北市',
          },
          {
            id: 2,
            name: '新北市',
          },
        ],
      };
    },
    methods: {
      update_city(val) {
        this.city = val;
      },
    },
  };
```

`PropsEmit.vue`

``` HTML
<template>
  <select v-model="propsCity">
    <option
      v-for="item in cityList"
      :key="item.id"
      :value="item.name"
    >
      {{ item.name }}
    </option>
  </select>
</template>
```

``` JavaScript
export default {
  props: {
    city: {
      type: String,
      default() {
        return '';
      },
    },
    cityList: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  computed: {
    propsCity: {
      get() {
        return this.city;
      },
      set(val) {
        this.$emit('handle_city', val);
      },
    },
  },
};
```

一般寫法就必須在 `父元件` 註冊一個自定義事件 `@handle_city` 來給 `子元件` 使用 emit 呼叫 `handle_city`，並且是執行 `handle_city` 所綁定的 method，進而達成父子元件雙向綁定。

來看看 .sync 是如何操作的

## .sync 操作

`index.vue`

``` HTML
<p>{{ city }}</p>
<PropsSync
  :city.sync="city"
  :city-list.sync="cityList"
/>
```

``` JavaScript
import PropsSync from '@/components/PropsSync.vue';
export default {
  components: {
    PropsSync,
  },
  data() {
    return {
      city: '台北市',
      cityList: [
        {
          id: 1,
          name: '台北市',
        },
        {
          id: 2,
          name: '新北市',
        },
      ],
    };
  },
};
```

`PropsSync.vue`

``` HTML
<template>
  <div>
    <select v-model="synCity">
      <option
        v-for="item in cityList"
        :key="item.id"
        :value="item.name"
      >
        {{ item.name }}
      </option>
    </select>
  </div>
</template>
```

``` JavaScript
export default {
  props: {
    city: {
      type: String,
      default() {
        return '';
      },
    },
    cityList: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  computed: {
    synCity: {
      get() {
        return this.city;
      },
      set(val) {
        this.$emit('update:city', val);
      },
    },
  },
};
```

由此可知，使用 `.sync` 就可以少寫 `@handle_city="update_city"` 和 `methods 事件`，所以 .sync 就是幫我們做了以下的事情:

``` HTML
v-bind:city="city" v-on:update:city="city = $event”
```

## 參考資料

[從原型鏈的角度看 -> 為什麼 Vue 組件中的 data 必須是一個 Function 函數](https://ichigoichie.medium.com/%E5%BE%9E%E5%8E%9F%E5%9E%8B%E9%8F%88%E7%9A%84%E8%A7%92%E5%BA%A6%E7%9C%8B-%E7%82%BA%E4%BB%80%E9%BA%BC-vue-%E7%B5%84%E4%BB%B6%E4%B8%AD%E7%9A%84-data-%E5%BF%85%E9%A0%88%E6%98%AF%E4%B8%80%E5%80%8B-function-%E5%87%BD%E6%95%B8-319d824655c8)
