---
layout: post
title:  "gre_over_vpn"
date:   2012-12-21 10:55:22 +0400
categories: vpn
tags: vpn
---

# gre_over_vpn
Stagdok

interface Tunnel0
 bandwidth 2048
 ip unnumbered Loopback1
 ip nat outside
 ip virtual-reassembly
 ip tcp adjust-mss 1300
 load-interval 30
 traffic-shape rate 2048000 51200 51200 1000
 tunnel source FastEthernet0/0.10
 tunnel destination 10.192.3.1
!
interface Loopback1
 ip address 81.20.196.11 255.255.255.255




interface FastEthernet0/0.10
 description #IPVPN via PSI radio (D-link #24)
 encapsulation dot1Q 10
 ip address 10.192.10.198 255.255.255.252
 no snmp trap link-status

ip nat Stateful id 1
ip nat inside source list 1 interface Loopback1 overload

access-list 1 permit 192.168.1.0 0.0.0.255









CDE-C3


interface Tunnel1
 description # OAO Stagdok; Tunneled through NLMK VPN #LN 4060_58
 bandwidth 2048
 ip unnumbered Loopback0
 ip flow ingress
 traffic-shape rate 2048000 51200 51200 1000
 tunnel source Loopback10
 tunnel destination 10.192.10.194
 tunnel vrf nlmk-vpn
end

interface Loopback0
 description # Interface for Tunnel endpoint, IP/MPLS and BGP exchanges
 ip address 81.20.192.78 255.255.255.255
end

interface Loopback10
 description # POP address in IPVPN NLMK
 ip vrf forwarding nlmk-vpn
 ip address 10.192.3.1 255.255.255.255
end





