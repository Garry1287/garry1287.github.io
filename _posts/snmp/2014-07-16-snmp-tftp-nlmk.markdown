---
layout: post
title:  "snmp-tftp-nlmk"
date:   2014-07-16 23:27:09 +0400
categories: snmp
tags: snmp
---

# snmp-tftp-nlmk
access-list 55 permit 10.192.10.252
access-list 55 permit 10.192.10.253
access-list 55 permit 10.192.10.190                                                                                                                                                                                                                
access-list 55 deny any                                                                                                                    
snmp-server tftp-server-list 55 

access-list 56 permit 172.19.4.0 0.0.3.255
access-list 56 permit 10.192.10.190                                                                                                                                                                                                                   
access-list 56 deny any
snmp-server community Fv8Ya64PQ RO 56




snmp-server file-transfer access-group 55 protocol tftp







access-list 57 permit 10.192.10.190
access-list 57 deny   any


access-list 10 permit 10.192.10.0 0.0.0.255
access-list 10 deny   any



line vty 0 4
 access-class 10 in
line vty 5 15
 access-class 10 in






!

snmp ifmib ifindex persist
!
















snmp-server host outside 10.192.10.190 community Udgl48dS
snmp-server location Vienna
snmp-server contact iptech@sc.ru
snmp-server community Udgl48dS
snmp-server enable traps snmp authentication linkup linkdown coldstart
