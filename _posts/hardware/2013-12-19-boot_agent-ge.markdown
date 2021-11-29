---
layout: post
title:  "Boot from LAN"
date:   2013-12-19 12:28:14 +0400
categories: hardware
tags: hardware
---

# Boot from LAN
Go into the BIOS (F10 as you power on) and change the boot order to remove "boot from LAN" from the options. You have it trying to boot from network before the hard drive. 

А так обычно в биосе загрузку по сети вырубаешь и всё. Или PCI-слот-такой-то-BootROM disable.

    Выполните вход в программу настроек BIOS и найдите список порядка устройств загрузки.
    Переместите агент загрузки вниз списка после жесткого диска или устройства, с которого вы предпочитаете выполнять загрузку.


[http://www.intel.ru/content/www/ru/ru/support/network-and-i-o/ethernet-products/000005626.html](http://www.intel.ru/content/www/ru/ru/support/network-and-i-o/ethernet-products/000005626.html)

[https://downloadcenter.intel.com/ru/download/19186?_ga=1.258316558.529821750.1482153685](https://downloadcenter.intel.com/ru/download/19186?_ga=1.258316558.529821750.1482153685)

[http://www.intel.ru/content/www/ru/ru/support/software/manageability-products/000005790.html](http://www.intel.ru/content/www/ru/ru/support/software/manageability-products/000005790.html)

- FLASHDISABLE или-FD
