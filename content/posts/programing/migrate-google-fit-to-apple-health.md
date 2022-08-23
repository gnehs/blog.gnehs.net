---
title: '將 Google Fit 體重資料匯入至 Apple Health'
author: '勝勝'
tags: ['iOS', 'Apple Health', 'Google Fit']
date: 2022-08-23T23:42:14+08:00
draft: false
categories: ['JS']
---
因為勝勝希望可以把 Google Fit 的體重資料匯入到蘋果的「健康」 App 裡面，不過剛開始找只有看到付費 APP 提供轉換，在勝勝努力之下，終於找到了方法，分享給大家，如果你也有相同的需求，照著這篇教學就可以了。 ><

## 匯出 Google Fit 資料
首先你要先去 [Google Takeout](https://takeout.google.com/settings/takeout) 把你的 Google Fit 資料通通匯出，記得勾 Google Fit 就好，不要選太多不然匯出會很慢很慢。
## 整理資料
### 找到你的體重檔案
你應該會在匯出的檔案中找到 `derived_com.google.weight_com.google.android.g.json`，打開後大概長這樣。
```json
{
    "Data Source": "derived:com.google.weight:com.google.android.gms:merge_weight",
    "Data Points": [
        {
            "fitValue": [
                {
                    "value": {
                        "fpVal": 55
                    }
                }
            ],
            "originDataSourceId": "raw:com.google.weight:com.google.android.apps.fitness:user_input",
            "endTimeNanos": 1434620350091000000,
            "dataTypeName": "com.google.weight",
```
### 只拿需要的資料
我們只需要其中的日期與體重而已，下面我們分成兩個方法進行轉換，後面的雖然可能比較難懂，不過如果你會的話會快很多
#### 如果你不會 Javascript
你可以透過線上的 [JSON to CSV Converter](https://data.page/json/csv) 把你的 JSON 轉換為 Excel 檔，下載成 Excel 檔案後清除多餘的欄位，並將欄位順序調整為日期、體重。

對了，日期的部分你可以透過 `=TEXT(日期欄位/1000000/24/60/60/1000 + 25569,"YYYY-MM-DD HH:MM")` 進行轉換，不然可能捷徑會看不懂這個日期。

另外記得將上方的標題欄清掉，只保留日期與時間的值即可。

#### 如果你會 Javascript
你可以透過下列程式碼進行整理，之後存成 CSV 檔案就好了
```js
.map(x=>`${new Date(x.startTimeNanos/1000000).toLocaleString('en-US')},${x.fitValue[0].value.fpVal}`).join(`\n`)
```
## 傳送檔案
接著把整理好的資料存成 CSV 檔案，並傳送到你的 iPhone 上面。
## 安裝捷徑
接著在你的 iPhone 裡面安裝「[Import Weight to Health App](https://www.icloud.com/shortcuts/0e1d23127c154341b3c57729c6f58671)」，這個捷徑是勝勝在 Google 裡面逛到的，可能會不見，不過到時候再說。
## 修改程式碼
因為台灣人常用的單位是公斤，不過捷徑中所用的單位是磅，因此你可能需要將捷徑下方「記錄健康樣本」裡面的單位換成公斤。
## 匯入資料
準備那麼久，你終於可以將資料匯入「健康」裡頭了，匯入前別忘了先開好權限讓捷徑能讀寫「健康」中的資料。

你只需要輕觸捷徑，選取你整理好的 CSV 檔案就大功告成了！🎉

## 參考資料
- [How to Export Your Google Fit Data](https://www.howtogeek.com/694075/how-to-export-your-google-fit-data/)
