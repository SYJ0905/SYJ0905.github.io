---
title: Git - 重新命名分支
tags:
  - Git
  - GitHub
categories:
  - Git
description: 本篇將介紹如何在不刪除分支情況下，重新命名分支名稱。
abbrlink: 2627644797
date: 2020-11-15 00:00:00
---
## 指令介紹
* `git branch -m [old branch name] [new branch name]`
  * old branch name: 舊分支名稱 ex: Cloud
  * new branch name: 新分支名稱 ex: newCloud

* `git push origin -m [new branch name] :[old branch name]`
  ex: git push origin -m newCloud :Cloud
  如此一來，就可以在 github 上看到重新命名的分支了。

## 注意
由於 `master` 是主分支，所以並不能替 `master` 重新命名，這點要特別注意。


## 參考資料
[GitHub 重新命名分支名稱](https://hsiangfeng.github.io/git/20190802/1198998279/)