---
layout: post
title:  "Retn-via-lo"
date:   2009-09-06 04:16:53 +0400
categories: PSI
tags: PSI
---

# Retn-via-lo
neighbor 180.225.11.1 ebgp-multihop
neighbor 180.225.11.1 update-source loopback 0

И 2 статика к lo, через существующие линковочные адреса


[http://noc.demos.su/helps/bgp_routing.shtml](http://noc.demos.su/helps/bgp_routing.shtml)


Дать команду или нет

maximum-paths 2 
Надо давать если будет 2 сессии






Балансировка нагрузки

Если все каналы подключены с обеих сторон к одному маршрутизатору CISCO, 
то возможна балансировка нагрузки по методу, аналогичному балансировке нагрузки при статическом роутинге. 
Со своей стороны, при наличии предварительной договоренности, 
мы можем также обеспечить подключение Ваших каналов к одному маршрутизатору с нашей стороны. 
Мы не можем гарантировать приемлемость данного метода при использовании маршрутизаторов, отличных от CISCO.

Суть данного метода в применении к BGP состоит в указании с обеих сторон нескольких маршрутов с одинаковым приоритетом к BGP peer'у, 
соответствующих разным каналам. Необходимо также отключить route-cache на интерфейсах, к которым подключены упомянутые выше каналы. 
Учтите, что BGP сессия в этом случае одна.
Ниже приведен пример фрагмента конфигурации маршрутизатора CISCO со стороны клиента.

!
interface Loopback1
 description Interface for Demos BGP
 ip address 192.124.176.1 255.255.255.252
 no shutdown
!
interface Serial0
 description Link to Demos N1
 ip unnumbered Ethernet0
 bandwidth 256
 no ip route-cache
 no shutdown
!
interface Serial1
 description Link to Demos N2
 ip unnumbered Ethernet0
 bandwidth 256
 no ip route-cache
 no shutdown
!
!
ip route 192.124.176.2 255.255.255.252 Serial0
ip route 192.124.176.2 255.255.255.252 Serial1
!
!
router bgp 1234
...
 neighbor 192.124.176.2 remote-as 2578
 neighbor 192.124.176.2 ebgp-multihop 2
 neighbor 192.124.176.2 update-source Loopback1
...
!
