---
title: axios - 管理 API
tags:
  - axios
  - JavaScript
  - w3HexSchool
categories:
  - Axios
description: 本篇將介紹該如何將專案內的 API 統一管理，並根據元件引入特定 API 來做使用，大大提高程式碼的可讀性跟維護性。
abbrlink: 611398329
date: 2020-03-15 00:00:00
---
## 前言
不知道大家有沒有遇過 `API` 已經設定好了，某天被告知 `domain` 有調整過，或是某些 `get`、`post`方法需要多加參數等設定，導致必須不斷地找專案內 `call API` 的地方，有時還會遺漏幾處產生嚴重問題呢。以下教各位如何高效率的管理專案內的 `API`，即便是小專案也該如此。

## 官方 axios 範例
``` JavaScript
import axios from 'axios'; /* 依照你的專案形式引入套件 */

/* GET */
axios.get('http://api/user')
.then(res =>{
    console.log(res);
}).catch(err => {
    console.log(err);
})

/* POST */
axios.post('http://api/user', {
    firstName: 'Cloud',
    lastName: 'Su'
})
.then(res => {
    console.log(response);
})
.catch(err => {
    console.log(error);
});
```
這種作法相當直覺，針對特定功能去 `call api`，確實可以這樣寫，但當專案 `API` 超過 10 支、20支甚至更多時，這樣子的寫法就變得不好管理，如果 `domain`、`參數`一改，就得一個一個找出來慢慢改，真的很麻煩。

## 高效率管理 API 方法
使用官方的 `axios.create` 方法，可以利用此方法來新增一個 `axios` 實體。
首先建立 `api.js`，之後 `API` 都在這支檔案內管理。
``` JavaScript
import axios from 'axios';

/* 購物車 API */
const CartRequest = axios.create({
  baseURL: `${process.env.API_PATH}/shopping/cart`,
  headers: {
    'api-caller': 'xxx',
    'api-version': 1,
    'api-position': 'JH',
    'api-language': 'zh-TW',
    cart_serial: {
      toString() {
        return `${localStorage.getItem('cart_serial')}`;
      },
    },
    Authorization: {
      toString() {
        return `bearer ${localStorage.getItem('loginToken')}`;
      },
    },
  },
});

/* 折價券 API */
const CouponRequest = axios.create({
  baseURL: `${process.env.API_PATH}/shopping/coupon`,
  headers: {
    'api-caller': 'xxx',
    'api-version': 1,
    'api-position': 'JH',
    'api-language': 'zh-TW',
    cart_serial: {
      toString() {
        return `${localStorage.getItem('cart_serial')}`;
      },
    },
    Authorization: {
      toString() {
        return `bearer ${localStorage.getItem('loginToken')}`;
      },
    },
  },
});

/* 登入 API */
const loginRequest = axios.create({
  baseURL: `${process.env.API_PATH}/login`,
  headers: {
    'Content-Type': 'application/x-www-form-urlencoded;charset=UTF-8',
  },
});

/* 購物車 API */
export const API_CART_SERIAL = (data) => CartRequest.put('/init', data);
export const API_CART = () => CartRequest.get();
export const API_ADDTO_CART = (data) => CartRequest.post('/item', data);
/* delete 的參數必須先用 Object 包起來 */
export const API_DELETE_CART = (data) => CartRequest.delete('/item', { data }); 

/* 登入 API */
/* post 必須要有第一個 url 參數，都不寫的話就是指向 API 的根目錄 */
export const API_LOGIN = (data) => loginRequest.post('', data);

/* 折價券 API */
/* 還可使用傳入參數來變更 API 路徑 */
export const API_USE_COUPON = (couponCode) => CouponRequest.post(`/${couponCode}`);
```

要使用的話，直接 `import` 這支 `api.js`
``` JavaScript
/* 只 import 要使用的 API */
import { API_LOGIN, API_USE_COUPON, API_DELETE_CART } from 'api.js';

async login() {
  const loginForm = {
    UserName: 'xxx',
    Password: 'xxx',
  };
  const data = vm.Qs.stringify(loginForm);
  try {
    await API_LOGIN(data);
  } catch (err) {
    console.error(err);
  }
}

async use_shopping_coupon(context, couponCode) {
  try {
    await API_USE_COUPON(couponCode);
  } catch (error) {
    console.log(error);
  }
},

async delete_cart(context, id) {
  const product = {
    is_need_cart_data: true,
    product_spec_serial: id,
  };
  try {
    API_DELETE_CART(product);
  } catch (error) {
    console.log(error);
  }
},
```

## 高效率的管理優點
1. 可以確保所有的 `API` 都是同一進入點，即便在各元件 `js` 內呼叫 `API`，最後只需管理一支 `api`，對於日後 `API` 有需要要修改會方便很多。
2. 使用 `axios.create` 產生出的實體可以透過變數的方式給予新的 `API 名稱`，透過團隊命名規範來清楚知道 `API` 的功能。
3. 除了可以減少超長的 `api url`，還能大幅減少程式碼的撰寫，並搭配 `axios` 回傳的 `Promise` 特性，可以使用 `Async / Await` 減少 `.then()` 的寫法，提高程式碼可讀性

## 參考資料
[使用Axios你的API都怎麼管理？](https://medium.com/i-am-mike/%E4%BD%BF%E7%94%A8axios%E6%99%82%E4%BD%A0%E7%9A%84api%E9%83%BD%E6%80%8E%E9%BA%BC%E7%AE%A1%E7%90%86-557d88365619)