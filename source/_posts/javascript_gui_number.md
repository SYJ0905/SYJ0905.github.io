---
title: JavaScript - 統一編號驗證實作
tags:
  - JavaScript
  - Vue
categories:
  - JavaScript
description: 用最簡單的方式來做統一編號驗證吧!!
abbrlink: 2134109134
date: 2019-11-19 00:00:00
---
## 前言
雖然說後端也能做統編驗證，但實務上客戶在下單後，後端還要處理統編驗證再回傳確實會不夠快速。
所以選擇在輸入時前端就直接根據輸入的內容進行判斷來做提示，或是能否進一步結帳等行為。

## 統一編號說明
統一編號（簡稱：統編）是臺灣營利事業機構的個別法人身分代號，為一組8位數字。機構有開統編及未開統編公司課的稅賦是相同的。
驗證規則如下: 
* 假設統一編號為 A B C D E F G H
* A - G 為編號, H 為檢查碼
* A - G 個別乘上特定倍數, 若乘出來的值為二位數則將十位數和個位數相加
* A x 1
* B x 2
* C x 1
* D x 2
* E x 1
* F x 2
* G x 4
* H x 1
* 最後將所有數值加總, 被 10 整除就為正確
* 若上述演算不正確並且 G 為 7 得話, 再加上 1 被 10 整除也為正確

## 驗證範例 - 傳統形式
直接上 code 吧!!
``` JavaScript
function check_tax_number() {
  const gui_number = document.querySelector('.gui_number').value; // 取欄位內容
  const cx = [1, 2, 1, 2, 1, 2, 4, 1];
  const cnum = gui_number.split('');
  let sum = 0;
  function cc(num) {
    let total = num;
    if (total > 9) {
      let s = total.toString();
      const n1 = s.substring(0, 1) * 1;
      const n2 = s.substring(1, 2) * 1;
      total = n1 + n2;
    }
    return total;
  }
  if (gui_number.length !== 8) {
    alert('統編錯誤，要有 8 個數字');
    return;
  }
  cnum.forEach((item, index) => {
    if (gui_number.charCodeAt() < 48 || gui_number.charCodeAt() > 57) {
      alert('統編錯誤，要有 8 個 0-9 數字組合');
      return;
    }
    sum += cc(item * cx[index]);
  });
  if (sum % 10 === 0) {
    alert('統編正確');
  } else if (cnum[6] === '7' && (sum + 1) % 10 === 0) {
    alert('統編正確2');
  } else {
    alert('統編錯誤');
  }
}
```
``` HTML
<body>
  <input type="text" class="gui_number" name="gui_number" maxlength="8">
  <input type="button" value="驗證" onclick="check_tax_number()">
</body>
```

## 驗證範例 - Vue
``` JavaScript
methods: {
  check_tax_number() { // 統編驗證
    const vm = this;
    const cx = [1, 2, 1, 2, 1, 2, 4, 1];
    if (vm.receipt_taxnum.length !== 8) { // receipt_taxnum v-model 綁定欄位
      vm.receipt_taxnum_hint = '統編錯誤，要有 8 個數字'; // receipt_taxnum_hint 我自定義的提示
      return;
    }
    let sum = 0;
    let cnum = vm.receipt_taxnum.split('');
    function cc(num) {
      let total = num;
      if (total > 9) {
        let s = total.toString();
        const n1 = s.substring(0, 1) * 1;
        const n2 = s.substring(1, 2) * 1;
        total = n1 + n2;
      }
      return total;
    }
    cnum.forEach((item, index) => {
      sum += cc(item * cx[index]);
      if (sum % 10 === 0) {
        vm.receipt_taxnum_hint = '';
      } else if (cnum[6] === '7' && (sum + 1) % 10 === 0) {
        vm.receipt_taxnum_hint = '';
      } else {
        vm.receipt_taxnum_hint = '統一編號錯誤';
      }
    });
  },
}
```
``` HTML
<input type="tel" placeholder="請輸入統編" minlength="8" maxlength="8"
  v-model="receipt_taxnum" @input="check_tax_number()">
<span class="text-danger">{{ receipt_taxnum_hint }}</span>
```

## 結尾
驗證規則不算太複雜，可根據自己的寫法來調整呦，本篇提供兩種寫法供大家參考，感謝各位觀看!!
