---
title: webpack 架設 - 使用 SCSS 撰寫樣式
date: 2019-09-11
tags: webpack
categories: webpack
description: 在 webpack 加入 scss 插件
---
## 前言
相信各位小夥伴多少都會使用 CSS 預處理器在撰寫樣式，像是 SASS 、Stylus、LESS、PostCSS 等等，但使用這類工具都必須經過編譯過後產生真正的 CSS 檔案才能夠讓瀏覽器渲染，因為瀏覽器只看得懂 CSS ，本篇教大家如何在 webpack 中使用 SCSS 吧!!

## 安裝相關套件
[sass-loader](https://github.com/webpack-contrib/sass-loader)
輸入以下安裝指令
```
npm install css-loader sass-loader node-sass mini-css-extract-plugin --save-dev
```
註: `css-loader` sass 官網雖然沒有寫在安裝指令內，但還是必須要安裝，因為讓網站能夠顯示 CSS 樣式的插件
`mini-css-extract-plugin` 是用來將每個由 webpack 產生內含有 css 的 js 檔案轉成 css 檔。
在 `src` 底下建立一個只存放 scss 的資料夾，並新增一隻檔案 all.scss，試著寫點 scss 代碼之後方便測試

## 修改設定檔
在 `webpack.config.js` 加入設定
```
const HtmlWebpackPlugin = require('html-webpack-plugin');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
const path = require('path');

module.exports = {
  entry: [
    './src/main.js',
    './src/assets/all.scss', // scss 進入點
  ],
  output: {
    filename: 'js/main.bundle.js',
    path: path.resolve(__dirname, 'dist')
  },
  module: {
    rules: [
      {
        test: /\.s[ac]ss$/i,
        use: [
          MiniCssExtractPlugin.loader,
          'css-loader',
          'sass-loader',
        ],
      },
    ],
  },
  plugins: [
    new HtmlWebpackPlugin({
      title: 'webpack demo',
      meta: {
        'Content-Security-Policy': { 'http-equiv': 'X-UA-Compatible', 'content': 'ie=edge' },
        viewport: 'width=device-width, initial-scale=1, shrink-to-fit=no',
      }
    }),
    new MiniCssExtractPlugin({
      filename: '/css/all.css',
    }),
  ],
};
```
輸入 `npm run dev` 就能產出 css 資料夾以及檔案，並且也能正確顯示 CSS 樣式
![](https://i.imgur.com/ZqMGpkj.png)

## 加入 sourcemap
如果不使用 sorcemap 的話，在瀏覽器查看樣式時會看到合併完成的檔案，這會讓開發人員難以找出問題所在的原始檔案。使用 sourcemap 就能在開發時也清楚知道每一行的樣式是在哪隻 SCSS 檔案內。
相關設定可以在 [sass-loader](https://github.com/webpack-contrib/sass-loader) 中搜尋 `Source maps` 就能找到啦!!
或是可以參考以下修改配置
```
const HtmlWebpackPlugin = require('html-webpack-plugin');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
const path = require('path');

module.exports = {
  entry: [
    './src/main.js',
    './src/assets/all.scss', // scss 進入點
  ],
  output: {
    filename: 'js/main.bundle.js',
    path: path.resolve(__dirname, 'dist')
  },
  devtool: 'source-map', // 必須要有
  module: {
    rules: [
      {
        test: /\.s[ac]ss$/i,
        use: [
          MiniCssExtractPlugin.loader,
          {
            loader: 'css-loader',
            options: {
              sourceMap: true, // 開啟功能
            },
          },
          {
            loader: 'sass-loader',
            options: {
              sourceMap: true, // 開啟功能
            },
          },
        ],
      },
    ],
  },
  plugins: [
    new HtmlWebpackPlugin({
      title: 'webpack demo',
      meta: {
        'Content-Security-Policy': { 'http-equiv': 'X-UA-Compatible', 'content': 'ie=edge' },
        viewport: 'width=device-width, initial-scale=1, shrink-to-fit=no',
      }
    }),
    new MiniCssExtractPlugin({
      path: path.resolve(__dirname, 'dist'),
      filename: '/css/all.css',
    }),
  ],
};
```
## 模組化 SCSS
首先必須要搞清楚相對路徑和絕對入境以及 SCSS 的進入點，在 `assets` 底下建立 `layout` 資料夾，並新增 `_layout.scss`，這是等一下要引入的檔案。
來到 `all.scss` 引入剛新建的 scss ，以下提供兩種引入方法，根據個人喜好則一即可
```
@import './layout/layout'; // 相對路徑 => 進入點是 all.scss 這是根據 webpack 設定
@import 'src/assets/layout/layout'; // 絕對路徑
```
![](https://i.imgur.com/HIXOTLD.png)

## 引入第三方資源 Bootstrap
相信各位小夥伴就算沒用也肯定有聽過 Bootstrap 這套 CSS 框架吧。該如何加進自己的專案內呢?跟著以下步驟一起學習吧!
首先使用 npm 來安裝 `Bootstrap`
```
npm install bootstrap --save
```
我習慣在 `assets` 底下多開一個資料夾 `vendors` 放入第三方資源，在其中創建 `_bootstrap.scss` 並引入 Bootstrap
```
@import '~bootstrap/scss/functions'; // (選) 若要客製化變數就必須引入
@import 'src/asstes/xxx/variables'; // (選)可以引入自訂變數
@import '~bootstrap/scss/bootstrap'; // (必)若單純引入這支檔案，內容就是整個 Bootstrap，但會無法客製化
```
![](https://i.imgur.com/BkDvbOg.png)

## 結尾
執行 `npm run dev` 編譯檔案，查看 `all.css` ，若有出現 Bootstrap 的代碼就是成功囉!!沒有出現的話，請再次檢查檔案是否有誤。有任何問題都可以在底下留言，我會盡快回覆小夥伴們~~
![](https://i.imgur.com/KFJ7VUE.png)