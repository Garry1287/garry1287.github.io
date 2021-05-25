---
layout: post
title:  "rumelco_change"
date:   2009-06-16 17:57:01 +0400
categories: zavod
tags: zavod
---

# rumelco_change



На rumelco-ce0

убрать 108 влан

Сделать default
ip route 0.0.0.0 0.0.0.0 10.192.10.153



Добавить

router ospf 110
 redistribute connected metric 1 metric-type 1 subnets
 redistribute static metric 1 metric-type 1 subnets
 redistribute bgp 65017 metric 1 metric-type 1 subnets
 passive-interface default
 no passive-interface Fastethernet0/1
 network 10.29.253.224 0.0.0.7 area 0


Добавить
router bgp 65022
no bgp router-id 10.192.10.29
bgp router-id 10.192.10.154 
no neighbor 10.192.10.30 remote-as 3216

address-family ipv4
  redistribute ospf 110 metric 1
   no neighbor 10.192.10.30 activate
   no neighbor 10.192.10.30 weight 100
   no neighbor 10.192.10.30 prefix-list rumelco_net_29 out
   no neighbor 10.192.10.153 prefix-list rumelco_net_no_29 out
   neighbor 10.192.10.153 prefix-list rumelco_net out



no route-map prep-out-beeline permit 30

убрать 11 и 110 вланы

Передёрнуть bgp














На новом CE1


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


interface FastEthernet0/0
 description #Uplink to Beeline
 bandwidth 10240
 encapsulation dot1Q 108
 ip address 10.192.10.29 255.255.255.252
 service-policy output PLATINUM-ETH-10MB

ip route 0.0.0.0 0.0.0.0 10.192.10.30

interface FastEthernet0/1
 description # IPVPN data-transmit
 ip address 10.29.253.226 255.255.255.248
 load-interval 30
 duplex auto
 speed auto




router ospf 110
 redistribute connected metric 1 metric-type 1 subnets
 redistribute static metric 1 metric-type 1 subnets
 redistribute bgp 65017 metric 1 metric-type 1 subnets
 passive-interface default
 no passive-interface GigabitEthernet0/0
 network 10.29.253.224 0.0.0.7 area 0




ip prefix-list rumelco_net seq 10 permit 10.10.1.0/24 le 30
ip prefix-list rumelco_net seq 20 permit 10.10.15.0/24 le 30
ip prefix-list rumelco_net seq 30 permit 10.10.120.0/24 le 30
ip prefix-list rumelco_net seq 40 permit 10.29.0.0/16 le 30
ip prefix-list rumelco_net seq 50 permit 10.33.0.0/16 le 30
ip prefix-list rumelco_net seq 60 deny 0.0.0.0/0 le 32




router bgp 65017

 bgp log-neighbor-changes
 neighbor 10.192.10.30 remote-as 3216
 !
 address-family ipv4
 redistribute connected
 redistribute static
 redistribute ospf 110 metric 1
 neighbor 10.192.10.30 activate
 neighbor 10.192.10.30 prefix-list rumelco_net out
 no auto-summary
 no synchronization
 network 10.10.1.0 mask 255.255.255.0
 network 10.10.15.0 mask 255.255.255.0
 network 10.10.120.0 mask 255.255.255.0
 network 10.29.0.0 mask 255.255.0.0
 network 10.33.0.0 mask 255.255.0.0
 exit-address-family




access-list 10 permit 10.192.10.0 0.0.0.255
access-list 10 deny   any
access-list 56 permit 10.192.10.190
access-list 56 permit 172.19.4.0 0.0.3.255
access-list 56 deny   any
access-list 57 permit 10.192.10.252
access-list 57 permit 10.192.10.253
access-list 57 permit 10.192.10.190
access-list 57 deny   any
access-list 61 remark NTP: access-group peer
access-list 61 permit 10.192.10.252
access-list 61 permit 10.192.10.253
access-list 61 deny   any
access-list 62 remark NTP: access-group serve-only
access-list 62 permit 10.0.0.0 0.255.255.255
access-list 62 deny   any


snmp-server community Fv8Ya64PQ RO 56
snmp-server community Fv8Ya64PQ RW 57
snmp-server ifindex persist
snmp-server location RUMELCO-CE0
snmp-server contact iptech@sc.ru
snmp-server tftp-server-list 57




logging history size 0
logging trap notifications
logging origin-id hostname
logging facility local2
logging 10.192.10.190
logging 10.192.10.253





ntp logging
ntp access-group peer 61
ntp access-group serve-only 62
ntp update-calendar
ntp server 10.192.10.252 prefer
ntp server 10.192.10.253

line vty 0 4
 access-class 10 in
 exec-timeout 480 0
 transport input telnet ssh
 transport output telnet ssh
line vty 5 15
 access-class 10 in
 exec-timeout 480 0
 transport input telnet ssh
 transport output telnet ssh



















logging buffered 32768 informational
logging rate-limit 1000
enable secret OagVawra



aaa new-model
aaa authentication login default local

username hd secret Teetomna


line vty 0 4
 access-class 10 in
 exec-timeout 480 0
 transport input telnet ssh
 transport output telnet ssh
line vty 5 15
 access-class 10 in
 exec-timeout 480 0
 transport input telnet ssh
 transport output telnet ssh



10.29.253.226




















ip prefix-list rumelco_net seq 10 permit 10.10.1.0/24 le 30
ip prefix-list rumelco_net seq 20 permit 10.10.15.0/24 le 30
ip prefix-list rumelco_net seq 30 permit 10.10.120.0/24 le 30
ip prefix-list rumelco_net seq 40 permit 10.29.0.0/16 le 30
ip prefix-list rumelco_net seq 50 permit 10.33.0.0/16 le 30
ip prefix-list rumelco_net seq 60 deny 0.0.0.0/0 le 32


Убрать


ip prefix-list rumelco_net seq 5 permit 10.10.1.0/24 le 30
ip prefix-list rumelco_net seq 10 permit 10.10.15.0/24 le 30
ip prefix-list rumelco_net seq 15 permit 10.10.120.0/24 le 30
ip prefix-list rumelco_net seq 20 permit 10.29.0.0/16 le 30
ip prefix-list rumelco_net seq 25 permit 10.33.0.0/24 le 30
ip prefix-list rumelco_net seq 30 deny 0.0.0.0/0 le 32
!
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
!
ip prefix-list rumelco_net_no_29 seq 5 permit 10.10.1.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 10 permit 10.10.15.0/24 le 30
ip prefix-list rumelco_net_no_29 seq 15 deny 10.10.120.0/24 le 30
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
ip prefix-list rumelco_net_no_29 seq 75 permit 10.33.0.0/16 le































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
 no auto-summary
 no synchronization
 network 10.10.1.0 mask 255.255.255.0
 network 10.10.15.0 mask 255.255.255.0
 network 10.10.120.0 mask 255.255.255.0
 network 10.29.0.0 mask 255.255.0.0
 network 10.33.0.0 mask 255.255.0.0
 exit-address-family




































