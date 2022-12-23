---
title: '讓 Google Drive 下載的解壓檔解壓縮到相同資料夾'
author: '勝勝'
tags: ['Google Drive','Zip']
date: 2022-12-24T01:32:00+08:00
draft: false
categories: ['Software']
---
勝勝剛從 Google Drive 撈了一個資料夾下來，可是你也知道的，Google 會把它拆成很多小的壓縮檔，於是解壓縮後就會變成這樣
- abc
- abc 1
- abc 2
- ...

勝勝希望可以將解壓縮的檔案都放在一起，經過勝勝的調查，發現了這個指令
```bash
mkdir combined
for archive in *.zip; do ditto -V -x -k --sequesterRsrc --rsrc "$archive" combined; done
```
這樣就會把目前資料夾內的 zip 檔案通通解壓縮，並丟到 `combined` 資料夾內，也順帶解決參考資料第一個中會出現 UTF-8 編碼錯誤的問題

> 參考資料
> https://stackoverflow.com/questions/68201952/merge-combine-multiple-downloaded-zip-files-from-google-drive-on-mac
> https://github.com/CocoaPods/CocoaPods/issues/7711