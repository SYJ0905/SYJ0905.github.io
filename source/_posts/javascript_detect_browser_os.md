---
title: JavaScript - 判斷瀏覽器版本及作業系統
date: 2020-02-03
tags: 
  - JavaScript
  - w3HexSchool
categories: JavaScript
description: 先前已撰寫過如何判斷 IE 用戶以及使用者裝置等文章，本篇將介紹更詳細的判斷瀏覽器及作業系統。
---
## 前言
前些日子，公司的購物網發現有少許用戶會重複在短時間內 call 相同的 API，為了抓出這些錯誤的來源，只用判定裝置已經是不夠了，必須還要知道使用者的瀏覽器是哪一款、版本號、以及作業系統，這樣後端接收到數據後就知道是哪邊出問題了。

## 瀏覽器、作業系統列表
先整理好需要判斷的資料
``` JavaScript
dataBrowser: [
  {
    string: navigator.userAgent,
    subString: 'Chrome',
    identity: 'Chrome',
  },
  {
    string: navigator.userAgent,
    subString: 'OmniWeb',
    versionSearch: 'OmniWeb/',
    identity: 'OmniWeb',
  },
  {
    string: navigator.vendor,
    subString: 'Apple',
    identity: 'Safari',
    versionSearch: 'Version',
  },
  {
    prop: window.opera,
    identity: 'Opera',
    versionSearch: 'Version',
  },
  {
    string: navigator.vendor,
    subString: 'iCab',
    identity: 'iCab',
  },
  {
    string: navigator.vendor,
    subString: 'KDE',
    identity: 'Konqueror',
  },
  {
    string: navigator.userAgent,
    subString: 'Firefox',
    identity: 'Firefox',
  },
  {
    string: navigator.vendor,
    subString: 'Camino',
    identity: 'Camino',
  },
  {
    // for newer Netscapes (6+)
    string: navigator.userAgent,
    subString: 'Netscape',
    identity: 'Netscape',
  },
  {
    string: navigator.userAgent,
    subString: 'MSIE',
    identity: 'Explorer',
    versionSearch: 'MSIE',
  },
  {
    string: navigator.userAgent,
    subString: 'Gecko',
    identity: 'Mozilla',
    versionSearch: 'rv',
  },
  {
    // for older Netscapes (4-)
    string: navigator.userAgent,
    subString: 'Mozilla',
    identity: 'Netscape',
    versionSearch: 'Mozilla',
  },
],
dataOS: [
  {
    string: navigator.platform,
    subString: 'Win',
    identity: 'Windows',
  },
  {
    string: navigator.platform,
    subString: 'Mac',
    identity: 'Mac',
  },
  {
    string: navigator.userAgent,
    subString: 'iPhone',
    identity: 'iPhone/iPod',
  },
  {
    string: navigator.platform,
    subString: 'Linux',
    identity: 'Linux',
  },
],
```

## 判定設定
程式部分沒有太過艱深，就一直再迴圈判定 `navigator.userAgent` 及各種字串等等。
相關說明我會直接寫在註解內，最後會附上 Github 的完整 Demo 連結。
``` JavaScript
function detect() {
  /* 初始化物件 */
  let BrowserDetect = {
    init() {
      this.browser = this.searchString(this.dataBrowser) || 'An unknown browser';
      this.version = this.searchVersion(navigator.userAgent) || this.searchVersion(navigator.appVersion) || 'an unknown version';
      this.OS = this.searchString(this.dataOS) || 'an unknown OS';
    },
    /* 判定瀏覽器種類 */
    searchString(data) {
      for (let i = 0; i < data.length; i += 1) {
        let dataString = data[i].string;
        let dataProp = data[i].prop;
        this.versionSearchString = data[i].versionSearch || data[i].identity;
        if (dataString) {
          if (dataString.indexOf(data[i].subString) !== -1) {
            const result = data[i].identity;
            /* 加強 Windows 作業系統版本判定 */
            if (result === 'Windows') {
              const userAgentInfor = navigator.userAgent.toLowerCase();
              const windowsVersion = userAgentInfor.substr(userAgentInfor.indexOf('windows nt ') + 11, 4);
              return this.searchOSversion(windowsVersion);
            }
            return result;
          }
        } else if (dataProp) {
          return data[i].identity;
        }
      }
    },
    /* 瀏覽器版本判定 */
    searchVersion(dataString) {
      let index = dataString.indexOf(this.versionSearchString);
      if (index === -1) {
        return;
      }
      return parseFloat(dataString.substring(index + this.versionSearchString.length + 1));
    },
    /* Windows 作業系統版本判定 */
    searchOSversion(version) {
      let resultVersion = '';
      switch (version) {
        case '5.1':
          resultVersion = 'Windows XP';
          break;
        case '6.1':
          resultVersion = 'Windows 7';
          break;
        case '6.3':
          resultVersion = 'Windows 8';
          break;
        case '10.0':
          resultVersion = 'Windows 10';
          break;
        default:
          resultVersion = 'Windows 其他';
          break;
      }
      return resultVersion;
    },
    dataBrowser: [], /* 資料為上一步的陣列內容 */
    dataOS: [], /* 資料為上一步的陣列內容 */
  };
  /* 避免頁面重複判定(非必要) */
  if (typeof BrowserDetect.browser === 'undefined') {
    BrowserDetect.init();
  }
  /* 回傳物件 */
  const info = {
    info_os: BrowserDetect.OS,
    info_browser: BrowserDetect.browser,
    info_browser_version: BrowserDetect.version,
    info_resolution: `${window.screen.width} x ${window.screen.height}`,
    BrowserDetect,
  };

  return info;
}
const detectDevice = detect();
console.log(detectDevice);
```

## 結尾 Demo
[JavaScript - 判斷瀏覽器版本及作業系統](https://syj0905.github.io/detect_browser_os/)
開啟後查看一下 `console` 如果有出現以下圖片代表成功囉!!
![判斷瀏覽器版本及作業系統](https://i.imgur.com/7Jqb0LD.png)
基本上以上範例是可以打包成 .js 檔的，其餘就是看各位的專案適用哪種方式再引入 JS 檔啦。

## 參考資料
[JavaScript 判斷瀏覽器種類及作業系統](https://frank198978104.github.io/2017/11/30/browser-and-os-detect/)
[利用Javascript判斷作業系統的型別實現不同作業系統下的相容性](https://codertw.com/%E5%89%8D%E7%AB%AF%E9%96%8B%E7%99%BC/291616/)