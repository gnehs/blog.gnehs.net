---
title: 'ChatGPT 能夠勝任字幕翻譯的任務嗎？'
author: '勝勝'
tags: ['ChatGPT','Subtitle']
date: 2023-03-08T10:13:00+08:00
draft: false
categories: ['Software']
---
![](/img/223497376-71fc2b16-d77e-4993-9acb-9a59c64ed31a.png)
在 ChatGPT 應用百花齊放的如今，勝勝想要知道 ChatGPT 是否能夠勝任字幕翻譯的任務，於是便開始寫了一個程式來看看 ChatGPT 的表現如何。
<!--more-->
# 先說結論
雖然品質相較 [網易見外](https://jianwai.youdao.com/) 等產品已經好上不少，但還是跟真人翻譯差得遠，有著簡繁體不分、翻譯腔重等問題。
# 翻譯品質
在與 ChatGPT 的對談中應該也有感受到他的翻譯腔很重，感覺都可以從字裡行間看出他的英文原文是什麼，同時也會使用中國用語，這部分可能需要手動修正。

指示它翻成繁體還是會出現一些簡體，遇到那些具有多重涵義的單字也翻不太好，像 STOP 該翻成「阻止」卻翻成「停止」，更讀不懂那些字裡行間中深層的涵意，雖然可以叫它看前後文，但是考量到翻譯成本，也不太可能直接把字幕全部一次丟下去。

對於科幻影集、科普影片的翻譯品質都是難以接受的，除了名詞翻譯前後不一，人名的翻譯甚至會有時丟出原文，有時會給前後不一的譯文。

此外 ChatGPT 也很難控制好，在翻譯過程中偶爾會回應不符預期的格式，或是給出奇怪的文字，甚至直接失控幫你續寫接下來的字幕。
# 翻譯速度
因為翻譯還是要給前後文，而且 ChatGPT 回應也要時間，所以速度上有點慢，要確保有足夠的時間與穩定的網路連線。
# 翻譯成本
翻譯 Kurzgesagt 的 [The Best Way to Boost Your Immune System (With Science!)](https://youtu.be/M-K7mxdN62M) 大約是 0.15USD ≈ 4.59TWD，會因字幕的長度、數量而有所不同。
# 下載
你可以在下面 GitHub 的連結下載到這個程式，其中 Node.js 版本僅為最小可行性產品，做為概念驗證之用，未來新增新功能主要會以 Electron 版本為主，你當然也可以自行修改程式碼來達到你想要的效果。

- `Electron` 版本： https://github.com/gnehs/subtitle-translator-electron
- `Node.js` 版本： https://github.com/gnehs/subtitle-translator




