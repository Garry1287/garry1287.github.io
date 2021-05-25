---
layout: post
title:  "vpn_nlmk_device"
date:   2015-09-07 21:34:39 +0300
categories: zavod
tags: zavod
---

# vpn_nlmk_device
service password-encryption
service timestamps debug datetime msec localtime
service timestamps log datetime localtime
clock timezone MSK +4 
clock calendar-valid
ntp update-calendar
access-list 61 remark NTP: access-group peer
access-list 61 permit 10.192.10.252
access-list 61 permit 10.192.10.253
access-list 61 deny any
access-list 62 remark NTP: access-group serve-only
access-list 62 permit 10.0.0.0 0.255.255.255
access-list 62 deny any
ntp access-group peer 61
ntp access-group serve-only 62
ntp logging
ntp server 10.192.10.252 prefer
ntp server 10.192.10.253


logging on
logging buffered informational
logging facility local2
logging 10.192.10.253
logging monitor debugging
logging trap notifications
logging origin-id hostname
logging history size 0
logging buffered 32768

do sh run | b access-list

no access-list 57
access-list 57 permit 10.192.10.252
access-list 57 permit 10.192.10.253
access-list 57 permit 10.192.10.190                                                                                                                                                                                                                
access-list 57 deny any                                                                                                                    
snmp-server tftp-server-list 57 

access-list 56 permit 172.19.4.0 0.0.3.255
access-list 56 permit 10.192.10.190                                                                                                                                                                                                                   
access-list 56 deny any
snmp-server community Fv8Ya64PQ RO 56
snmp-server file-transfer access-group 57 protocol tftp
snmp-server contact iptech@sc.ru

snmp-server community Sh73ah91Kld RW 57



access-list 10 permit 10.192.10.0 0.0.0.255
access-list 10 deny   any

no access-list 10
access-list 10 permit 10.192.10.0 0.0.0.255
access-list 10 permit 10.74.254.0 0.0.0.255
access-list 10 deny   any


access-list 23 permit 10.90.19.0 0.0.0.255
access-list 23 permit 10.10.10.0 0.0.0.7
access-list 23 permit 10.192.10.0 0.0.0.255





line vty 0 4
 exec-timeout 480 0
 access-class 10 in
line vty 5 15
 exec-timeout 480 0
 access-class 10 in



 network 10.74.253.8 0.0.0.7 area 0
 network 10.74.254.0 0.0.0.255 area 0










clock timezone MSK 4
logging enable
logging timestamp
logging monitor debugging
logging buffered informational
logging trap notifications
logging asdm informational
logging facility 18
logging device-id hostname
logging host outside 10.192.10.42

snmp-server location Maxi-ASA
snmp-server contact iptech@sc.ru
snmp-server enable traps snmp authentication linkup linkdown coldstart

ntp server 10.192.10.190 source outside prefer
ntp server 10.192.10.252 source prefer 
ntp server 10.192.10.253















logging facility local2
logging 81.20.192.11
logging trap debugging


clock set 15:59:01 6 March 2013


