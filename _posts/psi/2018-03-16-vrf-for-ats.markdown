---
layout: post
title:  "vrf-for-ats"
date:   2018-03-16 04:40:50 +0300
categories: PSI
tags: PSI
---

# vrf-for-ats
route add -net 192.168.253.16/30 dev vlan99

ip vrf mngt-for-ats
 description # Mngt for ATS
 rd 20866:418
 route-target export 20866:4180
 route-target import 20866:4180
 maximum routes 500 100

router bgp 20866
 address-family ipv4 vrf mngt-for-ats
 redistribute connected
 redistribute static
 default-information originate
 no synchronization
 exit-address-family



 encapsulation dot1Q 99
 ip vrf forwarding mngt-for-ats
 ip address 192.168.253.21 255.255.255.252
 mpls netflow egress