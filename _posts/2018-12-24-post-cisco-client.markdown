---
layout: post
title:  "Получить адрес по dhcp на cisco роутер"
date:   2018-12-24 10:10:15 +0300
categories: networking cisco
---


# Получить адрес по dhcp на cisco роутер #

Ни разу до сегодняшнего дня не стояло задачи получить адрес по dhcp на cisco роутер.

При этом необходимо было не получать default по умолчанию.

Вот ссылка и кусок конфига.

[https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/ipaddr_dhcp/configuration/12-4/dhcp-12-4-book/config-dhcp-client.html](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/ipaddr_dhcp/configuration/12-4/dhcp-12-4-book/config-dhcp-client.html)


```
interface GigabitEthernet0/0.7
 description #Link to LAN
 encapsulation dot1Q 7
 no ip dhcp client request router
 ip address dhcp
```
