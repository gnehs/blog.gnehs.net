---
title: '透過 JS 即時偵測系統外觀是否處於深色模式'
author: '勝勝'
tags: ['js','web'] 
date: 2019-12-14T12:36:43+08:00
draft: false
categories: ['js','web']
---

在撰寫網頁時若要用 JS 來檢測系統的主題，你會需要用到 CSS 的 `prefers-color-scheme: dark` 來檢測是否適用於該條規則，我們可以在 js 使用 `matchMedia` 來查看檢測後的結果。

* * *

程式碼如下

```
const darkModeMediaQuery = window.matchMedia(`(prefers-color-scheme: dark)`);
darkModeMediaQuery.addListener(e => {
  //當系統變更主題時都會執行這裡
  const darkMode = e.matches;
  // darkMode: [true(深色主題開啟)|false(深色主題關閉)]
});
```