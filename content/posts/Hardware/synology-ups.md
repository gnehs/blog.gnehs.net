---
title: "在其他裝置上使用 Synology NAS 的 UPS 伺服器"
author: "勝勝"
tags: ["UPS"]
date: 2024-06-05T18:00:00+08:00
draft: false
categories: ["Hardware"]
---

事情是這樣的，勝勝家最近停電，但是我忘記搞定 UPS 的設定，所以只有 Synology NAS 有設定好 UPS，不過 Synology 有個設定可以當作 UPS 伺服器，可以把關機訊號傳遞給在網路上的其他裝置。

但是在設定 UPS 時，無論是在 Windows 上或是 UNRAID 都無法連上 UPS 伺服器，但是我明明就有把 IP 都填進去白名單。

後來在[這篇文章](https://forum.netgate.com/topic/183961/nut-package-2-8-1-and-above/3?lang=zh-TW)上發現原來 Synology 是使用寫死的 UPS 名稱、帳號和密碼，照著輸入就能成功連線了！

> Notes on Synology
>
> Synology's NUT implementation uses hardcoded values for several items:
>
> - UPS Name: ups
> - Username: monuser
> - Password: secret

順便提一下 UPS 用的軟體好了！

我在 Windows 上用的是 [WinNUT-Client](https://github.com/nutdotnet/WinNUT-Client/releases)

![](/img/SCR-20240606-baiw.png)

UNRAID 上用的是 [Network UPS Tools (NUT) for UNRAID](https://forums.unraid.net/topic/60217-plugin-nut-v2-network-ups-tools/)

![](/img/SCR-20240606-baog.png)

另外記得把路由器接上 UPS，這樣才能在斷電時傳送關機訊號給其他裝置！
