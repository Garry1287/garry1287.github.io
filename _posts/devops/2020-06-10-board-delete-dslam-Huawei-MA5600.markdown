---
layout: post
title:  "Отключение абонентской карты на dslam Huawei MA 5600"
date:   2021-06-10 09:42:10 +0300
categories: ros duty huawei
---



# Отключение абонентской карты на dslam Huawei MA 5600


### Отключение абонентской карты xdsl0-dbk (15 слот)
Требуется отключить карту в dslam

Профили для iptv удаляем
```
xdsl0-dbk(config-btv)#igmp user delete slot 0/15
```
Удаляем сервис-порты (вот такие 
service-port vlan 2030 adsl 0/15/2 vpi 35 vci 33 rx-cttr 6 tx-cttr 6)
```
xdsl0-dbk(config)#undo service-port board 0/15 
```
Убираем саму карту
``` 
board delete 0/15
```