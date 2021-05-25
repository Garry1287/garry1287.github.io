---
layout: post
title:  "Megafon-change"
date:   2011-06-11 12:56:10 +0400
categories: PSI
tags: PSI
---

# Megafon-change

Перед началом необходимо обновить информацию для AS20866 в БД RIPE


router bgp 20866
 neighbor 78.25.66.221 remote-as 31133
 neighbor 78.25.66.221 update-source Te1/3/0
 address-family ipv4
neighbor 78.25.66.221 activate
  neighbor 78.25.66.221 prefix-list deny_lesnets_from_uplinks in
  neighbor 78.25.66.221 prefix-list adv-to-megafon out



1. Объявлять только нас и наших клиентов (Индезит, НЛМК)
2. На первом этапе только нас, для теста
3. IBGP настроить для комбината между всеми BGW и k9-c0




На k9-c0 дать команду

router bgp 20866

 neighbor 81.20.192.75 remote-as 20866
 neighbor 81.20.192.75 update-source Loopback0
 neighbor 81.20.192.75 prefix-list ibgp-neigb-in in
 neighbor 81.20.192.75 prefix-list ibgp-neigb-out out



4. Перенастроить внутренний линк


int Po3
  shut




int Po3
  shut

int Po3.13
  shut
  no ip address 81.20.192.52 255.255.255.240

interface Te0/3/0
 no ip address
 ip flow ingress
 load-interval 30
 negotiation auto
end

int Te0/3/0.13
 description #OSPF-link
 encapsulation dot1Q 13
 ip address 81.20.192.52 255.255.255.240
 ip flow ingress
 ip flow egress
 ip ospf priority 50
 ip ospf mtu-ignore


router ospf 110
passive-interface Port-channel3.13
no passive-interface Te0/3/0.13





5. В ospf поменять местами маршруты
6. Beeline выключить




router ospf 110
default-information originate



router ospf 110
default-information originate metric 10




















ip prefix-list adv-to-megafon seq 5 permit 81.20.192.0/20 le 24
ip prefix-list adv-to-megafon seq 10 permit 193.104.11.0/24 le 32
ip prefix-list adv-to-megafon seq 100 deny 0.0.0.0/0 le 32

ip prefix-list allow-les-only seq 5 permit 195.34.224.0/19 le 21
ip prefix-list allow-les-only seq 15 permit 172.24.0.0/14
ip prefix-list allow-les-only seq 20 permit 178.234.0.0/16 le 21
ip prefix-list allow-les-only seq 30 permit 95.179.0.0/17 le 21
ip prefix-list allow-les-only seq 100 deny 0.0.0.0/0 le 32



 

























ip prefix-list default seq 10 permit 0.0.0.0/0
ip prefix-list default seq 20 deny 0.0.0.0/0 ge 1
!
ip prefix-list ibgp-neigb-in seq 20 deny 0.0.0.0/0 le 32
!
ip prefix-list ibgp-neigb-out seq 5 permit 81.20.194.0/24 le 32
ip prefix-list ibgp-neigb-out seq 20 deny 0.0.0.0/0 le 32
!
ip prefix-list nlmk-194-in seq 5 permit 81.20.194.0/24 le 32
ip prefix-list nlmk-194-in seq 20 deny 0.0.0.0/0 le 32
















router bgp 20866
neighbor 81.16.117.9 shutdown

  neighbor 81.16.117.9 activate
  neighbor 81.16.117.9 send-community both
  neighbor 81.16.117.9 weight 700
  neighbor 81.16.117.9 prefix-list deny_lesnets_from_uplinks in
  neighbor 81.16.117.9 prefix-list adv-to-stk out
  neighbor 81.16.117.9 route-map prep-out-start out



!