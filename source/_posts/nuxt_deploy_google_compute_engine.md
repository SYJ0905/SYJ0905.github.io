---
title: Nuxt 部署策略 - 部署 Google Compute Engine
tags:
  - Nuxt
  - JavaScript
categories:
  - Vue
description: 本篇將介紹如何將 Nuxt 專案部署至 GCE (Google Compute Engine)
abbrlink: 868523524
date: 2021-02-05 14:30:00
---
## 建立 Google Compute Engine 環境

* 建立 VM 執行個體
![建立 VM 執行個體](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/Nuxt%20%E9%83%A8%E7%BD%B2%E7%AD%96%E7%95%A5%20-%20%E9%83%A8%E7%BD%B2%20Google%20Compute%20Engine%20%2F%E5%BB%BA%E7%AB%8B%20GCE.jpg?alt=media&token=651a1011-d3eb-4797-99ac-78001a75a1bb)

* 執行個體設定
需要設定 `cpu`、`ram` 以及這台虛擬主機的`作業系統`
請參考底下流程:
![VM 規格設定](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/Nuxt%20%E9%83%A8%E7%BD%B2%E7%AD%96%E7%95%A5%20-%20%E9%83%A8%E7%BD%B2%20Google%20Compute%20Engine%20%2FVM%20%E8%A6%8F%E6%A0%BC%E8%A8%AD%E5%AE%9A.JPG?alt=media&token=c3fbc10c-25e9-43cc-b14a-3603855a9d94)

![設定開機硬碟](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/Nuxt%20%E9%83%A8%E7%BD%B2%E7%AD%96%E7%95%A5%20-%20%E9%83%A8%E7%BD%B2%20Google%20Compute%20Engine%20%2F%E8%A8%AD%E5%AE%9A%E9%96%8B%E6%A9%9F%E7%A1%AC%E7%A2%9F.JPG?alt=media&token=054b476e-9ed7-4b99-bc5a-4d92aa52394b)

![設定開機硬碟細節](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/Nuxt%20%E9%83%A8%E7%BD%B2%E7%AD%96%E7%95%A5%20-%20%E9%83%A8%E7%BD%B2%20Google%20Compute%20Engine%20%2F%E8%A8%AD%E5%AE%9A%E9%96%8B%E6%A9%9F%E7%A1%AC%E7%A2%9F%E7%B4%B0%E7%AF%80.JPG?alt=media&token=03b1a78f-fbb2-4f8c-9d77-1fc951bd28f0)

## 虛擬主機 linux 設定

選擇 `在瀏覽器視窗中開啟`，稍等一下後就會進入虛擬主機的 linux 介面
![linux 介面](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/Nuxt%20%E9%83%A8%E7%BD%B2%E7%AD%96%E7%95%A5%20-%20%E9%83%A8%E7%BD%B2%20Google%20Compute%20Engine%20%2F%E9%96%8B%E5%95%9F%20linux%20%E4%BB%8B%E9%9D%A2.JPG?alt=media&token=454cd67a-e97e-40fa-9386-b66db221c9c7)

## 專案安裝 Nuxt 架站套件

需要先在本機端安裝 `pm2`、`nuxt-start`，

* pm2
直接在全域安裝即可

``` npm
npm install pm2 -g
```

接著要初始化 `pm2` 執行文件

``` CMD
pm2 init
```

接著會產生 `ecosystem.config.js` 的文件，也會有預設的內容
不過可以先使用以下範例就好，其他先註解沒關係，因為都是在優化主機而已

``` JavaScript
module.exports = {
  apps: [
    {
      name: 'nuxt-sample',
      script: './node_modules/nuxt-start/bin/nuxt-start.js',
      instances: 'max', /* 負載平衡模式下的 CPU 數量 */
      exec_mode: 'cluster', /* CPU 負載平衡模式 */
      max_memory_restart: '1G', /* 緩存了多少記憶體重新整理 */
      port: 3001, /* 指定伺服器上的 port */
    },
  ],
};
```

* nuxt-start
安裝在專案內

``` npm
npm install nuxt-start
```

## 本機端測試生產環境

上面步驟設定完後執行以下指令，讓本機端當做一台伺服器開啟網站

``` powershell
npm run build
```

``` powershell
pm2 start
```

接著執行 `http://localhost:3001/` 若有正確執行 nuxt 專案，代表已經在本機端測試成功
接下來就是要在 GCE 中也安裝這些內容，並執行 `pm2 start`

![pm2 start](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/Nuxt%20%E9%83%A8%E7%BD%B2%E7%AD%96%E7%95%A5%20-%20%E9%83%A8%E7%BD%B2%20Google%20Compute%20Engine%20%2Fpm2%20start.JPG?alt=media&token=8daf9384-dcf0-4874-89ca-f83cff50b1f5)

## VM 安裝套件

首先進入到 vm 的 linux 介面，安裝 `node.js、pm2、nginx、git`

* 安裝 node.js

``` linux
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
```

安裝與專案相同的 node 版本

``` linux
nvm install v10.15.0
```

* 安裝 pm2

``` linux
npm install -g pm2
```

* 安裝 git

先更新套件指令

``` linux
sudo apt update
```

再執行安裝指令

``` linux
sudo apt install git
```

* 安裝 nginx

先更新套件指令

``` linux
sudo apt update
```

再執行安裝指令

``` linux
sudo apt install nginx
```

## linux 取得專案

使用 Git 將專案拉到虛擬主機上，接著就依序執行部署指令

``` linux
npm install
npm run build
pm2 start
```

沒出錯的話就表示已經在 vm 上執行成功

## DNS 與 IP 設定

需要將 GCE 的 IP 改成靜態
![IP 設定](https://firebasestorage.googleapis.com/v0/b/cloud-f2e-blog.appspot.com/o/Nuxt%20%E9%83%A8%E7%BD%B2%E7%AD%96%E7%95%A5%20-%20%E9%83%A8%E7%BD%B2%20Google%20Compute%20Engine%20%2FIP%20%E8%A8%AD%E5%AE%9A.JPG?alt=media&token=44ef472c-e898-408e-865c-849fc976fce1)

接著到`網域註冊商將 DNS 指向 靜態IP`，這部分可以直接請負責人員設定或是自己去買一個來玩玩

## nginx 設定

在 linux 中輸入以下指令:
<註> `yourdomain` 請填寫是要使用的網域

``` linux
cd /etc/nginx
cd conf.d
sudo nano yourdomain.conf
```

執行完後會出現一個編輯器，複製以下範例即可

``` linux
server {
  server_name yourdomain.com www.yourdomain.com;
  location / {
    proxy_pass http://localhost:3001; 
  }
}
```

接下來重新整理 nginx

``` linux
sudo nginx -s reload
```

最後在本機上打開網址 `yourdomain.com` 應該就會看到 Nuxt 專案內容了。

## Https 設定

使用 `SSL For Free` 服務，取得免費 SSL 憑證，憑證發行機構是 `Let's Encrypt`
另外，憑證每三個月會過期，需要取得新憑證
而 linux 透過 `certbot` 來自動更新憑證

安裝流程:

``` linux
sudo apt-get update
sudo apt-get install software-properties-common // 載入 certbot 的 ppa
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
sudo apt-get install python-certbot-nginx

sudo certbot --nginx // 產生憑證
sudo nginx -s reload

sudo certbot renew --dry-run // 檢查憑證續約狀況
sudo certbot renew // 執行憑證續約動作
```

## 手動完整部署流程

1. 本地端開發 develop
2. commit
3. master merge develop
4. 登入 linux 主機
5. cd 專案
6. git pull origin master
7. npm run build
8. pm2 reload id

執行上述步驟，Nuxt 專案就會更新完成囉。

## 指令整理

* pm2

``` linux
pm2 start // 啟動 pm2 → ecosystem.config.js
pm2 list  // 查看目前有架多少站台
pm2 delete 3 // 刪除id為3的站台
pm2 delete all   // 刪除所有站台 
pm2 reload all  // 重新整理所有站台
pm2 save // 儲存目前的pm2 站台，重開機後會還原
pm2 log // pm2出錯時擬難排除 
```

* nginx

``` linux
sudo nginx  // 啟動 nginx 伺服器 (預設裝好己啟動)
sudo nginx -s reload // 重整nginx 伺服器
sudo nginx -s stop // 快速停止伺服器
cd /etc/nginx // nginx 位置
cd /var/log/nginx // nginx log 檔位置

```

## 參考資料

[How to Install Git on Ubuntu 18.04](https://linuxize.com/post/how-to-install-git-on-ubuntu-18-04/)
[How To Install Nginx on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-18-04)
[PM2 官網](https://pm2.keymetrics.io/docs/usage/pm2-doc-single-page/)
[5個提高Node.js應用性能的技巧](https://kknews.cc/code/zmxjx3.html)
[Using NGINX as a reverse proxy](https://zh.nuxtjs.org/docs/2.x/deployment/nginx-proxy/)
[letsencrypt](https://letsencrypt.org/)
[SSL For Free](https://www.sslforfree.com/)
[certbot](https://certbot.eff.org/)
