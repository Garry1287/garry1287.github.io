---
layout: post
title:  "domolink_cisco_pppoe"
date:   2010-11-08 03:18:43 +0300
categories: zavod
tags: zavod
---

# domolink_cisco_pppoe
ip name-server 195.34.224.1
ip name-server 195.34.224.2




interface GigabitEthernet0/0
 description #donwlink to RosTel inet (pppoe)
 bandwidth 2048
 no ip address
 ip flow ingress
 ip route-cache policy
 load-interval 30
 duplex auto
 speed auto
 pppoe enable group global
 pppoe-client dial-pool-number 1
!


interface GigabitEthernet0/1
 description # Dolomit LAN
 ip address 10.210.10.1 255.255.254.0
 ip nat inside
 ip virtual-reassembly in
 rate-limit input 4088000 768000 1532000 conform-action transmit exceed-action drop
 rate-limit output 4088000 768000 1532000 conform-action transmit exceed-action drop
 duplex auto
 speed auto
 no snmp trap link-status
!



!
interface Dialer1
 bandwidth 2048
 ip address negotiated
 ip flow ingress
 ip nat outside
 ip virtual-reassembly in
 encapsulation ppp
 ip route-cache policy
 ip tcp adjust-mss 1400
 load-interval 30
 dialer pool 1
 ppp chap hostname ll60206
 ppp chap password 7 075B7054175113011D
 no cdp enable
!


ip nat inside source list 1 interface Dialer1 overload


access-list 1 permit 192.168.1.0 0.0.0.255
access-list 1 permit 10.210.10.0 0.0.1.255
access-list 1 permit 10.210.254.0 0.0.1.255
access-list 1 deny   any





Доступ
aaa new-model
!
!
aaa authentication login default local
!
username amdin secret
enable secret


line vty 0 4
 access-class 10 in
 transport input telnet ssh
line vty 5 15
 access-class 10 in
 transport input telnet ssh
