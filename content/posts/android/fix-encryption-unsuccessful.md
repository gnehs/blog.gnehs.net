---
title: '解決刷機產生的Data分區加密問題'
author: '勝勝'
tags: ['root','TWRP','F2FS'] 
date: 2017-02-28T03:07:59+08:00
draft: false
categories: ['android']
---

我是不知道其他系統或手機能不能用啦，反正我 P9 是成功了<!--more--> ![](https://i.imgur.com/wbDD7Hs.png) 就是這個 Encryption Unsuccessful 害我浪費了一小時生命 :( ![](https://i.imgur.com/cqgzetq.jpg) 首先進入TWRP，選"Wipe" ![](https://i.imgur.com/YkyVBsj.jpg) 選"Advanced Wipe" ![](https://i.imgur.com/vix1hnZ.jpg) "Data"分區打勾，進入"Repair or Change File System" ![](https://i.imgur.com/T88QQma.jpg) 選"Change File System" ![](https://i.imgur.com/J7aCo4u.jpg) 選"F2FS" \*我是不知道為什麼要選 F2FS 啦，也許你可以試試其他的 ![](https://i.imgur.com/0Jw4lNw.jpg) 滑過去就好了 參考文章 ["Encryption Unsuccessful" CROMBI-KK and GRIMKERNEL](https://forum.xda-developers.com/transformer-tf300t/help/encryption-unsuccessful-crombi-kk-t2804606) [ \[How To\] Install OxygenOS 2.2.0 Update (Root/Non Root Users) Without Data Loss!!](https://forums.oneplus.net/threads/how-to-install-oxygenos-2-2-0-update-root-non-root-users-without-data-loss.412517/page-8#post-14143361)