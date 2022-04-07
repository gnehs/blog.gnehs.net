---
title: 'Nokia N1 B19 救磚'
author: '勝勝'
tags: ['Nokia N1'] 
date: 2018-04-15T08:46:59+00:00
draft: false
categories: ['android']
---

我手上的 Nokia N1 因為被搞到 bootloop 不得已只好來 `adb sideload` 了 思路是這樣的

1.  於 boot 分區刷入官方 Recovery
2.  使用 `adb sideload` 刷入官方更新檔
3.  刷回原本的 boot 分區

準備材料

*   [官方 B19 更新檔 & 官方 Recovery & boot.img](https://drive.google.com/file/d/1DgIpW8_sn8FK4tBihdChVO25Cw73bC8B/view?usp=sharing)
*   fastboot & adb
*   一台已解鎖的 N1(解鎖很簡單，不用我多說了吧)

1.首先將平板關機，接著長按 電源鍵 ＋ 音量下，直到可愛的 Android 機器人出現 ![](https://i.imgur.com/SrmzmUc.jpg) 2.將平板接上電腦，輸入 `fastboot flash boot <官方 Recovery>` 來把 boot 刷入 Recovery（因官方不給刷 Recovery 分區），然後選擇 NORMAL BOOT 進入 Recovery ![](https://i.imgur.com/FgtSO8k.png) 3.這時會看到一隻躺著的 Android 機器人，按 電源鍵 ＋ 音量上  後會看到 Recovery 介面，利用音量上下鍵將選項選到 `apply update from ADB` 並按下電源鍵 ![](https://i.imgur.com/39xyb8b.jpg) 4.輸入 `adb sideload <A5FMB19_update.zip(官方更新檔)>` 來刷入系統 ![](https://i.imgur.com/aTV8ZDp.png) 5.利用音量上下鍵將選項選到 `reboot to bootloder` 並按下電源鍵，來重開機回 fastboot ![](https://i.imgur.com/TLhGaPk.jpg) 6.輸入 `fastboot flash boot <boot.img>` 來把 boot 刷回，然後選擇 NORMAL BOOT 進入系統 ![](https://i.imgur.com/nfx9EfX.png) 7.大功告成，第一次開機可能會超過五分鐘，請耐心等待