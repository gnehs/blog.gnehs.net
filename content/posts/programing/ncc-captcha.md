---
title: '破解 NCC「型式認證資料查詢」頁面的驗證碼'
author: '勝勝'
tags: ['NCC', 'Captcha']
date: 2023-02-08T12:35:00+08:00
draft: false
categories: ['JS']
---
是這樣的，勝勝想寫一個程式定期去 NCC 那邊看 Apple 最近出的大 HomePod 過審了沒，但是那個網頁有個驗證碼，勝勝就在想要怎麼解決他，後來勝勝找到了方法，下面就來分享給大家。
<!--more-->
![](/img/SCR-20230208-h9k.png)
<div style="text-align: center;">NCC 網站的驗證碼</div>

你可以看到 NCC 的網站有個驗證碼，勝勝發現了一個超級簡單的方法來處理他，那就是把他拉進去 Photoshop 裡面調一下臨界值


![](/img/SCR-20230208-hc3.png)
<div style="text-align: center;">稍微在 Photoshop 裡面調一下臨界值</div>

🪄 你看驗證碼的數字就如魔法般輕輕鬆鬆就被我們弄出來了，接下來過個 OCR 就可以解出驗證碼了，實際的程式碼如下

```js
import Tesseract from 'tesseract.js';
import sharp from 'sharp';
let captchaImage = await sharp(`captcha.jpg`)
captchaImage = captchaImage.threshold(90)
captchaImage = await captchaImage.toBuffer()

const { data: { text } } = await Tesseract.recognize(captchaImage, 'eng')
let captchaText = text.replace(/[^0-9]/g, '')
console.log('captcha', captchaText)
```

對了，這裡是 GitHub 的連結，有興趣的話可以去看看 [gnehs/apple-ncc-feed](https://github.com/gnehs/apple-ncc-feed)，另外你可以透過發送指令 `/subscribe apple-ncc` 給機器人 [@gnehsBot](https://t.me/gnehsBot) 免費接收蘋果 NCC 審核資訊的即時通知。