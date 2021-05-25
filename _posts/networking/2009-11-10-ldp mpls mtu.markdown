---
layout: post
title:  "ldp mpls mtu"
date:   2009-11-10 13:57:01 +0300
categories: Networking
tags: Networking
---

# ldp mpls mtu
 Try to check match LDP configuration if you have changed LDP timers

- Try to check the negotiated MTU for the TCP session is supported on the path

- Check for possible packet drops in the path

- Check if you have any performance issue (high CPU etc) on any end routers



[http://www.cisco.com/c/en/us/td/docs/ios-xml/ios/mp_ldp/configuration/xe-3s/asr1000/mp-ldp-xe-3s-asr1000-book/mp-ldp-overview.html](http://www.cisco.com/c/en/us/td/docs/ios-xml/ios/mp_ldp/configuration/xe-3s/asr1000/mp-ldp-xe-3s-asr1000-book/mp-ldp-overview.html)
[http://www.cisco.com/c/en/us/td/docs/ios-xml/ios/mp_ldp/configuration/12-4m/mp-ldp-12-4m-book.pdf](http://www.cisco.com/c/en/us/td/docs/ios-xml/ios/mp_ldp/configuration/12-4m/mp-ldp-12-4m-book.pdf)
[http://blog.gmane.org/gmane.network.protocols.mpls/page=23](http://blog.gmane.org/gmane.network.protocols.mpls/page=23)
[https://blog.apnic.net/2014/12/15/ip-mtu-and-tcp-mss-missmatch-an-evil-for-network-performance/](https://blog.apnic.net/2014/12/15/ip-mtu-and-tcp-mss-missmatch-an-evil-for-network-performance/)
[http://www.ciscopress.com/articles/article.asp?p=680824&seqNum=5](http://www.ciscopress.com/articles/article.asp?p=680824&seqNum=5)
[http://www.rogerperkin.co.uk/ccie/mpls/mpls-ldp-troubleshooting/](http://www.rogerperkin.co.uk/ccie/mpls/mpls-ldp-troubleshooting/)
[http://anetworkerblog.com/2009/09/26/mpls-ldp-time-to-converge/](http://anetworkerblog.com/2009/09/26/mpls-ldp-time-to-converge/)

Выводы проблемы с мультикастом
Проблемы с mtu


router ospf 110
mpls ldp autoconfig



По умолчанию значение MTU – 1500 байт. Размер назначаемого MTU зависит от функций которые Вы будите применять в сети MPLS.
 Для простой коммутации пометкам достаточно указать значение MTU равное 1504 байт. Для MPLS VPN – 1508 байт, а для MPLS VPN c Traffic Engineering равное 1512.







mpls label protocol ldp
 mpls ldp discovery transport-address interface
 mpls ip

mpls ldp router-id Loopback0 force


show mpls interface GI0/1.10 detail





sh mpls interface 
 sh mpls ldp neighbor
sho mpls forwarding-table 



Прописать
ip ospf network non-broadcast
Не помогло



Router_1#conf t
Router_1(config)#ip cef – включаем Cisco Express Forwarding, технология быстрой коммутации пакетов на 3-ем уровне компании cisco (если не включено);
Router_1(config)#mpls ip – включаем глобально процесс коммутации по меткам (MPLS);
Router_1(config)#mpls label protocol ldp – выбираем протокол, по которому будут обмениваться метками LSR (ELSR) между собой (есть еще TDP, он является проприетарным);
Router_1(config)#mpls ldp router-id loopback 0 – определяем, какой интерфейс (IP-адрес) берется в качестве ID роутера в процессе MPLS;
Router_1(config)#int fa 1/0
Router_1(config-if)#mpls ip – включаем MPLS на интерфейсе;
Router_1(config-if)#mpls mtu 1512 – увеличиваем размер mtu для избегания фрагментации (разбивки) фреймов (стандартный размер 1500);
Router_1(config-if)#exit
Router_1(config)#int fa 2/0
Router_1(config-if)#mpls ip
Router_1(config-if)#mpls mtu 1512
Router_1(config-if)#exit
Router_1(config)#exit
Router_1#wr
Router_1# 




[http://www.ciscopress.com/articles/article.asp?p=680824&seqNum=5](http://www.ciscopress.com/articles/article.asp?p=680824&seqNum=5)
[http://admindoc.ru/1469/mpls-troubleshooting-frame-mode/](http://admindoc.ru/1469/mpls-troubleshooting-frame-mode/)


Давайте определимся:
payload + icmp header + L3 header = пакет = L3 PDU
L3 PDU + L2 header = фрейм = L2 PDU
icmp header = 8 байт
L3 header = 20 байт
L2 header = 18 байт (SA+DA+EType+FCS)

Исходные данные:
В конфиге IOS присутствует команда mtu 1500.
sh int показывает нам mtu 1500 на интерфейсе.
запускаем пинг с параметрами size=1500, df-bit set. Пинг проходит.
запускаем пинг с параметрами size=1501, df-bit set. Пинг не проходит.
Исходя из этого опыта, анализа документации cisco.com и топиков на cisco.support.community, делаю вывод, что:
1)size, который я указываю команде пинг в ИОСе - это размер L3 PDU.
2) команда mtu 1500 в ИОСе определяет размер полезной нагрузки фрейма(L2 PDU) _БЕЗ_ учета L2 header. 


MPLS IGP синхронизация
[http://resources.intenseschool.com/mpls-ldp-igp-synchronization/](http://resources.intenseschool.com/mpls-ldp-igp-synchronization/)
[http://blog.ipspace.net/2011/11/ldp-igp-synchronization-in-mpls.html](http://blog.ipspace.net/2011/11/ldp-igp-synchronization-in-mpls.html)