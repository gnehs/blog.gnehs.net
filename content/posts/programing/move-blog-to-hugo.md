---
title: '將部落格遷移到 Hugo'
author: '勝勝'
tags: ['Hugo']
date: 2021-03-20T15:30:50+08:00
draft: false
categories: ['hugo']
---
# 前言
其實我之前就打算把部落格從 WordPress 搬走了，只是之前都懶得弄。

Hugo 除了很快之外，也能直接用 Markdown 來寫文章，除此之外不需要資料庫用起來真的很香。
# 為什麼是 Hugo
先前嘗試過 Hexo，但是上面的主題感覺好少而且很多~~都不是很漂亮~~，相較之下，Hugo 除了有很多漂亮的主題，執行速度也比 Hexo 快很多，因此就選擇了 Hugo 作為我的部落格。
# 初始化 Hugo
## 安裝
如果你有安裝 [Homebrew](https://brew.sh/index_zh-tw) 的話，在 macOS 上只要 `brew install hugo` 就裝好了！

如果你用其他系統請查看 [官方安裝文件](https://gohugo.io/getting-started/installing)
## 看看你有沒有裝好
在終端機輸入 `hugo version`，沒意外的話應該可以看到 Hugo 版本號
```bash
$ hugo version
hugo v0.81.0+extended darwin/amd64 BuildDate=unknown
```
## 建立部落格
使用底下指令在目前資料夾建立以 `<blog-name>` 為名的部落格
```sh
hugo new site <blog-name>
```

耶，此時你的部落格就建立好了，讓我介紹一下這些可愛的資料夾結構ㄅ
# 設定 Hugo 
## 安裝主題
建立好部落格後，可以到 [https://themes.gohugo.io/](https://themes.gohugo.io/) 找找喜歡的主題，並按照主題開發者的安裝指南來設定部落格。
## 文章遷移
如果你剛好也用 WordPress ，可以看看 [將 WordPress 文章匯入到 Hugo](http://blog.gnehs.net/wordpress-posts-to-hugo/) 來了解如何將 WordPress 文章轉換為 Hugo 可用之格式。

若為其他 Blog 系統也可以參考 [官方文件](https://gohugo.io/tools/migrations/) 來將文章遷移到 Hugo。
## 試運行
一切準備就緒後，可以試試看 `hugo server -D` 在本機執行伺服器試試看運行是否正常。

## 部署
直接執行 `hugo`，便可在 `public` 資料夾找到 build 後的網站。

將 `public` 資料夾中的檔案丟到伺服器上就好了，你可以查看 [利用 GitHub Action 自動部署 Hugo 部落格](http://blog.gnehs.net/hugo-github-actions/) 來看看如何部署到 GitHub Pages。
# 總結
靜態網站跑起來真的很快，在 GitHub Pages 上也可以運作，不必再另外找伺服器。
# 參考資料
- [官方文件](https://gohugo.io/getting-started/quick-start/)

# 相關文章
- [將 WordPress 文章匯入到 Hugo](http://blog.gnehs.net/wordpress-posts-to-hugo/)
- [利用 GitHub Action 自動部署 Hugo 部落格](http://blog.gnehs.net/hugo-github-actions/)