---
title: "在 Home Assistant 中顯示 BTC 等虛擬貨幣價格"
author: '勝勝'
tags: ['HA']
date: 2021-09-22T09:30:57+08:00
draft: false
categories: ['IoT']
---
這篇文章將教您如何在 Home Assistant 中顯示 BTC 等虛擬貨幣價格。
<!--more-->
![](https://user-images.githubusercontent.com/16719720/134269680-1c63ada4-6bc6-4d46-9e3b-e7c33ebe48e9.png)

在 `configuration.yaml` 中加入以下設定：
```yaml
rest:
  - scan_interval: 60
    resource: https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&ids=bitcoin%2Cethereum%2Cbinance-coin%2Csolana&order=market_cap_desc&sparkline=false&price_change_percentage=1d
    sensor:
      - name: BTC
        json_attributes_path: "$[0]"
        value_template: "{{ value_json[0].current_price }}"
        unit_of_measurement: USD
        json_attributes:
          - id
          - current_price
          - price_change_percentage_24h
          - last_updated
      - name: ETH
        json_attributes_path: "$[1]"
        value_template: "{{ value_json[1].current_price }}"
        unit_of_measurement: USD
        json_attributes:
          - id
          - current_price
          - price_change_percentage_24h
          - last_updated
      - name: SOL
        json_attributes_path: "$[2]"
        value_template: "{{ value_json[2].current_price }}"
        unit_of_measurement: USD
        json_attributes:
          - id
          - current_price
          - price_change_percentage_24h
          - last_updated
```

即可看到貨幣出現在 Sensor 之中。
![image](https://user-images.githubusercontent.com/16719720/134269818-3da458e4-f433-443a-9bbd-76d2d57fd56e.png)
