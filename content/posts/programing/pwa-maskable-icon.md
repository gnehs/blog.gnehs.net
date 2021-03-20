---
title: '在 PWA 應用程式中使用遮罩圖示（maskable icon）'
date: Sun, 22 Dec 2019 10:28:35 +0000
draft: false
categories: ['js']
---

Chrome 最近釋出 79 版，終於支援了遮罩圖示（看看 Android 8 都出多久了），這篇教學會教你如何使用遮罩圖示。

準備清單
----

*   已更新 Chrome 79 的 Android 手機
*   要修改的 PWA 應用程式

圖示製作
----

要製作圖示必須保留相對應的安全區域，免得要顯示的內容被裁掉。

你可以在 [Maskable​.app](https://maskable.app/) 預覽套用後的效果 ![file](https://i.loli.net/2019/12/22/Ufgv4mlo1euY78T.png)

修改 manifest.json
----------------

將 icons 中的圖示標示 `"purpose": "maskable"` 便可以使用遮罩了

```
{
  "scope": "/",
  "name": "PokaPlayer",
  "short_name": "PokaPlayer",
  "icons": [{
      "src": "./img/icons/icon.png",
      "sizes": "512x512",
      "type": "image/png"
    },
    {
      "src": "./img/icons/icon-maskable.png",
      "sizes": "512x512",
      "type": "image/png",
      "purpose": "maskable"
    }
  ],
  "start_url": "/",
  "display": "standalone",
  "background_color": "#2f2b3e",
  "theme_color": "#ffffff"
}
```

在手機上查看套用效果
----------

套用成功了 ![file](https://i.loli.net/2019/12/22/R1OHAGDYJdtzMlk.png) 參考資料

> [Maskable Icons: Android Adaptive Icons for Your PWA](https://css-tricks.com/maskable-icons-android-adaptive-icons-for-your-pwa/)