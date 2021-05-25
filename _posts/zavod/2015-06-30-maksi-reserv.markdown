---
layout: post
title:  "maksi-reserv"
date:   2015-06-30 04:34:24 +0300
categories: zavod
tags: zavod
---

# maksi-reserv

Viz-Sov-Ce0

interface FastEthernet0/0
 description Uplink for MNG and Video
 no ip address
 duplex auto
 speed auto
!         
interface FastEthernet0/0.19
 description #Managment Vlan #pheonix 19.11.2008 
 encapsulation dot1Q 19
 ip address 10.90.19.1 255.255.255.0
 no cdp enable
!         
interface FastEthernet0/1
 no ip address
 shutdown 
 duplex auto
 speed auto


interface Serial0/1/0
 description # Uplink to Golden-Telecom IPVPN
 bandwidth 2048
 ip address 10.192.10.90 255.255.255.252
 load-interval 30
 service-policy output PLATINUM
!         
interface Serial0/1/1
 no ip address
 shutdown 
 clock rate 2000000

!         
router ospf 110
 log-adjacency-changes
 redistribute connected metric 1 metric-type 1 subnets
 redistribute static metric 1 metric-type 1 subnets
 redistribute bgp 65021 metric 1 metric-type 1 subnets
 passive-interface default
 no passive-interface FastEthernet0/0.19
 network 10.90.19.0 0.0.0.255 area 0
!         
router bgp 65021
 bgp log-neighbor-changes
 neighbor 10.192.10.89 remote-as 3216
 
address-family ipv4
  neighbor 10.192.10.89 activate
  no auto-summary
  no synchronization
  network 10.90.0.0 mask 255.255.255.0
  network 10.90.1.0 mask 255.255.255.252
  network 10.90.4.0 mask 255.255.255.0
  network 10.90.18.1 mask 255.255.255.255
  network 10.90.18.8 mask 255.255.255.248
  network 10.90.18.16 mask 255.255.255.252
  network 10.90.19.0 mask 255.255.255.0
  network 10.192.3.8 mask 255.255.255.248
  network 10.192.10.88 mask 255.255.255.252
 exit-address-family





Viz-TTK-CE1
interface FastEthernet0/0
 description # Link to TTK
 ip address 10.192.10.114 255.255.255.252
 load-interval 30
 duplex full
 speed 100
!         
interface FastEthernet0/0.19
 ip ospf cost 200
!         
interface FastEthernet0/1
 description #Uplink to MNG NET #pheonix 20.11.2008
 no ip address
 duplex auto
 speed auto
!         
interface FastEthernet0/1.18
 ip ospf cost 200
!         
interface FastEthernet0/1.19
 encapsulation dot1Q 19
 ip address 10.90.19.4 255.255.255.0

!         
router ospf 110
 log-adjacency-changes
 redistribute connected metric 1 metric-type 1 subnets
 redistribute static metric 1 metric-type 1 subnets
 redistribute bgp 65021 metric 1 metric-type 1 subnets
 passive-interface default
 no passive-interface FastEthernet0/1
 no passive-interface FastEthernet0/1.19
 network 10.90.19.0 0.0.0.255 area 0
!         
router bgp 65021
 bgp log-neighbor-changes
 neighbor 10.192.10.90 remote-as 65021
 neighbor 10.192.10.113 remote-as 20485
 !        
 address-family ipv4
  neighbor 10.192.10.90 activate
  neighbor 10.192.10.113 activate
  neighbor 10.192.10.113 route-map viz-backup out
  no auto-summary
  no synchronization
  network 10.90.0.0 mask 255.255.0.0
  network 10.90.0.0 mask 255.255.255.0
  network 10.90.4.0 mask 255.255.255.0
  network 10.90.18.1 mask 255.255.255.255
  network 10.90.18.8 mask 255.255.255.248
  network 10.90.18.16 mask 255.255.255.252
  network 10.90.19.0 mask 255.255.255.0
  network 10.90.254.0 mask 255.255.255.0
  network 10.192.10.112 mask 255.255.255.252
 exit-address-family
!         











!         
interface FastEthernet0/0.18
 description #NLMK LAN
 encapsulation dot1Q 18
 ip address 10.90.18.11 255.255.255.248
 no cdp enable
!         
interface FastEthernet0/0.19
 description Managment Lan
 encapsulation dot1Q 19
 ip address 10.90.19.3 255.255.255.0
 no cdp enable
!         
interface FastEthernet0/1
 no ip address
 shutdown 
 duplex auto
 speed auto
!         
interface FastEthernet0/0/0
!         
interface FastEthernet0/0/1
!         
interface FastEthernet0/0/2
!         
interface FastEthernet0/0/3
!         
interface Vlan1
 no ip address
!         
router ospf 110
 log-adjacency-changes
 redistribute connected metric 1 metric-type 1 subnets
 redistribute static metric 1 metric-type 1 subnets
 passive-interface default
 no passive-interface FastEthernet0/0.18
 no passive-interface FastEthernet0/0.19
 network 10.90.18.8 0.0.0.7 area 0
 network 10.90.19.0 0.0.0.255 area 0


