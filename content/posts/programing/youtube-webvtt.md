---
title: 'YouTube 字幕特效是如何製作的？'
author: '勝勝'
tags: ['YouTube'] 
date: 2019-01-29T15:21:05+08:00
draft: false
categories: ['web']
---

因為時不時可以在一些 MV 裡看見一些很庫蹦來蹦去的字幕，於是便上網搜尋，了解後發現 YouTube 用了 webVTT 當作字幕好朋友來用，可以隨意更改位置和大小，看起來應該是類似 SRT 那樣。

像是這首
{{< youtube HIRiduzNLzQ >}} 

和這首
{{< youtube wIft-t-MQuE >}} 

若要為 YouTube 上的字幕改一點位置，利用 [youtube-dl](https://github.com/rg3/youtube-dl) 把字幕下載下來後就可以來亂改位置了

> ```
> youtube-dl --skip-download --sub-format vtt --write-sub --sub-lang zh-TW <link>
> ```

![](https://i.imgur.com/lALbVtT.png)

字幕搞下來後拿個編輯器打開就可以改了

![](https://i.imgur.com/h0llxmF.png)

> ```
> 00:00:00.000 --> 00:00:07.075
> 這是原本的字幕
> ```

![](https://i.imgur.com/3FmQLy7.png)

> ```
> 00:00:00.000 --> 00:00:07.075 align:left size:35% position:0%
> 在時間後方加上一些樣式便會移到左方了，喔對每行時間都要加
> ```

* * *

[W3C](https://w3c.github.io/webvtt) 裡面還有更詳細的說明，像是可以像 CSS 那樣幫每段字幕加上 class 來套用相同的樣式。

### 參考資料

> How to change the positioning of captions in YouTube [https://medium.com/@mlockrey/how-to-change-the-positioning-of-captions-in-youtube-c75bb9ac0aff](https://medium.com/@mlockrey/how-to-change-the-positioning-of-captions-in-youtube-c75bb9ac0aff)

> WebVTT: The Web Video Text Tracks Format [https://w3c.github.io/webvtt/](https://w3c.github.io/webvtt/)