---
layout: post
title:  "Резервирование каналов средствами BGP"
date:   2009-05-04 21:54:23 +0400
categories: backup
tags: backup bgp
---


```
# backup-bgp-ipvpn-stk
class-map match-any CHK-PRE
 match ip precedence 3 
class-map match-any CHK-REA
 match ip precedence 5 




policy-map CHK-PRIO
 class CHK-REA
    priority percent 40
 class CHK-PRE
    bandwidth percent 50
 class class-default
    fair-queue

policy-map CHK-QOS
 class class-default
    shape average 1024000
  service-policy CHK-PRIO


interface GigabitEthernet0/0.291
 description # Chicken Kingdom IPVPN (LES)
 encapsulation dot1Q 291
 ip vrf forwarding chkingdom-ipvpn
 ip address 10.10.10.5 255.255.255.252
 ip flow ingress
 no cdp enable
 service-policy output CHK-QOS
end
```


Стагдок
```
class-map match-any STANDARD
 match ip precedence 0  1 
class-map match-any REAL-TIME
 match ip precedence 5 
class-map match-any PREMIUM
 match ip precedence 3 
!         
!         
policy-map PLATINUM
 class REAL-TIME
  priority percent 60
 class PREMIUM
  bandwidth percent 15
  random-detect
 class class-default
policy-map PLATINUM-ETH-10MB
 class class-default
  shape average 10240000
  service-policy PLATINUM
policy-map PLATINUM-SUB
 class class-default
  shape average percent 100
  service-policy PLATINUM
!         
interface FastEthernet0/0.109
 description #Uplink to Starttelekom
 bandwidth 10240
 encapsulation dot1Q 109
 ip address 10.192.10.154 255.255.255.252
 service-policy output PLATINUM-ETH-10MB



interface Serial0/2/0:0.16 point-to-point
 description # NLMK IPVPN Link
 bandwidth 1984
 ip address 10.192.10.29 255.255.255.252
 frame-relay class EQUANT-FR
 frame-relay interface-dlci 16


router bgp 65017
 bgp router-id 10.192.10.29
 bgp log-neighbor-changes
 neighbor 10.192.10.30 remote-as 2854
 neighbor 10.192.10.153 remote-as 8744
 !        
 address-family ipv4
 redistribute connected
 redistribute static
 neighbor 10.192.10.30 activate
 neighbor 10.192.10.30 prefix-list rumelco_net_no_29 out
 neighbor 10.192.10.30 route-map prep-out-equant out
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


ip prefix-list rumelco_net seq 5 permit 10.10.1.0/24 le 30
ip prefix-list rumelco_net seq 10 permit 10.10.15.0/24 le 30
ip prefix-list rumelco_net seq 15 permit 10.10.120.0/24 le 30
ip prefix-list rumelco_net seq 20 permit 10.29.0.0/16 le 30
ip prefix-list rumelco_net seq 25 permit 10.33.0.0/24 le 30
ip prefix-list rumelco_net seq 30 deny 0.0.0.0/0 le 32



route-map prep-out-equant permit 60
 set as-path prepend 65017 65017 65017 65017 65017 65017 65017 65017
```



65500 выделан AS для IPVPN Ростелеком



### Bgp резервирование
weight 32768 по умолчанию для маршрутов, которые объявляет маршрутизатор, для внешних 0.
Чтобы больше weight у внешних, тем они приоритетьнее, поэтому для того, чтобы исходящий траффик шёл
через нужный аплинк, то этому нейбору надо предоставить больший weight

Это входящего траффика нужны препенды, чем больше препендов, тем длинее путь, тем хуже канал и входящий траффик идёт через другой
Один линк

```
router bgp 65015
 bgp router-id 10.192.10.198
 bgp log-neighbor-changes
 neighbor 10.192.10.197 remote-as 20866
 neighbor 10.192.10.193 remote-as 65500
 !
 address-family ipv4
 neighbor 10.192.10.197 activate
 neighbor 10.192.10.197 route-map prep-out-psi out
 neighbor 10.192.10.197 prefix-list stagdok_net out
 neighbor 10.192.10.193 shutdown
 neighbor 10.192.10.193 weight 100
 neighbor 10.192.10.193 prefix-list stagdok_net out
 no auto-summary
 no synchronization
 network 10.192.10.192 mask 255.255.255.252
 network 10.192.10.196 mask 255.255.255.252
 network 10.194.0.0 mask 255.255.255.0
 network 10.194.1.0 mask 255.255.255.252
 network 10.194.4.0 mask 255.255.255.0
 network 10.194.10.0 mask 255.255.255.0
 exit-address-family
!

ip route 10.194.4.0 255.255.255.0 10.194.1.2
ip route 10.194.10.0 255.255.255.0 10.194.1.2


route-map prep-out-psi permit 60
 set as-path prepend 65015 65015 65015


ip prefix-list stagdok_net seq 5 permit 10.192.10.192/30 le 30
ip prefix-list stagdok_net seq 10 permit 10.192.10.196/30 le 30
ip prefix-list stagdok_net seq 15 permit 10.194.0.0/24 le 30
ip prefix-list stagdok_net seq 20 permit 10.194.1.0/24 le 30
ip prefix-list stagdok_net seq 25 permit 10.194.4.0/24 le 30
ip prefix-list stagdok_net seq 30 permit 10.194.10.0/24 le 30
ip prefix-list stagdok_net seq 35 deny 0.0.0.0/0 le 32
```







