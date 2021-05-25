---
layout: post
title:  "native_vlan"
date:   2017-06-23 23:03:19 +0300
categories: Networking
tags: Networking
---

# native_vlan
Native vlan	


Одно из отличий коммутаторов Cisco от коммутаторов других производителей, это введение так называемого  Native   VLAN . Что он из себе представляет?
 Native   VLAN  - это влан к которому коммутатор относит все кадры идущие без тега, или кадры получаемые с не распределенных портов (портов которые явно не включены ни в один влан). То есть если коммутатор получает нетегированные кадры на транковом порту он автоматически причисляет их к  Native   VLAN . И точно так же кадры генерируемые с не распределенных портов при попадании в транк-порт причисляются к  Native   VLAN .
Продемонстрировать все это для наглядности можно все в том же Packet Tracer в режиме симуляции.	

[http://www.netconfig.org/switching/1060/](http://www.netconfig.org/switching/1060/)
[http://hghltd.yandex.net/yandbtm?text=native%20vlan&url=http%3A%2F%2Fblog.evgenybelkin.ru%2F2011%2F05%2Fnative-vlan.html&fmode=inject&mime=html&l10n=ru&sign=07792d86fd8c3100afe28b1bda12c604&keyno=0](http://hghltd.yandex.net/yandbtm?text=native%20vlan&url=http%3A%2F%2Fblog.evgenybelkin.ru%2F2011%2F05%2Fnative-vlan.html&fmode=inject&mime=html&l10n=ru&sign=07792d86fd8c3100afe28b1bda12c604&keyno=0)