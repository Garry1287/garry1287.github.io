---
layout: post
title:  "Обновление прошивки juniper"
date:   2013-03-13 04:04:42 +0400
categories: juniper Networking
tags: juniper
---

# Обновление прошивки juniper

[https://kb.juniper.net/InfoCenter/index?page=content&id=JSA10613](https://kb.juniper.net/InfoCenter/index?page=content&id=JSA10613)

[http://forum.nag.ru/forum/index.php?showtopic=92380&st=20](http://forum.nag.ru/forum/index.php?showtopic=92380&st=20)


[http://wtf.hijacked.us/wiki/index.php/Juniper](http://wtf.hijacked.us/wiki/index.php/Juniper)

```
 #run show interface ge-0/0/1

->To see the vlan number 501 Brief Information
#run show interface vlan.501

->To see port satus vlan member taging and Blocking information
#run show ether-switching interface ge0/0/1

->To see MAC learn from which vlan and port
#run show ether-switching table

->To see MAC learn from which port and only Vlan name "Configuration"
#run show ether-switching table | match Configuration

->Route Information
#run show route 194.193.222.0/24

->To see CPU and memory usage
#run show system process extensive

->To see only sfid Process information
#run show system process extensive | match sfid

->To see the all Configuration
#show configuration
#show configuration | no-more | display set

->To see running protocol
#show protocol

->To See any Firewall
#show firewal

->Spanning tree interface parameters
#run show spanning-tree interface

->Spanning Tree Bridge Parameter
#run show spanning-tree bridge

->Juniper model and software version
#run show version

->To see last shutdown and configured time
#run show system uptime

->To see Current Data and Time
#run show system uptime  

->Neighbor Connectivity of Juniper
#run show lldp neighbor

->To see the arp list
#run show arp

->To see Chassis mac address
#show chassis mac-address
```




Let's Apply the per-packet(flow) load-balancing forwarding policy for per-packet(flow) load balancing 

set policy-options policy-statement Policy-1 then load-balance per-packet
set routing-options forwarding-table export Policy-1

As we can see the policy is applied globally but it has impact on instance Router1 as well.

Насколько близок к значения моего свитча

- 16K ARP entries
- 300 ARP/sec learn rate per PFE
- 32K learned MAC addresses
Размер таблицы MAC-адресов  32K
Размер таблицы маршрутизации 10K IPv4 1K IPv6

```
> show route summary 
#> show ethernet-switching statistics mac-learning
Learning stats: 20 learn msg rcvd, 0 error, 9 forced update
#> show arp 
```

# Обновление прошивки Juniper

On EX4500 or EX4550 switches, the software forwarding infrastructure daemon (sfid) might continuously create core files, causing interruptions in traffic, because packets are erroneously freed twice. A possible trigger is the handling of Layer 2 protocol tunneling packets. [PR/941482: This issue has been resolved.]


[http://www.juniper.net/support/downloads/?p=ex4550#sw](http://www.juniper.net/support/downloads/?p=ex4550#sw)
[http://xcat.su/juniper/update-junos-cli/](http://xcat.su/juniper/update-junos-cli/)





Have you find RCA for your problem yet ?
I have similar problem when running EX4500+EX4200 VC (12.3R3).
CPU varied high/low rapidly because of sfid.

 
I have checked spanning-tree but but it's seem normally.
I've captured and saw some strange packet:
- There are many packet with TTL = 1 and ip destination which doesn't exist. Because TTL = 1 so Switch have to reply with TTL exceed (may cause CPU high). I've tried to discard these packet but not success because switch doesn't support filter packet with ttl=1 yet Smiley Sad
- There are some broadcast ARP message from switch to find MAC address of IP destination which doesn't exist. I have tried to discard these IP destination by configure static route discard.


Have anyone know shell command to check detail sfid process ?

```
set firewall family inet filter BLOCKTTL1 term TTL from ttl 1
set firewall family inet filter BLOCKTTL1 term TTL then accept
set firewall family inet filter BLOCKTTL1 term ACeetALTTL then accept

commit check
```

