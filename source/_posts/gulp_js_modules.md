---
title: Gulp - 使用 Browserify 解決 JavaScript 模塊化問題
tags:
  - Gulp
  - JavaScript
  - w3HexSchool
categories:
  - Git
description: 本文將介紹如何在 Gulp 中使用 ES6 的 import export 功能。
abbrlink: 2647002883
date: 2020-04-05 00:00:00
---
## 前言
相信各位使用 `Gulp` 時都會搭配 `gulp-concat` 合併檔案，但如果是 `JS` 要 `import` 其他檔案(ex: JS、JSON) 就不能用 `gulp-concat`　合併而已，因為這樣會在使用的時候，出現　xxx(import 進來的變數宣告) is not defined。
`gulp-concat` 只是純粹合併檔案，沒有包括 `ES6` 的解析功能，所以若是不加以處理的話，會在合併過後的 `JS` 檔依舊出現 `import xxx from '../data.js'` 這樣的程式碼哩。

## 安裝套件
輸入以下安裝代碼
```
npm install  browserify -S
npm install vinyl-source-stream -S
npm install vinyl-buffer -S
```
並在 `gulp.js` 添加任務
``` JavaScript
var browserify = require('browserify'); /* 插件，實際是 node 系 */
var stream = require('vinyl-source-stream'); /* 轉成 stream 流，gulp 系 */
var buffer = require('vinyl-buffer'); /* 轉成二進制流，gulp 系 */

gulp.task('browserify', () => 
  browserify('./src/js/main.js') /* 合併過後的 js 檔 */
    .bundle()
    .pipe(stream('main.js'))
    .pipe(buffer())
    .pipe(gulp.dest('./dist/js')) /* 輸出檔案位置 */
    .pipe(browserSync.stream()) /* 若有使用 browserSync 就需要加 */
);
/* 清除編譯後 js */
gulp.task('cleanJs', () =>
  gulp.src(['./src/js/main.js', './src/js/main.js.map'], { read: false, allowEmpty: true })
    .pipe($.clean())
);

/* 正式環境任務 */
gulp.task('build',
  gulp.series(
    'js',
    'browserify',
    'cleanJs',
  )
)

/* 測試環境任務 */
gulp.task('default',
  gulp.series(
    'js',
    'browserify',
    'cleanJs',
    function (done) {
      browserSync.init({
        server: {
          baseDir: "./dist"
        },
        reloadDebounce: 2000
      });
      gulp.watch(['./src/js/**/*.js', '!./src/js/main.js', '!./src/js/main.js.map'], gulp.series('js', 'browserify', 'cleanJs'));
      done();
    }
  )
)
```

## 測試
接下來在就可以在個別的 `JS` 檔中使用 `import`、`export` 功能
ex: 在 `all.js` 中引入 `json` 檔
``` JavaScript
/* all.js */
import languageData from '../data/language.json';
(function($) {
  console.log(languageData);
})(jQuery);
```
執行 `gulp` 後即可看到 `import` 進來的 json 資料，同理也可使用在 `js` 的 `modules function` 上。

## 參考資料
[在 Gulp 中使用 Browserify](https://csspod.com/using-browserify-with-gulp/)
[gulp + browserify 搭建es6环境](https://www.jianshu.com/p/34d9782f9cd6)


