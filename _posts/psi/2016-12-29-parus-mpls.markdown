---
layout: post
title:  "parus-mpls"
date:   2016-12-29 07:41:20 +0300
categories: PSI
tags: PSI
---

# parus-mpls


interface GigabitEthernet0/1.680
 description #Test Eburg MPLS
 encapsulation dot1Q 680
 ip address 81.20.192.113 255.255.255.252
 ip flow egress
 ip ospf priority 3
 ip ospf mtu-ignore
 mpls label protocol ldp
 mpls ip
 no cdp enable
end






interface GigabitEthernet0/1.122
 description #Parus INET Termination #smithy 20150226
 encapsulation dot1Q 122
 ip address 81.20.193.145 255.255.255.252
 ip flow ingress
 ip flow egress
 rate-limit input 2048000 384000 772000 conform-action transmit exceed-action drop
 rate-limit output 2048000 384000 772000 conform-action transmit exceed-action drop
 ip ospf network non-broadcast
 ip ospf mtu-ignore
 no cdp enable
end



neighbor 81.20.193.146












1. Loopback
interface Loopback0
 description # Interface for Tunnel endpoint, IP/MPLS and BGP exchanges
 ip address 81.20.192.67 255.255.255.255

Переделать DNS и обратную запись сделать


2. Включить mpls


ip domain name Parus-C0
ip cef
no ipv6 cef
multilink bundle-name authenticated
!
mpls label protocol ldp

clock timezone MSK 3 0
clock calendar-valid
!
ip icmp rate-limit unreachable 1000
mpls ldp router-id Loopback0



interface FastEthernet0/0.122
 mpls label protocol ldp
 mpls ip  


{}
interface FastEthernet0/0.122
 description #Parus-INET #pheonix 17.03.2009
 encapsulation dot1Q 122
 ip address 81.20.193.146 255.255.255.252
 ip access-group 101 in
 rate-limit input 256000 48000 96000 conform-action set-prec-continue 0 exceed-action set-prec-continue 0
 rate-limit input 4096000 772000 1544000 conform-action transmit exceed-action drop
 ip ospf network non-broadcast
 ip ospf priority 0
 ip ospf mtu-ignore
 no snmp trap link-status
 mpls netflow egress
{}



router bgp 20866
 bgp log-neighbor-changes
 neighbor 81.20.192.64 remote-as 20866
 neighbor 81.20.192.64 update-source Loopback0
 neighbor 81.20.192.66 remote-as 20866
 neighbor 81.20.192.66 update-source Loopback0
 neighbor 81.20.192.70 remote-as 20866
 neighbor 81.20.192.70 update-source Loopback0
 neighbor 81.20.192.71 remote-as 20866
 neighbor 81.20.192.71 update-source Loopback0
 neighbor 81.20.192.72 remote-as 20866
 neighbor 81.20.192.72 update-source Loopback0
 neighbor 81.20.192.74 remote-as 20866
 neighbor 81.20.192.74 update-source Loopback0
 neighbor 81.20.192.76 remote-as 20866
 neighbor 81.20.192.76 update-source Loopback0
 neighbor 81.20.192.77 remote-as 20866
 neighbor 81.20.192.77 update-source Loopback0
 neighbor 81.20.192.79 remote-as 20866
 neighbor 81.20.192.79 update-source Loopback0
 neighbor 81.20.193.248 remote-as 20866
 neighbor 81.20.193.248 update-source Loopback0
 neighbor 81.20.196.49 remote-as 20866
 neighbor 81.20.196.49 update-source Loopback0
 !
 address-family vpnv4
  neighbor 81.20.192.64 activate
  neighbor 81.20.192.64 send-community extended
  neighbor 81.20.192.66 activate
  neighbor 81.20.192.66 update-source Loopback0
  neighbor 81.20.192.70 activate
  neighbor 81.20.192.70 send-community extended
  neighbor 81.20.192.71 activate
  neighbor 81.20.192.71 send-community extended
  neighbor 81.20.192.72 activate
  neighbor 81.20.192.72 send-community extended
  neighbor 81.20.192.74 activate
  neighbor 81.20.192.74 send-community extended
  neighbor 81.20.192.76 activate
  neighbor 81.20.192.76 send-community extended
  neighbor 81.20.192.77 activate
  neighbor 81.20.192.77 send-community extended
  neighbor 81.20.192.79 activate
  neighbor 81.20.192.79 send-community extended
  neighbor 81.20.193.248 activate
  neighbor 81.20.193.248 send-community extended
  neighbor 81.20.196.49 activate
  neighbor 81.20.196.49 send-community extended
 exit-address-family



На всех mpls роутерах добавить 

router bgp 20866
  neighbor 81.20.192.67 remote-as 20866
  neighbor 81.20.192.67 update-source Loopback0
 address-family vpnv4
  neighbor 81.20.192.67 activate
  neighbor 81.20.192.67 send-community extended

3. Телефония



4.Убрать BGP с комбинатом

На NLMK-CE(0|1) в том числе

добавить vrf комбинатовский

ip vrf nlmk-vpn
 description ### IPVPN NLMK
 rd 20866:101
 maximum routes 500 100
 route-target export 20866:1010
 route-target import 20866:1010

router bgp 20866
 address-family ipv4 vrf nlmk-vpn
  redistribute connected
  redistribute static
 exit-address-family


interface FastEthernet0/1
 description # Parus LAN
 ip vrf forwarding nlmk-vpn
 ip address 10.186.24.1 255.255.255.0
 duplex auto
 speed auto
 no cdp enable

5. Парус переделать, клиентов проверить.

