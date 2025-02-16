---
title: "自建電子發票儲存服務"
author: "勝勝"
tags: ["發票"]
date: 2025-02-16T16:16:35+08:00
draft: false
categories: ["Selfhosted"]
---

在 APP 商店有很多發票的 APP，但大部分的都會儲存你資料進行分析，從發票資料中，甚至可以知道你平常在哪消費等資訊，可以參考這篇文章：[從 API 串接角度評估電子發票存摺 APP 可以怎樣出賣使用者個資](https://blog.user.today/invoice-api-problem/)

我真的沒有想繼續把資料賣給這些廠商，所以開發了一個發票儲存服務，我已經包成 Docker 格式，只要你有相關的經驗，應該能夠在十分鐘內架設好這個服務。

# 修改密碼

為了避免原本的發票 APP 繼續取得你的發票資訊，建議你可以把密碼改掉後再進行下面的步驟，你可以到 [財政部電子發票整合服務平台](https://www.einvoice.nat.gov.tw/) 做這件事

# 架設 NocoDB

NocoDB 是一款資料庫的介面軟體，可以透過他查看資料庫內的資料，可以連接現有的資料庫，或是使用內建的 SQLite 來作為資料庫，可以參考 [官方的部署指南](https://docs.nocodb.com/getting-started/self-hosted/installation/docker-install) 來了解如何部署。

# 在 NocoDB 建立 API Key 和取得 Base ID

這是等一下會用到的妙妙工具

# 架設 nocodb-einvoice

NocoDB einvoice 是由我開發的發票匯入工具，可以設定成每天自動執行把發票資料匯入到 NocoDB，你可以參考 [README 文件](https://github.com/gnehs/nocodb-einvoice) 來了解如何架設

## 環境變數

### 必填

- `NOCODB_URL`: NocoDB 的 URL
- `NOCODB_API_KEY`: NocoDB 的 API Key
- `NOCODB_BASE_ID`: NocoDB 的 Base ID （可以在瀏覽器的網址列中找到）
- `EINVOICE_USERNAME`: 電子發票的帳號（電話號碼）
- `EINVOICE_PASSWORD`: 電子發票的密碼（又稱驗證碼）

### 選填

- `CRON_SCHEDULE`
  - 預設值：`0 3 * * *`，每天凌晨 3 點執行
  - 可參考 [crontab.guru](https://crontab.guru/) 了解如何設定
- `MAX_SYNC_MONTHS`
  - 預設值：無限制
  - 同步的最大月份，預設同步可查詢到的全部發票，建議在首次同步後設定此值為 `3`，以避免同步過多資料造成電子發票系統的負擔
- `REQUEST_DELAY`
  - 預設值：`1000` 毫秒，即 1 秒
  - 每個請求之間的延遲（毫秒），避免造成電子發票系統的負擔

## 在 Docker 上部署

```bash
docker run -d --name nocodb-einvoice \
  -e NOCODB_URL=https://<HOST>:<PORT> \
  -e NOCODB_API_KEY=your-api-key \
  -e NOCODB_BASE_ID=your-base-id \
  -e EINVOICE_USERNAME=your-username \
  -e EINVOICE_PASSWORD=your-password \
  -e CRON_SCHEDULE="0 3 * * *" \
  ghcr.io/gnehs/nocodb-einvoice:latest
```

# 完成

如果設定沒錯的話，你應該會在 nocodb-einvoice 的 log 看到同步的相關日誌，另外程式將自動建立相關資料表，請不要修改資料表與欄位名稱

```bash
3:00:10 AM [發票] 測試驗證碼：84585
3:00:15 AM [發票] 登入成功
3:00:15 AM [發票] 正在同步 2025 年 2 月發票
3:00:17 AM [發票] - 正在取得第 1/1 頁發票
3:00:19 AM [發票] - 發票 KJXXXXXXXX 新增成功
3:00:21 AM [發票] - 發票 KGXXXXXXXX 新增成功
3:00:22 AM [發票] 正在同步 2025 年 1 月發票
3:00:24 AM [發票] - 正在取得第 1/1 頁發票
3:00:24 AM [發票] 正在同步 2024 年 12 月發票
3:00:26 AM [發票] - 正在取得第 1/1 頁發票
3:00:27 AM [發票] 同步完成
```

接下來發票工具就會根據你設定的排程自動進行匯入了

# 載具小工具

iOS 的朋友可以透過 [斯揪發票](https://skog-einvoice.gnehs.net/) 小工具來產生載具圖片，並搭配 [Widgetsmith](https://apps.apple.com/tw/app/widgetsmith/id1523682319) 放置圖片小工具在桌面喔

![](/img/self-hosted-e-invoice-storage-service/skog-einvoice.jpeg)
