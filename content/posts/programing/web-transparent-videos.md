---
title: '怎麼輸出網頁上可用的透明影片'
author: '勝勝'
tags: ['Firefox','Chrome'] 
date: 2020-04-07T14:32:39+08:00
draft: false
categories: ['js','web']
---
你有看過透明影片嗎，有想過在網頁上放超酷的透明影片製造與眾不同的視覺效果嗎，這篇教學會一步一步教你如何將透明影片放在網頁上，並講述現有瀏覽器的限制。
# 技術限制
現在幾乎各大瀏覽器像是 Firefox、Chrome 跟 Safari 都支援了，但 Safari 跟大家不一樣，所以你必須分別為 Safari 輸出另一種格式的影片。 

## Chrome
Chrome 在 v31 就支援了透明影片，但截至目前 v100 僅支援格式為 VP8 或 VP9 的 WebM 影片檔案。
- [Alpha transparency in Chrome video](https://developer.chrome.com/blog/alpha-transparency-in-chrome-video/)
## Firefox
Firefox 我沒特別查，反正會動
## Safari
Safari 目前（Safari 15.4）僅支援格式為 HEVC 帶有 Alpha 圖層的 .mov 影片檔案，VP9 格式雖然支援，但是顯示不出透明效果，你可以在蘋果的網站上找到相關說明。
- [HEVC Video with Alpha - WWDC19](https://developer.apple.com/videos/play/wwdc2019/506/)
# 影片製造
在這裡我先用 AE 輸出含有 Alpha 圖層的 QuickTime 格式檔案
![](/img/2022-04-07_17.14.02.png)
## 輸出 Safari 格式（HEVC）
Safari 的部分超級麻煩，反正蘋果就是專門來坑開發者的，不過 ffmpeg 目前似乎還不支援輸出透明的 HEVC，這邊用了 Compressor 示範。

雖然 AE 可以直接輸出透明的 mov 檔案，但輸出的 mov 檔案太大而且也沒辦法在 Safari 播放，所以你還是需要轉檔。
![](/img/2022-04-07_17.17.02.png)
*Compressor 的輸出設定值，別忘了勾上 Preserve alpha*

![](/img/2022-04-07_17.18.02.png)
*輸出後可以把影片直接丟進 Safari 看看有沒有變透明*
## 輸出 Chrome 格式（WebM）
這部分就簡單了些，你只需要安裝 [AdobeWebM](https://github.com/fnordware/AdobeWebM) 就可以在 Adobe 軟體中直接輸出該格式。
![](/img/2022-04-07_16.50.53.jpg)
*Adobe Media Encoder 的輸出設定值，別忘了勾上 Include Alpha Channel*

此外 [Handbrake](https://handbrake.fr/downloads.php) 與 [ffmpeg](https://www.ffmpeg.org/download.html) 也支援輸出該格式的影片。
# 放到網頁上
使用下面的程式碼將影片放到網頁上，這樣就可以在網頁上播放了，這邊要特別注意，給 Safari 的影片要在最上面，不然他吃到 VP9 的影片魔法就會消失了。
```html 
<video autoplay loop muted playsinline>
  <source 
    src="/path/to/video-hevc.mov" 
    type='video/mp4; codecs="hvc1"'>
  <source 
    src="/path/to/video-webm.webm" 
    type="video/webm">
</video>
```
# 參考資料
- [How to make HEVC, H265 and VP9 videos with an alpha channel for the web](https://kitcross.net/hevc-web-video-alpha-channel/)
- [How to use transparent videos on the web in 2021](https://rotato.app/blog/transparent-videos-for-the-web)