---
layout: post
title:  "problem-bgp"
date:   2014-05-21 23:42:40 +0400
categories: routing
tags: routing
---

# problem-bgp
CTD-C5#traceroute 
Protocol [ip]: 
Target IP address: 213.180.193.3
Source address: 78.25.66.222
Numeric display [n]: n
Timeout in seconds [3]: 
Probe count [3]: 
Minimum Time to Live [1]: 
Maximum Time to Live [30]: 
Port Number [33434]: 
Loose, Strict, Record, Timestamp, Verbose[none]: 
Type escape sequence to abort.
Tracing the route to 213.180.193.3
VRF info: (vrf in name/id, vrf out name/id)
  1 78.25.66.221 1 msec 1 msec 1 msec
  2 10.222.48.113 [AS 3356] [MPLS: Label 5846 Exp 0] 29 msec 21 msec 14 msec
  3 10.222.71.6 [AS 3356] [MPLS: Label 4274 Exp 0] 11 msec
    10.222.71.2 [AS 3356] [MPLS: Label 7188 Exp 0] 12 msec
    10.222.71.6 [AS 3356] [MPLS: Label 4274 Exp 0] 10 msec
  4 10.222.77.10 [AS 3356] 13 msec 11 msec 11 msec
  5 10.222.177.142 [AS 3356] 11 msec
    10.222.177.150 [AS 3356] 17 msec
    10.222.177.142 [AS 3356] 16 msec
  6 37.29.106.154 [AS 31133] 10 msec 13 msec 11 msec
  7 93.158.140.62 [AS 13238] 10 msec 10 msec 12 msec
  8  *  *  * 
  9 87.250.239.99 [AS 13238] [MPLS: Label 17012 Exp 3] 11 msec 13 msec
    213.180.213.10 [AS 13238] 19 msec
 10  *  * 
    87.250.239.61 [AS 13238] [MPLS: Label 677299 Exp 3] 12 msec
 11 213.180.193.3 [AS 13238] 11 msec
    87.250.239.43 [AS 13238] 10 msec 10 msec


Jun 14 22:39:21: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:39:23: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:39:25: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:39:27: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:39:29: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:39:32: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:39:34: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:39:36: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:39:38: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:39:40: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:39:43: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:39:45: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:39:47: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:39:49: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:39:51: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:39:54: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:39:56: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:39:58: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:00: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:02: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:04: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:07: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:09: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:11: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:13: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:15: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:18: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:21.561: GigabitEthernet0/0/3 added as member-3 to port-channel3
 
Jun 14 22:40:20: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:22: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:24: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:26: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:29: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:31: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:33: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:35: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:37: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:39: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:42: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:44: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:46: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:48: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:50: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:53: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:55: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:57: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:40:59: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:01: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:03: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:06: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:08: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:10: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:12: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:14: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:17: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:19: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:21: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:23: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:25: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:28: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:30: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:32: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:34: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:36: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:38: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:41: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:43: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:45: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:47: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:49: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:52.608: GigabitEthernet0/0/3 taken out of port-channel3

Jun 14 22:41:52: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:54: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:56: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:41:58: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:00: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:03: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:05: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:07: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:09: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:11: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:13: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:16: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:18: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:20: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:22: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:24: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:27: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:29: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:31: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:33: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:35: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:38: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:40: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:42: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:44: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:46: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:48: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:51: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:53: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:55: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:57: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:42:59: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:02: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:04: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:06: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:08: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:10: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:13: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:15: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:17.803: GigabitEthernet0/0/3 added as member-3 to port-channel3
 
Jun 14 22:43:17: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:19: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:21: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:23: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:26: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:28: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:30: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:32: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:34: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:37: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:39: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:41: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:43: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:45: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:48: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0
Jun 14 22:43:50: %ETH_SPA_MAC-3-INTR_BURST: SIP0/3: Interrupts from MAC have crossed burst limit of 10 in 1000 msec for port 0/3/0


router ospf 110
 passive-interface Po3


 router-id 81.20.192.52
 redistribute connected metric 1 metric-type 1 subnets
 redistribute static metric 1 metric-type 1 subnets
  default
 vTenGigabitEthernet0/3/0.1

Te0/3/0.13

Jun 14 22:16:02: %SFF8472-5-THRESHOLD_VIOLATION: Te1/6: Tx power low alarm; Operating value: -40.0 dBm, Threshold value: -12.2 dBm.


sh int Te1/6 transceiver detail 
ITU Channel not available (Wavelength not available),
Transceiver is internally calibrated.
mA: milliamperes, dBm: decibels (milliwatts), NA or N/A: not applicable.
++ : high alarm, +  : high warning, -  : low warning, -- : low alarm.
A2D readouts (if they differ), are reported in parentheses.
The threshold values are calibrated.

                              High Alarm  High Warn  Low Warn   Low Alarm
          Temperature         Threshold   Threshold  Threshold  Threshold
Port       (Celsius)          (Celsius)   (Celsius)  (Celsius)  (Celsius)
--------- ------------------  ----------  ---------  ---------  ---------
Te1/6       31.6                74.0        70.0         0.0       -4.0

                              High Alarm  High Warn  Low Warn   Low Alarm
           Voltage            Threshold   Threshold  Threshold  Threshold
Port       (Volts)            (Volts)     (Volts)    (Volts)    (Volts)
---------  ---------------    ----------  ---------  ---------  ---------
Te1/6      3.22                   N/A         N/A         N/A        N/A

           Optical            High Alarm  High Warn  Low Warn   Low Alarm
           Transmit Power     Threshold   Threshold  Threshold  Threshold
Port       (dBm)              (dBm)       (dBm)      (dBm)      (dBm)
---------  -----------------  ----------  ---------  ---------  ---------
Te1/6        1.0                 4.4         0.4        -8.2      -12.2

           Optical            High Alarm  High Warn  Low Warn   Low Alarm
           Receive Power      Threshold   Threshold  Threshold  Threshold
Port       (dBm)              (dBm)       (dBm)      (dBm)      (dBm)
-------    -----------------  ----------  ---------  ---------  ---------
Te1/6      -22.2                 4.4         0.4       -14.4      -18.4



