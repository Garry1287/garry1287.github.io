---
layout: post
title:  "maxi-without-vrf"
date:   2012-08-23 08:44:13 +0400
categories: zavod
tags: zavod
---

# maxi-without-vrf

Ебург



Убрать роутер оspf 110
на 15 поменять mg-video


в 109 распределять bgp 65022

72 нах не нужен


В bgp


interface FastEthernet0/0.15
 description # Maxi_Group LAN
 encapsulation dot1Q 15
 ip vrf forwarding mg-video
 ip address 192.168.1.8 255.255.252.0
 no cdp enable
!
!
interface FastEthernet0/0.65
 description # Link to Maxi_Group-CE0
 encapsulation dot1Q 65
 ip address 10.98.254.65 255.255.255.248
!
interface FastEthernet0/0.72
 description # Video-conferenece Link to Maxi_Group-CE0 New
 encapsulation dot1Q 72
 ip vrf forwarding mg-video
 ip address 10.98.254.73 255.255.255.248


router ospf 110 vrf mg-video
 log-adjacency-changes
 redistribute connected metric 1 metric-type 1 subnets
 redistribute static metric 1 metric-type 1 subnets
 redistribute bgp 65022 metric 1 metric-type 1 subnets
 passive-interface default
 no passive-interface FastEthernet0/0.72
 network 10.98.254.72 0.0.0.7 area 0
!

redistribute bgp 65022 metric 1 metric-type 1 subnets

router ospf 109
 log-adjacency-changes
 redistribute connected metric 1 metric-type 1 subnets
 redistribute static metric 1 metric-type 1 subnets
 passive-interface default
 no passive-interface FastEthernet0/0.13
 no passive-interface FastEthernet0/0.14
 no passive-interface FastEthernet0/0.65
 network 10.98.254.0 0.0.0.3 area 0
 network 10.98.254.4 0.0.0.3 area 0
 network 10.98.254.8 0.0.0.3 area 0
 network 10.98.254.12 0.0.0.3 area 0
 network 10.98.254.64 0.0.0.7 area 0













Убрать из mg-video


 address-family ipv4 vrf mg-video
  redistribute connected
  redistribute static
  redistribute ospf 110 vrf mg-video metric 1
  default-information originate
  no synchronization
  network 10.98.0.0 mask 255.255.255.0
  network 10.98.1.0 mask 255.255.255.0
  network 10.98.2.0 mask 255.255.255.0
  network 10.98.3.0 mask 255.255.255.0
  network 10.98.4.0 mask 255.255.255.240
  network 10.98.16.0 mask 255.255.255.0
 exit-address-family


Дефолт убарть, на нуль убрать из mg-video
ip route vrf mg-video 0.0.0.0 0.0.0.0 10.98.254.74
ip route vrf mg-video 10.98.0.0 255.255.0.0 Null0








Ревда



Убрать из этих 5

interface FastEthernet0/1.11
 description # Video-conference ethernet segment
 encapsulation dot1Q 11
 ip vrf forwarding mg-video
 ip address 10.98.1.1 255.255.255.0


interface FastEthernet0/1.12
 description # Maxi-Group LAN
 encapsulation dot1Q 12
 ip vrf forwarding mg-video
 ip address 192.168.100.159 255.255.252.0


interface FastEthernet0/1.15
 description # Maxi-Group Lan # Server's Group # pheonix 28/08/09
 encapsulation dot1Q 15
 ip vrf forwarding mg-video
 ip address 10.98.4.1 255.255.255.240
!         
interface FastEthernet0/1.20
 description #Maxi-Group LAN new
 encapsulation dot1Q 20
 ip vrf forwarding mg-video
 ip address 10.98.252.1 255.255.255.252



interface Serial0/1/0:0
 description #Secondary  Uplink #HD
 bandwidth 2048
 ip vrf forwarding mg-video
 ip address 10.192.10.106 255.255.255.252
 load-interval 30
 mpls ip  
 mpls accounting experimental input
 mpls accounting experimental output
 service-policy output PLATINUM




Перенести из vrf
 !        
 address-family ipv4 vrf mg-video
  redistribute connected
  redistribute static
  neighbor 10.192.10.105 remote-as 20485
  neighbor 10.192.10.105 update-source Serial0/1/0:0
  neighbor 10.192.10.105 activate
  neighbor 10.192.10.105 weight 200
  neighbor 10.192.10.105 prefix-list MG-REVDA-ADV out
  no synchronization
  network 10.98.4.0 mask 255.255.255.240
  network 10.98.24.0 mask 255.255.248.0
  network 10.98.252.0 mask 255.255.255.252
  network 10.98.254.4 mask 255.255.255.252
  network 10.98.254.16 mask 255.255.255.252
  network 192.168.100.0 mask 255.255.252.0
 exit-address-family

Перенести маршрут
ip route vrf mg-video 10.98.24.0 255.255.248.0 10.98.252.2











Березовский

Поменять
interface FastEthernet0/1.11
 description # Video-conference ethernet segment
 encapsulation dot1Q 11
 ip vrf forwarding mg-video
 ip address 10.98.2.1 255.255.255.0
!         
interface FastEthernet0/1.12
 description # Maxi-Group LAN
 encapsulation dot1Q 12
 ip vrf forwarding mg-video
 ip address 192.168.40.30 255.255.252.0
!         
!         
interface FastEthernet0/1.20
 description #Maxi-Group LAN new
 encapsulation dot1Q 20
 ip vrf forwarding mg-video
 ip address 10.98.252.9 255.255.255.252



Убрать и поменять
ip route vrf mg-video 10.98.20.0 255.255.252.0 10.98.252.10














Серьги


interface FastEthernet0/1.11
 description # Video-conference ethernet segment
 encapsulation dot1Q 11
 ip vrf forwarding mg-video
 ip address 10.98.3.1 255.255.255.0
!
interface FastEthernet0/1.12
 description # Maxi-Group LAN
 encapsulation dot1Q 12
 ip vrf forwarding mg-video
 ip address 192.168.201.152 255.255.252.0
!
!
interface FastEthernet0/1.20
 description #Maxi-Group Lan new
 encapsulation dot1Q 20
 ip vrf forwarding mg-video
 ip address 10.98.252.5 255.255.255.2



Убрать и поменять
ip route vrf mg-video 10.98.32.0 255.255.252.0 10.98.252.6
















ASA 
Уебать 10.98.254.74 и 75
