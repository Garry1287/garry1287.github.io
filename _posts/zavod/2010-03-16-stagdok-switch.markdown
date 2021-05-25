---
layout: post
title:  "stagdok-switch"
date:   2010-03-16 01:20:21 +0300
categories: zavod
tags: zavod
---

# stagdok-switch
interface Loopback12
 description Bras-172.31.3.3
 ip address 172.31.3.3 255.255.255.255
 ip flow ingress
 ip route-cache same-interface
 ip route-cache policy



interface Loopback13
 description #Bras-172.31.3.5
 ip address 172.31.3.5 255.255.255.255
 ip flow ingress
 ip route-cache same-interface
 ip route-cache policy


interface Loopback14
 description Bras-172.31.3.8
 ip address 172.31.3.8 255.255.255.255
 ip flow ingress
 ip route-cache same-interface
 ip route-cache policy



router bgp 20866
 address-family ipv4 vrf equant-test
  neighbor 10.192.10.198 remote-as 65015
  neighbor 10.192.10.198 activate


DES-2108:>sh switch                                                            
Command:  sh switch

Product Name:DES-2108                               
Firmware Version:2.00.08
Protocol Version:2.001.002
DHCP:Disable
IP Address:10.194.0.2
Subnet mask:255.255.255.0
Default gateway:10.194.0.1
Trap IP:0.0.0.0
MAC address:00-13-46-26-95-c1
System Name:
Location Name:
System Contact:
System Aging Time:300
VLAN Type:802.1Q BASE
Login Timeout (minutes):5
System UpTime:9 days 0 hours 2 mins 27 seconds
Web Server Port:80
