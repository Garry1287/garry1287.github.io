---
layout: post
title:  "Hybrid vlan на QSW-3750-28T-AC"
date:   2021-06-10 13:46:05 +0300
categories: ros duty qtech
tags: qtech ros
---



# Hybrid vlan на QSW-3750-28T-AC


### Пример

заходим в режим конфигурирования порта 8
>(QSW-3750-28TX-AC) (Config)#interface 1/0/8
говорим, что порт будет работать в режиме hybrid. При этом по умолчанию любой трафик никуда не будет ходить.
>(QSW-3750-28TX-AC) (Interface 1/0/8)#switchport mode hybrid
 разрешаем тегированному трафику ходить только в 6 vlan, при этом мы снимаем метки о теги с трафика. 
>(QSW-3750-28TX-AC) (Interface 1/0/8)#switchport hybrid allowed vlan  6  untag
если на порт придет не тегированный трафик, то мы его отправим в vlan 10
при этом в отличии от trunk для native vlan мы не давали дополнительных разрешений.
>(QSW-3750-28TX-AC) (Interface 1/0/8)#switchport hybrid native vlan 10

http://netws.ru/2019/12/19/%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%B0%D0%B8%D0%B2%D0%B0%D0%B5%D0%BC-vlan-%D0%BD%D0%B0-qtech/
https://ftp.qtech.ru/Switch/Access/QSW-3750/QSW-3750-10T-AC/Manual/QSW-3750-10T-AC_Users_manual_Rus.pdf

### Перенастройка pppoe под точку доступа
```
no switchport access vlan
switchport mode hybrid
switchport hybrid allowed vlan 2726 tag
switchport hybrid native vlan 50
switchport hybrid allowed vlan 50 untag
```