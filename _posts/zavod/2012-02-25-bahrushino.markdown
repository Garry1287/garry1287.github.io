---
layout: post
title:  "bahrushino"
date:   2012-02-25 22:19:05 +0400
categories: zavod
tags: zavod
---

# bahrushino
1. На макси групп или ??? найти двойное подключение

interface FastEthernet0/1
 description #Rezerv kanal from Starttelecom
 ip address 10.192.10.94 255.255.255.252
 duplex auto
 speed auto



interface Serial0/2/0:0
 description # Uplink to NLMK IPVPN via Golden-Telcom
 bandwidth 2048
 ip address 10.192.10.98 255.255.255.252
 load-interval 30
 service-policy output PLATINUM
!



router bgp 65022
 bgp log-neighbor-changes
 neighbor 10.192.10.93 remote-as 8744
 neighbor 10.192.10.97 remote-as 3216
 !
 address-family ipv4
  redistribute connected
  redistribute static
  redistribute ospf 110 metric 1
  neighbor 10.192.10.93 activate
  neighbor 10.192.10.93 weight 50
  neighbor 10.192.10.93 prefix-list maxi_net out
  neighbor 10.192.10.93 route-map prep-out-start out
  neighbor 10.192.10.97 activate
  neighbor 10.192.10.97 weight 100
  neighbor 10.192.10.97 prefix-list maxi_net out
  no auto-summary
  no synchronization
  network 10.98.0.0 mask 255.255.255.0
  network 10.98.1.0 mask 255.255.255.0
  network 10.98.2.0 mask 255.255.255.0
  network 10.98.3.0 mask 255.255.255.0
  network 10.98.4.0 mask 255.255.255.240
  network 10.98.16.0 mask 255.255.255.0
  network 10.98.254.0 mask 255.255.255.0
  network 10.192.10.96 mask 255.255.255.252
 exit-address-family
!         
ip forward-protocol nd
ip route 0.0.0.0 0.0.0.0 10.192.10.97


ip prefix-list maxi_net seq 5 permit 10.98.0.0/16 le 30
ip prefix-list maxi_net seq 15 deny 0.0.0.0/0 le 32


logging trap debugging
logging facility local6
logging 10.192.10.190
access-list 10 permit 10.192.10.0 0.0.0.255
access-list 30 remark NTP: access-group peer
access-list 30 permit 10.192.10.190
access-list 30 deny   any
access-list 57 permit 10.192.10.190
access-list 57 deny   any
snmp-server community Sh73ah91Kld RW 57
snmp-server community public RO
snmp-server ifindex persist
snmp-server location Maxi_Group-CEO
snmp-server contact iptech@sc.ru
route-map prep-out-start permit 60
 set as-path prepend 65022 65022 65022 65022 65022


2.
router bgp 65017
  neighbor 10.192.10.153 remote-as 8744
  neighbor 10.192.10.153 shutdown
ПРописать дополнительного нейбора и сделать для него weight 100
weight используется для исходящего траффика, 0 у всех полученных маршрутов. 32768 - для исходящих маршрутов
делаем 100, чтобы исходящий траффик шёл через старт. Чем больше weight, тем лучше полученный маршрутов

На Экватнт прописывает prepend, это для входящего траффика. Чем больше препедов, тем длинее путь к нам 
route map применяется на out, потому что мы распространяем эту информацию

 !        
 address-family ipv4
 neighbor 10.192.10.30 activate
 neighbor 10.192.10.153 shutdown
 neighbor 10.192.10.153 weight 100 

 neighbor 10.192.10.30 route-map prep-out-equant out
 
no auto-summary
 no synchronization
 network 10.10.1.0 mask 255.255.255.0
 network 10.10.15.0 mask 255.255.255.0
 network 10.10.120.0 mask 255.255.255.0
 network 10.29.0.0 mask 255.255.0.0
 network 10.33.0.0 mask 255.255.255.0
 exit-address-family



route-map prep-out-equant permit 60
 set as-path prepend 65017 65017 65017 65017 65017



3. Зафильтровать все маршруты туда и обратно 

neighbor 10.192.10.153 prefix-list filter_net out
neighbor 10.192.10.153 prefix-list filter_net in

Потом сначала принять маршруты (убрать in)
А затем отправить

ip prefix-list filter_net seq 5 deny 0.0.0.0/0 le 32

4.Проверить результат трейсом туда и обратно, посмотреть маршруты, должны быть двойными




interface FastEthernet0/0.109
 
  description #Uplink to Starttelekom
 bandwidth 10240
 encapsulation dot1Q 109
 ip address 10.192.10.154 255.255.255.252
!   





































1. Сделать weight для Билайна меньше чем Старттелекома, чтобы исходящий шёл на Старттелеком
2. Удалить ip prefix-list rumelco_net_29
3. rumelco_net на Starttelecom
4. rumelco_net_no_29 на Beeline















router bgp 65017
 bgp router-id 10.192.10.29
 bgp log-neighbor-changes
 neighbor 10.192.10.30 remote-as 3216
 neighbor 10.192.10.153 remote-as 8744
 !
 address-family ipv4
 redistribute connected
 redistribute static
 neighbor 10.192.10.30 activate
 neighbor 10.192.10.30 prefix-list rumelco_net_no_29 out
 neighbor 10.192.10.30 route-map prep-out-beeline out
 neighbor 10.192.10.153 activate
 neighbor 10.192.10.153 weight 100
 neighbor 10.192.10.153 prefix-list rumelco_net out
 no auto-summary
 no synchronization
 network 10.10.1.0 mask 255.255.255.0
 network 10.10.15.0 mask 255.255.255.0
 network 10.10.120.0 mask 255.255.255.0
 network 10.29.0.0 mask 255.255.0.0
 network 10.33.0.0 mask 255.255.255.0
 exit-address-family






ip route 10.10.0.0 255.255.0.0 Null0
ip route 10.10.1.0 255.255.255.0 10.29.1.2
ip route 10.10.15.0 255.255.255.0 10.29.1.2
ip route 10.10.120.0 255.255.255.0 10.29.1.2
ip route 10.29.0.0 255.255.0.0 Null0
ip route 10.29.2.0 255.255.255.0 10.29.1.2
ip route 10.29.4.0 255.255.255.0 10.29.1.2
ip route 10.29.5.0 255.255.255.0 10.29.1.2
ip route 10.29.14.0 255.255.255.0 10.29.1.2
ip route 10.29.15.0 255.255.255.0 10.29.4.254
ip route 10.29.16.0 255.255.255.0 10.29.4.254
ip route 10.29.17.0 255.255.255.0 10.29.4.254
ip route 10.33.0.0 255.255.255.0 10.29.1.2


ip prefix-list filter_net seq 5 deny 0.0.0.0/0 le 32
!
ip prefix-list rumelco_net seq 5 permit 10.10.1.0/24 le 30
ip prefix-list rumelco_net seq 10 permit 10.10.15.0/24 le 30
ip prefix-list rumelco_net seq 15 permit 10.10.120.0/24 le 30
ip prefix-list rumelco_net seq 20 permit 10.29.0.0/16 le 30
ip prefix-list rumelco_net seq 25 permit 10.33.0.0/24 le 30
ip prefix-list rumelco_net seq 30 deny 0.0.0.0/0 le 32
!
ip prefix-list rumelco_net_29 seq 20 permit 10.29.0.0/24 le 30
ip prefix-list rumelco_net_29 seq 30 deny 0.0.0.0/0 le 32
!
ip prefix-list rumelco_net_no_29 seq 5 permit 10.10.1.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 10 permit 10.10.15.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 15 deny 10.10.120.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 17 permit 10.10.0.0/16 le 30
ip prefix-list rumelco_net_no_29 seq 19 deny 10.29.0.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 20 permit 10.29.0.0/16 le 30
ip prefix-list rumelco_net_no_29 seq 25 permit 10.33.0.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 35 deny 0.0.0.0/0 le 32




S       10.10.0.0/16 is directly connected, Null0
S       10.10.1.0/24 [1/0] via 10.29.1.2
S       10.29.17.0/24 [1/0] via 10.29.4.254
S       10.29.16.0/24 [1/0] via 10.29.4.254
S       10.10.15.0/24 [1/0] via 10.29.1.2
S       10.29.5.0/24 [1/0] via 10.29.1.2
S       10.29.4.0/24 [1/0] via 10.29.1.2
S       10.29.2.0/24 [1/0] via 10.29.1.2
S       10.29.0.0/16 is directly connected, Null0
S       10.29.15.0/24 [1/0] via 10.29.4.254
S       10.29.14.0/24 [1/0] via 10.29.1.2
S       10.33.0.0/24 [1/0] via 10.29.1.2
S       10.10.120.0/24 [1/0] via 10.29.1.2

C       10.29.1.0/30 is directly connected, FastEthernet0/1                                                                                                  
C       10.29.0.0/24 is directly connected, FastEthernet0/0.110                                                                                              
C       10.192.10.152/30 is directly connected, FastEthernet0/0.109                                                                                          
C       10.29.128.0/24 is directly connected, FastEthernet0/0.11                                                                                             
C       10.192.10.28/30 is directly connected, FastEthernet0/0.108  



sh ip bgp neighbors 10.192.10.30 advertised-routes 
   Network          Next Hop            Metric LocPrf Weight Path                                                                                            
*> 10.10.1.0/24     10.29.1.2                0         32768 i                                                                                               
*> 10.10.15.0/24    10.29.1.2                0         32768 i                                                                                               
*> 10.10.120.0/24   10.29.1.2                0         32768 i                                                                                               
*> 10.29.0.0/24     0.0.0.0                  0         32768 ?                                                                                               
*> 10.29.0.0/16     0.0.0.0                  0         32768 i                                                                                               
*> 10.29.1.0/30     0.0.0.0                  0         32768 ?                                                                                               
*> 10.29.2.0/24     10.29.1.2                0         32768 ?
*> 10.29.4.0/24     10.29.1.2                0         32768 ?
*> 10.29.5.0/24     10.29.1.2                0         32768 ?
*> 10.29.14.0/24    10.29.1.2                0         32768 ?
*> 10.29.15.0/24    0.0.0.0                  0         32768 ?
*> 10.29.16.0/24    0.0.0.0                  0         32768 ?
*> 10.29.17.0/24    0.0.0.0                  0         32768 ?
*> 10.29.128.0/24   0.0.0.0                  0         32768 ?
*> 10.33.0.0/24     10.29.1.2                0         32768 i




RUMELCO-CE0#sh ip bgp neighbors 10.192.10.153 advertised-routes 
BGP table version is 2837, local router ID is 10.192.10.29
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale
Origin codes: i - IGP, e - EGP, ? - incomplete

   Network          Next Hop            Metric LocPrf Weight Path
*> 10.10.0.0/24     10.192.10.30                         100 3216 20866 ?
*> 10.10.0.0/16     0.0.0.0                  0         32768 ?
*> 10.10.1.0/24     10.29.1.2                0         32768 i
*> 10.10.15.0/24    10.29.1.2                0         32768 i
*> 10.29.0.0/16     0.0.0.0                  0         32768 i
*> 10.29.1.0/30     0.0.0.0                  0         32768 ?
*> 10.29.2.0/24     10.29.1.2                0         32768 ?
*> 10.29.4.0/24     10.29.1.2                0         32768 ?
*> 10.29.5.0/24     10.29.1.2                0         32768 ?
*> 10.29.14.0/24    10.29.1.2                0         32768 ?
*> 10.29.15.0/24    0.0.0.0                  0         32768 ?
*> 10.29.16.0/24    0.0.0.0                  0         32768 ?
*> 10.29.17.0/24    0.0.0.0                  0         32768 ?
*> 10.29.128.0/24   0.0.0.0                  0         32768 ?
*> 10.33.0.0/24     10.29.1.2                0         32768 i





















no ip prefix-list rumelco_net_no_29 seq 5 permit 10.10.1.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 5 deny 10.10.1.0/24 le 30



ip route 10.10.1.0 255.255.255.0 10.29.1.2
ip route 10.10.15.0 255.255.255.0 10.29.1.2
ip route 10.10.120.0 255.255.255.0 10.29.1.2
ip route 10.29.2.0 255.255.255.0 10.29.1.2
ip route 10.29.4.0 255.255.255.0 10.29.1.2
ip route 10.29.5.0 255.255.255.0 10.29.1.2
ip route 10.29.14.0 255.255.255.0 10.29.1.2
ip route 10.29.15.0 255.255.255.0 10.29.4.254
ip route 10.29.16.0 255.255.255.0 10.29.4.254
ip route 10.29.17.0 255.255.255.0 10.29.4.254
ip route 10.33.0.0 255.255.255.0 10.29.1.2




ip prefix-list rumelco_net_no_29 seq 5 permit 10.10.1.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 10 permit 10.10.15.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 15 deny 10.10.120.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 17 permit 10.10.0.0/16 le 30
ip prefix-list rumelco_net_no_29 seq 19 deny 10.29.0.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 20 permit 10.29.0.0/16 le 30
ip prefix-list rumelco_net_no_29 seq 25 permit 10.33.0.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 35 deny 0.0.0.0/0 le 32





















	      Раунд 2

Какова была идея?
Исходящий трафик идёт через Стартов по weight (150 больше 100)
Входящий трафик идёт через Стартов так как от него объявлены более специфичные префиксы кроме 10.29.0.0/24, а через Билайн запрещены префиксы,
разрешены /16, и разрешена 10.29.0.0/24


Что нам надо сделать.
Надо сделать наоборот
1. Поменять weight местами
2. Со Стартов объявлять только /16

ip prefix-list rumelco_start seq 10 permit 10.29.0.0/16
ip prefix-list rumelco_start seq 20 permit 10.10.0.0/16

3. С Билайна объявлять специфики (все сети, прописанные в ip route).
Просто убираем префикс лист
no neighbor 10.192.10.30 prefix-list rumelco_net_29 out


Возвращаем нагрузку на Мегафон
1. Поменять weight местами
2. Возвращем как было
 neighbor 10.192.10.30 prefix-list rumelco_net_29 out
 neighbor 10.192.10.153 prefix-list rumelco_net_no_29 out

10.29.0.0/24  - видео терминалы
10.10.120.0/24 - звонилки

Цель - через Старттелеком всё
Через Билайн только


router bgp 65017
 bgp router-id 10.192.10.29
 bgp log-neighbor-changes
 neighbor 10.192.10.30 remote-as 3216
 neighbor 10.192.10.153 remote-as 8744
 !
 address-family ipv4
 redistribute connected
 redistribute static
 neighbor 10.192.10.30 activate
 neighbor 10.192.10.30 weight 100
 neighbor 10.192.10.30 prefix-list rumelco_net_29 out
 neighbor 10.192.10.153 activate
 neighbor 10.192.10.153 weight 150
 neighbor 10.192.10.153 prefix-list rumelco_net_no_29 out

ip route 10.10.0.0 255.255.0.0 Null0
ip route 10.10.1.0 255.255.255.0 10.29.1.2
ip route 10.10.15.0 255.255.255.0 10.29.1.2
ip route 10.10.120.0 255.255.255.0 10.29.1.2
ip route 10.29.0.0 255.255.0.0 Null0
ip route 10.29.2.0 255.255.255.0 10.29.1.2
ip route 10.29.4.0 255.255.255.0 10.29.1.2
ip route 10.29.5.0 255.255.255.0 10.29.1.2
ip route 10.29.14.0 255.255.255.0 10.29.1.2
ip route 10.29.15.0 255.255.255.0 10.29.4.254
ip route 10.29.16.0 255.255.255.0 10.29.4.254
ip route 10.29.17.0 255.255.255.0 10.29.4.254
ip route 10.29.30.0 255.255.255.0 10.29.1.2
ip route 10.33.0.0 255.255.0.0 Null0
ip route 10.33.0.0 255.255.255.0 10.29.1.2
ip route 10.33.4.0 255.255.255.0 10.29.1.2
ip route 10.33.5.0 255.255.255.0 10.29.1.2



ip prefix-list rumelco_net_29 seq 5 deny 10.10.1.0/24 le 30
ip prefix-list rumelco_net_29 seq 10 deny 10.10.15.0/24 le 30
ip prefix-list rumelco_net_29 seq 15 permit 10.10.120.0/24 le 30
ip prefix-list rumelco_net_29 seq 20 permit 10.10.0.0/16 le 30
ip prefix-list rumelco_net_29 seq 25 permit 10.29.0.0/24 le 30
ip prefix-list rumelco_net_29 seq 26 deny 10.29.1.0/24 le 30
ip prefix-list rumelco_net_29 seq 30 deny 10.29.2.0/24 le 30
ip prefix-list rumelco_net_29 seq 35 deny 10.29.4.0/24 le 30
ip prefix-list rumelco_net_29 seq 40 deny 10.29.5.0/24 le 30
ip prefix-list rumelco_net_29 seq 45 deny 10.29.14.0/24 le 30
ip prefix-list rumelco_net_29 seq 50 deny 10.29.15.0/24 le 30
ip prefix-list rumelco_net_29 seq 55 deny 10.29.17.0/24 le 30
ip prefix-list rumelco_net_29 seq 57 deny 10.29.30.0/24 le 30
ip prefix-list rumelco_net_29 seq 60 permit 10.29.0.0/16 le 30
ip prefix-list rumelco_net_29 seq 65 permit 10.33.0.0/24 le 30
ip prefix-list rumelco_net_29 seq 70 permit 10.33.5.0/24 le 30
ip prefix-list rumelco_net_29 seq 75 permit 10.33.0.0/16 le 30
ip prefix-list rumelco_net_29 seq 100 deny 0.0.0.0/0 le 32



ip prefix-list rumelco_net_29 seq 5 deny 10.10.1.0/24 le 30
ip prefix-list rumelco_net_29 seq 10 deny 10.10.15.0/24 le 30

Билайн запрещаем 29-е сети, кроме 10.29.0.0/24
10.10.1.0/24
10.10.15.0/24


RUMELCO-CE0#sh ip bgp neighbors 10.192.10.30 advertised-routes  
BGP table version is 113005, local router ID is 10.192.10.29
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale
Origin codes: i - IGP, e - EGP, ? - incomplete

   Network          Next Hop            Metric LocPrf Weight Path
*> 10.10.0.0/16     0.0.0.0                  0         32768 ?
*> 10.10.120.0/24   10.29.1.2                0         32768 ?
*> 10.29.0.0/24     0.0.0.0                  0         32768 ?
*> 10.29.0.0/16     0.0.0.0                  0         32768 ?
*> 10.29.16.0/24    0.0.0.0                  0         32768 ?
*> 10.29.128.0/24   0.0.0.0                  0         32768 ?
*> 10.29.253.224/29 0.0.0.0                  0         32768 ?
*> 10.33.0.0/24     10.29.1.2                0         32768 ?
*> 10.33.0.0/16     0.0.0.0                  0         32768 ?
*> 10.33.4.0/24     10.29.1.2                0         32768 ?
*> 10.33.5.0/24     10.29.1.2                0         32768 ?





Старты 
запрещаем 
10.29.0.0/24


ip prefix-list rumelco_net_no_29 seq 5 permit 10.10.1.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 10 permit 10.10.15.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 15 permit 10.10.120.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 20 permit 10.10.0.0/16 le 30
ip prefix-list rumelco_net_no_29 seq 25 deny 10.29.0.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 26 permit 10.29.1.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 30 permit 10.29.2.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 35 permit 10.29.4.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 40 permit 10.29.5.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 45 permit 10.29.14.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 50 permit 10.29.15.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 55 permit 10.29.17.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 57 permit 10.29.30.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 60 permit 10.29.0.0/16 le 30
ip prefix-list rumelco_net_no_29 seq 65 permit 10.33.0.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 70 permit 10.33.5.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 75 permit 10.33.0.0/16 le 30
ip prefix-list rumelco_net_no_29 seq 100 deny 0.0.0.0/0 le 32

sh ip bgp neighbors 10.192.10.153 advertised-routes 
BGP table version is 113005, local router ID is 10.192.10.29
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale
Origin codes: i - IGP, e - EGP, ? - incomplete

   Network          Next Hop            Metric LocPrf Weight Path
*> 10.10.0.0/16     0.0.0.0                  0         32768 ?
*> 10.10.1.0/24     10.29.1.2                0         32768 ?
*> 10.10.15.0/24    10.29.1.2                0         32768 ?
*> 10.10.120.0/24   10.29.1.2                0         32768 ?
*> 10.29.0.0/16     0.0.0.0                  0         32768 ?
*> 10.29.1.0/30     0.0.0.0                  0         32768 ?
*> 10.29.2.0/24     10.29.1.2                0         32768 ?
*> 10.29.4.0/24     10.29.1.2                0         32768 ?
*> 10.29.5.0/24     10.29.1.2                0         32768 ?
*> 10.29.14.0/24    10.29.1.2                0         32768 ?
*> 10.29.15.0/24    0.0.0.0                  0         32768 ?
*> 10.29.16.0/24    0.0.0.0                  0         32768 ?
*> 10.29.17.0/24    0.0.0.0                  0         32768 ?
*> 10.29.30.0/24    10.29.1.2                0         32768 ?
*> 10.29.128.0/24   0.0.0.0                  0         32768 ?
*> 10.29.253.224/29 0.0.0.0                  0         32768 ?
*> 10.33.0.0/24     10.29.1.2                0         32768 ?
*> 10.33.0.0/16     0.0.0.0                  0         32768 ?
*> 10.33.4.0/24     10.29.1.2                0         32768 ?
*> 10.33.5.0/24     10.29.1.2                0         32768 ?







Маршрут будет разрешен или запрещен на основании следующих правил:

    Пустой лист разрешает все префиксы
    Если префикс разрешен, то маршрут используется, иначе – не используется
    Лист префиксов содержит нумерованные записи, маршрутизатор начинает проверку соответствия начиная сверху списка, с записи с минимальным номером
    Если соответствие найдено, то просмотр листа префиксов прекращается. Для повышения эффективности располагайте записи с наибольшей вероятностью совпадения вверху списка с меньшими порядковыми номерами
    Если не произошло ни одного соответствия, будет применена неявная политика по умолчанию deny any




















Переделка Бахрушина

1.Повесит secondary, сейчас
ip address 10.29.253.225 255.255.255.248 secondary
2. Расформировать одного из BGP нейборов
3. Через внутренний адрес сконфигурировать СE1

Проверить, что всё заработало


Конфиг роутера
class-map match-any REAL-TIME
 match ip precedence 5 
class-map match-any PREMIUM
 match ip precedence 3 
!
policy-map PLATINUM
 class REAL-TIME
  priority percent 60
 class PREMIUM
  bandwidth percent 15 
  random-detect
 class class-default
policy-map PLATINUM-ETH-20MB
 class class-default
  shape average 204800000
   service-policy PLATINUM
policy-map PLATINUM-ETH-100MB
 class class-default
  shape average 102400000
   service-policy PLATINUM




router ospf 110
 redistribute connected metric 1 metric-type 1 subnets
 redistribute static metric 1 metric-type 1 subnets
 redistribute bgp 65050 metric 1 metric-type 1 subnets
 passive-interface default
 no passive-interface GigabitEthernet0/1
 network 10.170.254.0 0.0.0.255 area 0
!
router bgp 65050
 bgp log-neighbor-changes
 neighbor 10.192.10.169 remote-as 20866
 !
 address-family ipv4
  aggregate-address 10.170.0.0 255.255.0.0 summary-only
  redistribute connected
  redistribute static
  redistribute ospf 110 match internal external 1 external 2
  neighbor 10.192.10.169 activate
  neighbor 10.192.10.169 prefix-list vienna-net out
 exit-address-family


ip prefix-list vienna-net seq 10 permit 10.170.0.0/16 le 30
ip prefix-list vienna-net seq 20 permit 10.192.10.168/30 le 32
ip prefix-list vienna-net seq 90 deny 0.0.0.0/0 le 32


logging history size 0
logging trap notifications
logging origin-id hostname
logging facility local2
logging host 10.192.10.253
logging host 10.192.10.252


snmp-server community Sh73ah91Kld RW 57
snmp-server community Fv8Ya64PQ RO 56
snmp-server ifindex persist
snmp-server tftp-server-list 57
snmp-server location Vienna-CE0
snmp-server contact iptech@sc.ru
snmp-server file-transfer access-group 57 protocol tftp



line vty 0 4
 access-class 10 in
 exec-timeout 480 0
 privilege level 15
 login local
 transport input ssh
line vty 5 15
 access-class 10 in
 exec-timeout 480 0
 privilege level 15
 login local
 transport input ssh
!
scheduler allocate 20000 1000
ntp logging
ntp access-group peer 61
ntp access-group serve-only 62
ntp update-calendar
ntp server 10.192.10.252 prefer
ntp server 10.192.10.253



4. Зайти через внутренний интерфейс на новый CE0 через CE1 и настроить BGP
