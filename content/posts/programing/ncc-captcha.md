---
title: '破解 NCC「型式認證資料查詢」頁面的驗證碼'
author: '勝勝'
tags: ['NCC', 'Captcha']
date: 2023-02-08T12:35:00+08:00
draft: false
categories: ['JS']
---
勝勝想要寫一個程式定期檢查 NCC 網站上 Apple 最近推出的大 HomePod 是否已經通過審核。但網頁上有一個驗證碼，這讓勝勝不知如何處理。後來，勝勝找到了一個超級簡單的方法，下面就來分享給大家。
<!--more-->
## 更新
政府的開放資料網站有提供整個資料庫，但有些欄位如附件、通過日期等是沒有提供的，另外更新頻率根據頁面的資料為每季。
https://data.gov.tw/dataset/5996
## 如何讓機器解讀驗證碼
![](/img/SCR-20230208-h9k.png)
你可以看到 NCC 的網站有個驗證碼，勝勝發現了一個超級簡單的方法來處理他，那就是把他拉進去 Photoshop 裡面調一下臨界值


![](/img/SCR-20230208-hc3.png)
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