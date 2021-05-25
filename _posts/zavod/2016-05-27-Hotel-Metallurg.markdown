---
layout: post
title:  "Hotel-Metallurg"
date:   2016-05-27 20:27:03 +0300
categories: zavod
tags: zavod
---

# Hotel-Metallurg
Сменить IOS



weight 100 на 214, чтобы уходил траффик через него

Препенд, чтобы траффик приходил через другой интерфейс


interface FastEthernet0/0.2013
 description #NLMK-VPN rezerv (CDE-c2)
 encapsulation dot1Q 2013
 ip address 10.192.10.218 255.255.255.252
 no cdp enable
!
interface FastEthernet0/0.3057
 description #NLMK-VPN-Uplink #14.03.2011
 encapsulation dot1Q 3057
 ip address 10.192.10.214 255.255.255.252
 no cdp enable







router bgp 65049
 bgp router-id 10.192.10.198
 bgp log-neighbor-changes
 neighbor 10.192.10.213 remote-as 20866
 neighbor 10.192.10.217 remote-as 20866


 address-family ipv4
 neighbor 10.192.10.213 activate
 neighbor 10.192.10.213 weight 100
 neighbor 10.192.10.213 prefix-list hotmet_net out
 neighbor 10.192.10.217 activate
 neighbor 10.192.10.217 prefix-list hotmet_net out
 neighbor 10.192.10.217 route-map prep-out-psi out
 no auto-summary
 no synchronization
 network 10.192.10.212 mask 255.255.255.252
 network 10.192.10.216 mask 255.255.255.252
 network 10.214.0.0 mask 255.255.255.0
 exit-address-family



ip prefix-list hotmet_net seq 5 permit 10.214.0.0/24 le 30
ip prefix-list hotmet_net seq 100 deny 0.0.0.0/0 le 32



route-map prep-out-psi permit 60
 set as-path prepend 65049 65049 65049











ctd-c7

router bgp 20866
address-family ipv4 vrf nlmk-vpn
 neighbor 10.192.10.214 remote-as 20866
 neighbor 10.192.10.214 activate



cde-c3

router bgp 20866
address-family ipv4 vrf nlmk-vpn
 neighbor 10.192.10.218 remote-as 20866
 neighbor 10.192.10.218 activate

 






boot system tftp c1700-spservicesk9-mz.123-15.bin 10.192.10.189