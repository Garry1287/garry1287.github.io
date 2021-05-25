---
layout: post
title:  "KNMPZ-tunnel"
date:   2013-07-18 09:20:58 +0400
categories: zavod
tags: zavod
---

# KNMPZ-tunnel
Выключить BGP на резервном канале Beeline и через него поднять туннель в Калугу



interface Tunnel10
desc #Tunnel via Beeline kanal to Kaluga
 ip vrf forwarding nlmk-vpn
 ip address 10.192.11.237 255.255.255.252
shutdown
 tunnel source GigabitEthernet0/0.857
 tunnel destination 10.192.10.70

ip route vrf nlmk-vpn 10.60.0.0 255.255.0.0 Tunnel10




interface Tunnel10
desc #Tunnel via Beeline kanal to Lipetsk
ip address 10.192.11.238 255.255.255.252
shutdown
 tunnel source GigabitEthernet0/2
 tunnel destination 10.192.10.77

ip route 0.0.0.0 0.0.0.0 Tunnel10
