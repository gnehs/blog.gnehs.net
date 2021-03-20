---
title: '[64位元]將模擬市民 2 語言更改為繁體中文'
date: Tue, 27 Jun 2017 16:12:12 +0000
draft: false
categories: ['game']
---

最近想來玩一下，但是不知道出了什麼差錯，居然變成了英文，然後網上的教學都不管用，因為我是 64 位元的 QQQ ![](https://i.imgur.com/EOSnM0u.png) 好了，廢話不多說，按下"Win"+"R"鍵後輸入"regedit"來打開登錄檔編輯程式 ![](https://i.imgur.com/765Ks8V.png)進到"HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Wow6432Node\\EA GAMES\\The Sims 2 Mansion and Garden Stuff\\1.0"裡面 \*The Sims 2 Mansion and Garden Stuff 為你電腦裡最新安裝的 資料片/物品包 名稱 ![](https://i.imgur.com/34J4GWK.png) 雙擊"Language"，確定底數是"十六進位"後將裏頭的數字改為"12" ![](https://i.imgur.com/R09t9P4.png) 接著雙擊"LanguageName"，將資料改成"Traditional Chinese" 弄好之後就能打包走人了www

* * *

附上懶人登錄檔，把裏頭的內容貼到記事本存成 xxx.reg 就能用了，如果你真她喵懶的話，[點這裡直接下載](https://gist.github.com/anonymous/a4ffed2052e5dd42c33d04fc20850e5e/archive/eb7c783580616f7c6f7738d428c181e5dd687f2b.zip)