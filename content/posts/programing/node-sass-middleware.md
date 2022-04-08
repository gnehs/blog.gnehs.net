---
title: '讓 node-sass-middleware 轉換 SASS'
author: '勝勝'
tags: ['sass'] 
date: 2018-12-02T08:46:59+00:00
draft: false
categories: ['JS','Node']
---

最近在試 node-sass-middleware，但是怎麼試都不會動，開了 log 才發現說找不到 scss 檔案
<!--more-->
![](https://i.imgur.com/Ipudffg.png)

後來努力去看了一下文件，發現是這樣的

> *   `indentedSyntax` - `[true | false]`, false by default. Compiles files with the `.sass` extension instead of `.scss` in the `src` directory.

幹誰會知道一個拿 SASS 取名的東西預設會是吃 SCSS 啦

所以你如果要讓他吃 SASS，你要這樣寫

```
app.use(sassMiddleware({
    src: __dirname + '/sass',
    dest: __dirname + '/public/css',
    outputStyle: 'compressed',
    indentedSyntax: true,
    prefix: '/css'
}));
```