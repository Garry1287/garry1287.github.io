---
layout: post
title:  "nat_pool_forward"
date:   2009-11-30 10:43:05 +0300
categories: Networking
tags: Networking
---

# nat_pool_forward
ip nat pool FWR-KASKAD 192.168.0.101 192.168.0.101 netmask 255.255.255.0 type rotary
ip nat inside destination list 150 pool FWR-KASKAD
access-list 150 permit udp any any range 12000 12225
access-list 150 permit tcp any any range 12000 12225














ip access-list extended KASKAD_SIP
permit udp any any range 12000 12225
permit tcp any any range 12000 12225

route-map KASKAD_SIP_MAP permit 10
  match ip address KASKAD_SIP

ip nat inside source static 192.168.0.101 81.20.196.69 vrf cust9 route-map KASKAD_SIP_MAP extendable





