---
title: Security - SSH keys 或 HTTPS 設定步驟
tags:
  - SSH
  - Security
categories:
  - Security
description: 本篇來介紹如何生成 SSH 並且綁定 Github 帳號
abbrlink: 3632503978
date: 2021-04-06 11:59:00
---
## SSH (Secure Shell)

SSH 是指遠端登入協定，特色在於處理作業採用加密機制，安全性高，可以避免資料竊取或外洩的問題。
以往在 Github 都是採用 `Https` 來 clone 專案下來，但此方式存在著安全性問題。
如果是 Windows 系統的話，可以搜尋 `認證管理員`，你就會在視窗中查到有關 Github 的帳號密碼或是暫時性的帳號。
然而，使用 `SSH` 則會避免這種狀況發生，接下來就依序產生 SSH 並綁定 Github 帳號吧。

## SSH 公私鑰

由於 Windows 在 1803 版提供了 OpenSSH 工具，所以不用額外安裝，可以使用 `CMD` or `git bash` 來輸入指令

* 生成公私鑰
有兩種指令都可以生成公私鑰

``` CMD
ssh-keygen -t rsa -C "your_email@example.com"
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

* 指定 SSH Keys 位置及名稱
會出現 Generating public/private rsa key pair.
接著可以指定 SSH keys 要放的位置，如果不設定，Windows 預設的位置是：/c/Users/user/.ssh/id_rsa
由於 SSH 可以生成多組，所以這邊可以替 SSH 重新命名，以便綁定不同 Github 帳號喔。

``` CMD
/c/Users/user/.ssh/自定義名稱_rsa
```

後續會詢問要不要設定密碼之類的，不想設定就一路 Enter 下去即可

* 查看 SSH 檔案
查看 `C:\Users\user\.ssh` 內是否以下兩個檔案:
`id_rsa`：私鑰 private key，這是給自己用的。
`id_rsa.pub`：公鑰 public key，這是給外部系統用的，綁定 Github 帳戶就是用這個

* 綁定 Github
Github 點頭像 > Settings > Account settings > SSH and GPG keys
選擇 `News SSH key`，`title` 自行命名即可
將 `id_rsa.pub` 中的內容完整複製到 `Key` 輸入欄內(可以用 VSCODE 開啟 `id_rsa.pub`)
綁定後會寄封郵件，再重新整理就會看到 SSH 了

* 設定 SSH agent

``` CMD
ssh -T git@github.com
```

因為是首次連線，而且無法確認 host 主機的真實性，只知道這個即將連結的遠端主機的 SSH key fingerprint，是否確定要連線？

`GitHub’s SSH key fingerprints`：官方提供比對的 fingerprint。
可以跟 `Git Bash` 出現的「Github RSA key fingerprint is SHA256…」
比對確認與 Github 官方提供的一樣之後，再輸入 yes。
沒意外的話，應該就可以連線了。

* SSH agent
開啟 SSH agent 的指令，成功的話會回傳 Agent pid 59566

``` CMD
eval $(ssh-agent -s)
```

把 key 加到 SSH agent 的指令，完成此步驟之後就可以在 Github 中使用 SSH 方式 Git clone 專案

``` CMD
ssh-add ~/.ssh/id_rsa
```

檢查是否有現存的 SSH keys，有的話就不用重新產生啦！

``` CMD
ls -al ~/.ssh
```

## 參考資料

[Git 踩坑紀錄（二）git clone with SSH keys 或 HTTPS 設定步驟](https://tsengbatty.medium.com/git-%E8%B8%A9%E5%9D%91%E7%B4%80%E9%8C%84-%E4%BA%8C-git-clone-with-ssh-keys-%E6%88%96-https-%E8%A8%AD%E5%AE%9A%E6%AD%A5%E9%A9%9F-bdb721bd7cf2)
