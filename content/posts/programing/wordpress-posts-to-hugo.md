---
title: '將 WordPress 文章匯入到 Hugo'
date: 2021-03-14T21:31:50+08:00
draft: false
categories: ['hugo']
---

Hugo 官方有推薦幾個套件來協助文章的遷移，我先是先用了 [wordpress-to-hugo-exporter](https://github.com/SchumacherFM/wordpress-to-hugo-exporter)，不過安裝後似乎無法成功開啟。

之後我用了 [blog2md](https://github.com/palaniraja/blog2md) 便能順利匯入文章了。
# 事前準備
1. 將文章從 WordPress 匯出
1. 下載 [blog2md](https://github.com/palaniraja/blog2md)
1. 安裝 [Node.js](https://nodejs.org/en/)
# 開始轉換
1. `cd ./blog2md-master/` 
1. 安裝 node 套件（註：需要 node.js） `npm i`
1. 轉換檔案 `node index.js w your-wordpress-backup-export.xml out`

之後將 `out` 資料夾中的內容複製到 `/content/posts` 就完工了！