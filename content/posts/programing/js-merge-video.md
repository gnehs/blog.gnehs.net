---
title: '如何使用 Javascript 將多部影片混合為一個影片'
date: Sat, 06 Jun 2020 15:18:14 +0000
draft: false
categories: ['js','web']
---

最近在製作 [How 發聲器](https://howfun.futa.gg/?text=%E9%9F%93%E5%9C%8B%E7%91%9C%E6%8E%B0%E6%8E%B0) 因為影片每個發音播放時都會有間隙，超討厭，但 [How哥產生器](https://howger.orange.tw/?mode=share&id=5edbb61209015) 聽說是用 ffmpeg 來做輸出，要後端而且看起來很燒錢，所以在尋找純前端的做法。

我先說，這真的有夠搞剛，超級無敵麻煩，另外，如果你用 Node.js 用 fluent-ffmpeg 就好了。

在尋找的時候看到這個 [How do i append two video files data to a source buffer using media source api?](https://stackoverflow.com/a/18026530) ，而且下面的 [解法](http://plnkr.co/edit/KBbopiad1wR25nqtrvxw?p=preview&preview) 還會動，甚至支援不同尺寸影片混合，所以我把它偷過來就好了嗎。

錯誤！
---

他根本不會動，只知道不停地噴錯，明明我放的跟他一樣都是 MP4，我完全不知道他 Demo 怎麼會動 ![](https://i.imgur.com/srj2fND.png)

解法
--

在網路上尋找不同解法後，看了這篇文章「[Transcoding assets for Media Source Extensions](https://developer.mozilla.org/en-US/docs/Web/API/Media_Source_Extensions_API/Transcoding_assets_for_MSE)」，發現是 MP4 少了幾個 Flag 以及 codec 要自己拿 MP4Box 看了之後填進程式碼，拿 ffmpeg 處理過後就會動了。

結果處理時加這行就好了 `-movflags frag_keyframe+empty_moov+default_base_moof` ，害我花了快半天，真棒 ![](https://i.imgur.com/5XRJEnK.png)

Demo
----

你可以使用 Chrome 查看 [How 發聲器](https://howfun.futa.gg/?text=%E9%9F%93%E5%9C%8B%E7%91%9C%E6%8E%B0%E6%8E%B0)

雖然有點音聲不同步，算了隨便啦