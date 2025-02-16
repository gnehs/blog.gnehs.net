---
title: "改裝 RD-160HH！使用 ESP32 取代日立除濕機內建 Wi-Fi 模組"
author: "勝勝"
tags: ["HA"]
date: 2025-02-16T17:45:57+08:00
draft: false
categories: ["IoT"]
---

事情是這樣的，我的除濕機原本是用 [JciHitachiHA](https://github.com/qqaatw/JciHitachiHA) 接進 Home Assistant，但是他常常斷線，控制時延遲也很高，我不知道是那個模組的問題還是日立的伺服器有問題。

最近更新 Home Assistant 後那個 Integration 好像因為沒更新的關係就沒辦法使用了，後來爬到支援 Wi-Fi 模組的可以使用 ESP32 接上去控制

## 好處

- 內網控制：不用再走日立的伺服器操控，就算網路斷掉或他們伺服器關掉也還能控制
- 低延遲：因為在內網操控的關係，延遲超低。
- 沒有追蹤：透過開源的 ESPHome，除濕機的使用資料也不會被傳進日立的伺服器
- 更穩定的連線品質：ESPHome 和 Home Assistant 是好朋友，不用擔心更新後除濕機就連不上

## 準備材料

- ESP32 開發板
- 支援 TaiSEIA 的除濕機
- 一些杜邦線

## 改裝

### 先幫 ESP32 燒錄 ESPHome

先在 ESPHome 裡設定好你的 ESP32，等等接好之後如果要修改設定的話可以用無線 OTA 的方式更新

可以參考這個型號非常類似的 RD-240HH 的設定檔：[dehumidifier-faikin-rd-240hh.yaml](https://github.com/tsunglung/taixia/blob/master/examples/Hitachi/dehumidifier/dehumidifier-faikin-rd-240hh.yaml) 我有試過功能應該都是正常的

### 拆機

首先把除濕機背板的螺絲都拆掉

> 我這台在把手裡面還有兩個螺絲，要記得拆掉，不要大力出奇蹟

> 水箱那邊也有藏螺絲，一定要拆掉

### 接線

拆掉原廠模組，把 ESP32 接上去，另外因為 ESP32 的電壓是 3.3V，可能會需要降壓，但是網路上有討論說 [ESP32 可以不降壓](https://www.facebook.com/groups/esp32tw/posts/3954606918111180/)，你自己決定

![](/img/esphome-hitachi-dehumidifier/IMG_6053.jpg)

接線按照以下指示：

- 除濕機的 `TX` 接到 ESP32 的 `RX`（這個你要自己在 ESPHome 的設定檔裡設定針腳）
- 除濕機的 `RX` 接到 ESP32 的 `TX`（這個你要自己在 ESPHome 的設定檔裡設定針腳）
- 除濕機的 `GND` 接到 ESP32 的 `GND`
- 除濕機的 `5V` 接到 ESP32 的 `VIN`

接好後大概長這樣（我這邊少接了一條線）
![](/img/esphome-hitachi-dehumidifier/IMG_6061.jpg)

### 測試看看

複製設定檔並刷入到 ESP32，測試看看接入有沒有問題，沒問題的話把 ESP32 固定好就可以把背板裝回去了

## 參考資料

- [xangin/TaiSEIA_ESPhome_samples](https://github.com/xangin/TaiSEIA_ESPhome_samples)
- [tsunglung/taixia](https://github.com/tsunglung/taixia)
