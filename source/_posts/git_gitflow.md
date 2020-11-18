---
title: Git Flow 與 Commit 團隊協作規範
tags:
  - Git
  - Git Flow
categories:
  - Git
description: 本篇將介紹在團隊協作時該如何使用 Git Flow 的分支概念，並且搭配有規範的 Commit 說明，如此將有效的管理專案版控。
abbrlink: 138987188
date: 2020-11-04 00:00:00
---
## Git Flow
於 2010 年提出的[`開發流程觀念`](https://nvie.com/posts/a-successful-git-branching-model/)，往後還有其他諸如 `GitHub Flow`、`Gitlab Flow`，而這些流程的最終目的都是 `讓專案變得更好維護管理`

## 分支介紹
主要會有 `main`、`develop`、`hotfix`、`release` 以及 `feature`，除了 `main`、`develop` 兩個以外，其餘都會因為完成該分支任務後就被刪除，而這兩個又被稱為長期分支，一直會保存在整份版控內。
以下將介紹各分支的主要負責範疇:
* main (原為 master，於 2020/10變更)
[master更名成main](https://www.ithome.com.tw/news/140094)
主要為穩定、上線的版本，分支來源僅能從其他分支合併過來，不該允許開發者直接 `commit` 到 `main` 分支。一般在專案初期環境建好後都會拉出 `develop` 分支出去，並維持 main 分支獨立性。

* develop
為所有開發分支的基礎，也就是說當新增/修改功能的時候，都由此分支切出去，而完成之後會合併於此分支

* hotfix
當線上版本發生緊急問題需要修復的時候，會由 `main` 切出一個 `hotfix` 分支修復進級問題，修復完成後也會合併回 `main` 分支，但也記得要合併到 develop 分支。
由於 develop 可能還在開發中，所以一開始並不會從 develop 切出 `hotfix` 分支，避免在合併到 `main` 分支時出現更嚴重問題。

* feature
當需要開發新功能時，會從 develop 切出 `feature` 分支，並且在分支命名上會採用 `feature/功能名稱` 的形式，是由於若只使用 `feature` 作為分支名稱，會讓其他團隊成員無法開 `feature/功能名稱` 的分支，這是 Git 開分支原則所導致的。

* release
由 develop 切出來，是當仗勢上線前的最終測試分支，測試通過後會將 `release` 合併到 `main` 以及 `develop`，以確保在 `release` 時有修正一些問題能同步到 `main` `develop`。

## Git Commit 規範
Commit 的 type
* `feat` - 新增/修改功能
* `fix` - 修正 Bug
* `docs` - 修改/新增文件
* `style` - 修改程式碼格式或風格，不影響原有運作，ex: ESLint、stylelint..etc
* `refactor` - 重構 or 優化，不屬於 bug 也不屬於新增功能等
* `test` - 增加測試功能
* `chore` - 增加或修改第三方套件等

必須將以往執行 `git commit -m 'xxxx'` 方式改成 `git commit`，會出現 `vi編輯器`，隨後開始編輯([i]鍵)，完成後則結束編輯([:] 鍵)，最後輸入 `wq`(儲存[q]、編輯[q])，就會上傳 Commit。


## 參考資料
[Git Flow 是什麼？為什麼需要這種東西？](https://gitbook.tw/chapters/gitflow/why-need-git-flow.html)
[淺談 Git Flow 與 commit 規範](https://hsiangfeng.github.io/git/20200914/1124442109/)


