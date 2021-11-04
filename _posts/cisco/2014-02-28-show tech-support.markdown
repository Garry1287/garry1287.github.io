---
layout: post
title:  "Вывод tech-support на cisco ASR"
date:   2014-02-28 13:19:04 +0400
categories: cisco
tags: cisco
---

# Show tech-support
```
CTD-C5# show tech-support 

------------------ show clock ------------------


14:54:05.541 MSK Wed Oct 1 2014

------------------ show version ------------------

Cisco IOS Software, IOS-XE Software (PPC_LINUX_IOSD-ADVIPSERVICES-M), Version 15.1(1)S, RELEASE SOFTWARE (fc1)
Technical Support: [http://www.cisco.com/techsupport](http://www.cisco.com/techsupport)
Copyright (c) 1986-2010 by Cisco Systems, Inc.
Compiled Mon 22-Nov-10 12:19 by mcpre


Cisco IOS-XE software, Copyright (c) 2005-2010 by cisco Systems, Inc.
All rights reserved.  Certain components of Cisco IOS-XE software are
licensed under the GNU General Public License ("GPL") Version 2.0.  The
software code licensed under GPL Version 2.0 is free software that comes
with ABSOLUTELY NO WARRANTY.  You can redistribute and/or modify such
GPL code under the terms of GPL Version 2.0.  For more details, see the
documentation or "License Notice" file accompanying the IOS-XE software,
or the applicable URL provided on the flyer accompanying the IOS-XE
software.


ROM: IOS-XE ROMMON

CTD-C5 uptime is 7 weeks, 3 days, 6 hours, 22 minutes
Uptime for this control processor is 7 weeks, 3 days, 6 hours, 25 minutes
System returned to ROM by reload at 11:02:21 MSK Wed Nov 20 2013
System restarted at 08:31:14 MSK Sun Aug 10 2014
System image file is "bootflash:/asr1000rp1-advipservices.03.02.00.S.151-1.S.bin"
Last reload reason: PowerOn


cisco ASR1004 (RP1) processor with 1719831K/6147K bytes of memory.
8 Gigabit Ethernet interfaces
2 Ten Gigabit Ethernet interfaces
32768K bytes of non-volatile configuration memory.
4194304K bytes of physical memory.
937983K bytes of eUSB flash at bootflash:.
39004543K bytes of SATA hard disk at harddisk:.

Configuration register is 0x2102


------------------ show running-config ------------------


Building configuration...

Current configuration : 15272 bytes
!
! Last configuration change at 15:02:46 MSK Thu Sep 18 2014 by garry
! NVRAM config last updated at 15:02:47 MSK Thu Sep 18 2014 by garry
!
version 15.1
service timestamps debug datetime msec localtime
service timestamps log datetime localtime
no platform punt-keepalive disable-kernel-core
!
hostname CTD-C5
!
boot-start-marker
boot-end-marker
!
!
vrf definition Mgmt-intf
 !
 address-family ipv4
 exit-address-family
 !
 address-family ipv6
 exit-address-family
!
logging buffered 32768
enable secret 4 NMb8u8AOiG3HvyEDXrwmXrVG3a.pM7rX0A9AWdAbrhk
!
aaa new-model
aaa session-mib disconnect
!
!
aaa authentication login default local
aaa authorization exec default local 
!
!
!
!
!
aaa session-id unique
!
!
!
clock timezone MSK 4 0
ip source-route
!
!
!
no ip domain lookup
ip domain name ctd-c5.sc.ru
ip name-server 81.20.192.16
ip name-server 81.20.192.17
no ip dhcp relay information check
ip dhcp excluded-address 10.254.0.1
!
!
!
!
!
multilink bundle-name authenticated
!
!
!
!
!
!
!
!
username garry secret 4 <removed>
username smithy secret 4 <removed>
username gold_555 secret 4 <removed>
!
redundancy
 mode none
!
!
!
ip tcp path-mtu-discovery
ip tftp source-interface GigabitEthernet0
!
class-map match-any RETN-Policy
 match any 
!
policy-map RETN-Policy
 class RETN-Policy
  police cir 600000000 bc 112800000 be 225600000
policy-map Anders-Policy
 class RETN-Policy
  police cir 100000000 bc 19000000 be 38000000
policy-map BIGTELECOM-Policy-300
 class RETN-Policy
  police cir 307200000 bc 57600000 be 115200000
policy-map RETN-Policy-400
 class RETN-Policy
  police cir 512000000 bc 9960000 be 19320000
policy-map RETN-Policy-750
 class RETN-Policy
  police cir 768000000 bc 144000000 be 288000000
policy-map BEELINE-Policy-500
 class RETN-Policy
  police cir 512000000 bc 9600000 be 19200000
policy-map RETN-Policy-1000
 class RETN-Policy
  police cir 1024000000 bc 19200000 be 38400000
policy-map RETN-Policy-800
 class RETN-Policy
  police cir 819200000 bc 15360000 be 30720000
!
!
!
!
!
interface Loopback0
 description # Interface for Tunnel endpoint, IP/MPLS and BGP exchanges
 ip address 81.20.192.75 255.255.255.255
!
interface Port-channel3
 description #CTD-S6 Po3 802.1q INET
 no ip address
 ip flow ingress
 load-interval 30
 shutdown
 negotiation auto
!
interface Port-channel3.13
 description OSPF-link 120 #pheonix 20.05.2011
 encapsulation dot1Q 13
 ip flow ingress
 ip flow egress
 ip ospf priority 50
 ip ospf mtu-ignore
 shutdown
!
interface GigabitEthernet0/0/0
 no ip address
 shutdown
 negotiation auto
!
interface GigabitEthernet0/0/1
 description CTD-S6 Gi2/18 RETN-3kanal
 no ip address
 ip flow ingress
 ip route-cache policy
 load-interval 30
 negotiation auto
!
interface GigabitEthernet0/0/2
 description CTD-S6 Gi2/9 (Po3) INET
 no ip address
 ip flow ingress
 load-interval 30
 negotiation auto
 channel-group 3 mode passive
!
interface GigabitEthernet0/0/3
 description CTD-S6 Gi2/13 (Po3) INET
 no ip address
 ip flow ingress
 load-interval 30
 negotiation auto
 channel-group 3 mode passive
!
interface GigabitEthernet0/0/4
 description CTD-S6 Gi2/15 (Po3) INET
 no ip address
 ip flow ingress
 load-interval 30
 negotiation auto
 channel-group 3 mode passive
!
interface GigabitEthernet0/0/5
 description #RETN-INTERNET1 Uplink
 ip address 87.245.241.134 255.255.255.252
 ip flow ingress
 ip flow egress
 load-interval 30
 shutdown
 negotiation auto
 service-policy input RETN-Policy-1000
 service-policy output RETN-Policy-1000
!
interface GigabitEthernet0/0/6
 description #CTD-S6 Gi2/17 RETN-INET-2kanal
 ip address 87.245.241.146 255.255.255.252
 ip flow ingress
 ip flow egress
 load-interval 30
 shutdown
 negotiation auto
 service-policy input RETN-Policy-1000
 service-policy output RETN-Policy-1000
!
interface GigabitEthernet0/0/7
 description #BEELINE-INTERNET Uplink
 ip address 87.229.223.118 255.255.255.252
 ip flow ingress
 ip flow egress
 load-interval 30
 negotiation auto
 service-policy input RETN-Policy-1000
 service-policy output RETN-Policy-1000
!
interface TenGigabitEthernet0/3/0
 description #to Catalyst4900
 no ip address
 ip flow ingress
 load-interval 30
!
interface TenGigabitEthernet0/3/0.13
 description #OSPF-link
 encapsulation dot1Q 13
 ip address 81.20.192.52 255.255.255.240
 ip flow ingress
 ip flow egress
 ip ospf priority 50
 ip ospf mtu-ignore
!
interface TenGigabitEthernet0/3/0.1042
 description #Bigtelecom
 bandwidth 307200
 encapsulation dot1Q 1042
 ip address 81.20.192.149 255.255.255.252
 ip flow ingress
 ip flow egress
 shutdown
 service-policy input BIGTELECOM-Policy-300
 service-policy output BIGTELECOM-Policy-300
!
interface TenGigabitEthernet1/3/0
 description #Megafon
 ip address 78.25.66.222 255.255.255.252
 ip flow ingress
 ip flow egress
 load-interval 30
!
interface GigabitEthernet0
 description #mngt27 to CTD-S0 Fa0/8
 vrf forwarding Mgmt-intf
 ip address 192.168.121.31 255.255.255.0
 negotiation auto
!
router ospf 110
 router-id 81.20.192.52
 redistribute connected metric 1 metric-type 1 subnets
 redistribute static metric 1 metric-type 1 subnets
 passive-interface default
 no passive-interface TenGigabitEthernet0/3/0.13
 no passive-interface Port-channel3.13
 network 81.20.192.48 0.0.0.15 area 0
 default-information originate
 distribute-list prefix no-sc-local-distribution out
!
router bgp 20866
 bgp log-neighbor-changes
 no bgp default ipv4-unicast
 neighbor 78.25.66.221 remote-as 31133
 neighbor 78.25.66.221 update-source TenGigabitEthernet1/3/0
 neighbor 81.20.192.78 remote-as 20866
 neighbor 81.20.192.78 update-source Loopback0
 neighbor 81.20.192.79 remote-as 20866
 neighbor 81.20.192.79 update-source Loopback0
 neighbor 81.20.192.150 remote-as 196770
 neighbor 81.20.192.150 update-source TenGigabitEthernet0/3/0.1042
 neighbor 87.229.223.117 remote-as 3216
 neighbor 87.229.223.117 update-source GigabitEthernet0/0/7
 neighbor 87.245.241.133 remote-as 9002
 neighbor 87.245.241.133 shutdown
 neighbor 87.245.241.133 update-source GigabitEthernet0/0/5
 neighbor 87.245.241.145 remote-as 9002
 neighbor 87.245.241.145 shutdown
 neighbor 87.245.241.145 update-source GigabitEthernet0/0/6
 !
 address-family ipv4
  network 81.20.192.0 mask 255.255.254.0
  network 81.20.195.0 mask 255.255.255.0
  network 81.20.196.0 mask 255.255.252.0
  network 81.20.200.0 mask 255.255.248.0
  network 81.20.200.0 mask 255.255.252.0
  network 81.20.204.0 mask 255.255.252.0
  redistribute connected
  neighbor 78.25.66.221 activate
  neighbor 78.25.66.221 prefix-list deny_lesnets_from_uplinks in
  neighbor 78.25.66.221 prefix-list adv-to-megafon out
  neighbor 81.20.192.78 activate
  neighbor 81.20.192.79 activate
  neighbor 81.20.192.150 activate
  neighbor 81.20.192.150 default-originate
  neighbor 81.20.192.150 prefix-list bigtelecom_net in
  neighbor 81.20.192.150 prefix-list deny_lesnets_from_uplinks out
  maximum-paths 2
  maximum-paths ibgp 2
 exit-address-family
!
!
ip bgp-community new-format
no ip http server
!
!
ip prefix-list adv-to-beeline seq 5 permit 81.20.192.0/20 le 24
ip prefix-list adv-to-beeline seq 10 permit 193.104.11.0/24 le 32
ip prefix-list adv-to-beeline seq 35 deny 0.0.0.0/0 le 32
!
ip prefix-list adv-to-beeline2 seq 5 permit 81.20.192.0/23 le 24
ip prefix-list adv-to-beeline2 seq 10 permit 81.20.194.0/24
ip prefix-list adv-to-beeline2 seq 15 permit 81.20.195.0/24
ip prefix-list adv-to-beeline2 seq 20 permit 81.20.196.0/22 le 24
ip prefix-list adv-to-beeline2 seq 30 permit 193.104.11.0/24 le 32
ip prefix-list adv-to-beeline2 seq 35 deny 0.0.0.0/0 le 32
!
ip prefix-list adv-to-megafon seq 5 permit 81.20.192.0/20 le 24
ip prefix-list adv-to-megafon seq 10 permit 193.104.11.0/24 le 32
ip prefix-list adv-to-megafon seq 20 permit 194.0.68.0/22 le 32
ip prefix-list adv-to-megafon seq 100 deny 0.0.0.0/0 le 32
!
ip prefix-list adv-to-retn seq 5 permit 81.20.192.0/20 le 24
ip prefix-list adv-to-retn seq 35 deny 0.0.0.0/0 le 32
!
ip prefix-list allow-les-only seq 5 permit 195.34.224.0/19 le 21
ip prefix-list allow-les-only seq 15 permit 172.24.0.0/14
ip prefix-list allow-les-only seq 20 permit 178.234.0.0/16 le 21
ip prefix-list allow-les-only seq 30 permit 95.179.0.0/17 le 21
ip prefix-list allow-les-only seq 100 deny 0.0.0.0/0 le 32
!
ip prefix-list bgp2ospf seq 5 permit 195.34.224.0/19 le 21
ip prefix-list bgp2ospf seq 10 permit 85.90.108.0/22
ip prefix-list bgp2ospf seq 15 permit 172.24.0.0/14
ip prefix-list bgp2ospf seq 20 permit 178.234.0.0/16 le 21
ip prefix-list bgp2ospf seq 25 permit 89.21.150.0/23
ip prefix-list bgp2ospf seq 45 permit 193.104.11.0/24 le 32
ip prefix-list bgp2ospf seq 90 permit 93.180.0.0/18 le 21
ip prefix-list bgp2ospf seq 100 deny 0.0.0.0/0 le 32
!
ip prefix-list bigtelecom_net seq 10 permit 194.0.68.0/22 le 32
ip prefix-list bigtelecom_net seq 50 deny 0.0.0.0/0 le 32
!
ip prefix-list deny-199-only seq 5 deny 81.20.199.240/29
ip prefix-list deny-199-only seq 100 permit 0.0.0.0/0 le 32
!
ip prefix-list deny_lesnets_from_uplinks seq 10 deny 195.34.224.0/19 ge 20
ip prefix-list deny_lesnets_from_uplinks seq 12 deny 95.179.0.0/17 le 21
ip prefix-list deny_lesnets_from_uplinks seq 13 deny 178.234.0.0/16 le 21
ip prefix-list deny_lesnets_from_uplinks seq 50 permit 0.0.0.0/0 le 32
!
ip prefix-list no-10-net seq 1 deny 10.0.0.0/8 le 32
ip prefix-list no-10-net seq 10 permit 0.0.0.0/0 le 32
!
ip prefix-list no-sc-local-distribution seq 1 permit 10.254.0.0/16 le 32
ip prefix-list no-sc-local-distribution seq 2 deny 10.0.0.0/8 le 32
ip prefix-list no-sc-local-distribution seq 5 permit 172.20.0.0/16 le 32
ip prefix-list no-sc-local-distribution seq 6 permit 172.31.3.0/24 le 32
ip prefix-list no-sc-local-distribution seq 7 permit 192.168.90.0/30
ip prefix-list no-sc-local-distribution seq 10 deny 172.16.0.0/12 le 32
ip prefix-list no-sc-local-distribution seq 20 deny 192.168.0.0/16 le 32
ip prefix-list no-sc-local-distribution seq 50 permit 0.0.0.0/0 le 32
!
ip prefix-list no-sc-local-sb-distribution seq 2 deny 81.20.192.240/29 le 32
ip prefix-list no-sc-local-sb-distribution seq 3 deny 81.20.192.64/26 le 32
ip prefix-list no-sc-local-sb-distribution seq 4 deny 10.0.0.0/16 le 32
ip prefix-list no-sc-local-sb-distribution seq 5 deny 172.20.0.0/14 le 32
ip prefix-list no-sc-local-sb-distribution seq 6 deny 172.31.3.0/24 le 32
ip prefix-list no-sc-local-sb-distribution seq 9 permit 81.20.192.48/28 le 32
ip prefix-list no-sc-local-sb-distribution seq 10 permit 0.0.0.0/0 le 32
logging esm config
logging history size 0
logging trap notifications
logging origin-id hostname
logging facility local3
logging source-interface Loopback0
logging 192.168.121.26
logging 81.20.196.53
access-list 10 permit 81.20.192.0 0.0.0.255
access-list 10 permit 192.168.121.0 0.0.0.255
access-list 10 permit 192.168.113.0 0.0.0.255
access-list 10 permit 192.168.1.0 0.0.0.255
access-list 10 deny   any
access-list 57 permit 192.168.121.1
access-list 57 permit 192.168.113.1
access-list 57 permit 81.20.192.0 0.0.0.127
access-list 57 permit 192.168.1.0 0.0.0.255
access-list 57 deny   any
access-list 61 remark NTP: access-group peer
access-list 61 permit 81.20.196.53
access-list 61 permit 81.20.196.54
access-list 61 deny   any
access-list 62 remark NTP: access-group serve-only
access-list 62 permit 192.168.0.0 0.0.255.255
access-list 62 permit 172.20.0.0 0.0.255.255
access-list 62 permit 81.20.192.0 0.0.15.255
access-list 62 deny   any
access-list 101 permit ip 172.20.96.0 0.0.31.255 172.16.0.0 0.15.255.255
access-list 101 permit ip 172.20.96.0 0.0.31.255 81.20.192.0 0.0.15.255
access-list 101 permit ip 172.20.96.0 0.0.31.255 195.34.224.0 0.0.31.255
access-list 101 permit ip 172.20.96.0 0.0.31.255 95.128.0.0 0.127.255.255
access-list 101 permit ip 172.20.96.0 0.0.31.255 93.180.0.0 0.0.63.255
access-list 101 deny   ip any any
access-list 102 permit ip 172.16.0.0 0.15.255.255 172.20.96.0 0.0.31.255
access-list 102 permit ip 81.20.192.0 0.0.15.255 172.20.96.0 0.0.31.255
access-list 102 permit ip 195.34.224.0 0.0.31.255 172.20.96.0 0.0.31.255
access-list 102 permit ip 95.128.0.0 0.127.255.255 172.20.96.0 0.0.31.255
access-list 102 permit ip 93.180.0.0 0.0.63.255 172.20.96.0 0.0.31.255
access-list 102 deny   ip any any
!
route-map prep-out-beeline permit 10
 set as-path prepend 20866 20866 20866 20866 20866 20866 20866 20866 20866 20866
!
route-map setcommunity-beeline-m9 permit 10
 set community 3216:5000 3216:5010 3216:5020 3216:5040 3216:5060 3216:5070 3216:5090 3216:5100 3216:5110 3216:5120 3216:5130 3216:5140 3216:5200 3216:5210 3216:5220 3216:5240 3216:5250 3216:5260 3216:5270 3216:5280 3216:5290 3216:5310 3216:5330 3216:5340
!
route-map deny-199-only permit 10
 match ip address prefix-list deny-199-only
!
route-map bgp2ospf permit 10
 match ip address prefix-list bgza bgp2ospf
!
route-map deny-199-onlyddd permit 10
!
route-map rm-adv-to-retn deny 10
 description # Do not advertise LES prefix to Retn
 match ip address prefix-list allow-les-only
!
route-map rm-adv-to-retn permit 60
 match ip address prefix-list adv-to-retn
!
route-map setcommunity-bee1000 permit 10
 set community 3216:5000 3216:5010 3216:5020 3216:5040 3216:5054 3216:5064 3216:5074 3216:5090 3216:5100 3216:5110 3216:5120 3216:5130 3216:5140 3216:5204 3216:5214 3216:5220 3216:5234 3216:5244 3216:5254 3216:5264 3216:5274 3216:5284 3216:5296 3216:5304
!
route-map setcommunity-bee750 permit 10
 set community 3216:5000 3216:5010 3216:5020 3216:5040 3216:5054 3216:5064 3216:5074 3216:5090 3216:5100 3216:5110 3216:5120 3216:5130 3216:5140 3216:5204 3216:5210 3216:5220 3216:5234 3216:5244 3216:5254 3216:5264 3216:5274 3216:5284 3216:5290 3216:5304
!
route-map setcommunity-beeline-5xx0 permit 10
 set as-path prepend 20866 20866 20866 20866 20866 20866 20866 20866 20866 20866
 set community 3216:5000 3216:5010 3216:5020 3216:5040 3216:5050 3216:5060 3216:5070 3216:5090 3216:5100 3216:5110 3216:5120 3216:5130 3216:5140 3216:5200 3216:5210 3216:5220 3216:5230 3216:5240 3216:5250 3216:5260 3216:5270 3216:5280 3216:5290 3216:5300
!
route-map dist_bras_int permit 10
 match ip address 32
!
route-map setcommunity-beeline-5xx6 permit 10
 set as-path prepend 20866 20866 20866 20866 20866 20866 20866 20866 20866 20866
 set community 3216:5006 3216:5016 3216:5026 3216:5046 3216:5056 3216:5066 3216:5076 3216:5096 3216:5106 3216:5116 3216:5126 3216:5136 3216:5146 3216:5206 3216:5216 3216:5226 3216:5236 3216:5246 3216:5256 3216:5266 3216:5276 3216:5286 3216:5296 3216:5306
!
snmp-server community <removed> RO 57
snmp-server community <removed> RW 57
snmp-server location CTD-C5
snmp-server enable traps snmp authentication linkdown linkup coldstart warmstart
snmp-server enable traps tty
snmp-server enable traps bgp
snmp-server enable traps mpls ldp
snmp-server enable traps mpls traffic-eng
snmp-server enable traps entity
snmp-server enable traps mpls vpn
snmp-server host 192.168.121.1 version 2c <removed> 
snmp-server host 81.20.192.19 version 2c <removed> 
snmp ifmib ifindex persist
!
!
!
control-plane
!
!
!
!
!
line con 0
 stopbits 1
line aux 0
 stopbits 1
line vty 0 4
 access-class 10 in vrf-also
 exec-timeout 480 0
line vty 5 15
 access-class 10 in vrf-also
 exec-timeout 480 0
!
ntp logging
ntp clock-period 17321455
ntp access-group peer 61
ntp access-group serve-only 62
ntp server 81.20.196.53 prefer
ntp server 81.20.196.54
end


------------------ show redundancy history ------------------

00:00:22 client added: Redundancy Mode RF(29) seq=60

00:00:22 client added: IfIndex(139) seq=61

00:00:22 client added: CHKPT RF(25) seq=68

00:00:22 client added: ASR1000-RP Platform RF(1340) seq=101

00:00:22 client added: Cat6k CWAN HA(1501) seq=102

00:00:22 client added: Network RF Client(22) seq=109

00:00:22 client added: Cat6k SPA TSM(1505) seq=115

00:00:22 client added: ASR1000-RP SBC RF(1344) seq=126

00:00:22 client added: SBC-RF RF Client(227) seq=127

00:00:22 client added: XDR RRP RF Client(71) seq=134

00:00:22 client added: CEF RRP RF Client(24) seq=135

00:00:22 client added: MFIB RRP RF Client(306) seq=144

00:00:22 client added: Cat6k CWAN Interface Events(1504) seq=151

00:00:22 client added: RFS RF(520) seq=156

00:00:22 client added: Config Sync RF client(5) seq=158

00:00:22 client added: DHCPC(100) seq=202

00:00:22 client added: DHCPD(101) seq=203

00:00:22 client added: SNMP RF Client(34) seq=215

00:00:22 client added: CWAN APS HA RF Client(1502) seq=216

00:00:22 client added: History RF Client(35) seq=226

00:00:22 client added: ARP(57) seq=257

00:00:22 client added: ASR1000 SpaFlow(1342) seq=275

00:00:22 client added: ASR1000 IF Flow(1343) seq=276

00:00:22 client added: IOS STILE RF Client(1111) seq=277

00:00:22 client added: MQC QoS(102) seq=310

00:00:22 client added: IP Tunnel RF(151) seq=318

00:00:22 client added: Config Verify RF client(94) seq=319

00:00:22 client added: DHCPv6 Relay(148) seq=337

00:00:22 client added: ISSU Test Client(4005) seq=346

00:00:22 client added: Network RF 2 Client(93) seq=350

00:00:22 client added: FEC Client(205) seq=352

00:00:22 client added: DATA DESCRIPTOR RF CLIENT(141) seq=360

00:00:22 client added: IOS Config ARCHIVE(4020) seq=389

00:00:22 client added: IOS Config ROLLBACK(4021) seq=390

00:00:24 *my state = INITIALIZATION(2) peer state = DISABLED(1)

00:00:24 RF_PROG_INITIALIZATION(100) First Client(0) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) Slave(3) op=0 rc=23

00:00:24 RF_PROG_INITIALIZATION(100) Redundancy Mode RF(29) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) IfIndex(139) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) CHKPT RF(25) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) ASR1000-RP Platform RF(1340) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) Cat6k CWAN HA(1501) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) Network RF Client(22) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) Cat6k SPA TSM(1505) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) ASR1000-RP SBC RF(1344) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) SBC-RF RF Client(227) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) XDR RRP RF Client(71) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) CEF RRP RF Client(24) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) MFIB RRP RF Client(306) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) Cat6k CWAN Interface Events(1504) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) RFS RF(520) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) Config Sync RF client(5) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) DHCPC(100) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) DHCPD(101) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) SNMP RF Client(34) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) CWAN APS HA RF Client(1502) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) History RF Client(35) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) ARP(57) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) ASR1000 SpaFlow(1342) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) ASR1000 IF Flow(1343) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) IOS STILE RF Client(1111) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) MQC QoS(102) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) IP Tunnel RF(151) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) Config Verify RF client(94) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) DHCPv6 Relay(148) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) ISSU Test Client(4005) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) Network RF 2 Client(93) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) FEC Client(205) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) DATA DESCRIPTOR RF CLIENT(141) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) IOS Config ARCHIVE(4020) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) IOS Config ROLLBACK(4021) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) Slave(3) op=0 rc=11

00:00:24 RF_PROG_INITIALIZATION(100) Last Client(65000) op=0 rc=11

00:00:24 *my state = NEGOTIATION(3) peer state = DISABLED(1)

00:00:24 RF_REGISTRATION_STATUS(407) Cat6k CWAN HA(1501) op=0 rc=0

00:00:24 RF_REGISTRATION_STATUS(407) Cat6k CWAN Interface Events(1504) op=0 rc=0

00:00:24 RF_REGISTRATION_STATUS(407) CWAN APS HA RF Client(1502) op=0 rc=0

00:00:24 RF_EVENT_GO_ACTIVE(512) op=0 rc=0

00:00:24 *my state = ACTIVE-FAST(9) peer state = DISABLED(1)

00:00:24 RF_PROG_ACTIVE_FAST(200) First Client(0) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) Slave(3) op=0 rc=23

00:00:24 RF_PROG_ACTIVE_FAST(200) Redundancy Mode RF(29) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) IfIndex(139) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) CHKPT RF(25) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) ASR1000-RP Platform RF(1340) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) Cat6k CWAN HA(1501) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) Network RF Client(22) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) Cat6k SPA TSM(1505) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) ASR1000-RP SBC RF(1344) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) SBC-RF RF Client(227) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) XDR RRP RF Client(71) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) CEF RRP RF Client(24) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) MFIB RRP RF Client(306) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) Cat6k CWAN Interface Events(1504) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) RFS RF(520) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) Config Sync RF client(5) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) DHCPC(100) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) DHCPD(101) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) SNMP RF Client(34) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) CWAN APS HA RF Client(1502) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) History RF Client(35) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) ARP(57) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) ASR1000 SpaFlow(1342) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) ASR1000 IF Flow(1343) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) IOS STILE RF Client(1111) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) MQC QoS(102) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) IP Tunnel RF(151) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) Config Verify RF client(94) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) DHCPv6 Relay(148) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) ISSU Test Client(4005) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) Network RF 2 Client(93) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) FEC Client(205) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) DATA DESCRIPTOR RF CLIENT(141) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) IOS Config ARCHIVE(4020) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) IOS Config ROLLBACK(4021) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) Slave(3) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_FAST(200) Last Client(65000) op=0 rc=11

00:00:24 *my state = ACTIVE-DRAIN(10) peer state = DISABLED(1)

00:00:24 RF_PROG_ACTIVE_DRAIN(201) First Client(0) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) Slave(3) op=0 rc=23

00:00:24 RF_PROG_ACTIVE_DRAIN(201) Redundancy Mode RF(29) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) IfIndex(139) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) CHKPT RF(25) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) ASR1000-RP Platform RF(1340) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) Cat6k CWAN HA(1501) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) Network RF Client(22) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) Cat6k SPA TSM(1505) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) ASR1000-RP SBC RF(1344) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) SBC-RF RF Client(227) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) XDR RRP RF Client(71) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) CEF RRP RF Client(24) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) MFIB RRP RF Client(306) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) Cat6k CWAN Interface Events(1504) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) RFS RF(520) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) Config Sync RF client(5) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) DHCPC(100) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) DHCPD(101) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) SNMP RF Client(34) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) CWAN APS HA RF Client(1502) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) History RF Client(35) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) ARP(57) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) ASR1000 SpaFlow(1342) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) ASR1000 IF Flow(1343) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) IOS STILE RF Client(1111) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) MQC QoS(102) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) IP Tunnel RF(151) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) Config Verify RF client(94) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) DHCPv6 Relay(148) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) ISSU Test Client(4005) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) Network RF 2 Client(93) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) FEC Client(205) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) DATA DESCRIPTOR RF CLIENT(141) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) IOS Config ARCHIVE(4020) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) IOS Config ROLLBACK(4021) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) Slave(3) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_DRAIN(201) Last Client(65000) op=0 rc=11

00:00:24 *my state = ACTIVE_PRECONFIG(11) peer state = DISABLED(1)

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) First Client(0) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) Slave(3) op=0 rc=23

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) Redundancy Mode RF(29) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) IfIndex(139) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) CHKPT RF(25) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) ASR1000-RP Platform RF(1340) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) Cat6k CWAN HA(1501) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) Network RF Client(22) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) Cat6k SPA TSM(1505) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) ASR1000-RP SBC RF(1344) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) SBC-RF RF Client(227) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) XDR RRP RF Client(71) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) CEF RRP RF Client(24) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) MFIB RRP RF Client(306) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) Cat6k CWAN Interface Events(1504) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) RFS RF(520) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) Config Sync RF client(5) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) DHCPC(100) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) DHCPD(101) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) SNMP RF Client(34) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) CWAN APS HA RF Client(1502) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) History RF Client(35) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) ARP(57) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) ASR1000 SpaFlow(1342) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) ASR1000 IF Flow(1343) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) IOS STILE RF Client(1111) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) MQC QoS(102) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) IP Tunnel RF(151) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) Config Verify RF client(94) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) DHCPv6 Relay(148) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) ISSU Test Client(4005) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) Network RF 2 Client(93) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) FEC Client(205) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) DATA DESCRIPTOR RF CLIENT(141) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) IOS Config ARCHIVE(4020) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) IOS Config ROLLBACK(4021) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) Slave(3) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_PRECONFIG(202) Last Client(65000) op=0 rc=11

00:00:24 *my state = ACTIVE_POSTCONFIG(12) peer state = DISABLED(1)

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) First Client(0) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) Slave(3) op=0 rc=23

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) Redundancy Mode RF(29) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) IfIndex(139) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) CHKPT RF(25) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) ASR1000-RP Platform RF(1340) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) Cat6k CWAN HA(1501) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) Network RF Client(22) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) Cat6k SPA TSM(1505) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) ASR1000-RP SBC RF(1344) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) SBC-RF RF Client(227) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) XDR RRP RF Client(71) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) CEF RRP RF Client(24) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) MFIB RRP RF Client(306) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) Cat6k CWAN Interface Events(1504) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) RFS RF(520) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) Config Sync RF client(5) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) DHCPC(100) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) DHCPD(101) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) SNMP RF Client(34) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) CWAN APS HA RF Client(1502) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) History RF Client(35) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) ARP(57) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) ASR1000 SpaFlow(1342) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) ASR1000 IF Flow(1343) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) IOS STILE RF Client(1111) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) MQC QoS(102) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) IP Tunnel RF(151) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) Config Verify RF client(94) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) DHCPv6 Relay(148) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) ISSU Test Client(4005) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) Network RF 2 Client(93) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) FEC Client(205) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) DATA DESCRIPTOR RF CLIENT(141) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) IOS Config ARCHIVE(4020) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) IOS Config ROLLBACK(4021) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) Slave(3) op=0 rc=11

00:00:24 RF_PROG_ACTIVE_POSTCONFIG(203) Last Client(65000) op=0 rc=11

00:00:24 *my state = ACTIVE(13) peer state = DISABLED(1)

00:00:24 RF_PROG_ACTIVE(204) First Client(0) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) Slave(3) op=0 rc=23

00:00:24 RF_PROG_ACTIVE(204) Redundancy Mode RF(29) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) IfIndex(139) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) CHKPT RF(25) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) ASR1000-RP Platform RF(1340) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) Cat6k CWAN HA(1501) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) Network RF Client(22) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) Cat6k SPA TSM(1505) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) ASR1000-RP SBC RF(1344) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) SBC-RF RF Client(227) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) XDR RRP RF Client(71) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) CEF RRP RF Client(24) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) MFIB RRP RF Client(306) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) Cat6k CWAN Interface Events(1504) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) RFS RF(520) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) Config Sync RF client(5) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) DHCPC(100) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) DHCPD(101) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) SNMP RF Client(34) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) CWAN APS HA RF Client(1502) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) History RF Client(35) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) ARP(57) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) ASR1000 SpaFlow(1342) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) ASR1000 IF Flow(1343) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) IOS STILE RF Client(1111) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) MQC QoS(102) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) IP Tunnel RF(151) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) Config Verify RF client(94) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) DHCPv6 Relay(148) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) ISSU Test Client(4005) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) Network RF 2 Client(93) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) FEC Client(205) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) DATA DESCRIPTOR RF CLIENT(141) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) IOS Config ARCHIVE(4020) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) IOS Config ROLLBACK(4021) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) Slave(3) op=0 rc=11

00:00:24 RF_PROG_ACTIVE(204) Last Client(65000) op=0 rc=11

00:00:26 client added: ASR1000 DPIDX(1341) seq=114

00:00:26 client added: Network Clock(4006) seq=364

00:00:26 client added: CCM RF(82) seq=225

00:00:26 client added: L2TP(118) seq=223

00:00:26 client added: Multicast ISSU Consolidation RF(305) seq=107

00:00:26 client added: HDLC(49) seq=178

00:00:26 client added: LSD HA Proc(72) seq=179

00:00:26 client added: IPROUTING NSF RF client(20) seq=200

00:00:26 client added: TPM RF client(402) seq=155

00:00:26 client added: LDP HA(73) seq=255

00:00:26 client added: MPLS VPN HA Client(74) seq=213

00:00:26 client added: MFI STATIC HA Proc(113) seq=180

00:00:26 client added: RSVP HA Services(90) seq=238

00:00:26 client added: TSPTUN HA(78) seq=106

00:00:26 client added: AToM manager(84) seq=293

00:00:26 client added: IPRM(76) seq=256

00:00:26 client added: XC L2TP HA manager(119) seq=224

00:00:26 client added: ETHERNET LMI RF(202) seq=190

00:00:26 client added: ETHERNET OAM RF(200) seq=187

00:00:26 client added: ECFM RF(207) seq=189

00:00:26 client added: TCP(1601) seq=316

00:00:26 client added: BGP(1602) seq=317

00:00:26 client added: Tableid HA(75) seq=125

00:00:26 client added: AAA(69) seq=221

00:00:26 client added: AC RF Client(83) seq=291

00:00:26 client added: ATM(52) seq=217

00:00:26 client added: BFD RF Client(146) seq=137

00:00:26 client added: Frame Relay(23) seq=177

00:00:26 client added: GLBP(114) seq=111

00:00:26 client added: HSRP(88) seq=110

00:00:26 client added: MRIB RP RF Client(301) seq=140

00:00:26 client added: NAT HA(401) seq=153

00:00:26 client added: NAT64 HA(404) seq=154

00:00:26 client added: Netsync RF Client(403) seq=420

00:00:26 client added: SSM(85) seq=294

00:00:26 client added: VRRP(225) seq=112

00:00:26 client added: Virtual Template RF Client(68) seq=174

00:00:26 client added: LACP(226) seq=193

00:00:26 client added: IP multicast RF Client(304) seq=108

00:00:26 client added: VOIP RF CLIENT(1345) seq=128

00:00:26 client added: SNMP HA RF Client(54) seq=254

00:00:26 client added: Call-Home RF(1510) seq=312

00:00:26 client added: EEM Server RF CLIENT(250) seq=250

00:00:26 client added: EEM POLICY-DIR RF CLIENT(252) seq=252

00:00:26 client added: FH_RF_Event_Detector_stub(50) seq=264

00:00:34 System initialization complete




------------------ show redundancy states ------------------

       my state = 13 -ACTIVE 
     peer state = 1  -DISABLED 
           Mode = Simplex
           Unit = Primary
        Unit ID = 48

Redundancy Mode (Operational) = Non-redundant
Redundancy Mode (Configured)  = Non-redundant
Redundancy State              = Non Redundant
    Manual Swact = disabled (system is simplex (no peer unit))
 Communications = Down      Reason: Simplex mode

   client count = 79
 client_notification_TMR = 30000 milliseconds
           RF debug mask = 0x0   


------------------ show redundancy switchover history ------------------



------------------ show stacks ------------------


Minimum process stacks:
 Free/Size   Name
11416/12000  ISSU Infra API Delayed Registration Process
11432/12000  CDP BLOB
23400/24000  MFIB RP IPC
22984/24000  MRIB IPv6 Init Process
23240/24000  MRIB IPv4 Init Process
 6696/12000  MGMT VRF Process
 7976/12000  ASR1000 LIIN config
11432/12000  Inspect Init Msg
11416/12000  SPAN Subsystem
11276/12000  LACP Protocol
118552/120000  EEM Auto Registration Proc
11432/12000  SASL MAIN
23000/24000  Router Init
119208/120000  script background loader
 9560/12000  IPC ISSU Versioning Process
 9336/12000  IPC ISSU Receive Process
10680/12000  RTTY Client Registration
11224/12000  RADIUS INITCONFIG
14440/24000  Init
10744/12000  BGP Open
11432/12000  IP SLAs Deferred Schedule Processor
 5160/6000   Rom Random Update Process
11384/12000  URPF stats
142312/144000  TCP Command
11272/12000  BGP Accepter
16952/24000  Virtual Exec

Interrupt level stacks:
Level    Called Unused/Size  Name
  2           0  57392/65536  Network Interrupt
  3           0  52256/65536  Aux Thread

------------------ show interfaces ------------------


GigabitEthernet0/0/0 is administratively down, line protocol is down 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6c00 (bia b414.8901.6c00)
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is unknown media type
  output flow-control is unsupported, input flow-control is unsupported
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 1 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0/0/1 is up, line protocol is up 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6c01 (bia b414.8901.6c01)
  Description: CTD-S6 Gi2/18 RETN-3kanal
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is LX
  output flow-control is on, input flow-control is on
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 00:00:14, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     9121344 packets input, 777967424 bytes, 0 no buffer
     Received 455169 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 714752 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 2 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0/0/2 is down, line protocol is down 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6cc2 (bia b414.8901.6c02)
  Description: CTD-S6 Gi2/9 (Po3) INET
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is SX
  output flow-control is on, input flow-control is on
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 2 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0/0/3 is down, line protocol is down 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6cc2 (bia b414.8901.6c03)
  Description: CTD-S6 Gi2/13 (Po3) INET
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is LX
  output flow-control is on, input flow-control is on
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 2 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0/0/4 is down, line protocol is down 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6cc2 (bia b414.8901.6c04)
  Description: CTD-S6 Gi2/15 (Po3) INET
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is LX
  output flow-control is on, input flow-control is on
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 2 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0/0/5 is administratively down, line protocol is down 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6c05 (bia b414.8901.6c05)
  Description: #RETN-INTERNET1 Uplink
  Internet address is 87.245.241.134/30
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is unknown media type
  output flow-control is unsupported, input flow-control is unsupported
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 1 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0/0/6 is administratively down, line protocol is down 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6c06 (bia b414.8901.6c06)
  Description: #CTD-S6 Gi2/17 RETN-INET-2kanal
  Internet address is 87.245.241.146/30
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is unknown media type
  output flow-control is unsupported, input flow-control is unsupported
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 1 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0/0/7 is down, line protocol is down 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6c07 (bia b414.8901.6c07)
  Description: #BEELINE-INTERNET Uplink
  Internet address is 87.229.223.118/30
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is BX10U
  output flow-control is on, input flow-control is on
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 2 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
TenGigabitEthernet0/3/0 is up, line protocol is up 
  Hardware is SPA-1X10GE-L-V2, address is b414.8901.6c30 (bia b414.8901.6c30)
  Description: #to Catalyst4900
  MTU 1500 bytes, BW 10000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 47/255, rxload 27/255
  Encapsulation 802.1Q Virtual LAN, Vlan ID  1., loopback not set
  Keepalive not supported 
  Full Duplex, 10000Mbps, link type is force-up, media type is 10GBase-LR
  output flow-control is on, input flow-control is on
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 00:00:11, output 00:00:03, output hang never
  Last clearing of "show interface" counters 01:12:35
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 1062624000 bits/sec, 240995 packets/sec
  30 second output rate 1853895000 bits/sec, 253637 packets/sec
     986817047 packets input, 537495628945 bytes, 0 no buffer
     Received 73 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     6005 input errors, 5713 CRC, 290 frame, 0 overrun, 0 ignored
     0 watchdog, 4558 multicast, 0 pause input
     1038829318 packets output, 956745842415 bytes, 0 underruns
     0 output errors, 0 collisions, 0 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
TenGigabitEthernet0/3/0.13 is up, line protocol is up 
  Hardware is SPA-1X10GE-L-V2, address is b414.8901.6c30 (bia b414.8901.6c30)
  Description: #OSPF-link
  Internet address is 81.20.192.52/28
  MTU 1500 bytes, BW 10000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 47/255, rxload 27/255
  Encapsulation 802.1Q Virtual LAN, Vlan ID  13.
  ARP type: ARPA, ARP Timeout 04:00:00
  Keepalive not supported 
  Last clearing of "show interface" counters never
TenGigabitEthernet0/3/0.1042 is administratively down, line protocol is down 
  Hardware is SPA-1X10GE-L-V2, address is b414.8901.6c30 (bia b414.8901.6c30)
  Description: #Bigtelecom
  Internet address is 81.20.192.149/30
  MTU 1500 bytes, BW 307200 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 47/255, rxload 27/255
  Encapsulation 802.1Q Virtual LAN, Vlan ID  1042.
  ARP type: ARPA, ARP Timeout 04:00:00
  Keepalive not supported 
  Last clearing of "show interface" counters never
TenGigabitEthernet1/3/0 is up, line protocol is up 
  Hardware is SPA-1X10GE-L-V2, address is b414.8901.6c70 (bia b414.8901.6c70)
  Description: #Megafon
  Internet address is 78.25.66.222/30
  MTU 1500 bytes, BW 10000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 26/255, rxload 47/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 10000Mbps, link type is force-up, media type is 10GBase-ER
  output flow-control is on, input flow-control is on
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 00:09:47, output 00:09:47, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 1845925000 bits/sec, 253605 packets/sec
  30 second output rate 1055429000 bits/sec, 240974 packets/sec
     942565259391 packets input, 946761733523178 bytes, 0 no buffer
     Received 3753 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     11 input errors, 0 CRC, 11 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     756697334383 packets output, 417245428118431 bytes, 0 underruns
     0 output errors, 0 collisions, 2 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0 is up, line protocol is up 
  Hardware is RP management port, address is b414.8901.6c80 (bia b414.8901.6c80)
  Description: #mngt27 to CTD-S0 Fa0/8
  Internet address is 192.168.121.31/24
  MTU 1500 bytes, BW 100000 Kbit/sec, DLY 100 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive set (10 sec)
  Full Duplex, 100Mbps, link type is auto, media type is RJ45
  output flow-control is unsupported, input flow-control is unsupported
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 00:00:04, output 00:00:04, output hang never
  Last clearing of "show interface" counters 1w6d
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     430081 packets input, 59591444 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     325177 packets output, 59938735 bytes, 0 underruns
     0 output errors, 0 collisions, 0 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
Loopback0 is up, line protocol is up 
  Hardware is Loopback
  Description: # Interface for Tunnel endpoint, IP/MPLS and BGP exchanges
  Internet address is 81.20.192.75/32
  MTU 1514 bytes, BW 8000000 Kbit/sec, DLY 5000 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation LOOPBACK, loopback not set
  Keepalive set (10 sec)
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/0 (size/max)
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 0 interface resets
     0 unknown protocol drops
     0 output buffer failures, 0 output buffers swapped out
Port-channel3 is administratively down, line protocol is down 
  Hardware is GEChannel, address is b414.8901.6cc2 (bia b414.8901.6cc2)
  Description: #CTD-S6 Po3 802.1q INET
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation 802.1Q Virtual LAN, Vlan ID  1., loopback not set
  Keepalive set (10 sec)
  ARP type: ARPA, ARP Timeout 04:00:00
    No. of active members in this channel: 0 
    No. of PF_JUMBO supported members in this channel : 3
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/0/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/0 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 0 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
Port-channel3.13 is administratively down, line protocol is down 
  Hardware is GEChannel, address is b414.8901.6cc2 (bia b414.8901.6cc2)
  Description: OSPF-link 120 #pheonix 20.05.2011
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation 802.1Q Virtual LAN, Vlan ID  13.
  ARP type: ARPA, ARP Timeout 04:00:00
  Keepalive set (10 sec)
  Last clearing of "show interface" counters never

------------------ show interfaces history ------------------



------------------ show controllers ------------------


GigabitEthernet0/0/0
     0 input vlan errors
     0 ingress over sub drops
     0 Number of sub-interface configured
GigabitEthernet0/0/1
     8970878 input vlan errors
     0 ingress over sub drops
     0 Number of sub-interface configured
GigabitEthernet0/0/2
     0 input vlan errors
     0 ingress over sub drops
     0 Number of sub-interface configured
GigabitEthernet0/0/3
     0 input vlan errors
     0 ingress over sub drops
     0 Number of sub-interface configured
GigabitEthernet0/0/4
     0 input vlan errors
     0 ingress over sub drops
     0 Number of sub-interface configured
GigabitEthernet0/0/5
     0 input vlan errors
     0 ingress over sub drops
     0 Number of sub-interface configured
GigabitEthernet0/0/6
     0 input vlan errors
     0 ingress over sub drops
     0 Number of sub-interface configured
GigabitEthernet0/0/7
     0 input vlan errors
     0 ingress over sub drops
     0 Number of sub-interface configured
TenGigabitEthernet0/3/0
     0 input vlan errors
     0 ingress over sub drops
     2 Number of sub-interface configured
TenGigabitEthernet1/3/0
     0 input vlan errors
     0 ingress over sub drops
     0 Number of sub-interface configured

------------------ show user ------------------


    Line       User       Host(s)              Idle       Location
*  2 vty 0     garry      idle                 00:00:00 81.20.192.32

  Interface    User               Mode         Idle     Peer Address


------------------ show data-corruption ------------------


No data inconsistency errors have been recorded.


------------------ show memory statistics ------------------


                Head    Total(b)     Used(b)     Free(b)   Lowest(b)  Largest(b)
Processor   30090008   1761021364   735281136   1025740228   1019403296   1020971556
 lsmpi_io   992611D0     6295088     6294120         968         968         968

------------------ show process memory ------------------


Processor Pool Total: 1761021364 Used:  735260900 Free: 1025760464
 lsmpi_io Pool Total:    6295088 Used:    6294116 Free:        972

 PID TTY  Allocated      Freed    Holding    Getbufs    Retbufs Process
   0   0  277474840   19110552  197418676        758   26151448 *Init*          
   0   0        160  627151268        160          1          1 *Sched*         
   0   0   93294852  131786852     900176        115        112 *Dead*          
   0   0          0          0     393428          0          0 *MallocLite*    
   1   0     581232          0     598460          0          0 Chunk Manager   
   2   0        236        236      11228          0          0 Load Meter      
   4   0          0          0      17228          0          0 Retransmission o
   5   0      52472          0      17228          0          0 IPC ISSU Dispatc
   6   0     572392      14724     551804          0          0 RF Slave Main Th
   7   0      65588          0     118816          0          0 EDDRI_MAIN      
   8   0       3396        236      20388          0          0 Check heaps     
   9   0     151888     151888      17228         45          0 Pool Manager    
  10   0          0          0      17228          0          0 DiscardQ Backgro
  11   0        236        236      17228          0          0 Timers          
  12   0          0          0      11228          0          0 WATCH_AFS       
  13   0  142693164  142656700      53692     583021     583021 ARP Input       
  14   0   19526552   19526552      17228        866        866 ARP Background  
  15   0        236        236      17228          0          0 ATM Idle Timer  
  16   0          0          0      17228          0          0 ATM ASYNC PROC  
  17   0          0          0      17228          0          0 AAA_SERVER_DEADT
  18   0          0          0      29228          0          0 Policy Manager  
  19   0      51620          0      68848        212        212 Entity MIB API  
  20   0    2660992          0    2684220       4805       4773 EEM ED Syslog   
  21   0      12744      12744      17228          0          0 PrstVbl         
  22   0        236        236      17228          0          0 Serial Backgroun
  23   0          0          0      17228          0          0 RO Notify Timers
  24   0          0          0      11228          0          0 RMI RM Notify Wa
  25   0        236        236      17228          0          0 DDR Timers      
  26   0          0          0      17228          0          0 CEF MIB API     
  27   0        236        236      23228          0          0 ATM AutoVC Perio
  28   0        236        236      17228          0          0 ATM VC Auto Crea
  29   0          0          0      17228          0          0 ifIndex Receive 
  30   0          0          0      17228          0          0 IPC Event Notifi
  31   0          0          0      17228          0          0 IPC Mcast Pendin
  32   0          0          0      17228          0          0 ASR1000 appsess 
  33   0          0          0      17228          0          0 IPC Dynamic Cach
  34   0          0          0      17228          0          0 IPC Service NonC
  35   0          0          0      17228          0          0 IPC Zone Manager
  36   0          0          0      17228    1354720    1354720 IPC Periodic Tim
  37   0          0          0      17228          0          0 IPC Deferred Por
  38   0          0          0      17228          0          0 IPC Process leve
  39   0       1996       2564      22388          0          0 IPC Seat Manager
  40   0          0          0      17228          0          0 IPC Check Queue 
  41   0     317892          0     279540        135        123 IPC Seat RX Cont
  42   0          0          0      17228          0          0 IPC Seat TX Cont
  43   0      28756        708      45276    2709444    2709444 IPC Keep Alive M
  44   0          0          0      17228          0          0 IPC Loadometer  
  45   0          0          0      17228          0          0 SENSOR-MGR event
  46   0          0          0      17228          0          0 Compute SRP rate
  47   0          0          0      17228          0          0 ASR1000 heartbea
  48   0        236        236      17228          0          0 GraphIt         
  49   0          0          0      17228          0          0 SERIAL A'detect 
  50   0        236        236      29228          0          0 Dialer event    
  51   0      32036       2120      47640         21         21 client_entity_se
  52   0       1728          0      18956          0          0 RF SCTPthread   
  53   0          0          0      17228          0          0 ASR1000 signals 
  54   0          0          0      17228          0          0 Critical Bkgnd  
  55   0      77160        392      31084         56         56 Net Background  
  56   0       2480       2224      29484          0          0 IDB Work        
  57   0        236        236      29228       9498       9498 Logger          
  58   0        236       1104      17228         12         12 TTY Background  
  59   0       4728          0      21956          0          0 IPC Apps Task   
  60   0       1648        884      17992          0          0 IF-MGR control p
  61   0      11668          0      25664         16         16 IF-MGR event pro
  62   0          0          0      23228          0          0 REDUNDANCY FSM  
  63   0          0          0      17228          0          0 SBC IPC Hold Que
  64   0   88821340       3368    3803312        262        262 IOSD ipc task   
  65   0          0          0      53228          0          0 IOSD chasfs task
  66   0        236        236      11228    2257160    2257160 PuntInject Keepa
  67   0          0          0      17296          0          0 cpf_msg_holdq_pr
  68   0          0          0      17228          0          0 cpf_msg_rcvq_pro
  69   0          0          0      17228          0          0 Network-rf Notif
  70   0          0          0      17228          0          0 CWAN APS HA Proc
  71   0          0          0      17228          6          6 Environmental Mo
  72   0          0          0      17228          0          0 ASR1000-RP HA Pe
  73   0          0          0      17228          0          0 REDUNDANCY peer 
  74   0          0          0      17228          0          0 100ms check     
  75   0          0          0      17228          0          0 RF CWAN HA Proce
  76   0          0          0      17228          0          0 CWAN IF EVENT HA
  77   0          0          0      17228          0          0 CHKPT Test clien
  78   0          0          0      17228          0          0 DHCPC HA        
  79   0          0          0      17228          0          0 DHCPD HA        
  80   0          0          0      17228          0          0 DHCPv6 Relay HA 
  81   0          0          0      17228          0          0 ARP HA          
  82   0          0          0      23228          0          0 CONSOLE helper p
  83   0  509871768  508875152      37040   28077475   28077475 ASR1000-RP Punt 
  84   0          0          0      17228          0          0 ASR1000-RP SPA T
  85   0      22100      39408      27904          0          0 RF Master Main T
  86   0       1676          0      18904          0          0 RF Master KPA Th
  87   0       1676          0      18904          0          0 RF Master Status
  88   0          0          0      17228     376238     376238 Net Input       
  89   0        236        236      17228          0          0 Compute load avg
  90   0       3416       1628      20644          0          0 Per-minute Jobs 
  91   0          0          0      23228          0          0 Per-Second Jobs 
  92   0          0          0      17228          0          0 cpf_process_tpQ 
  93   0          0     836448      17228          0          0 Transport Port A
  94   0          0          0      17228          0          0 DSX3MIB ll handl
  95   0          0          0      17228          0          0 POS APS Event Pr
  96   0        236        236      17228          1          1 netclk_process  
  97   0          0          0      17228          0          0 netclk_ha_proces
  98   0       5412       6024      17228          6          6 FPD Management P
  99   0          0          0      17228          0          0 FPD Action Proce
 100   0          0          0      17228          0          0 ASR1000-RP FastP
 101   0        236        236      17228          0          0 FEC_Link_event_h
 102   0          0          0      29228          0          0 MCP RP autovc pr
 103   0          0          0      17228          0          0 CWAN CHOCX PROCE
 104   0          0          0      17228          0          0 CE3 Mailbox     
 105   0          0          0      17228          0          0 CT3 Mailbox     
 106   0          0          0      17228          0          0 HAL Mailbox     
 107   0        236        236      17228          0          0 MIP Mailbox     
 108   0    3039596      31368    1646784        200        200 CWAN OIR Handler
 109   0          0          0      23296          4          4 BGP Scheduler   
 110   0          0          0      17228          0          0 ASR1K ESMC Proce
 111   0          0          0      17228          0          0 MGMTE stats Proc
 112   0          0          0      17228          0          0 ASR1000-RP SPA A
 113   0          0          0      17228          0          0 RTTYS Process   
 114   0      18468        236      35460          0          0 AAA Server      
 115   0          0          0      17228          0          0 AAA ACCT Proc   
 116   0      49384          0      66612          0          0 ACCT Periodic Pr
 117   0          0          0      17228          0          0 AAA System Acct 
 118   0          0          0      23228          0          0 IPv6 RIB Event H
 119   0        236        236      17228          0          0 AAA Dictionary R
 120   0          0          0      17228          0          0 EAP Framework   
 121   0          0          0      17228          0          0 EAP Test        
 122   0          0          0      23228          0          0 HQF TUNNEL      
 123   0        236        236      17228          0          0 IPAM/ODAP Events
 124   0      49420          0      78648          0          0 IPAM Manager    
 125   0        236        236      29228          0          0 IPAM Events     
 126   0      48708      10376      65880        103        103 IP ARP Adjacency
 127   0      49384          0      66612          0          0 IP ARP Retry Age
 128   0          0          0      29228     109724     109724 IP Input        
 129   0          0          0      17228          0          0 ICMP event handl
 130   0        236        236      17228          0          0 PIM register asy
 131   0          0          0      17228          0          0 IPv6 ping proces
 132   0        236        236      17228          0          0 OCE punted Pkts 
 133   0          0          0      17228          0          0 LSP Tunnel FRR  
 134   0          0          0      23228          0          0 MPLS Auto-Tunnel
 135   0          0          0      17228          0          0 O-UNI Client Msg
 136   0          0          0      17300          0          0 AAA EPD HANDLER 
 137   0          0          0      17228          0          0 PM EPD API      
 138   0        236        236      17228          0          0 PPP SIP         
 139   0        236        236      17228          0          0 PPP Bind        
 140   0        236        236      29228          0          0 PPP IP Route    
 141   2    1057924    1049444      37708        650        632 Virtual Exec    
 142   0        236        236      29228          0          0 SSM connection m
 143   0        472        236      17464          0          0 Spanning Tree   
 144   0          0          0      17228          0          0 VRRS            
 145   0        236          0      29464          0          0 CEF switching ba
 146   0        224          0      11524          0          0 ADJ NSF process 
 147   0        476        252      29452          1          1 ADJ resolve proc
 148   0        236        236      29228          0          0 ATM OAM Input   
 149   0        236        236      29228          0          0 ATM OAM TIMER   
 150   0          0          0      29228          0          0 SSS Manager     
 151   0          0          0      29228          0          0 SSS Policy Manag
 152   0          0          0      17228          0          0 SSS Feature Mana
 153   0          0          0      17228          0          0 SSS Feature Time
 154   0          0          0      29228          0          0 SSS PM SHIM QOS 
 155   0          0          0      17228          0          0 SG DPM          
 156   0          0          0      17228          0          0 Timer handler fo
 157   0          0          0      17228          0          0 Prepaid response
 158   0          0          0      17228          0          0 Timed Policy act
 159   0          0          0      17228          0          0 AAA response han
 160   0          0          0      17228          0          0 SG CMD HANDLER  
 161   0        236        236      17228          0          0 IP PORTBUNDLE   
 162   0        236        236      29228          0          0 IP Static Sessio
 163   0          0          0      17228          0          0 RADIUS Proxy    
 164   0          0          0      29228          0          0 TC SIP          
 165   0        236        236      29228          0          0 Ethernet LMI    
 166   0        236        236      23228          0          0 Ethernet OAM Pro
 167   0        236        236      29228          0          0 Ethernet CFM    
 168   0        236        236      29228          0          0 Ethernet Timer C
 169   0        236        236      29228          0          0 Ethernet Msec Ti
 170   0          0          0      17228          0          0 PPCP RP Stats Ba
 171   0          0          0      17228          0          0 CCM             
 172   0          0          0      17228          0          0 CCM IPC flow con
 173   0      11488          0      40716          0          0 IMA PROC        
 174   0          0          0      17228          0          0 Call Home Timer 
 175   0        236        236      29228          0          0 RG Faults Timer 
 176   0          0          0      17228          0          0 RG VP           
 177   0        236        236      29228          0          0 RG Protocol Time
 178   0        236        236      29228          0          0 RG Transport Tim
 179   0          0          0      17228          0          0 HDLC HA         
 180   0     209108          0      15108          0          0 SBC initializer 
 181   0          0          0      17228          0          0 AC Switch       
 182   0          0          0      17228          0          0 FRR Background P
 183   0      30672       8096      51132         39         39 CEF background p
 184   0        224          0      29452          0          0 fib_fib_bfd_sb e
 185   0          0          0      23228          0          0 IP IRDP         
 186   0          0          0      17300          0          0 SNMP Timers     
 187   0        224          0      17452          0          0 XDR background p
 188   0          0          0      17228          0          0 XDR mcast       
 189   0       6356          0      23584          0          0 LSD HA Proc     
 190   0          0          0      17228          0          0 IPC LC Message H
 191   0          0          0      17228          0          0 XDR RP Ping Back
 192   0          0          0      17228          0          0 XDR RP backgroun
 193   0          0          0      17228          0          0 XDR RP Test Back
 194   0          0          0      29228          0          0 Routing Topology
 195   0  149227284  254120872  105404500   12480518   12480518 IP RIB Update   
 196   0      14564      15440      23760         42         42 IP Background   
 197   0      43596       1920      64348          0          0 IP Connected Rou
 198   0          0          0      29228          0          0 cdp init process
 199   0          0          0      17228          0          0 IP Traceroute   
 200   0          0          0      17228          0          0 Socket Timers   
 201   0        236        236      17228          0          0 Flow Exporter Ti
 202   0          0      17380      29228    5898785    5898785 TCP Timer       
 203   0    4936380          0      29228          0          0 TCP Protocols   
 204   0        940          0      24168          0          0 HTTP CORE       
 205   0        224       1024      29452         18         18 Collection proce
 206   0        224          0      17452          0          0 CEF RP IPC Backg
 207   0        232          0      29460          0          0 MFIB Master back
 208   0        472        236      23464          0          0 Multicast Offloa
 209   0      84808       2664      64688          5          5 CEF: IPv4 proces
 210   0        288          0      17516          6          6 ADJ background  
 211   0        236        236      23228          0          0 static          
 212   0          0          0      17228          0          0 MFI Comm RP Proc
 213   0          0          0      29228          0          0 Path set broker 
 214   0          0          0      17228          0          0 LDP HA          
 215   0        236        236      17228          0          0 MPLS VPN HA Clie
 216   0       4728          0      21956          0          0 RSVP HA Services
 217   0        236        236      17228          0          0 TSPTUN HA       
 218   0        236        336      17228          0          0 Inter Chassis Pr
 219   0        400        400      17228          0          0 LFDp Input Proc 
 220   0   42913884   42913884      17228          0          0 QoS stats proces
 221   0      19492        236      36484          0          0 SCTP Main Proces
 222   0        236        236      17228          0          0 PPP Compress Inp
 223   0        236        236      17228          0          0 PPP Compress Res
 224   0        940          0     126168          0          0 COPS            
 225   0        236        236      17228          0          0 Dialer Forwarder
 226   0          0          0      17228         55         55 RARP Input      
 227   0        236        236      17228          0          0 PPP NBF         
 228   0        472        236      11464          0          0 PfR BR Learn    
 229   0          0          0      17228          0          0 PAD InCall      
 230   0        236        236      29228          0          0 X.25 Background 
 231   0          0          0      17228          0          0 X.25 Encaps Mana
 232   0        236        236      17228          0          0 RBSCP Background
 233   0          0          0      29228          0          0 VPDN call manage
 234   0         84          0      17312          0          0 XC RIB MGR      
 235   0        236        236      29228          0          0 IP Inband Sessio
 236   0        236        236      29228          0          0 IP SIP Process  
 237   0        236        236      17228          0          0 EFP Errd        
 238   0        236        236      17228          0          0 Ether Infra RP  
 239   0          0          0      17228          0          0 ECFM HA IPC flow
 240   0          0          0      17228          0          0 IGMPSN L2MCM    
 241   0          0          0      17228          0          0 IGMPSN MRD      
 242   0          0          0      17228          0          0 IGMPSN          
 243   0          0          0      17228          0          0 TCP HA PROC     
 244   0          0          0      17228          0          0 BGP HA SSO      
 245   0          0          0      17228          0          0 RETRY_REPOPULATE
 246   0        228          0      17456          0          0 XDR FOF process 
 247   0          0          0      17228          0          0 AAA HA          
 248   0          0          0      17228          0          0 ac_atm_state_eve
 249   0      32820          0      62048          0          0 ATM HA          
 250   0          0          0      17228          0          0 ATM HA IPC flow 
 251   0          0          0      17228          0          0 ATM HA AC       
 252   0          0          0      17228          0          0 BFD HA          
 253   0          0          0      17228          0          0 FR HA           
 254   0          0          0      17228          0          0 GLBP HA         
 255   0          0          0      17228          0          0 Probe Input     
 256   0          0          0      17228          0          0 HSRP HA         
 257   0        236        236      17228          0          0 Inspect process 
 258   0        224          0      17452          0          0 LACP Protocol   
 259   0        232          0      29460          0          0 MRIB RP Proxy   
 260   0          0          0      17228          0          0 IPv6 ACL RP Proc
 261   0          0          0      17228          0          0 Netsync IPC flow
 262   0        236        236      17228          0          0 PPPoE VRRS EVT M
 263   0        236        236      29228          0          0 RG Media Timer  
 264   0        236        236      29276          1          1 MCPRP RG Timer  
 265   0       1176        236      18168          0          0 URL filter proc 
 266   0          0          0      17228          0          0 VPDN CCM Backgro
 267   0          0          0      17228          0          0 VRRP HA         
 268   0          0          0      17228          0          0 VTEMPLATE IPC fl
 269   0          0          0      17228          0          0 SBC Msg Ack Time
 270   0        292        292      11228          0          0 L2X Switching Ev
 271   0        296        296      17228          0          0 AAA Cached Serve
 272   0          0          0      17228          0          0 EM Background Pr
 273   0          0          0      17228          0          0 IDMGR CORE      
 274   0       6724       3456      20496          0          0 LOCAL AAA       
 275   0          0          0      17228          0          0 MPLS Auto Mesh P
 276   0   31051132  608874816      23296   13691778   13691778 BGP I/O         
 277   0        304        304      17228          0          0 ENABLE AAA      
 278   0        304        304      17228          0          0 LINE AAA        
 279   0      66692        304      18028          0          0 TPLUS           
 280   0      44012      44012      23228          0          0 DynCmd Package P
 281   0     212200        304     229124          0          0 FLEX DSPRM MAIN 
 282   0        304        304      17228          0          0 VSP_MGR         
 283   0      27920        304      80844          0          0 STUN_APP        
 284   0        992          0      54220          0          0 STUN_TEST       
 285   0     491704          0     514932          0          0 QOS_MODULE_MAIN 
 286   0          0          0      53228          0          0 VoIP AAA        
 287   0          0          0      23228          0          0 QOS PERUSER     
 288   0        540        304      17464          0          0 PIM HA          
 289   0        380          0      53608          0          0 RPMS_PROC_MAIN  
 290   0       1012          0     126240          0          0 http client proc
 291   0  432803660  517870936      17296     895081     895081 DiagCard1/-1    
 292   0       8940      43828      17228          0          0 AAA SEND STOP EV
 293   0          0          0      29228          0          0 Test AAA Client 
 294   0       3700          0      26928          0          0 EEM ED Routing  
 295   0       3852          0      27080          0          0 EEM ED Track    
 296   0       3964          0      27192          0          0 EEM ED Resource 
 297   0          0          0      17228          0          0 Syslog Traps    
 299   0        228          0      17456          0          0 DATA Transfer Pr
 300   0        228          0      17456          0          0 DATA Collector  
 301   0          0          0      17228          0          0 SONET Traps     
 302   0  720896324  557208512    1433716     810812     810812 OSPF-110 Router 
 303   0        228          0      17456          0          0 Online Diag EEM 
 304   0  178703592  178684344      36476     751586     751586 SPA ENTITY Proce
 305   0     189128          0     206356          0          0 EEM Server      
 306   0     101368      41320      96984          0          0 Call Home proces
 307   0      16100       1848      31480          0          0 EEM Policy Direc
 308   0       3700          0      26928          0          0 EEM ED CLI      
 309   0       3700          0      26928          0          0 EEM ED Counter  
 310   0       3700          0      26928          0          0 EEM ED Interface
 311   0       3700          0      26928          0          0 EEM ED IOSWD    
 312   0       3700          0      26928          0          0 EEM ED None     
 313   0       3700          0      26928          0          0 EEM ED OIR      
 314   0       4308          0      27080          0          0 EEM ED RF       
 315   0       3700          0      26928          0          0 EEM ED SNMP     
 316   0       3700          0      26928          0          0 EEM ED SNMP Noti
 317   0       3700          0      26928          0          0 EEM ED Timer    
 318   0       3700          0      26928          0          0 EEM ED Test     
 319   0       3700          0      26928          0          0 EEM ED Config   
 320   0       3700          0      26928          0          0 EEM ED Env      
 321   0       3700          0      26928          0          0 EM ED GOLD      
 322   0       8752          0      31980          0          0 EEM ED Nf       
 323   0       3700          0      26928          0          0 EEM ED Ipsla    
 324   0    1132440    1135320      31148      14306      14306 Syslog          
 325   0          0          0      17228          0          0 VDC process     
 326   0          0          0      17228          0          0 IP SLAs Ethernet
 327   0          0          0      17228          0          0 ISSU Utility Pro
 328   0        276          0      17504          0          0 Online Diag CNS 
 329   0        228          0      17456          0          0 Online Diag CNS 
 330   0        244        244      17228          0          0 DiagCard2/-1    
 331   0          0          0      17228          0          0 IPC ISSU Version
 332   0          0          0      17228          0          0 IPC ISSU Version
 333   0          0          0      17228          0          0 IPC ISSU Version
 334   0          0          0      17228          0          0 IPC ISSU Version
 335   0          0          0      17228          0          0 IPC ISSU Version
 336   0          0          0      17228          0          0 IPC ISSU Version
 337   0          0          0      17228          0          0 IPC ISSU Version
 338   0          0          0      17228          0          0 IPC ISSU Version
 339   0          0          0      17228          0          0 IPC ISSU Version
 340   0          0          0      17228          0          0 IPC ISSU Version
 341   0          0          0      17228          0          0 IPC ISSU Version
 342   0          0          0      17228          0          0 IPC ISSU Version
 343   0          0          0      17228          0          0 IPC ISSU Version
 344   0          0          0      17228          0          0 IPC ISSU Version
 345   0          0          0      17228          0          0 IPC ISSU Version
 346   0          0          0      17228          0          0 IPC ISSU Version
 347   0          0          0      17228          0          0 IPC ISSU Version
 348   0          0          0      17228          0          0 IPC ISSU Version
 349   0          0          0      17228          0          0 IPC ISSU Version
 350   0          0          0      17228          0          0 IPC ISSU Version
 351   0          0          0      17228          0          0 IPC ISSU Version
 352   0          0          0      17228          0          0 IPC ISSU Version
 353   0          0          0      17228          0          0 IPC ISSU Version
 354   0          0          0      17228          0          0 IPC ISSU Version
 355   0          0          0      17228          0          0 IPC ISSU Version
 356   0          0          0      17228          0          0 IPC ISSU Version
 357   0          0          0      17228          0          0 IPC ISSU Version
 358   0          0          0      17228          0          0 IPC ISSU Version
 359   0          0          0      17228          0          0 IPC ISSU Version
 360   0          0          0      17228          0          0 IPC ISSU Version
 361   0          0          0      17228          0          0 IPC ISSU Version
 362   0          0          0      17228          0          0 IPC ISSU Version
 363   0          0          0      17228          0          0 IPC ISSU Version
 364   0          0          0      17228          0          0 IPC ISSU Version
 365   0          0          0      17228          0          0 IPC ISSU Version
 366   0          0          0      17228          0          0 IPC ISSU Version
 367   0          0          0      17228          0          0 IPC ISSU Version
 368   0          0          0      17228          0          0 IPC ISSU Version
 369   0       4728          0      21956          0          0 IPC ISSU Version
 370   0          0          0      17228          0          0 IPC ISSU Version
 371   0          0          0      17228          0          0 IPC ISSU Version
 372   0          0          0      17228          0          0 IPC ISSU Version
 373   0          0          0      17228          0          0 IPC ISSU Version
 374   0          0          0      17228          0          0 IPC ISSU Version
 375   0          0          0      17228          0          0 IPC ISSU Version
 376   0          0          0      17228          0          0 IPC ISSU Version
 377   0        244        244      17228          0          0 DiagCard3/-1    
 378   0        244        244      17228          0          0 DiagCard4/-1    
 379   0          0          0      17228          0          0 IPC ISSU Version
 380   0          0          0      17228          0          0 IPC ISSU Version
 381   0          0          0      17228          0          0 IPC ISSU Version
 382   0          0          0      17228          0          0 IPC ISSU Version
 383   0          0          0      17228          0          0 IPC ISSU Version
 384   0          0          0      17228          0          0 IPC ISSU Version
 385   0          0          0      17228          0          0 IPC ISSU Version
 386   0          0          0      17228          0          0 IPC ISSU Version
 387   0          0          0      17228          0          0 IPC ISSU Version
 388   0          0          0      17228          0          0 IPC ISSU Version
 389   0          0          0      17228          0          0 IPC ISSU Version
 390   0          0          0      17228          0          0 IPC ISSU Version
 391   0          0          0      17228          0          0 IPC ISSU Version
 392   0          0          0      17228          0          0 IPC ISSU Version
 393   0          0        292      17228          0          0 CWAN OIR IPC Rea
 394   0   99760564       1332   99947232          0          0 SBC main process
 395   0     118784        236     147776          0          0 MRIB Process    
 397   0 1576053404  293423152  314933492     117405     117405 BGP Router      
 398   0          0  187751244      23296          0          0 BGP Scanner     
 399   0  622033316    5626064     588412          0          0 BGP Task        
 400   0          0          0      17228          0          0 TCP Listener    
 401   0  606567940  606313132      30224    4109688    4109688 IP SNMP         
 402   0   94406828       1764      29228          0          0 PDU DISPATCHER  
 403   0 4098062816 4192140212     609820       3545       3545 SNMP ENGINE     
 404   0       1184        236      30176          0          0 IP SNMPV6       
 405   0          0          0      29228          0          0 SNMP ConfCopyPro
 406   0  183702232  183713372      29860     449146     449146 SNMP Traps      
 407   0          0          0      17228          0          0 MPLS MIB traps  
 408   0      23032        236      22420     147091     147091 NTP             
 409   0          0          0      17228          0          0 IFCOM Msg Hdlr  
 410   0          0          0      17228          0          0 IFCOM Msg Hdlr  
 411   0          0          0      17228          0          0 IFCOM Msg Hdlr  
 412   0      24912  162255168      41128    4326176    4326176 OSPF-110 Hello  
 413   0          0          0      17296          0          0 BGP Event       
 414   0      18248      17608      17868         66         66 Ether-SPA backgr
                                741304244 Total

------------------ show process cpu ------------------


CPU utilization for five seconds: 1%/0%; one minute: 2%; five minutes: 2%
 PID Runtime(ms)     Invoked      uSecs   5Sec   1Min   5Min TTY Process 
   1           2          16        125  0.00%  0.00%  0.00%   0 Chunk Manager    
   2       24198      903148         26  0.00%  0.00%  0.00%   0 Load Meter       
   4           1           8        125  0.00%  0.00%  0.00%   0 Retransmission o 
   5           2           4        500  0.00%  0.00%  0.00%   0 IPC ISSU Dispatc 
   6          15          12       1250  0.00%  0.00%  0.00%   0 RF Slave Main Th 
   7           0           1          0  0.00%  0.00%  0.00%   0 EDDRI_MAIN       
   8    40098804     2218992      18070  0.79%  0.88%  0.86%   0 Check heaps      
   9           4          20        200  0.00%  0.00%  0.00%   0 Pool Manager     
  10           0           1          0  0.00%  0.00%  0.00%   0 DiscardQ Backgro 
  11           0           2          0  0.00%  0.00%  0.00%   0 Timers           
  12           3         392          7  0.00%  0.00%  0.00%   0 WATCH_AFS        
  13      170809      581756        293  0.07%  0.00%  0.00%   0 ARP Input        
  14        4859     4707022          1  0.00%  0.00%  0.00%   0 ARP Background   
  15           0           2          0  0.00%  0.00%  0.00%   0 ATM Idle Timer   
  16           0           1          0  0.00%  0.00%  0.00%   0 ATM ASYNC PROC   
  17           0           1          0  0.00%  0.00%  0.00%   0 AAA_SERVER_DEADT 
  18           0           1          0  0.00%  0.00%  0.00%   0 Policy Manager   
  19          17          28        607  0.00%  0.00%  0.00%   0 Entity MIB API   
  20         157        4755         33  0.00%  0.00%  0.00%   0 EEM ED Syslog    
  21         349          59       5915  0.00%  0.00%  0.00%   0 PrstVbl          
  22           0           2          0  0.00%  0.00%  0.00%   0 Serial Backgroun 
  23           0           1          0  0.00%  0.00%  0.00%   0 RO Notify Timers 
  24           0           1          0  0.00%  0.00%  0.00%   0 RMI RM Notify Wa 
  25           0           2          0  0.00%  0.00%  0.00%   0 DDR Timers       
  26           0           1          0  0.00%  0.00%  0.00%   0 CEF MIB API      
  27           0           2          0  0.00%  0.00%  0.00%   0 ATM AutoVC Perio 
  28           0           2          0  0.00%  0.00%  0.00%   0 ATM VC Auto Crea 
  29           0           1          0  0.00%  0.00%  0.00%   0 ifIndex Receive  
  30         430      903040          0  0.00%  0.00%  0.00%   0 IPC Event Notifi 
  31        2803     4406774          0  0.00%  0.00%  0.00%   0 IPC Mcast Pendin 
  32           0           1          0  0.00%  0.00%  0.00%   0 ASR1000 appsess  
  33          96       75262          1  0.00%  0.00%  0.00%   0 IPC Dynamic Cach 
  34         499      903040          0  0.00%  0.00%  0.00%   0 IPC Service NonC 
  35           0           1          0  0.00%  0.00%  0.00%   0 IPC Zone Manager 
  36        8787     4406793          1  0.00%  0.00%  0.00%   0 IPC Periodic Tim 
  37        2529     4406773          0  0.00%  0.00%  0.00%   0 IPC Deferred Por 
  38           0           1          0  0.00%  0.00%  0.00%   0 IPC Process leve 
  39       53434     1354729         39  0.00%  0.00%  0.00%   0 IPC Seat Manager 
  40         307      258029          1  0.00%  0.00%  0.00%   0 IPC Check Queue  
  41          12          57        210  0.00%  0.00%  0.00%   0 IPC Seat RX Cont 
  42           0           1          0  0.00%  0.00%  0.00%   0 IPC Seat TX Cont 
  43       10179      451660         22  0.00%  0.00%  0.00%   0 IPC Keep Alive M 
  44        5649      903042          6  0.00%  0.00%  0.00%   0 IPC Loadometer   
  45           0           1          0  0.00%  0.00%  0.00%   0 SENSOR-MGR event 
  46         292      451575          0  0.00%  0.00%  0.00%   0 Compute SRP rate 
  47        2290     2257189          1  0.00%  0.00%  0.00%   0 ASR1000 heartbea 
  48        3546     4515735          0  0.00%  0.00%  0.00%   0 GraphIt          
  49           0           1          0  0.00%  0.00%  0.00%   0 SERIAL A'detect  
  50           0           2          0  0.00%  0.00%  0.00%   0 Dialer event     
  51           4           9        444  0.00%  0.00%  0.00%   0 client_entity_se 
  52           0           1          0  0.00%  0.00%  0.00%   0 RF SCTPthread    
  53           0           1          0  0.00%  0.00%  0.00%   0 ASR1000 signals  
  54           0           1          0  0.00%  0.00%  0.00%   0 Critical Bkgnd   
  55        2776     1378731          2  0.00%  0.00%  0.00%   0 Net Background   
  56           0           3          0  0.00%  0.00%  0.00%   0 IDB Work         
  57          29        9428          3  0.00%  0.00%  0.00%   0 Logger           
  58        4415     4512926          0  0.00%  0.00%  0.00%   0 TTY Background   
  59           0           1          0  0.00%  0.00%  0.00%   0 IPC Apps Task    
  60           1          11         90  0.00%  0.00%  0.00%   0 IF-MGR control p 
  61           2          14        142  0.00%  0.00%  0.00%   0 IF-MGR event pro 
  62         587      645055          0  0.00%  0.00%  0.00%   0 REDUNDANCY FSM   
  63           0           1          0  0.00%  0.00%  0.00%   0 SBC IPC Hold Que 
  64     3987516    20032210        199  0.07%  0.06%  0.07%   0 IOSD ipc task    
  65      688847     3408112        202  0.00%  0.01%  0.00%   0 IOSD chasfs task 
  66       14506     2257163          6  0.00%  0.00%  0.00%   0 PuntInject Keepa 
  67           0           2          0  0.00%  0.00%  0.00%   0 cpf_msg_holdq_pr 
  68           0           1          0  0.00%  0.00%  0.00%   0 cpf_msg_rcvq_pro 
  69           0           1          0  0.00%  0.00%  0.00%   0 Network-rf Notif 
  70           0           1          0  0.00%  0.00%  0.00%   0 CWAN APS HA Proc 
  71       13198     4513000          2  0.00%  0.00%  0.00%   0 Environmental Mo 
  72        3413     4512934          0  0.00%  0.00%  0.00%   0 ASR1000-RP HA Pe 
  73        5303     4513017          1  0.00%  0.00%  0.00%   0 REDUNDANCY peer  
  74       33296    45155218          0  0.00%  0.00%  0.00%   0 100ms check      
  75         680       75264          9  0.00%  0.00%  0.00%   0 RF CWAN HA Proce 
  76           0           1          0  0.00%  0.00%  0.00%   0 CWAN IF EVENT HA 
  77           1           1       1000  0.00%  0.00%  0.00%   0 CHKPT Test clien 
  78           0           1          0  0.00%  0.00%  0.00%   0 DHCPC HA         
  79           0           1          0  0.00%  0.00%  0.00%   0 DHCPD HA         
  80           0           1          0  0.00%  0.00%  0.00%   0 DHCPv6 Relay HA  
  81           0           3          0  0.00%  0.00%  0.00%   0 ARP HA           
  82           0           1          0  0.00%  0.00%  0.00%   0 CONSOLE helper p 
  83     1570790    26580509         59  0.00%  0.03%  0.02%   0 ASR1000-RP Punt  
  84           0           1          0  0.00%  0.00%  0.00%   0 ASR1000-RP SPA T 
  85           4          12        333  0.00%  0.00%  0.00%   0 RF Master Main T 
  86           0           1          0  0.00%  0.00%  0.00%   0 RF Master KPA Th 
  87           0           1          0  0.00%  0.00%  0.00%   0 RF Master Status 
  88       10522      363019         28  0.00%  0.00%  0.00%   0 Net Input        
  89        3445      903269          3  0.00%  0.00%  0.00%   0 Compute load avg 
  90     1440493       75336      19120  0.00%  0.02%  0.00%   0 Per-minute Jobs  
  91       55883     4516677         12  0.00%  0.00%  0.00%   0 Per-Second Jobs  
  92           0           1          0  0.00%  0.00%  0.00%   0 cpf_process_tpQ  
  93         415      341320          1  0.00%  0.00%  0.00%   0 Transport Port A 
  94           0           1          0  0.00%  0.00%  0.00%   0 DSX3MIB ll handl 
  95           0           1          0  0.00%  0.00%  0.00%   0 POS APS Event Pr 
  96          12           3       4000  0.00%  0.00%  0.00%   0 netclk_process   
  97           0           1          0  0.00%  0.00%  0.00%   0 netclk_ha_proces 
  98          11           5       2200  0.00%  0.00%  0.00%   0 FPD Management P 
  99           0           1          0  0.00%  0.00%  0.00%   0 FPD Action Proce 
 100           0           1          0  0.00%  0.00%  0.00%   0 ASR1000-RP FastP 
 101           1           4        250  0.00%  0.00%  0.00%   0 FEC_Link_event_h 
 102       27925    35100717          0  0.00%  0.00%  0.00%   0 MCP RP autovc pr 
 103        2814     4512932          0  0.00%  0.00%  0.00%   0 CWAN CHOCX PROCE 
 104           0           1          0  0.00%  0.00%  0.00%   0 CE3 Mailbox      
 105           0           1          0  0.00%  0.00%  0.00%   0 CT3 Mailbox      
 106           0           1          0  0.00%  0.00%  0.00%   0 HAL Mailbox      
 107           0           2          0  0.00%  0.00%  0.00%   0 MIP Mailbox      
 108        4015      118990         33  0.00%  0.00%  0.00%   0 CWAN OIR Handler 
 109        3223     4406766          0  0.00%  0.00%  0.00%   0 BGP Scheduler    
 110           0           1          0  0.00%  0.00%  0.00%   0 ASR1K ESMC Proce 
 111        1254      902908          1  0.00%  0.00%  0.00%   0 MGMTE stats Proc 
 112           0           1          0  0.00%  0.00%  0.00%   0 ASR1000-RP SPA A 
 113           0           1          0  0.00%  0.00%  0.00%   0 RTTYS Process    
 114           3          99         30  0.00%  0.00%  0.00%   0 AAA Server       
 115           0           1          0  0.00%  0.00%  0.00%   0 AAA ACCT Proc    
 116           1           1       1000  0.00%  0.00%  0.00%   0 ACCT Periodic Pr 
 117           0           1          0  0.00%  0.00%  0.00%   0 AAA System Acct  
 118           0           3          0  0.00%  0.00%  0.00%   0 IPv6 RIB Event H 
 119           0           2          0  0.00%  0.00%  0.00%   0 AAA Dictionary R 
 120           0           1          0  0.00%  0.00%  0.00%   0 EAP Framework    
 121           0           1          0  0.00%  0.00%  0.00%   0 EAP Test         
 122           0           1          0  0.00%  0.00%  0.00%   0 HQF TUNNEL       
 123           0           2          0  0.00%  0.00%  0.00%   0 IPAM/ODAP Events 
 124       71303   138619209          0  0.00%  0.00%  0.00%   0 IPAM Manager     
 125           0           2          0  0.00%  0.00%  0.00%   0 IPAM Events      
 126          26          34        764  0.00%  0.00%  0.00%   0 IP ARP Adjacency 
 127       81545   138619003          0  0.00%  0.00%  0.00%   0 IP ARP Retry Age 
 128       12959      180399         71  0.00%  0.00%  0.00%   0 IP Input         
 129           0           1          0  0.00%  0.00%  0.00%   0 ICMP event handl 
 130           0           3          0  0.00%  0.00%  0.00%   0 PIM register asy 
 131           0           1          0  0.00%  0.00%  0.00%   0 IPv6 ping proces 
 132           0           2          0  0.00%  0.00%  0.00%   0 OCE punted Pkts  
 133           0           1          0  0.00%  0.00%  0.00%   0 LSP Tunnel FRR   
 134           0           1          0  0.00%  0.00%  0.00%   0 MPLS Auto-Tunnel 
 135           0           1          0  0.00%  0.00%  0.00%   0 O-UNI Client Msg 
 136           0           1          0  0.00%  0.00%  0.00%   0 AAA EPD HANDLER  
 137           0           1          0  0.00%  0.00%  0.00%   0 PM EPD API       
 138           0           2          0  0.00%  0.00%  0.00%   0 PPP SIP          
 139           0           2          0  0.00%  0.00%  0.00%   0 PPP Bind         
 140           0           2          0  0.00%  0.00%  0.00%   0 PPP IP Route     
 141         480         611        785  0.00%  0.03%  0.01%   2 Virtual Exec     
 142           1          22         45  0.00%  0.00%  0.00%   0 SSM connection m 
 143           0           2          0  0.00%  0.00%  0.00%   0 Spanning Tree    
 144           0           1          0  0.00%  0.00%  0.00%   0 VRRS             
 145           0           2          0  0.00%  0.00%  0.00%   0 CEF switching ba 
 146           0           1          0  0.00%  0.00%  0.00%   0 ADJ NSF process  
 147           1           3        333  0.00%  0.00%  0.00%   0 ADJ resolve proc 
 148           0           2          0  0.00%  0.00%  0.00%   0 ATM OAM Input    
 149           0           2          0  0.00%  0.00%  0.00%   0 ATM OAM TIMER    
 150           0           1          0  0.00%  0.00%  0.00%   0 SSS Manager      
 151           0           1          0  0.00%  0.00%  0.00%   0 SSS Policy Manag 
 152           0           1          0  0.00%  0.00%  0.00%   0 SSS Feature Mana 
 153       14728    17639595          0  0.00%  0.00%  0.00%   0 SSS Feature Time 
 154           0           1          0  0.00%  0.00%  0.00%   0 SSS PM SHIM QOS  
 155           0           1          0  0.00%  0.00%  0.00%   0 SG DPM           
 156           0           1          0  0.00%  0.00%  0.00%   0 Timer handler fo 
 157           0           1          0  0.00%  0.00%  0.00%   0 Prepaid response 
 158           0           1          0  0.00%  0.00%  0.00%   0 Timed Policy act 
 159           0           1          0  0.00%  0.00%  0.00%   0 AAA response han 
 160           0           1          0  0.00%  0.00%  0.00%   0 SG CMD HANDLER   
 161           0           2          0  0.00%  0.00%  0.00%   0 IP PORTBUNDLE    
 162         568     1102476          0  0.00%  0.00%  0.00%   0 IP Static Sessio 
 163           0           1          0  0.00%  0.00%  0.00%   0 RADIUS Proxy     
 164           0           1          0  0.00%  0.00%  0.00%   0 TC SIP           
 165           0           2          0  0.00%  0.00%  0.00%   0 Ethernet LMI     
 166           0           2          0  0.00%  0.00%  0.00%   0 Ethernet OAM Pro 
 167           0           2          0  0.00%  0.00%  0.00%   0 Ethernet CFM     
 168       18901    21579717          0  0.00%  0.00%  0.00%   0 Ethernet Timer C 
 169      459617   549835075          0  0.00%  0.00%  0.00%   0 Ethernet Msec Ti 
 170           0           1          0  0.00%  0.00%  0.00%   0 PPCP RP Stats Ba 
 171           0           1          0  0.00%  0.00%  0.00%   0 CCM              
 172           0           2          0  0.00%  0.00%  0.00%   0 CCM IPC flow con 
 173           0           1          0  0.00%  0.00%  0.00%   0 IMA PROC         
 174         159       75303          2  0.00%  0.00%  0.00%   0 Call Home Timer  
 175           0           2          0  0.00%  0.00%  0.00%   0 RG Faults Timer  
 176           0           1          0  0.00%  0.00%  0.00%   0 RG VP            
 177           0           2          0  0.00%  0.00%  0.00%   0 RG Protocol Time 
 178           0           2          0  0.00%  0.00%  0.00%   0 RG Transport Tim 
 179           0           1          0  0.00%  0.00%  0.00%   0 HDLC HA          
 180           1           1       1000  0.00%  0.00%  0.00%   0 SBC initializer  
 181           1           1       1000  0.00%  0.00%  0.00%   0 AC Switch        
 182           0           1          0  0.00%  0.00%  0.00%   0 FRR Background P 
 183         712      122614          5  0.00%  0.00%  0.00%   0 CEF background p 
 184           1           2        500  0.00%  0.00%  0.00%   0 fib_fib_bfd_sb e 
 185           0           1          0  0.00%  0.00%  0.00%   0 IP IRDP          
 186           0           3          0  0.00%  0.00%  0.00%   0 SNMP Timers      
 187           1           1       1000  0.00%  0.00%  0.00%   0 XDR background p 
 188           0           1          0  0.00%  0.00%  0.00%   0 XDR mcast        
 189           0           1          0  0.00%  0.00%  0.00%   0 LSD HA Proc      
 190           0           1          0  0.00%  0.00%  0.00%   0 IPC LC Message H 
 191           0           1          0  0.00%  0.00%  0.00%   0 XDR RP Ping Back 
 192         120       75300          1  0.00%  0.00%  0.00%   0 XDR RP backgroun 
 193           0           1          0  0.00%  0.00%  0.00%   0 XDR RP Test Back 
 194           0           2          0  0.00%  0.00%  0.00%   0 Routing Topology 
 195     2930176     6234656        469  0.07%  0.06%  0.04%   0 IP RIB Update    
 196         162       75322          2  0.00%  0.00%  0.00%   0 IP Background    
 197         898          54      16629  0.00%  0.00%  0.00%   0 IP Connected Rou 
 198        1952     4512932          0  0.00%  0.00%  0.00%   0 cdp init process 
 199           0           1          0  0.00%  0.00%  0.00%   0 IP Traceroute    
 200           0           1          0  0.00%  0.00%  0.00%   0 Socket Timers    
 201           0           3          0  0.00%  0.00%  0.00%   0 Flow Exporter Ti 
 202       27208     5937966          4  0.00%  0.00%  0.00%   0 TCP Timer        
 203          27          67        402  0.00%  0.00%  0.00%   0 TCP Protocols    
 204          21       15057          1  0.00%  0.00%  0.00%   0 HTTP CORE        
 205        3447          90      38300  0.00%  0.00%  0.00%   0 Collection proce 
 206           0           1          0  0.00%  0.00%  0.00%   0 CEF RP IPC Backg 
 207           0           5          0  0.00%  0.00%  0.00%   0 MFIB Master back 
 208           0           2          0  0.00%  0.00%  0.00%   0 Multicast Offloa 
 209        3593     2562022          1  0.00%  0.00%  0.00%   0 CEF: IPv4 proces 
 210           0           7          0  0.00%  0.00%  0.00%   0 ADJ background   
 211           0           2          0  0.00%  0.00%  0.00%   0 static           
 212           0           1          0  0.00%  0.00%  0.00%   0 MFI Comm RP Proc 
 213           0           1          0  0.00%  0.00%  0.00%   0 Path set broker  
 214           0           1          0  0.00%  0.00%  0.00%   0 LDP HA           
 215           0           2          0  0.00%  0.00%  0.00%   0 MPLS VPN HA Clie 
 216           0           1          0  0.00%  0.00%  0.00%   0 RSVP HA Services 
 217           0           2          0  0.00%  0.00%  0.00%   0 TSPTUN HA        
 218           0           4          0  0.00%  0.00%  0.00%   0 Inter Chassis Pr 
 219           0           2          0  0.00%  0.00%  0.00%   0 LFDp Input Proc  
 220        3956      451575          8  0.00%  0.00%  0.00%   0 QoS stats proces 
 221           1           2        500  0.00%  0.00%  0.00%   0 SCTP Main Proces 
 222           0           2          0  0.00%  0.00%  0.00%   0 PPP Compress Inp 
 223           0           2          0  0.00%  0.00%  0.00%   0 PPP Compress Res 
 224           0           1          0  0.00%  0.00%  0.00%   0 COPS             
 225           0           2          0  0.00%  0.00%  0.00%   0 Dialer Forwarder 
 226           2          46         43  0.00%  0.00%  0.00%   0 RARP Input       
 227           0           2          0  0.00%  0.00%  0.00%   0 PPP NBF          
 228        3570     4519154          0  0.00%  0.00%  0.00%   0 PfR BR Learn     
 229           0           1          0  0.00%  0.00%  0.00%   0 PAD InCall       
 230           0           2          0  0.00%  0.00%  0.00%   0 X.25 Background  
 231           0           1          0  0.00%  0.00%  0.00%   0 X.25 Encaps Mana 
 232       34212    44873717          0  0.00%  0.00%  0.00%   0 RBSCP Background 
 233           0           1          0  0.00%  0.00%  0.00%   0 VPDN call manage 
 234           0           1          0  0.00%  0.00%  0.00%   0 XC RIB MGR       
 235           0           2          0  0.00%  0.00%  0.00%   0 IP Inband Sessio 
 236       20684     1102476         18  0.00%  0.00%  0.00%   0 IP SIP Process   
 237           0           2          0  0.00%  0.00%  0.00%   0 EFP Errd         
 238           0           2          0  0.00%  0.00%  0.00%   0 Ether Infra RP   
 239           0           2          0  0.00%  0.00%  0.00%   0 ECFM HA IPC flow 
 240           0           1          0  0.00%  0.00%  0.00%   0 IGMPSN L2MCM     
 241           0           1          0  0.00%  0.00%  0.00%   0 IGMPSN MRD       
 242           0           1          0  0.00%  0.00%  0.00%   0 IGMPSN           
 243           0           1          0  0.00%  0.00%  0.00%   0 TCP HA PROC      
 244           0           1          0  0.00%  0.00%  0.00%   0 BGP HA SSO       
 245           0           1          0  0.00%  0.00%  0.00%   0 RETRY_REPOPULATE 
 246           0           2          0  0.00%  0.00%  0.00%   0 XDR FOF process  
 247           0           1          0  0.00%  0.00%  0.00%   0 AAA HA           
 248           0           1          0  0.00%  0.00%  0.00%   0 ac_atm_state_eve 
 249           0           1          0  0.00%  0.00%  0.00%   0 ATM HA           
 250           0           2          0  0.00%  0.00%  0.00%   0 ATM HA IPC flow  
 251           0           1          0  0.00%  0.00%  0.00%   0 ATM HA AC        
 252           0           1          0  0.00%  0.00%  0.00%   0 BFD HA           
 253           0           1          0  0.00%  0.00%  0.00%   0 FR HA            
 254           0           2          0  0.00%  0.00%  0.00%   0 GLBP HA          
 255           0           1          0  0.00%  0.00%  0.00%   0 Probe Input      
 256           1           2        500  0.00%  0.00%  0.00%   0 HSRP HA          
 257        6401     8807480          0  0.00%  0.00%  0.00%   0 Inspect process  
 258           0           1          0  0.00%  0.00%  0.00%   0 LACP Protocol    
 259           0           1          0  0.00%  0.00%  0.00%   0 MRIB RP Proxy    
 260           0           1          0  0.00%  0.00%  0.00%   0 IPv6 ACL RP Proc 
 261           0           2          0  0.00%  0.00%  0.00%   0 Netsync IPC flow 
 262           0           2          0  0.00%  0.00%  0.00%   0 PPPoE VRRS EVT M 
 263           0           2          0  0.00%  0.00%  0.00%   0 RG Media Timer   
 264           2           4        500  0.00%  0.00%  0.00%   0 MCPRP RG Timer   
 265           0           2          0  0.00%  0.00%  0.00%   0 URL filter proc  
 266           0           1          0  0.00%  0.00%  0.00%   0 VPDN CCM Backgro 
 267           0           2          0  0.00%  0.00%  0.00%   0 VRRP HA          
 268           0           2          0  0.00%  0.00%  0.00%   0 VTEMPLATE IPC fl 
 269           0           1          0  0.00%  0.00%  0.00%   0 SBC Msg Ack Time 
 270           0           2          0  0.00%  0.00%  0.00%   0 L2X Switching Ev 
 271           0           2          0  0.00%  0.00%  0.00%   0 AAA Cached Serve 
 272           0           1          0  0.00%  0.00%  0.00%   0 EM Background Pr 
 273           0           1          0  0.00%  0.00%  0.00%   0 IDMGR CORE       
 274           7          99         70  0.00%  0.00%  0.00%   0 LOCAL AAA        
 275           0           2          0  0.00%  0.00%  0.00%   0 MPLS Auto Mesh P 
 276     1590069    13032491        122  0.07%  0.03%  0.02%   0 BGP I/O          
 277           0           2          0  0.00%  0.00%  0.00%   0 ENABLE AAA       
 278           0           2          0  0.00%  0.00%  0.00%   0 LINE AAA         
 279           0           2          0  0.00%  0.00%  0.00%   0 TPLUS            
 280           3         147         20  0.00%  0.00%  0.00%   0 DynCmd Package P 
 281           1           2        500  0.00%  0.00%  0.00%   0 FLEX DSPRM MAIN  
 282           0           2          0  0.00%  0.00%  0.00%   0 VSP_MGR          
 283           1           2        500  0.00%  0.00%  0.00%   0 STUN_APP         
 284           0           1          0  0.00%  0.00%  0.00%   0 STUN_TEST        
 285           1           1       1000  0.00%  0.00%  0.00%   0 QOS_MODULE_MAIN  
 286           0           1          0  0.00%  0.00%  0.00%   0 VoIP AAA         
 287           0           1          0  0.00%  0.00%  0.00%   0 QOS PERUSER      
 288           0           2          0  0.00%  0.00%  0.00%   0 PIM HA           
 289           0           1          0  0.00%  0.00%  0.00%   0 RPMS_PROC_MAIN   
 290           1           1       1000  0.00%  0.00%  0.00%   0 http client proc 
 291       67685     1829590         36  0.00%  0.00%  0.00%   0 DiagCard1/-1     
 292           6          66         90  0.00%  0.00%  0.00%   0 AAA SEND STOP EV 
 293           0           1          0  0.00%  0.00%  0.00%   0 Test AAA Client  
 294           0           2          0  0.00%  0.00%  0.00%   0 EEM ED Routing   
 295           0           2          0  0.00%  0.00%  0.00%   0 EEM ED Track     
 296           0           3          0  0.00%  0.00%  0.00%   0 EEM ED Resource  
 297           0           1          0  0.00%  0.00%  0.00%   0 Syslog Traps     
 299           0           1          0  0.00%  0.00%  0.00%   0 DATA Transfer Pr 
 300           0           1          0  0.00%  0.00%  0.00%   0 DATA Collector   
 301           0           1          0  0.00%  0.00%  0.00%   0 SONET Traps      
 302       96394     5150802         18  0.00%  0.00%  0.00%   0 OSPF-110 Router  
 303           0           1          0  0.00%  0.00%  0.00%   0 Online Diag EEM  
 304      180567      828101        218  0.00%  0.00%  0.00%   0 SPA ENTITY Proce 
 305           6         153         39  0.00%  0.00%  0.00%   0 EEM Server       
 306           3           2       1500  0.00%  0.00%  0.00%   0 Call Home proces 
 307           1           2        500  0.00%  0.00%  0.00%   0 EEM Policy Direc 
 308           0           3          0  0.00%  0.00%  0.00%   0 EEM ED CLI       
 309           0           3          0  0.00%  0.00%  0.00%   0 EEM ED Counter   
 310           0           3          0  0.00%  0.00%  0.00%   0 EEM ED Interface 
 311           0           3          0  0.00%  0.00%  0.00%   0 EEM ED IOSWD     
 312           0           3          0  0.00%  0.00%  0.00%   0 EEM ED None      
 313           0           3          0  0.00%  0.00%  0.00%   0 EEM ED OIR       
 314           0           2          0  0.00%  0.00%  0.00%   0 EEM ED RF        
 315           1           3        333  0.00%  0.00%  0.00%   0 EEM ED SNMP      
 316           0           2          0  0.00%  0.00%  0.00%   0 EEM ED SNMP Noti 
 317         125      112901          1  0.00%  0.00%  0.00%   0 EEM ED Timer     
 318           0           3          0  0.00%  0.00%  0.00%   0 EEM ED Test      
 319           0           3          0  0.00%  0.00%  0.00%   0 EEM ED Config    
 320           0           3          0  0.00%  0.00%  0.00%   0 EEM ED Env       
 321           0           3          0  0.00%  0.00%  0.00%   0 EM ED GOLD       
 322           1           2        500  0.00%  0.00%  0.00%   0 EEM ED Nf        
 323           0           3          0  0.00%  0.00%  0.00%   0 EEM ED Ipsla     
 324          83        4711         17  0.00%  0.00%  0.00%   0 Syslog           
 325         763      903039          0  0.00%  0.00%  0.00%   0 VDC process      
 326           0           1          0  0.00%  0.00%  0.00%   0 IP SLAs Ethernet 
 327           0           1          0  0.00%  0.00%  0.00%   0 ISSU Utility Pro 
 328           0           1          0  0.00%  0.00%  0.00%   0 Online Diag CNS  
 329           0           1          0  0.00%  0.00%  0.00%   0 Online Diag CNS  
 330           0           2          0  0.00%  0.00%  0.00%   0 DiagCard2/-1     
 331           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 332           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 333           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 334           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 335           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 336           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 337           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 338           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 339           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 340           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 341           1           1       1000  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 342           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 343           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 344           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 345           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 346           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 347           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 348           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 349           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 350           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 351           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 352           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 353           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 354           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 355           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 356           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 357           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 358           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 359           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 360           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 361           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 362           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 363           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 364           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 365           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 366           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 367           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 368           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 369           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 370           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 371           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 372           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 373           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 374           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 375           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 376           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 377           0           2          0  0.00%  0.00%  0.00%   0 DiagCard3/-1     
 378           0           2          0  0.00%  0.00%  0.00%   0 DiagCard4/-1     
 379           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 380           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 381           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 382           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 383           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 384           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 385           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 386           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 387           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 388           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 389           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 390           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 391           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 392           0           1          0  0.00%  0.00%  0.00%   0 IPC ISSU Version 
 393           1           4        250  0.00%  0.00%  0.00%   0 CWAN OIR IPC Rea 
 394       15699     9019928          1  0.00%  0.00%  0.00%   0 SBC main process 
 395           0           2          0  0.00%  0.00%  0.00%   0 MRIB Process     
 397     3759360    17527739        214  0.00%  0.08%  0.08%   0 BGP Router       
 398    46550655     1001264      46491  0.00%  0.79%  1.08%   0 BGP Scanner      
 399     1038660     6413117        161  0.07%  0.01%  0.00%   0 BGP Task         
 400           1          15         66  0.00%  0.00%  0.00%   0 TCP Listener     
 401      339768     4261945         79  0.00%  0.00%  0.00%   0 IP SNMP          
 402       85812     2056231         41  0.00%  0.00%  0.00%   0 PDU DISPATCHER   
 403      406898     2057324        197  0.00%  0.00%  0.00%   0 SNMP ENGINE      
 404           0           2          0  0.00%  0.00%  0.00%   0 IP SNMPV6        
 405           0           1          0  0.00%  0.00%  0.00%   0 SNMP ConfCopyPro 
 406       54866       77597        707  0.00%  0.00%  0.00%   0 SNMP Traps       
 407           0           1          0  0.00%  0.00%  0.00%   0 MPLS MIB traps   
 408        9317     4589836          2  0.00%  0.00%  0.00%   0 NTP              
 409           0           1          0  0.00%  0.00%  0.00%   0 IFCOM Msg Hdlr   
 410           0           1          0  0.00%  0.00%  0.00%   0 IFCOM Msg Hdlr   
 411           0           1          0  0.00%  0.00%  0.00%   0 IFCOM Msg Hdlr   
 412      203395     4885171         41  0.00%  0.00%  0.00%   0 OSPF-110 Hello   
 413         574          14      41000  0.00%  0.00%  0.00%   0 BGP Event        
 414         373       19820         18  0.00%  0.00%  0.00%   0 Ether-SPA backgr

------------------ show process cpu history ------------------

                                                                  
                                                                  
                                                                  
                                   11111                    11111 
      1111          11111          00000                    44444 
  100                                                           
   90                                                           
   80                                                           
   70                                                           
   60                                                           
   50                                                           
   40                                                           
   30                                                           
   20                                                           
   10                              *****                    ****
     0....5....1....1....2....2....3....3....4....4....5....5....6
               0    5    0    5    0    5    0    5    0    5    0
               CPU% per second (last 60 seconds)

                                                                  
                                                                  
                                                                  
      1211 111111111111111111111111111111 111111111221111121111111
      484393333333233333303334330033333337333332303223830363334134
  100                                                           
   90                                                           
   80                                                           
   70                                                           
   60                                                           
   50                                                           
   40                                                           
   30  *                                                  *     
   20  *                                           ** *   *     
   10 **********************************************************
     0....5....1....1....2....2....3....3....4....4....5....5....6
               0    5    0    5    0    5    0    5    0    5    0
               CPU% per minute (last 60 minutes)
              * = maximum CPU%   # = average CPU%

                                                                              
                                                                              
                                                                              
      212222223222232222222222222222222322222222222222222222223232222223221222
      676676625266646266666466765576376666647666746662660666646256736663669666
  100                                                                       
   90                                                                       
   80                                                                       
   70                                                                       
   60                                                                       
   50                                                                       
   40         *                        *                      * *           
   30 * ***** * ***** ***** ******** ****** ***** *** ** **** * *** ****** *
   20 **********************************************************************
   10 **********************************************************************
     0....5....1....1....2....2....3....3....4....4....5....5....6....6....7..
               0    5    0    5    0    5    0    5    0    5    0    5    0  
                   CPU% per hour (last 72 hours)
                  * = maximum CPU%   # = average CPU%



------------------ show file systems ------------------


File Systems:

       Size(b)       Free(b)      Type  Flags  Prefixes
             -             -    opaque     rw   system:
             -             -    opaque     rw   tmpsys:
*    945377280     580759552      disk     rw   bootflash: flash:
    2823929856    1962762240      disk     ro   fpd:
   39313059840   36030201856      disk     rw   harddisk:
       2097152       1593344      disk     rw   obfl:
             -             -    opaque     rw   null:
             -             -    opaque     ro   tar:
             -             -   network     rw   tftp:
             -             -    opaque     wo   syslog:
      33554432      33535931     nvram     rw   nvram:
             -             -   network     rw   rcp:
             -             -   network     rw   ftp:
             -             -   network     rw   http:
             -             -    opaque     ro   cns:


------------------ show file descriptors ------------------


File Descriptors:

  No open file descriptors


------------------ show bootflash: all ------------------


-#- --length-- ---------date/time--------- path
  1       4096 Oct 01 2014 14:52:07 +00:00 /bootflash/
  2      16384 Jan 11 2011 00:16:07 +00:00 /bootflash/lost+found
  3  285776176 Jan 11 2011 00:17:40 +00:00 /bootflash/asr1000rp1-advipservices.03.02.00.S.151-1.S.bin
  4       4096 Jan 11 2011 00:17:45 +00:00 /bootflash/.installer
  5       4096 Nov 20 2013 11:06:09 +00:00 /bootflash/.prst_sync
  6       4096 Jan 11 2011 00:47:34 +00:00 /bootflash/.rollback_timer
  7     334511 Apr 30 2012 21:30:28 +00:00 /bootflash/crashinfo_RP_00_00_20120430-213027-MSK
  8     381528 Aug 12 2012 08:08:45 +00:00 /bootflash/crashinfo_RP_00_00_20120812-080844-MSK
  9     309314 Sep 25 2012 07:26:49 +00:00 /bootflash/crashinfo_RP_00_00_20120925-072648-MSK
 10     307029 Oct 28 2012 00:57:09 +00:00 /bootflash/crashinfo_RP_00_00_20121028-005708-MSK
 11     341291 Nov 06 2012 21:54:20 +00:00 /bootflash/crashinfo_RP_00_00_20121106-215418-MSK
 12     399835 Nov 14 2012 14:47:13 +00:00 /bootflash/crashinfo_RP_00_00_20121114-144712-MSK
 13     327043 Dec 02 2012 01:23:57 +00:00 /bootflash/crashinfo_RP_00_00_20121202-012356-MSK
 14     328991 Dec 04 2012 00:19:21 +00:00 /bootflash/crashinfo_RP_00_00_20121204-001920-MSK
 15     340963 Dec 08 2012 07:26:56 +00:00 /bootflash/crashinfo_RP_00_00_20121208-072655-MSK
 16     326629 Dec 09 2012 18:08:48 +00:00 /bootflash/crashinfo_RP_00_00_20121209-180847-MSK
 17     341911 Jan 22 2013 22:19:32 +00:00 /bootflash/crashinfo_RP_00_00_20130122-221931-MSK
 18     332035 Jan 23 2013 23:17:18 +00:00 /bootflash/crashinfo_RP_00_00_20130123-231717-MSK
 19     290172 Feb 06 2013 18:05:55 +00:00 /bootflash/crashinfo_RP_00_00_20130206-180554-MSK
 20     341923 Feb 14 2013 05:43:31 +00:00 /bootflash/crashinfo_RP_00_00_20130214-054329-MSK
 21     315238 Mar 28 2013 22:23:38 +00:00 /bootflash/crashinfo_RP_00_00_20130328-222336-MSK
 22     361216 Mar 29 2013 08:55:40 +00:00 /bootflash/crashinfo_RP_00_00_20130329-085539-MSK
 23     340641 Mar 31 2013 21:36:25 +00:00 /bootflash/crashinfo_RP_00_00_20130331-213624-MSK
 24     340801 Apr 03 2013 21:58:59 +00:00 /bootflash/crashinfo_RP_00_00_20130403-215858-MSK
 25     333461 Apr 05 2013 20:39:41 +00:00 /bootflash/crashinfo_RP_00_00_20130405-203940-MSK
 26     321728 Apr 10 2013 22:35:49 +00:00 /bootflash/crashinfo_RP_00_00_20130410-223547-MSK
 27     289073 Apr 15 2013 23:53:09 +00:00 /bootflash/crashinfo_RP_00_00_20130415-235307-MSK
 28     301595 Apr 26 2013 04:05:50 +00:00 /bootflash/crashinfo_RP_00_00_20130426-040548-MSK
 29     291864 May 03 2013 12:27:44 +00:00 /bootflash/crashinfo_RP_00_00_20130503-122742-MSK
 30     331642 May 04 2013 07:13:50 +00:00 /bootflash/crashinfo_RP_00_00_20130504-071349-MSK
 31     307251 May 09 2013 09:08:21 +00:00 /bootflash/crashinfo_RP_00_00_20130509-090819-MSK
 32     312839 May 13 2013 18:34:19 +00:00 /bootflash/crashinfo_RP_00_00_20130513-183417-MSK
 33     332123 May 27 2013 22:41:22 +00:00 /bootflash/crashinfo_RP_00_00_20130527-224120-MSK
 34     386411 May 31 2013 07:11:29 +00:00 /bootflash/crashinfo_RP_00_00_20130531-071127-MSK
 35   15644134 Jun 20 2013 17:04:56 +00:00 /bootflash/tftp
 36     327786 Jun 22 2013 22:58:34 +00:00 /bootflash/crashinfo_RP_00_00_20130622-225832-MSK
 37     305594 Jun 27 2013 09:34:45 +00:00 /bootflash/crashinfo_RP_00_00_20130627-093443-MSK
 38     347820 Jul 22 2013 19:14:11 +00:00 /bootflash/crashinfo_RP_00_00_20130722-191410-MSK
 39     328226 Jul 24 2013 22:17:56 +00:00 /bootflash/crashinfo_RP_00_00_20130724-221754-MSK
 40     301604 Jul 25 2013 01:19:48 +00:00 /bootflash/crashinfo_RP_00_00_20130725-011946-MSK
 41     291175 Jul 27 2013 13:01:53 +00:00 /bootflash/crashinfo_RP_00_00_20130727-130151-MSK
 42     332964 Jul 30 2013 08:19:11 +00:00 /bootflash/crashinfo_RP_00_00_20130730-081910-MSK
 43     314708 Aug 06 2013 14:54:09 +00:00 /bootflash/crashinfo_RP_00_00_20130806-145407-MSK
 44     376316 Aug 21 2013 00:36:43 +00:00 /bootflash/crashinfo_RP_00_00_20130821-003642-MSK
 45     350084 Aug 22 2013 23:02:26 +00:00 /bootflash/crashinfo_RP_00_00_20130822-230225-MSK
 46     325856 Sep 07 2013 08:30:58 +00:00 /bootflash/crashinfo_RP_00_00_20130907-083056-MSK
 47     348765 Sep 11 2013 00:32:36 +00:00 /bootflash/crashinfo_RP_00_00_20130911-003235-MSK
 48     340829 Sep 16 2013 20:47:23 +00:00 /bootflash/crashinfo_RP_00_00_20130916-204721-MSK
 49     332228 Sep 17 2013 21:29:57 +00:00 /bootflash/crashinfo_RP_00_00_20130917-212955-MSK
 50     327834 Sep 18 2013 00:06:18 +00:00 /bootflash/crashinfo_RP_00_00_20130918-000616-MSK
 51     329649 Sep 23 2013 05:07:44 +00:00 /bootflash/crashinfo_RP_00_00_20130923-050742-MSK

580759552 bytes available (316596224 bytes used)

Filesystem: bootflash
Filesystem Path: /bootflash
Filesystem Type: ext2
Mounted: Read/Write


------------------ show fpd: all ------------------

Error: fpd filesystem does not exist


------------------ show harddisk: all ------------------


-#- --length-- ---------date/time--------- path
  1       4096 Jan 11 2011 00:49:49 +00:00 /harddisk/
  2      16384 Jan 11 2011 00:38:31 +00:00 /harddisk/lost+found
  3      20480 Oct 01 2014 14:52:07 +00:00 /harddisk/tracelogs
  4        449 Oct 01 2014 14:26:51 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.607.20141001142651
  5       1031 Oct 01 2014 14:16:45 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.27613.20141001141645
  6       1030 Oct 01 2014 14:41:58 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.4765.20141001144158
  7       1029 Oct 01 2014 14:31:52 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.995.20141001143152
  8       1030 Oct 01 2014 14:52:03 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.8650.20141001145203
  9       1031 Oct 01 2014 13:56:35 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.19955.20141001135635
 10       1031 Oct 01 2014 14:06:40 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.23878.20141001140640
 11        450 Oct 01 2014 14:31:53 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.2414.20141001143153
 12        451 Oct 01 2014 14:52:06 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.10246.20141001145206
 13        451 Oct 01 2014 14:16:46 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.29213.20141001141646
 14       1030 Oct 01 2014 14:36:55 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.2786.20141001143655
 15        450 Oct 01 2014 14:41:59 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.6364.20141001144159
 16        451 Oct 01 2014 13:46:31 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.17669.20141001134631
 17        451 Oct 01 2014 13:56:36 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.21560.20141001135636
 18        450 Oct 01 2014 14:36:56 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.4341.20141001143656
 19       1030 Oct 01 2014 14:47:00 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.6729.20141001144700
 20       1031 Oct 01 2014 14:01:38 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.21931.20141001140138
 21        450 Oct 01 2014 14:47:02 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.8285.20141001144702
 22        451 Oct 01 2014 14:01:39 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.23505.20141001140139
 23        451 Oct 01 2014 14:06:41 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.25312.20141001140641
 24       1031 Oct 01 2014 13:51:33 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.18035.20141001135133
 25        451 Oct 01 2014 13:51:34 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.19590.20141001135134
 26       1031 Oct 01 2014 14:11:42 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.25678.20141001141142
 27        451 Oct 01 2014 14:11:44 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.27247.20141001141144
 28       1031 Oct 01 2014 14:21:47 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.29580.20141001142147
 29        451 Oct 01 2014 14:21:49 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.31135.20141001142149
 30       1031 Oct 01 2014 14:26:50 +00:00 /harddisk/tracelogs/inst_cleanup_R0-0.log.31500.20141001142650
 31       4096 Sep 23 2013 05:09:41 +00:00 /harddisk/core
 32   35418046 Sep 23 2013 05:09:41 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25436.core.gz
 33   35150021 Aug 12 2012 08:10:48 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25447.core.gz
 34   50145295 Jul 22 2013 19:16:32 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25451.core.gz
 35   36521960 Nov 06 2012 21:56:20 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25437.core.gz
 36   33843934 Nov 14 2012 14:49:12 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25423.core.gz
 37   34628722 Dec 02 2012 01:25:54 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25419.core.gz
 38   33099445 Dec 04 2012 00:21:17 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25442.core.gz
 39   31882431 Dec 08 2012 07:28:49 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25462.core.gz
 40   34080346 Dec 09 2012 18:10:50 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25452.core.gz
 41   42720427 Apr 05 2013 20:41:48 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25455.core.gz
 42   39620349 Sep 17 2013 21:32:03 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25438.core.gz
 43   38225645 Feb 06 2013 18:07:58 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25420.core.gz
 44   33739037 Feb 14 2013 05:45:29 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25426.core.gz
 45   38173360 Sep 11 2013 00:34:38 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25450.core.gz
 46   43577027 May 13 2013 18:36:28 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25440.core.gz
 47   44177267 Mar 31 2013 21:38:37 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25432.core.gz
 48   44206717 Apr 03 2013 22:01:10 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25429.core.gz
 49   37719453 Jul 25 2013 01:21:51 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25456.core.gz
 50   41102100 Apr 15 2013 23:55:16 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25446.core.gz
 51   40185414 Apr 26 2013 04:07:53 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25415.core.gz
 52   43822206 May 03 2013 12:29:54 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25443.core.gz
 53   36675300 May 04 2013 07:15:49 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25441.core.gz
 54   41567993 May 09 2013 09:10:27 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25445.core.gz
 55   49776372 May 27 2013 22:43:40 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25448.core.gz
 56   40286777 May 31 2013 07:13:32 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25463.core.gz
 57   48795969 Jun 22 2013 23:00:50 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25466.core.gz
 58   48169057 Aug 21 2013 00:38:58 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25422.core.gz
 59   45011169 Jul 24 2013 22:20:07 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25459.core.gz
 60   40628556 Jul 30 2013 08:21:15 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25405.core.gz
 61   44548858 Aug 22 2013 23:04:36 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25449.core.gz
 62   42438271 Sep 16 2013 20:49:30 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25468.core.gz
 63   34230118 Sep 18 2013 00:08:17 +00:00 /harddisk/core/ctd-c5-ISG_RP_0_linux_iosd-imag_25470.core.gz
 64          0 Oct 01 2014 14:53:36 +00:00 /harddisk/foo.bar

36030201856 bytes available (1285828608 bytes used)

Filesystem: harddisk
Filesystem Path: /harddisk
Filesystem Type: ext2
Mounted: Read/Write


------------------ show obfl: all ------------------


-#- --length-- ---------date/time--------- path
  1          0 Jan 01 1970 04:00:00 +00:00 /obfl/
  2      18864 Aug 10 2014 08:33:42 +00:00 /obfl/obfl_temp.log
  3       2480 Aug 10 2014 08:30:02 +00:00 /obfl/obfl_uptime.log
  4      16848 Aug 10 2014 08:33:42 +00:00 /obfl/obfl_volt.log
  5      36036 Jul 25 2013 01:27:26 +00:00 /obfl/obfl_volt.log.lastlog

1593344 bytes available (503808 bytes used)

Filesystem: obfl
Filesystem Path: /obfl
Filesystem Type: jffs2
Mounted: Read/Write


------------------ dir nvram: ------------------


Directory of nvram:/

32769  -rw-       15372                    <no date>  startup-config
32770  ----           5                    <no date>  private-config
32771  -rw-       15372                    <no date>  underlying-config
    1  ----         180                    <no date>  persistent-data
    2  -rw-         688                    <no date>  ifIndex-table
    3  -rw-          17                    <no date>  ecfm_ieee_mib

33554432 bytes total (33535931 bytes free)

------------------ show controllers t1 ------------------



------------------ show controllers e1 ------------------



------------------ show redundancy states ------------------

       my state = 13 -ACTIVE 
     peer state = 1  -DISABLED 
           Mode = Simplex
           Unit = Primary
        Unit ID = 48

Redundancy Mode (Operational) = Non-redundant
Redundancy Mode (Configured)  = Non-redundant
Redundancy State              = Non Redundant
    Manual Swact = disabled (system is simplex (no peer unit))
 Communications = Down      Reason: Simplex mode

   client count = 79
 client_notification_TMR = 30000 milliseconds
           RF debug mask = 0x0   


------------------ show ipc nodes ------------------

There are 64 nodes in this IPC realm.
   ID       Type               Name                             Last   Last    Bundle Support   MTU
                                                                Sent   Heard   Session/Seat
 0.10000    Local      IPC Master                               0      0       on/on              1450
 0.2000000  ICC        Card0                                    23     26      on/on              1500
 0.2010000  ICC        Card1                                    0      0       off/off             1500
 0.2020000  ICC        Card2                                    0      0       off/off             1500
 0.2030000  ICC        Card3                                    0      0       off/off             1500
 0.2040000  ICC        Card4                                    0      0       off/off             1500
 0.2050000  ICC        Card5                                    0      0       off/off             1500
 0.2070000  ICC        Card7                                    0      0       off/off             1500
 0.2080000  ICC        Card8                                    0      0       off/off             1500
 0.2090000  ICC        Card9                                    0      0       off/off             1500
 0.20A0000  ICC        Card10                                   0      0       off/off             1500
 0.20B0000  ICC        Card11                                   0      0       off/off             1500
 0.20C0000  ICC        Card12                                   0      0       off/off             1500
 0.20D0000  ICC        Card13                                   0      0       off/off             1500
 0.20E0000  ICC        Card14                                   0      0       off/off             1500
 0.20F0000  ICC        Card15                                   0      0       off/off             1500
 0.2100000  ICC        Card16                                   0      0       off/off             1500
 0.2110000  ICC        Card17                                   0      0       off/off             1500
 0.2120000  ICC        Card18                                   0      0       off/off             1500
 0.2130000  ICC        Card19                                   0      0       off/off             1500
 0.2140000  ICC        Card20                                   0      0       off/off             1500
 0.2150000  ICC        Card21                                   0      0       off/off             1500
 0.2160000  ICC        Card22                                   0      0       off/off             1500
 0.2170000  ICC        Card23                                   0      0       off/off             1500
 0.2180000  ICC        Card24                                   0      0       off/off             1500
 0.2190000  ICC        Card25                                   0      0       off/off             1500
 0.21A0000  ICC        Card26                                   0      0       off/off             1500
 0.21B0000  ICC        Card27                                   0      0       off/off             1500
 0.21C0000  ICC        Card28                                   0      0       off/off             1500
 0.21D0000  ICC        Card29                                   0      0       off/off             1500
 0.21E0000  ICC        Card30                                   0      0       off/off             1500
 0.21F0000  ICC        Card31                                   0      0       off/off             1500
 0.2200000  ICC        Card32                                   0      0       off/off             1500
 0.2210000  ICC        Card33                                   0      0       off/off             1500
 0.2220000  ICC        Card34                                   0      0       off/off             1500
 0.2230000  ICC        Card35                                   0      0       off/off             1500
 0.2240000  ICC        Card36                                   0      0       off/off             1500
 0.2250000  ICC        Card37                                   0      0       off/off             1500
 0.2260000  ICC        Card38                                   0      0       off/off             1500
 0.2270000  ICC        Card39                                   0      0       off/off             1500
 0.2280000  ICC        Card40                                   0      0       off/off             1500
 0.2290000  ICC        Card41                                   0      0       off/off             1500
 0.22A0000  ICC        Card42                                   0      0       off/off             1500
 0.22B0000  ICC        Card43                                   0      0       off/off             1500
 0.22C0000  ICC        Card44                                   0      0       off/off             1500
 0.22D0000  ICC        Card45                                   0      0       off/off             1500
 0.22E0000  ICC        Card46                                   0      0       off/off             1500
 0.22F0000  ICC        Card47                                   0      0       off/off             1500
 0.2300000  ICC        Card48                                   23     26      on/on              1500
 0.2310000  ICC        Card49                                   23     26      on/on              1500
 0.2320000  ICC        Card50                                   0      0       off/off             1500
 0.2330000  ICC        Card51                                   0      0       off/off             1500
 0.2340000  ICC        Card52                                   0      0       off/off             1500
 0.2350000  ICC        Card53                                   0      0       off/off             1500
 0.2360000  ICC        Card54                                   0      0       off/off             1500
 0.2370000  ICC        Card55                                   0      0       off/off             1500
 0.2380000  ICC        Card56                                   0      0       off/off             1500
 0.2390000  ICC        Card57                                   0      0       off/off             1500
 0.23A0000  ICC        Card58                                   0      0       off/off             1500
 0.23B0000  ICC        Card59                                   0      0       off/off             1500
 0.23C0000  ICC        Card60                                   0      0       off/off             1500
 0.23D0000  ICC        Card61                                   0      0       off/off             1500
 0.23E0000  ICC        Card62                                   0      0       off/off             1500
 0.23F0000  ICC        Card63                                   0      0       off/off             1500


------------------ show ipc ports ------------------

                             IPC ACTIVE PORT TABLE
There are 54 ports defined.

Port ID        Type       Name                    (current/peak/total)
   10000.1     unicast               IPC Master:Zone                      
   10000.2     unicast               IPC Master:Echo                      
  port_index = 0  seat_id = 0x2300000 last sent = 0     last heard = 28465
     rcv pending/peak/total       = 0/1/451573
     stateful_mode = 0     peer_port = 0,    peer_seat = 0
     seq-window size              = 128   number of messages in window = 0    
     maximum out-of-seq received  = 0     maximum pending in window    = 0    
     number of messages dropped   = 0     number of window resets      = 29892
     rcv bundling related msgs bdl/sub/nonbdl/err = 0/0/451573/0
  port_index = 1  seat_id = 0x2310000 last sent = 0     last heard = 28561
     rcv pending/peak/total       = 0/1/451573
     stateful_mode = 0     peer_port = 0,    peer_seat = 0
     seq-window size              = 128   number of messages in window = 0    
     maximum out-of-seq received  = 0     maximum pending in window    = 0    
     number of messages dropped   = 0     number of window resets      = 29796
     rcv bundling related msgs bdl/sub/nonbdl/err = 0/0/451573/0
  port_index = 2  seat_id = 0x2000000 last sent = 0     last heard = 28768
     rcv pending/peak/total       = 0/1/451573
     stateful_mode = 0     peer_port = 0,    peer_seat = 0
     seq-window size              = 128   number of messages in window = 0    
     maximum out-of-seq received  = 0     maximum pending in window    = 0    
     number of messages dropped   = 0     number of window resets      = 29589
     rcv bundling related msgs bdl/sub/nonbdl/err = 0/0/451573/0


   10000.3     multicast             IPC Master:Control                   
   10000.4     unicast               ERP Agent Port #0                    
   10000.5     unicast               ERP Agent Port #48                   
  port_index = 0  seat_id = 0x2000000 last sent = 0     last heard = 0    
     rcv pending/peak/total       = 0/0/0
     stateful_mode = 0     peer_port = 0,    peer_seat = 0
     seq-window size              = 128   number of messages in window = 0    
     maximum out-of-seq received  = 0     maximum pending in window    = 0    
     number of messages dropped   = 0     number of window resets      = 0    
     rcv bundling related msgs bdl/sub/nonbdl/err = 0/0/0/0
  port_index = 1  seat_id = 0x2300000 last sent = 0     last heard = 0    
     rcv pending/peak/total       = 0/0/0
     stateful_mode = 0     peer_port = 0,    peer_seat = 0
     seq-window size              = 128   number of messages in window = 0    
     maximum out-of-seq received  = 0     maximum pending in window    = 0    
     number of messages dropped   = 0     number of window resets      = 0    
     rcv bundling related msgs bdl/sub/nonbdl/err = 0/0/0/0
  port_index = 2  seat_id = 0x2310000 last sent = 0     last heard = 0    
     rcv pending/peak/total       = 0/0/0
     stateful_mode = 0     peer_port = 0,    peer_seat = 0
     seq-window size              = 128   number of messages in window = 0    
     maximum out-of-seq received  = 0     maximum pending in window    = 0    
     number of messages dropped   = 0     number of window resets      = 0    
     rcv bundling related msgs bdl/sub/nonbdl/err = 0/0/0/0


   10000.6     unicast               IPC-Apps:Active                      
   10000.7     unicast               RF : Active                          
   10000.8     unicast               ifindex_sync_active_port             
   10000.9     unicast               RED MODE: Active Port                
   10000.A     unicast               SBC IPC: Active Port                 
   10000.B     unicast               Config Sync ISSU nego active         
   10000.C     unicast               ISSU TEST::same port 0 0             
   10000.D     unicast               ISSU TEST::shared msg port 0 0       
   10000.E     unicast               ISSU TEST::same port 0 1             
   10000.F     unicast               ISSU TEST::shared msg port 0 1       
   10000.10    unicast               ISSU TEST::shared nego port 0 0      
   10000.11    unicast               CF : Active                          
   10000.12    unicast               Remote TTY Server Port               
   10000.13    unicast               RTTYEnh Master Port                  
  port_index = 0  seat_id = 0x2000000 last sent = 0     last heard = 0    
     rcv pending/peak/total       = 0/0/0
     stateful_mode = 0     peer_port = 0,    peer_seat = 0
     seq-window size              = 128   number of messages in window = 0    
     maximum out-of-seq received  = 0     maximum pending in window    = 0    
     number of messages dropped   = 0     number of window resets      = 0    
     rcv bundling related msgs bdl/sub/nonbdl/err = 0/0/0/0
  port_index = 1  seat_id = 0x2300000 last sent = 0     last heard = 0    
     rcv pending/peak/total       = 0/0/0
     stateful_mode = 0     peer_port = 0,    peer_seat = 0
     seq-window size              = 128   number of messages in window = 0    
     maximum out-of-seq received  = 0     maximum pending in window    = 0    
     number of messages dropped   = 0     number of window resets      = 0    
     rcv bundling related msgs bdl/sub/nonbdl/err = 0/0/0/0
  port_index = 2  seat_id = 0x2310000 last sent = 0     last heard = 0    
     rcv pending/peak/total       = 0/0/0
     stateful_mode = 0     peer_port = 0,    peer_seat = 0
     seq-window size              = 128   number of messages in window = 0    
     maximum out-of-seq received  = 0     maximum pending in window    = 0    
     number of messages dropped   = 0     number of window resets      = 0    
     rcv bundling related msgs bdl/sub/nonbdl/err = 0/0/0/0


   10000.14    unicast               FIB Master: DFS.process_level.msgs   
   10000.15    unicast               FIB Master: DFS.interrupt.msgs       
   10000.16    unicast               RP: MRIB.control.RIL                 
   10000.17    unicast               CWAN IPC Master:Init                 
   10000.18    unicast               RP: MFIB.RIL                         
   10000.19    unicast               IPC Master: Slot 0/0 ICP             
  port_index = 0  seat_id = 0x2000000 last sent = 0     last heard = 0    
     rcv pending/peak/total       = 0/0/0
     stateful_mode = 0     peer_port = 0,    peer_seat = 0
     seq-window size              = 128   number of messages in window = 0    
     maximum out-of-seq received  = 0     maximum pending in window    = 0    
     number of messages dropped   = 0     number of window resets      = 0    
     rcv bundling related msgs bdl/sub/nonbdl/err = 0/0/0/0


   10000.1A    unicast               IPC Master: Slot 0/3 ICP             
  port_index = 0  seat_id = 0x2300000 last sent = 0     last heard = 0    
     rcv pending/peak/total       = 0/0/0
     stateful_mode = 0     peer_port = 0,    peer_seat = 0
     seq-window size              = 128   number of messages in window = 0    
     maximum out-of-seq received  = 0     maximum pending in window    = 0    
     number of messages dropped   = 0     number of window resets      = 0    
     rcv bundling related msgs bdl/sub/nonbdl/err = 0/0/0/0


   10000.1B    unicast               IPC Master: Slot 1/3 ICP             
  port_index = 0  seat_id = 0x2310000 last sent = 0     last heard = 0    
     rcv pending/peak/total       = 0/0/0
     stateful_mode = 0     peer_port = 0,    peer_seat = 0
     seq-window size              = 128   number of messages in window = 0    
     maximum out-of-seq received  = 0     maximum pending in window    = 0    
     number of messages dropped   = 0     number of window resets      = 0    
     rcv bundling related msgs bdl/sub/nonbdl/err = 0/0/0/0


 2310000.3     multicast             Card49:Control                       
 2000000.3     multicast             Card0:Control                        
 2300000.3     multicast             Card48:Control                       
 2300000.2     unicast               Card48:Echo                          
 2000000.2     unicast               Card0:Echo                           
 2000000.5     unicast               ERP Agent Port #1024                 
 2300000.5     unicast               ERP Agent Port #1027                 
 2000000.A     unicast               Slot 0/0: ICP                        
 2300000.A     unicast               Slot 0/3: ICP                        
 2300000.B     unicast               RTTYEnh Client Port 02300000         
 2000000.B     unicast               RTTYEnh Client Port 02000000         
 2000000.8     unicast               Slot 0/0: Remote TTY Client Port     
 2000000.9     unicast               cwan0/0-bootflash                    
 2300000.8     unicast               Slot 0/3: Remote TTY Client Port     
 2300000.9     unicast               cwan0/3-bootflash                    
 2000000.6     unicast               Slot0: Console RPC Port              
 2000000.C     unicast               Remote TTY Test 02000000             
 2300000.6     unicast               Slot42: Console RPC Port             
 2300000.C     unicast               Remote TTY Test 02300000             
 2310000.2     unicast               Card49:Echo                          
 2310000.5     unicast               ERP Agent Port #2051                 
 2310000.A     unicast               Slot 1/3: ICP                        
 2310000.B     unicast               RTTYEnh Client Port 02310000         
 2310000.8     unicast               Slot 1/3: Remote TTY Client Port     
 2310000.9     unicast               cwan1/3-bootflash                    
 2310000.6     unicast               Slot43: Console RPC Port             
 2310000.C     unicast               Remote TTY Test 02310000             

RPC packets: current/peak/total
                                                            0/1/12
                            IPC STANDBY PORT TABLE
There are 0 ports defined.

Port ID        Type       Name                    (current/peak/total)

RPC packets: current/peak/total
                                                            0/1/12


------------------ show ipc queue ------------------

There are 0 IPC messages waiting for acknowledgement in the transmit queue.
There are 0 IPC messages waiting for a response.
There are 0 IPC messages waiting for additional fragments.
There are 0 IPC messages currently on the IPC inboundQ.
There are 0 IPC messages currently on the RX controller inboundQ.
There are 0 IPC messages currently on the TX controller inboundQ.
There are 0 IPC messages currently on the zone inboundQ.
Messages currently in use                     :         15
Message cache size                            :       1000
Maximum message cache usage                   :       1000

0  times message cache crossed       5000 [max]

Emergency messages currently in use           :          0

There are 15 messages currently reserved for reply msg.

Cache low watermark           [default/new]: [100/100]
         No of low watermark reached           :         0 
         Total get cache after low watermark   :         0 
         No of times zero cache reached        :         0 
         No of times one cache added           :         0 
         No of times cache chunk added         :         0 
         Max no of get cache between wake2grow :         0 


------------------ show ipc status ------------------



                            IPC System Status

 Time last IPC stat cleared all zones : 00:00:00

 This processor is the IPC master server in zone 0 (default).
 Do not drop output of IPC frames for test purposes.

 1000 IPC Message Headers Cached.

                                                    Rx Side     Tx Side

 Total Frames                                          2709630     2709596
 Total from Local Ports                                1354734     1354791
 Total Protocol Control Frames                              66           9
 Total Frames Dropped                                        1           0

                             Service Usage

 Total via Unreliable Connection-Less Service                0           0
 Total via Unreliable Sequenced Connection-Less Svc          0           0
 Total via Reliable Connection-Oriented Service        1354799     1354791
 Total Messages via Fragmentation                            0           3
 Total Fragments                                             0           6
 Total Internal IPC Messages                                35           0
 Total Messages Flushed                                      0           0

                      IPC Protocol Version 0

 Total Acknowledgements                                1354794     1354802
 Total Negative Acknowledgements                             0           0

                             Device Drivers

 Total via Local Driver                                      0           0
 Total via Platform Driver                             2709627     2709596
 Total Frames Dropped by Platform Drivers                    0           0
 Total Frames Sent when media is quiesced                                0

                     Reliable Tx Statistics

 Re-Transmission                                                         0
 Re-Tx Timeout                                                           0

          Rx Errors                              Tx Errors

 Unsupp IPC Proto Version          0  Tx Session Error                  0
 Corrupt Frame                     0  Tx Seat Error                     0
 Duplicate Frame                   1  Tx No Send Vector                 0
 Unrel Out-of-Seq Frame            0  Tx Driver Failed                  0
 Rx IPC Transform Errors           0  Tx IPC Transform Errors           0
 Unable to Deliver Msg             0  Tx Test Drop                      0
 Rx Msg Callback Hog               0  Ack Alloc Failed                  0
 Rel Out-of-Seq Frame              1
 Dest Port does Not Exist          0
 Rx IPC Msg Alloc Failed           0
 Rx IPC Frag Dropped               0
 Rx Bootstrap Delivered            0
 Rx Bootstrap Dropped              0

          Buffer Errors                          Misc Errors

 IPC Msg Alloc                     0  IPC Open Port                     0
 Emer IPC Msg Alloc                0  No HWQ                            0
 IPC Frame PakType Alloc           0  Hardware Error                    0
 IPC Frame MemD Alloc              0  Invalid Messages                  0
                                      IPC Backup Open Port              0
                                      IPC Fragment Errors               0
                                      Message Timer Errors              0
                                      Messages no xmt pending flag      0

          Tx Driver Errors

 No Transport                      0
 MTU Failure                       0
 Dest does not Exist               0



          IPC Message Bundling Statistics

 Seat-level    Tx Bundling (bdl/sub/nonbdl/urgent/err)  0/0/1354794/0/0
 Seat-level    Rx Bundling (bdl/sub/nonbdl/err)         0/0/2709627/0
 Session-level Tx Bundling (bdl/sub/nonbdl/urgent/err)  0/0/1354791/72/0
 Session-level Rx Bundling (bdl/sub/nonbdl/err)         0/0/1354788/0



------------------ show hw-module all fpd ------------------



==== ====================== ====== =============================================
                             H/W   Field Programmable   Current   Min. Required
Slot Card Type               Ver.  Device: "ID-Name"    Version      Version
==== ====================== ====== ================== =========== ==============
 0/0 SPA-8X1GE-V2            1.1   1-GE I/O FPGA          1.10        1.10     
---- ---------------------- ------ ------------------ ----------- --------------
 0/3 SPA-1X10GE-L-V2         1.5   1-10GE I/O FPGA        1.9         1.9      
---- ---------------------- ------ ------------------ ----------- --------------
 1/3 SPA-1X10GE-L-V2         1.5   1-10GE I/O FPGA        1.9         1.9      
==== ====================== ====== =============================================

sh environment temperature

------------------ show hw-module subslot all sensors ------------------

SPA-8X1GE-V2[0/0] temperature sensor 0, reading: 25C
SPA-8X1GE-V2[0/0] temperature sensor 1, reading: 25C
SPA-8X1GE-V2[0/0] nominal: 3.300V, reading: 3.292V
SPA-8X1GE-V2[0/0] nominal: 2.500V, reading: 2.501V
SPA-8X1GE-V2[0/0] nominal: 1.500V, reading: 1.497V
SPA-8X1GE-V2[0/0] nominal: 1.200V, reading: 1.200V
SPA-1X10GE-L-V2[0/3] temperature sensor 0, reading: 25C
SPA-1X10GE-L-V2[0/3] temperature sensor 1, reading: 24C
SPA-1X10GE-L-V2[0/3] nominal: 3.300V, reading: 3.292V
SPA-1X10GE-L-V2[0/3] nominal: 2.500V, reading: 2.497V
SPA-1X10GE-L-V2[0/3] nominal: 1.500V, reading: 1.493V
SPA-1X10GE-L-V2[0/3] nominal: 1.200V, reading: 1.199V
SPA-1X10GE-L-V2[0/3] nominal: 1.800V, reading: 1.791V
SPA-1X10GE-L-V2[0/3] nominal: 1.200V, reading: 1.200V
SPA-1X10GE-L-V2[0/3] nominal: 1.800V, reading: 1.793V
SPA-1X10GE-L-V2[0/3] nominal: 5.000V, reading: 4.918V
SPA-1X10GE-L-V2[0/3] nominal: -5.200V, reading: -5.213V
SPA-1X10GE-L-V2[1/3] temperature sensor 0, reading: 25C
SPA-1X10GE-L-V2[1/3] temperature sensor 1, reading: 24C
SPA-1X10GE-L-V2[1/3] nominal: 3.300V, reading: 3.286V
SPA-1X10GE-L-V2[1/3] nominal: 2.500V, reading: 2.501V
SPA-1X10GE-L-V2[1/3] nominal: 1.500V, reading: 1.493V
SPA-1X10GE-L-V2[1/3] nominal: 1.200V, reading: 1.197V
SPA-1X10GE-L-V2[1/3] nominal: 1.800V, reading: 1.794V
SPA-1X10GE-L-V2[1/3] nominal: 1.200V, reading: 1.196V
SPA-1X10GE-L-V2[1/3] nominal: 1.800V, reading: 1.795V
SPA-1X10GE-L-V2[1/3] nominal: 5.000V, reading: 4.927V
SPA-1X10GE-L-V2[1/3] nominal: -5.200V, reading: -5.257V


------------------ show hw-module subslot all oir ------------------

Module        Model                Operational Status
------------- -------------------- ------------------------
subslot 0/0   SPA-8X1GE-V2         ok
subslot 0/3   SPA-1X10GE-L-V2      ok
subslot 1/3   SPA-1X10GE-L-V2      ok


------------------ show ip nbar version ------------------



NBAR software version:  8

1   base                 Mv: 4
2   ftp                  Mv: 4
3   http                 Mv: 17
      Iv:               kazaa2 - 11
      Iv:              youtube - 6
      Iv:                  msn - 2
      Iv:                yahoo - 2
      Iv:          flash-video - 2
      Iv:           flashyahoo - 2
      Iv:         flashmyspace - 2
      Iv:      audio-over-http - 2
      Iv:     binary-over-http - 2
      Iv:      video-over-http - 2
      Iv:                  irc - 1
      Iv:             babelgum - 1
      Iv:               itunes - 1
      Iv:                sling - 1
      Iv:         google-earth - 1
      Iv:          baidu-movie - 1
      Iv:                pando - 1
      Iv:              napster - 1
      Iv:             songsari - 1
      Iv:           webthunder - 1
      Iv:              sopcast - 3
      Iv:          tunnel-http - 1
      Iv:             soribada - 2
4   static               Mv: 6
5   netbios              Mv: 1
      Iv:                 cifs - 1
6   socks                Mv: 2
      Iv:                yahoo - 2
      Iv:                  msn - 2
      Iv:                  aim - 2
      Iv:           bittorrent - 5
7   nntp                 Mv: 2
      Iv:                yahoo - 2
8   tftp                 Mv: 2
9   exchange             Mv: 3
10  vdolive              Mv: 1
11  sqlnet               Mv: 2
12  netshow              Mv: 3
13  sunrpc               Mv: 3
14  streamwork           Mv: 2
15  citrix               Mv: 11
16  fasttrack            Mv: 3
17  gnutella             Mv: 7
18  kazaa2               Mv: 11
      Iv:                 http - 17
19  custom-protocols     Mv: 1
20  dhcp                 Mv: 1
21  rtsp                 Mv: 5
22  rtp                  Mv: 7
      Iv:   telepresence-media - 2
23  mgcp                 Mv: 2
24  skinny               Mv: 3
      Iv:          cisco-phone - 3
25  h323                 Mv: 1
26  sip                  Mv: 4
      Iv:          cisco-phone - 3
      Iv: telepresence-control - 2
27  rtcp                 Mv: 4
      Iv: telepresence-control - 2
      Iv:   telepresence-media - 2
28  edonkey              Mv: 6
29  winmx                Mv: 4
30  bittorrent           Mv: 5
      Iv:                socks - 2
      Iv:                  wow - 2
31  directconnect        Mv: 4
32  hl7                  Mv: 3
33  fix                  Mv: 2
34  msn                  Mv: 2
      Iv:                socks - 2
      Iv:                 http - 17
35  dicom                Mv: 3
36  yahoo                Mv: 2
      Iv:                socks - 2
      Iv:                 http - 17
      Iv:                 nntp - 2
37  mapi                 Mv: 2
38  aim                  Mv: 2
      Iv:                socks - 2
39  cifs                 Mv: 2
      Iv:              netbios - 1
      Iv:          microsoftds - 2
40  cisco-phone          Mv: 3
      Iv:                  sip - 4
      Iv:               skinny - 3
      Iv: telepresence-control - 2
41  youtube              Mv: 6
      Iv:                 http - 17
42  imap                 Mv: 1
43  pop3                 Mv: 1
44  irc                  Mv: 2
      Iv:                 http - 17
45  skype                Mv: 3
46  sap                  Mv: 1
47  wow                  Mv: 2
      Iv:           bittorrent - 5
48  microsoftds          Mv: 2
      Iv:                 cifs - 2
49  telepresence-media   Mv: 2
      Iv:                  rtp - 7
      Iv:                 rtcp - 4
50  telepresence-control Mv: 2
      Iv:                 rtcp - 4
      Iv:          cisco-phone - 3
      Iv:                  sip - 4
51  zattoo               Mv: 3
52  sopcast              Mv: 3
      Iv:                 http - 17
53  flash-video          Mv: 2
      Iv:                 http - 17
54  flashyahoo           Mv: 2
      Iv:                 http - 17
55  flashmyspace         Mv: 2
      Iv:                 http - 17
56  audio-over-http      Mv: 2
      Iv:                 http - 17
57  binary-over-http     Mv: 2
      Iv:                 http - 17
58  video-over-http      Mv: 2
      Iv:                 http - 17
59  my-jabber-ft         Mv: 1
60  ayiya-ipv6-tunneled  Mv: 1
61  filetopia            Mv: 1
62  guruguru             Mv: 1
63  manolito             Mv: 1
64  radius               Mv: 1
65  teamspeak            Mv: 1
66  soribada             Mv: 2
      Iv:                 http - 17
67  dht                  Mv: 1
68  pptp                 Mv: 1
69  ntp                  Mv: 1
70  poco                 Mv: 1
71  ventrilo             Mv: 1
72  tomatopang           Mv: 1
73  maplestory           Mv: 1
74  itunes               Mv: 1
      Iv:                 http - 17
75  napster              Mv: 1
      Iv:                 http - 17
76  sling                Mv: 1
      Iv:                 http - 17
77  google-earth         Mv: 1
      Iv:                 http - 17
78  baidu-movie          Mv: 1
      Iv:                 http - 17
79  pando                Mv: 1
      Iv:                 http - 17
80  webthunder           Mv: 1
      Iv:                 http - 17
81  babelgum             Mv: 1
      Iv:                 http - 17
82  songsari             Mv: 1
      Iv:                 http - 17
83  tunnel-http          Mv: 1
      Iv:                 http - 17
84  teredo-ipv6-tunneled Mv: 1
85  sixtofour-ipv6-tunne Mv: 1
      Iv: isatap-ipv6-tunneled - 1
86  isatap-ipv6-tunneled Mv: 1
      Iv: sixtofour-ipv6-tunne - 1
87  iana                 Mv: 1


{<No.>}<PDLM name> Mv: <PDLM Version>, {Nv: <NBAR Software Version>; <File name>}
            {Iv: <PDLM Interdependency Name>   - <PDLM Interdependency Version>}


------------------ show raw reclaimed ------------------



------------------ show inventory ------------------

NAME: "Chassis", DESCR: "Cisco ASR1004 Chassis"
PID: ASR1004           , VID: V02, SN: FOX1448H24Z

NAME: "module 0", DESCR: "Cisco ASR1000 SPA Interface Processor 10"
PID: ASR1000-SIP10     , VID: V07, SN: JAE15020J8W

NAME: "SPA subslot 0/0", DESCR: "8-port Gigabit Ethernet Shared Port Adapter"
PID: SPA-8X1GE-V2      , VID: V02, SN: JAE14480UII

NAME: "subslot 0/0 transceiver 1", DESCR: "GE LX"
PID: N/A                 , VID:    , SN: F3K6499         

NAME: "subslot 0/0 transceiver 2", DESCR: "GE SX"
PID: SFP-GE-S            , VID: 06  , SN: AGM1452P3GA     

NAME: "subslot 0/0 transceiver 3", DESCR: "GE LX"
PID: N/A                 , VID: A0  , SN: H1M8912         

NAME: "subslot 0/0 transceiver 4", DESCR: "GE LX"
PID: N/A                 , VID: A0  , SN: H1M8913         

NAME: "subslot 0/0 transceiver 7", DESCR: "1000BASE BX10-U"
PID: N/A                 , VID: 1.0 , SN: CLGU310319      

NAME: "SPA subslot 0/3", DESCR: "1-port 10 Gigabit Ethernet Shared Port Adapter XFP based"
PID: SPA-1X10GE-L-V2   , VID: V04, SN: SAL1740DSEP

NAME: "subslot 0/3 transceiver 0", DESCR: "OC192 + 10GBASE-L"
PID: XFP-10GLR-OC192SR   , VID: A  , SN: XE29670001      

NAME: "module 1", DESCR: "Cisco ASR1000 SPA Interface Processor 10"
PID: ASR1000-SIP10     , VID: V07, SN: JAE14350FBK

NAME: "SPA subslot 1/3", DESCR: "1-port 10 Gigabit Ethernet Shared Port Adapter XFP based"
PID: SPA-1X10GE-L-V2   , VID: V04, SN: SAL1730A7D1

NAME: "subslot 1/3 transceiver 0", DESCR: "OC192 + 10GBASE-E"
PID: XFP-10GER-192IR+    , VID: A  , SN: XD4G320001      

NAME: "module R0", DESCR: "Cisco ASR1000 Route Processor 1"
PID: ASR1000-RP1       , VID: V06, SN: JAE14530BQ2

NAME: "module F0", DESCR: "Cisco ASR1000 Embedded Services Processor, 10Gbps"
PID: ASR1000-ESP10     , VID: V05, SN: JAE15020EYZ

NAME: "Power Supply Module 0", DESCR: "Cisco ASR1004 AC Power Supply"
PID: ASR1004-PWR-AC    , VID: V02, SN: ART1449K039

NAME: "Power Supply Module 1", DESCR: "Cisco ASR1004 AC Power Supply"
PID: ASR1004-PWR-AC    , VID: V02, SN: ART1449K02Z



------------------ show region ------------------


Region Manager:

      Start         End     Size(b)  Class  Media  Name
 0x1009E7F4  0x14AE430F    77880092  IText  R/W    text
 0x15D5A078  0x1661AD3F     9178312  IData  R/W    data
 0x1661AD40  0x18342753    30571028  IBss   R/W    bss
 0x30090008  0x99000DBB  1761021364  Local  R/W    heap
 0x992611D0  0x99861FFF     6295088  Iomem  R/W    lsmpi_mem
 0xBF9CC000  0xBF9E0FFF       86016  Local  R/W    stack


Free Region Manager:

      Start         End     Size(b)  Class  Media  Name



------------------ Mempool statistics ------------------


                Head    Total(b)     Used(b)     Free(b)   Lowest(b)  Largest(b)
Processor   30090008   1761021364   735270176   1025751188   1019403296   1020971556
 lsmpi_io   992611D0     6295088     6294120         968         968         968

-------------- Top 100 allocator pc summary -----------


Allocator PC Summary for: Processor

    PC          Total   Count  Name
0x10568828     100548      10  MGMT VRF Process
0x1299ED50      65588       1  MRIB route entry
0x10B8C980      65588       1  MRIB route entry
0x111114E8      65588       1  MFI: InfoRply
0x1110DF48      65588       1  MFI: Clnt SMsg
0x104C7ED4      65588       1  AAA DB Elt Chu
0x104FB588      65588       1  AAA AttrL Hdr
0x104FB6F0      65588       1  AAA AttrL Sub
0x11A3BAC4      65588       1  AAA Small Chun
0x104FA840      32820       1  AAA attr list handle IDs
0x10EEEE00      28456       1  IPv6 route
0x13010160      27468       3  IPC Port
0x1498FAC4      24744       4  IPv6 routing table
0x149B092C      19984       8  IP routing table
0x10EEEE38      18232       1  IPv6 adj
0x104D9740      18232       1  AAA Acct DB ch
0x13043B78      10212      11  IPC Tx Win info
0x104D6548       8824       1  AAA Acct Rec c
0x10EEE998       8436       1  IPv6 Watcher
0x11A94A5C       8436       1  Watched Boolea
0x10E632EC       6320       4  TCP CB
0x1009EBD8       4304       1  AAA Acct AVLno
0x10EE81BC       4240       2  MGMT VRF Process
0x104C7B88       4148       1  AAA Unique Id Hash Table
0x10EF91C8       3104       2  Freelist element
0x10DD7520       2748       3  RIB: Control Block
0x130EA0A0       2528      12  ISSU Proto Session
0x1057E7D0       2420      25  MGMT VRF Process
0x1057E7C0       2404      25  MGMT VRF Process
0x11ACB4E0       2040      10  VPN ecomm list
0x10587C7C       1952      24  MGMT VRF Process
0x1223DF2C       1896       2  Virtual Exec
0x10EEEE70       1708       1  IPv6 backup
0x11111470       1552       1  MFI: InfoReq
0x103195A8       1476       3  BGP session
0x1052CC98       1436       1  Connection
0x14086908       1292       1  *Software IDB*
0x149C56CC       1164       5  MGMT VRF Process
0x14988938       1080       1  Index Table Block
0x104FB800       1076       1  AAA attr list handle IDs
0x10EEF2E4        912       2  MGMT VRF Process
0x1034E114        800       1  BGP UI nbr topo
0x1035F97C        780       1  BGP UI nbr
0x12D46BA4        764       3  RTTY Client Registration
0x10ED9BD0        760       2  MGMT VRF Process
0x11ACD048        720       2  VPN record
0x11F8FB28        640       2  CEF: FIBSWSB control
0x11ACCFC4        576       3  VRF sub record
0x1409FF30        564       1  Virtual Exec
0x10EE7D44        532       1  IPv6 PDB
0x1054938C        484       5  NameDB String
0x13107764        472       2  message nego r
0x1053BE90        456       1  TTY timers array
0x100BD678        444       1  iprl
0x120753C4        420       2  IPv4 FIB subblock
0x11F8C220        388       1  CEF: FIBIDB
0x11ABCAA8        308       1  .1Q hwsb row
0x11661AA0        308       1  MQC: POLICYMAP_MODULE
0x119F6DA8        304       4  MGMT VRF Process
0x11AA9860        300       1  Virtual Exec
0x10F0DA2C        292       1  MGMT VRF Process
0x14995478        276       3  MGMT VRF Process
0x10B03B24        276       1  IPV4 STATS FWD sw subblock
0x149954BC        268       3  MGMT VRF Process
0x14995490        264       3  MGMT VRF Process
0x11ABE194        252       1  DOT1Q SW subblock
0x10B038E8        236       1  Virtual Exec
0x12F2D77C        228       1  Parser-Mode History Table
0x10EE7D98        228       1  MGMT VRF Process
0x11A3B824        216       1  AAA String Malloc
0x104D6518        216       1  AAA Acct Rec chunk
0x1009EBAC        216       1  AAA Acct AVLnode chunk
0x104D9714        216       1  AAA Acct DB chunk
0x104FB6B8        216       1  AAA AttrL Sub
0x11A3B688        204       1  AAA Small Chunk
0x117FDE5C        196       1  ROUTING TOPOLOGY: CONTEXT
0x12F568B8        196       1  ifindex Table Entry
0x14117A78        196       1  avp_array
0x10DD7584        184       2  IP: RIB Name
0x10EEF364        184       2  MGMT VRF Process
0x104FB554        184       1  AAA AttrL Hdr
0x104C7C24        180       1  AAA DB Elt Chunk
0x10EC0E0C        176       1  MGMT VRF Process
0x10EEF320        156       2  MGMT VRF Process
0x10E8DE94        152       1  IP: RIB Alternate Preference
0x116E8AF8        152       1  RIB: rpl asc
0x10B8C93C        152       1  MRIB IPv4 Init Process
0x10EF919C        152       2  MGMT VRF Process
0x1057CDDC        152       1  Parser Mode
0x1167A650        152       2  QOS policymap name
0x10A46FFC        148       1  IM_IF_INDEX_MGMT
0x102AE8D4        148       1  BGP sw subblock
0x10EF5270        144       1  MGMT VRF Process
0x11AC9134        144       1  MGMT VRF Process
0x1053BEA8        144       1  TTY timer block
0x1234B5C0        140       1  SWIDB_SB: NETBIOS Info
0x1423DCB0        136       1  PLIM QoS SW subblock
0x115B7228        116       1  Qos hw subblock
0x116555F0        112       1  MQC: POLICYMAP_MODULE
0x10DCDE4C        112       1  IDB: IPINFO
0x115B71E0        112       1  Qos sw subblock
0x1299ED0C        108       1  MRIB IPv6 Init Process
0x11662FD4        104       1  MQC: POLICYMAP_MODULE
0x116633B0         96       1  MQC: POLICYMAP_MODULE
0x1111FC6C         88       1  MPLS feature idb sw subblock
0x1050AAD4         84       1  AAA Cursor
0x116E53AC         80       1  MGMT VRF Process
0x116E8164         80       1  MGMT VRF Process
0x10DD7650         80       1  IP: RIB Name
0x13014394         80       1  IPC Name
0x10562774         76       1  Parser Linkage
0x1057CE48         76       1  Parser Mode Q1
0x1057CE6C         76       1  Parser Mode Q2
0x149B6A34         76       1  Linear ID desc
0x11ACE154         76       1  MGMT VRF Process
0x116E53C0         76       1  MGMT VRF Process
0x11416FD0         76       1  MGMT VRF Process
0x11416FE4         76       1  MGMT VRF Process
0x10EE7D5C         76       1  MGMT VRF Process
0x104F9CCC         76       1  AAA MI SG NAME
0x10EB66C4         76       1  IPRTG SWSB


Allocator PC Summary for: lsmpi_io

    PC          Total   Count  Name


------------------ show buffers ------------------


Buffer elements:
     1099 in free list (500 max allowed)
     85307303 hits, 0 misses, 618 created

Public buffer pools:
Small buffers, 104 bytes (total 1200, permanent 1200):
     1200 in free list (200 min, 2500 max allowed)
     31678688 hits, 0 misses, 0 trims, 0 created
     0 failures (0 no memory)
Middle buffers, 600 bytes (total 900, permanent 900):
     888 in free list (100 min, 2000 max allowed)
     49679415 hits, 0 misses, 0 trims, 0 created
     0 failures (0 no memory)
Big buffers, 1536 bytes (total 900, permanent 900, peak 944 @ 7w0d):
     900 in free list (50 min, 1800 max allowed)
     26772685 hits, 18 misses, 44 trims, 44 created
     0 failures (0 no memory)
VeryBig buffers, 4520 bytes (total 100, permanent 100):
     100 in free list (0 min, 300 max allowed)
     1491173 hits, 0 misses, 0 trims, 0 created
     0 failures (0 no memory)
Large buffers, 5024 bytes (total 100, permanent 100):
     100 in free list (0 min, 300 max allowed)
     1000 hits, 0 misses, 0 trims, 0 created
     0 failures (0 no memory)
VeryLarge buffers, 8228 bytes (total 100, permanent 100):
     100 in free list (0 min, 300 max allowed)
     3002 hits, 0 misses, 0 trims, 0 created
     0 failures (0 no memory)
Huge buffers, 18024 bytes (total 20, permanent 20):
     20 in free list (0 min, 33 max allowed)
     7000 hits, 0 misses, 0 trims, 0 created
     0 failures (0 no memory)

Interface buffer pools:
CF Small buffers, 104 bytes (total 100, permanent 100):
     100 in free list (100 min, 200 max allowed)
     0 hits, 0 misses, 0 trims, 0 created
     0 failures (0 no memory)
CF Middle buffers, 600 bytes (total 100, permanent 100):
     100 in free list (100 min, 200 max allowed)
     0 hits, 0 misses, 0 trims, 0 created
     0 failures (0 no memory)
Syslog ED Pool buffers, 600 bytes (total 1056, permanent 1056):
     1024 in free list (1056 min, 1056 max allowed)
     4805 hits, 0 misses
EOBC0 buffers, 1524 bytes (total 256, permanent 256):
     256 in free list (0 min, 256 max allowed)
     2709627 hits, 0 fallbacks
CF Big buffers, 1536 bytes (total 25, permanent 25):
     25 in free list (25 min, 50 max allowed)
     0 hits, 0 misses, 0 trims, 0 created
     0 failures (0 no memory)
IPC buffers, 4096 bytes (total 1176, permanent 1176):
     1160 in free list (392 min, 3920 max allowed)
     1354853 hits, 0 fallbacks, 0 trims, 0 created
     0 failures (0 no memory)
CF VeryBig buffers, 4520 bytes (total 2, permanent 2):
     2 in free list (2 min, 4 max allowed)
     0 hits, 0 misses, 0 trims, 0 created
     0 failures (0 no memory)
CF Large buffers, 5024 bytes (total 1, permanent 1):
     1 in free list (1 min, 2 max allowed)
     0 hits, 0 misses, 0 trims, 0 created
     0 failures (0 no memory)
Private Huge IPC buffers, 18024 bytes (total 0, permanent 0):
     0 in free list (0 min, 4 max allowed)
     0 hits, 0 misses, 0 trims, 0 created
     0 failures (0 no memory)
Private Huge buffers, 65280 bytes (total 0, permanent 0):
     0 in free list (0 min, 4 max allowed)
     0 hits, 0 misses, 0 trims, 0 created
     0 failures (0 no memory)

Header pools:
Header buffers, 0 bytes (total 266, permanent 256, peak 266 @ 7w0d):
     10 in free list (10 min, 512 max allowed)
     253 hits, 3 misses, 0 trims, 10 created
     0 failures (0 no memory)
     256 max cache size, 256 in cache
     26151215 hits in cache, 0 misses in cache

Particle Clones:
     1024 clones, 0 hits, 0 misses

Public particle pools:
F/S buffers, 256 bytes (total 384, permanent 384):
     128 in free list (128 min, 1024 max allowed)
     256 hits, 0 misses, 0 trims, 0 created
     0 failures (0 no memory)
     256 max cache size, 256 in cache
     0 hits in cache, 0 misses in cache
Normal buffers, 512 bytes (total 512, permanent 512):
     384 in free list (128 min, 1024 max allowed)
     128 hits, 0 misses, 0 trims, 0 created
     0 failures (0 no memory)
     128 max cache size, 128 in cache
     0 hits in cache, 0 misses in cache

Private particle pools:
lsmpi_rx buffers, 416 bytes (total 8194, permanent 8194):
     0 in free list (8194 min, 8194 max allowed)
     8194 hits, 0 misses
     8194 max cache size, 0 in cache
     32678974 hits in cache, 0 misses in cache
lsmpi_tx buffers, 416 bytes (total 4098, permanent 4098):
     0 in free list (4098 min, 4098 max allowed)
     4098 hits, 0 misses
     4098 max cache size, 4071 in cache
     28480356 hits in cache, 0 misses in cache



------------------ show buffers usage ------------------


Statistics for the Small pool
Number of Buffers used by packets generated by system: 1200
Number of Buffers used by incoming packets:               0

Statistics for the Middle pool
Output IDB   :        Ls0 count:       19
Caller pc    : 0x10E5F824 count:       20
Resource User: Virtual Ex count:       20
Number of Buffers used by packets generated by system:  900
Number of Buffers used by incoming packets:               0

Statistics for the Big pool
Number of Buffers used by packets generated by system:  900
Number of Buffers used by incoming packets:               0

Statistics for the VeryBig pool
Number of Buffers used by packets generated by system:  100
Number of Buffers used by incoming packets:               0

Statistics for the Large pool
Number of Buffers used by packets generated by system:  100
Number of Buffers used by incoming packets:               0

Statistics for the VeryLarge pool
Number of Buffers used by packets generated by system:  100
Number of Buffers used by incoming packets:               0

Statistics for the Huge pool
Number of Buffers used by packets generated by system:   20
Number of Buffers used by incoming packets:               0

Statistics for the CF Small pool
Number of Buffers used by packets generated by system:  100
Number of Buffers used by incoming packets:               0

Statistics for the CF Middle pool
Number of Buffers used by packets generated by system:  100
Number of Buffers used by incoming packets:               0

Statistics for the Syslog ED Pool pool
Caller pc    : 0x108074D0 count:       32
Resource User: EEM ED Sys count:       32
Number of Buffers used by packets generated by system: 1056
Number of Buffers used by incoming packets:               0

Statistics for the EOBC0 pool
Number of Buffers used by packets generated by system:  256
Number of Buffers used by incoming packets:               0

Statistics for the CF Big pool
Number of Buffers used by packets generated by system:   25
Number of Buffers used by incoming packets:               0

Statistics for the IPC pool
Caller pc    : 0x1303DD20 count:       16
Resource User:       Init count:        1
Resource User:     *Dead* count:        3
Resource User: IPC Seat R count:       12
Number of Buffers used by packets generated by system: 1176
Number of Buffers used by incoming packets:               0

Statistics for the CF VeryBig pool
Number of Buffers used by packets generated by system:    2
Number of Buffers used by incoming packets:               0

Statistics for the CF Large pool
Number of Buffers used by packets generated by system:    1
Number of Buffers used by incoming packets:               0

Statistics for the Private Huge IPC pool
Number of Buffers used by packets generated by system:    0
Number of Buffers used by incoming packets:               0

Statistics for the Private Huge pool
Number of Buffers used by packets generated by system:    0
Number of Buffers used by incoming packets:               0

Statistics for the Header pool
Number of Buffers used by packets generated by system:  266
Number of Buffers used by incoming packets:               0

Statistics for the FS Header pool
Caller pc    : 0x142213FC count:        1
Resource User:       Init count:       13
Caller pc    : 0x1452F06C count:        1
Caller pc    : 0x110FB224 count:        1
Caller pc    : 0x120C2AD0 count:        8
Caller pc    : 0x12C428BC count:        1
Caller pc    : 0x14256778 count:        1
Number of Buffers used by packets generated by system:   29
Number of Buffers used by incoming packets:               0

Statistics for the l2frag pak pool pool
Number of Buffers used by packets generated by system:    0
Number of Buffers used by incoming packets:               0


------------------ show platform ------------------


Chassis type: ASR1004             

Slot      Type                State                 Insert time (ago) 
--------- ------------------- --------------------- ----------------- 
0         ASR1000-SIP10       ok                    7w3d          
 0/0      SPA-8X1GE-V2        ok                    7w3d          
 0/3      SPA-1X10GE-L-V2     ok                    7w3d          
1         ASR1000-SIP10       ok                    7w3d          
 1/3      SPA-1X10GE-L-V2     ok                    7w3d          
R0        ASR1000-RP1         ok, active            7w3d          
F0        ASR1000-ESP10       ok, active            7w3d          
P0        ASR1004-PWR-AC      ok                    7w3d          
P1        ASR1004-PWR-AC      ps, fail              7w3d          

Slot      CPLD Version        Firmware Version                        
--------- ------------------- --------------------------------------- 
0         09111601            12.2(33r)XNC                        
1         09111601            12.2(33r)XNC                        
R0        07062111            12.2(33r)XNC                        
F0        07091401            12.2(33r)XNC                        


------------------ show platform software tech-support ------------------

---- show version installed ----

Package: Provisioning File, version: n/a, status: active
  File: consolidated:packages.conf, on: RP0
  Built: n/a, by: n/a
  File SHA1 checksum: 3f0cf45478260116fdc8f531463ca51c4e96a913

Package: rpbase, version: 03.02.00.S.151-1.S, status: active
  File: consolidated:asr1000rp1-rpbase.03.02.00.S.151-1.S.pkg, on: RP0
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: d3c5b5f5846dc47cf0b1eaafbde3ed698afdf06f

Package: rpcontrol, version: 03.02.00.S.151-1.S, status: active
  File: consolidated:asr1000rp1-rpcontrol.03.02.00.S.151-1.S.pkg, on: RP0/0
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: 530858273677b49fc36d60a0217388585e8727ea

Package: rpios-advipservices, version: 03.02.00.S.151-1.S, status: active
  File: consolidated:asr1000rp1-rpios-advipservices.03.02.00.S.151-1.S.pkg, on: RP0/0
  Built: 2010-11-22_13.36, by: mcpre
  File SHA1 checksum: ec70bfbf19d8d40bba41d447a4eda6104766a802

Package: rpaccess, version: 03.02.00.S.151-1.S, status: active
  File: consolidated:asr1000rp1-rpaccess.03.02.00.S.151-1.S.pkg, on: RP0/0
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: dfa96941af6a132b5555ba6ed02b2bdd05d67d68

Package: rpcontrol, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-rpcontrol.03.02.00.S.151-1.S.pkg, on: RP0/1
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: 530858273677b49fc36d60a0217388585e8727ea

Package: rpios-advipservices, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-rpios-advipservices.03.02.00.S.151-1.S.pkg, on: RP0/1
  Built: 2010-11-22_13.36, by: mcpre
  File SHA1 checksum: ec70bfbf19d8d40bba41d447a4eda6104766a802

Package: rpaccess, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-rpaccess.03.02.00.S.151-1.S.pkg, on: RP0/1
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: dfa96941af6a132b5555ba6ed02b2bdd05d67d68

Package: rpbase, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-rpbase.03.02.00.S.151-1.S.pkg, on: RP1
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: d3c5b5f5846dc47cf0b1eaafbde3ed698afdf06f

Package: rpcontrol, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-rpcontrol.03.02.00.S.151-1.S.pkg, on: RP1/0
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: 530858273677b49fc36d60a0217388585e8727ea

Package: rpios-advipservices, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-rpios-advipservices.03.02.00.S.151-1.S.pkg, on: RP1/0
  Built: 2010-11-22_13.36, by: mcpre
  File SHA1 checksum: ec70bfbf19d8d40bba41d447a4eda6104766a802

Package: rpaccess, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-rpaccess.03.02.00.S.151-1.S.pkg, on: RP1/0
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: dfa96941af6a132b5555ba6ed02b2bdd05d67d68

Package: rpcontrol, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-rpcontrol.03.02.00.S.151-1.S.pkg, on: RP1/1
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: 530858273677b49fc36d60a0217388585e8727ea

Package: rpios-advipservices, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-rpios-advipservices.03.02.00.S.151-1.S.pkg, on: RP1/1
  Built: 2010-11-22_13.36, by: mcpre
  File SHA1 checksum: ec70bfbf19d8d40bba41d447a4eda6104766a802

Package: rpaccess, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-rpaccess.03.02.00.S.151-1.S.pkg, on: RP1/1
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: dfa96941af6a132b5555ba6ed02b2bdd05d67d68

Package: espbase, version: 03.02.00.S.151-1.S, status: active
  File: consolidated:asr1000rp1-espbase.03.02.00.S.151-1.S.pkg, on: ESP0
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: edba6f3a0def649bf9b5ca5f3e5a08818756cacb

Package: espbase, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-espbase.03.02.00.S.151-1.S.pkg, on: ESP1
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: edba6f3a0def649bf9b5ca5f3e5a08818756cacb

Package: sipbase, version: 03.02.00.S.151-1.S, status: active
  File: consolidated:asr1000rp1-sipbase.03.02.00.S.151-1.S.pkg, on: SIP0
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: b444a306db405c6561f897ddbb17cec761762470

Package: sipspa, version: 03.02.00.S.151-1.S, status: active
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP0/0
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipspa, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP0/1
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipspa, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP0/2
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipspa, version: 03.02.00.S.151-1.S, status: active
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP0/3
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipbase, version: 03.02.00.S.151-1.S, status: active
  File: consolidated:asr1000rp1-sipbase.03.02.00.S.151-1.S.pkg, on: SIP1
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: b444a306db405c6561f897ddbb17cec761762470

Package: sipspa, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP1/0
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipspa, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP1/1
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipspa, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP1/2
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipspa, version: 03.02.00.S.151-1.S, status: active
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP1/3
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipbase, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipbase.03.02.00.S.151-1.S.pkg, on: SIP2
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: b444a306db405c6561f897ddbb17cec761762470

Package: sipspa, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP2/0
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipspa, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP2/1
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipspa, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP2/2
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipspa, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP2/3
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipbase, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipbase.03.02.00.S.151-1.S.pkg, on: SIP3
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: b444a306db405c6561f897ddbb17cec761762470

Package: sipspa, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP3/0
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipspa, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP3/1
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipspa, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP3/2
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipspa, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP3/3
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipbase, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipbase.03.02.00.S.151-1.S.pkg, on: SIP4
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: b444a306db405c6561f897ddbb17cec761762470

Package: sipspa, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP4/0
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipspa, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP4/1
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipspa, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP4/2
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipspa, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP4/3
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipbase, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipbase.03.02.00.S.151-1.S.pkg, on: SIP5
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: b444a306db405c6561f897ddbb17cec761762470

Package: sipspa, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP5/0
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipspa, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP5/1
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipspa, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP5/2
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipspa, version: 03.02.00.S.151-1.S, status: n/a
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP5/3
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

---- show version running ----

Package: Provisioning File, version: n/a, status: active
  File: consolidated:packages.conf, on: RP0
  Built: n/a, by: n/a
  File SHA1 checksum: 3f0cf45478260116fdc8f531463ca51c4e96a913

Package: rpbase, version: 03.02.00.S.151-1.S, status: active
  File: consolidated:asr1000rp1-rpbase.03.02.00.S.151-1.S.pkg, on: RP0
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: d3c5b5f5846dc47cf0b1eaafbde3ed698afdf06f

Package: rpcontrol, version: 03.02.00.S.151-1.S, status: active
  File: consolidated:asr1000rp1-rpcontrol.03.02.00.S.151-1.S.pkg, on: RP0/0
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: 530858273677b49fc36d60a0217388585e8727ea

Package: rpios-advipservices, version: 03.02.00.S.151-1.S, status: active
  File: consolidated:asr1000rp1-rpios-advipservices.03.02.00.S.151-1.S.pkg, on: RP0/0
  Built: 2010-11-22_13.36, by: mcpre
  File SHA1 checksum: ec70bfbf19d8d40bba41d447a4eda6104766a802

Package: rpaccess, version: 03.02.00.S.151-1.S, status: active
  File: consolidated:asr1000rp1-rpaccess.03.02.00.S.151-1.S.pkg, on: RP0/0
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: dfa96941af6a132b5555ba6ed02b2bdd05d67d68

Package: espbase, version: 03.02.00.S.151-1.S, status: active
  File: consolidated:asr1000rp1-espbase.03.02.00.S.151-1.S.pkg, on: ESP0
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: edba6f3a0def649bf9b5ca5f3e5a08818756cacb

Package: sipbase, version: 03.02.00.S.151-1.S, status: active
  File: consolidated:asr1000rp1-sipbase.03.02.00.S.151-1.S.pkg, on: SIP0
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: b444a306db405c6561f897ddbb17cec761762470

Package: sipspa, version: 03.02.00.S.151-1.S, status: active
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP0/0
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipspa, version: 03.02.00.S.151-1.S, status: active
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP0/3
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

Package: sipbase, version: 03.02.00.S.151-1.S, status: active
  File: consolidated:asr1000rp1-sipbase.03.02.00.S.151-1.S.pkg, on: SIP1
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: b444a306db405c6561f897ddbb17cec761762470

Package: sipspa, version: 03.02.00.S.151-1.S, status: active
  File: consolidated:asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg, on: SIP1/3
  Built: 2010-11-22_13.29, by: mcpre
  File SHA1 checksum: df7a1b3281982a1c83c28360a3ca961fa0a7a342

---- show platform hardware qfp active infrastructure punt config cause ----

QFP Punt Table Configuration

Punt table base addr : 0x8971AC00
  punt cause index     0
  punt cause name      Reserved 
  maximum instances    1
  punt table address : 0x8971AC00
  instance[0] ptr    : 0x8971B000
    *** This punt cause is disabled ***


Punt table base addr : 0x8971AC00
  punt cause index     1
  punt cause name      MPLS ICMP Can't Fragment
  maximum instances    1
  punt table address : 0x8971AC04
  instance[0] ptr    : 0x8971B004
    *** This punt cause is disabled ***


Punt table base addr : 0x8971AC00
  punt cause index     2
  punt cause name      IPv4 Options
  maximum instances    1
  punt table address : 0x8971AC08
  instance[0] ptr    : 0x8971B008
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B008
    fast failover address   : 0x8971A834
    Low priority policer    : 2
    High priority policer   : 3

Punt table base addr : 0x8971AC00
  punt cause index     3
  punt cause name      Layer2 control and legacy
  maximum instances    1
  punt table address : 0x8971AC0C
  instance[0] ptr    : 0x8971B00C
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B00C
    fast failover address   : 0x8971A834
    Low priority policer    : 4
    High priority policer   : 5

Punt table base addr : 0x8971AC00
  punt cause index     4
  punt cause name      PPP Control
  maximum instances    1
  punt table address : 0x8971AC10
  instance[0] ptr    : 0x8971B010
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B010
    fast failover address   : 0x8971A834
    Low priority policer    : 6
    High priority policer   : 7

Punt table base addr : 0x8971AC00
  punt cause index     5
  punt cause name      CLNS IS-IS Control
  maximum instances    1
  punt table address : 0x8971AC14
  instance[0] ptr    : 0x8971B014
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B014
    fast failover address   : 0x8971A834
    Low priority policer    : 8
    High priority policer   : 9

Punt table base addr : 0x8971AC00
  punt cause index     6
  punt cause name      HDLC keepalives
  maximum instances    1
  punt table address : 0x8971AC18
  instance[0] ptr    : 0x8971B018
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B018
    fast failover address   : 0x8971A834
    Low priority policer    : 10
    High priority policer   : 11

Punt table base addr : 0x8971AC00
  punt cause index     7
  punt cause name      ARP request or response
  maximum instances    1
  punt table address : 0x8971AC1C
  instance[0] ptr    : 0x8971B01C
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B01C
    fast failover address   : 0x8971A834
    Low priority policer    : 12
    High priority policer   : 13

Punt table base addr : 0x8971AC00
  punt cause index     8
  punt cause name      Reverse ARP request or repsonse
  maximum instances    1
  punt table address : 0x8971AC20
  instance[0] ptr    : 0x8971B020
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B020
    fast failover address   : 0x8971A834
    Low priority policer    : 14
    High priority policer   : 15

Punt table base addr : 0x8971AC00
  punt cause index     9
  punt cause name      Frame-relay LMI Control
  maximum instances    1
  punt table address : 0x8971AC24
  instance[0] ptr    : 0x8971B024
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B024
    fast failover address   : 0x8971A834
    Low priority policer    : 16
    High priority policer   : 17

Punt table base addr : 0x8971AC00
  punt cause index     10
  punt cause name      Incomplete adjacency
  maximum instances    1
  punt table address : 0x8971AC28
  instance[0] ptr    : 0x8971B028
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B028
    fast failover address   : 0x8971A834
    Low priority policer    : 18
    High priority policer   : 19

Punt table base addr : 0x8971AC00
  punt cause index     11
  punt cause name      For-us data
  maximum instances    1
  punt table address : 0x8971AC2C
  instance[0] ptr    : 0x8971B02C
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B02C
    fast failover address   : 0x8971A834
    Low priority policer    : 20
    High priority policer   : 21

Punt table base addr : 0x8971AC00
  punt cause index     12
  punt cause name      Mcast Directly Connected Source
  maximum instances    1
  punt table address : 0x8971AC30
  instance[0] ptr    : 0x8971B030
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B030
    fast failover address   : 0x8971A834
    Low priority policer    : 22
    High priority policer   : 23

Punt table base addr : 0x8971AC00
  punt cause index     13
  punt cause name      Mcast IPv4 Options data packet
  maximum instances    1
  punt table address : 0x8971AC34
  instance[0] ptr    : 0x8971B034
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B034
    fast failover address   : 0x8971A834
    Low priority policer    : 24
    High priority policer   : 25

Punt table base addr : 0x8971AC00
  punt cause index     14
  punt cause name      Skip egress processing
  maximum instances    1
  punt table address : 0x8971AC38
  instance[0] ptr    : 0x8971B038
    *** This punt cause is disabled ***


Punt table base addr : 0x8971AC00
  punt cause index     15
  punt cause name      MPLS TTL expired
  maximum instances    1
  punt table address : 0x8971AC3C
  instance[0] ptr    : 0x8971B03C
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B03C
    fast failover address   : 0x8971A834
    Low priority policer    : 26
    High priority policer   : 27

Punt table base addr : 0x8971AC00
  punt cause index     16
  punt cause name      MPLS Reserved label (ie: 0-15)
  maximum instances    1
  punt table address : 0x8971AC40
  instance[0] ptr    : 0x8971B040
    *** This punt cause is disabled ***


Punt table base addr : 0x8971AC00
  punt cause index     17
  punt cause name      IPv6 Bad hop limit
  maximum instances    1
  punt table address : 0x8971AC44
  instance[0] ptr    : 0x8971B044
    *** This punt cause is disabled ***


Punt table base addr : 0x8971AC00
  punt cause index     18
  punt cause name      IPV6 Hop-by-hop Options
  maximum instances    1
  punt table address : 0x8971AC48
  instance[0] ptr    : 0x8971B048
    *** This punt cause is disabled ***


Punt table base addr : 0x8971AC00
  punt cause index     19
  punt cause name      Mcast Internal Copy
  maximum instances    1
  punt table address : 0x8971AC4C
  instance[0] ptr    : 0x8971B04C
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B04C
    fast failover address   : 0x8971A834
    Low priority policer    : 28
    High priority policer   : 29

Punt table base addr : 0x8971AC00
  punt cause index     20
  punt cause name      Generic QFP generated packet
  maximum instances    1
  punt table address : 0x8971AC50
  instance[0] ptr    : 0x8971B050
    QFP interface handle : 3
    Interface name       : internal0/0/recycle:0
    instance address        : 0x8971B050
    fast failover address   : 0x8971A874
    Low priority policer    : 0
    High priority policer   : 0

Punt table base addr : 0x8971AC00
  punt cause index     21
  punt cause name      RP<->QFP keepalive
  maximum instances    1
  punt table address : 0x8971AC54
  instance[0] ptr    : 0x8971B054
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B054
    fast failover address   : 0x8971A834
    Low priority policer    : 0
    High priority policer   : 0

Punt table base addr : 0x8971AC00
  punt cause index     22
  punt cause name      QFP Fwall generated packet
  maximum instances    1
  punt table address : 0x8971AC58
  instance[0] ptr    : 0x8971B058
    QFP interface handle : 3
    Interface name       : internal0/0/recycle:0
    instance address        : 0x8971B058
    fast failover address   : 0x8971A874
    Low priority policer    : 0
    High priority policer   : 0

Punt table base addr : 0x8971AC00
  punt cause index     23
  punt cause name      Mcast IGMP Unroutable
  maximum instances    1
  punt table address : 0x8971AC5C
  instance[0] ptr    : 0x8971B05C
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B05C
    fast failover address   : 0x8971A834
    Low priority policer    : 30
    High priority policer   : 31

Punt table base addr : 0x8971AC00
  punt cause index     24
  punt cause name      Glean adjacency
  maximum instances    1
  punt table address : 0x8971AC60
  instance[0] ptr    : 0x8971B060
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B060
    fast failover address   : 0x8971A834
    Low priority policer    : 32
    High priority policer   : 33

Punt table base addr : 0x8971AC00
  punt cause index     25
  punt cause name      Mcast PIM signaling
  maximum instances    1
  punt table address : 0x8971AC64
  instance[0] ptr    : 0x8971B064
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B064
    fast failover address   : 0x8971A834
    Low priority policer    : 34
    High priority policer   : 35

Punt table base addr : 0x8971AC00
  punt cause index     26
  punt cause name      QFP ICMP generated packet
  maximum instances    1
  punt table address : 0x8971AC68
  instance[0] ptr    : 0x8971B068
    QFP interface handle : 3
    Interface name       : internal0/0/recycle:0
    instance address        : 0x8971B068
    fast failover address   : 0x8971A874
    Low priority policer    : 0
    High priority policer   : 0

Punt table base addr : 0x8971AC00
  punt cause index     27
  punt cause name      ESS session control
  maximum instances    1
  punt table address : 0x8971AC6C
  instance[0] ptr    : 0x8971B06C
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B06C
    fast failover address   : 0x8971A834
    Low priority policer    : 36
    High priority policer   : 37

Punt table base addr : 0x8971AC00
  punt cause index     28
  punt cause name      ESS data switching back
  maximum instances    1
  punt table address : 0x8971AC70
  instance[0] ptr    : 0x8971B070
    QFP interface handle : 3
    Interface name       : internal0/0/recycle:0
    instance address        : 0x8971B070
    fast failover address   : 0x8971A874
    Low priority policer    : 0
    High priority policer   : 0

Punt table base addr : 0x8971AC00
  punt cause index     29
  punt cause name      RP handled ICMP
  maximum instances    1
  punt table address : 0x8971AC74
  instance[0] ptr    : 0x8971B074
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B074
    fast failover address   : 0x8971A834
    Low priority policer    : 38
    High priority policer   : 39

Punt table base addr : 0x8971AC00
  punt cause index     30
  punt cause name      RP injected For-us data
  maximum instances    1
  punt table address : 0x8971AC78
  instance[0] ptr    : 0x8971B078
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B078
    fast failover address   : 0x8971A834
    Low priority policer    : 40
    High priority policer   : 41

Punt table base addr : 0x8971AC00
  punt cause index     31
  punt cause name      Punt adjacency
  maximum instances    1
  punt table address : 0x8971AC7C
  instance[0] ptr    : 0x8971B07C
    *** This punt cause is disabled ***


Punt table base addr : 0x8971AC00
  punt cause index     32
  punt cause name      SBC RTP DTMF
  maximum instances    1
  punt table address : 0x8971AC80
  instance[0] ptr    : 0x8971B080
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B080
    fast failover address   : 0x8971A834
    Low priority policer    : 42
    High priority policer   : 43

Punt table base addr : 0x8971AC00
  punt cause index     33
  punt cause name      Pseudowire VCCV control channel
  maximum instances    1
  punt table address : 0x8971AC84
  instance[0] ptr    : 0x8971B084
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B084
    fast failover address   : 0x8971A834
    Low priority policer    : 44
    High priority policer   : 45

Punt table base addr : 0x8971AC00
  punt cause index     34
  punt cause name      Generic QFP generated packet (keep GPM)
  maximum instances    1
  punt table address : 0x8971AC88
  instance[0] ptr    : 0x8971B088
    QFP interface handle : 3
    Interface name       : internal0/0/recycle:0
    instance address        : 0x8971B088
    fast failover address   : 0x8971A874
    Low priority policer    : 0
    High priority policer   : 0

Punt table base addr : 0x8971AC00
  punt cause index     35
  punt cause name      Ethernet slow protocol (ie: LACP, OAM) 
  maximum instances    1
  punt table address : 0x8971AC8C
  instance[0] ptr    : 0x8971B08C
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B08C
    fast failover address   : 0x8971A834
    Low priority policer    : 46
    High priority policer   : 47

Punt table base addr : 0x8971AC00
  punt cause index     36
  punt cause name      Ethernet OAM Loopback
  maximum instances    1
  punt table address : 0x8971AC90
  instance[0] ptr    : 0x8971B090
    *** This punt cause is disabled ***


Punt table base addr : 0x8971AC00
  punt cause index     37
  punt cause name      Egress to Ingress redirect
  maximum instances    1
  punt table address : 0x8971AC94
  instance[0] ptr    : 0x8971B094
    *** This punt cause is disabled ***


Punt table base addr : 0x8971AC00
  punt cause index     38
  punt cause name      SPA IPC packet
  maximum instances    1
  punt table address : 0x8971AC98
  instance[0] ptr    : 0x8971B098
    *** This punt cause is disabled ***


Punt table base addr : 0x8971AC00
  punt cause index     39
  punt cause name      Punt and replicate
  maximum instances    1
  punt table address : 0x8971AC9C
  instance[0] ptr    : 0x8971B09C
    *** This punt cause is disabled ***


Punt table base addr : 0x8971AC00
  punt cause index     40
  punt cause name      PPPoE control
  maximum instances    1
  punt table address : 0x8971ACA0
  instance[0] ptr    : 0x8971B0A0
    *** This punt cause is disabled ***


Punt table base addr : 0x8971AC00
  punt cause index     41
  punt cause name      PPPoE session
  maximum instances    1
  punt table address : 0x8971ACA4
  instance[0] ptr    : 0x8971B0A4
    *** This punt cause is disabled ***


Punt table base addr : 0x8971AC00
  punt cause index     42
  punt cause name      L2TP control
  maximum instances    1
  punt table address : 0x8971ACA8
  instance[0] ptr    : 0x8971B0A8
    *** This punt cause is disabled ***


Punt table base addr : 0x8971AC00
  punt cause index     43
  punt cause name      IP Subscriber control (ie: FSOL, keepalive)
  maximum instances    1
  punt table address : 0x8971ACAC
  instance[0] ptr    : 0x8971B0AC
    *** This punt cause is disabled ***


Punt table base addr : 0x8971AC00
  punt cause index     44
  punt cause name      L2TP session
  maximum instances    1
  punt table address : 0x8971ACB0
  instance[0] ptr    : 0x8971B0B0
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B0B0
    fast failover address   : 0x8971A834
    Low priority policer    : 48
    High priority policer   : 49

Punt table base addr : 0x8971AC00
  punt cause index     45
  punt cause name      BFD control
  maximum instances    1
  punt table address : 0x8971ACB4
  instance[0] ptr    : 0x8971B0B4
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B0B4
    fast failover address   : 0x8971A834
    Low priority policer    : 50
    High priority policer   : 51

Punt table base addr : 0x8971AC00
  punt cause index     46
  punt cause name      MVPN non-RPF signaling packet
  maximum instances    1
  punt table address : 0x8971ACB8
  instance[0] ptr    : 0x8971B0B8
    *** This punt cause is disabled ***


Punt table base addr : 0x8971AC00
  punt cause index     47
  punt cause name      MVPN PIM signalling packet
  maximum instances    1
  punt table address : 0x8971ACBC
  instance[0] ptr    : 0x8971B0BC
    *** This punt cause is disabled ***


Punt table base addr : 0x8971AC00
  punt cause index     48
  punt cause name      Mcast punt to RP
  maximum instances    1
  punt table address : 0x8971ACC0
  instance[0] ptr    : 0x8971B0C0
    *** This punt cause is disabled ***


Punt table base addr : 0x8971AC00
  punt cause index     49
  punt cause name      SBC generated packet
  maximum instances    1
  punt table address : 0x8971ACC4
  instance[0] ptr    : 0x8971B0C4
    QFP interface handle : 3
    Interface name       : internal0/0/recycle:0
    instance address        : 0x8971B0C4
    fast failover address   : 0x8971A874
    Low priority policer    : 0
    High priority policer   : 0

Punt table base addr : 0x8971AC00
  punt cause index     50
  punt cause name      IPv6 packet
  maximum instances    1
  punt table address : 0x8971ACC8
  instance[0] ptr    : 0x8971B0C8
    *** This punt cause is disabled ***


Punt table base addr : 0x8971AC00
  punt cause index     51
  punt cause name      DMVPN NHRP redirect
  maximum instances    1
  punt table address : 0x8971ACCC
  instance[0] ptr    : 0x8971B0CC
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B0CC
    fast failover address   : 0x8971A834
    Low priority policer    : 52
    High priority policer   : 53

Punt table base addr : 0x8971AC00
  punt cause index     52
  punt cause name      PFR monitored prefix logging
  maximum instances    1
  punt table address : 0x8971ACD0
  instance[0] ptr    : 0x8971B0D0
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B0D0
    fast failover address   : 0x8971A834
    Low priority policer    : 54
    High priority policer   : 55

Punt table base addr : 0x8971AC00
  punt cause index     53
  punt cause name      PFR top talkers logging
  maximum instances    1
  punt table address : 0x8971ACD4
  instance[0] ptr    : 0x8971B0D4
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B0D4
    fast failover address   : 0x8971A834
    Low priority policer    : 56
    High priority policer   : 57

Punt table base addr : 0x8971AC00
  punt cause index     54
  punt cause name      PFR top talkers application logging
  maximum instances    1
  punt table address : 0x8971ACD8
  instance[0] ptr    : 0x8971B0D8
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B0D8
    fast failover address   : 0x8971A834
    Low priority policer    : 58
    High priority policer   : 59

Punt table base addr : 0x8971AC00
  punt cause index     55
  punt cause name      For-us control
  maximum instances    1
  punt table address : 0x8971ACDC
  instance[0] ptr    : 0x8971B0DC
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B0DC
    fast failover address   : 0x8971A834
    Low priority policer    : 60
    High priority policer   : 61

Punt table base addr : 0x8971AC00
  punt cause index     56
  punt cause name      RP injected for-us control
  maximum instances    1
  punt table address : 0x8971ACE0
  instance[0] ptr    : 0x8971B0E0
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B0E0
    fast failover address   : 0x8971A834
    Low priority policer    : 62
    High priority policer   : 63

Punt table base addr : 0x8971AC00
  punt cause index     57
  punt cause name      QFP VTCP generated packet
  maximum instances    1
  punt table address : 0x8971ACE4
  instance[0] ptr    : 0x8971B0E4
    QFP interface handle : 3
    Interface name       : internal0/0/recycle:0
    instance address        : 0x8971B0E4
    fast failover address   : 0x8971A874
    Low priority policer    : 0
    High priority policer   : 0

Punt table base addr : 0x8971AC00
  punt cause index     58
  punt cause name      Layer2 bridge domain packet
  maximum instances    1
  punt table address : 0x8971ACE8
  instance[0] ptr    : 0x8971B0E8
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B0E8
    fast failover address   : 0x8971A834
    Low priority policer    : 64
    High priority policer   : 65

Punt table base addr : 0x8971AC00
  punt cause index     59
  punt cause name      QFP Stile generated packet
  maximum instances    1
  punt table address : 0x8971ACEC
  instance[0] ptr    : 0x8971B0EC
    QFP interface handle : 3
    Interface name       : internal0/0/recycle:0
    instance address        : 0x8971B0EC
    fast failover address   : 0x8971A874
    Low priority policer    : 0
    High priority policer   : 0

Punt table base addr : 0x8971AC00
  punt cause index     60
  punt cause name      IP subnet or broadcast packet
  maximum instances    1
  punt table address : 0x8971ACF0
  instance[0] ptr    : 0x8971B0F0
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B0F0
    fast failover address   : 0x8971A834
    Low priority policer    : 66
    High priority policer   : 67

Punt table base addr : 0x8971AC00
  punt cause index     61
  punt cause name      Ethernet CFM packet
  maximum instances    1
  punt table address : 0x8971ACF4
  instance[0] ptr    : 0x8971B0F4
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B0F4
    fast failover address   : 0x8971A834
    Low priority policer    : 68
    High priority policer   : 69

Punt table base addr : 0x8971AC00
  punt cause index     62
  punt cause name      Ethernet CFM notify packet
  maximum instances    1
  punt table address : 0x8971ACF8
  instance[0] ptr    : 0x8971B0F8
    QFP interface handle : 1
    Interface name       : internal0/0/rp:0
    instance address        : 0x8971B0F8
    fast failover address   : 0x8971A834
    Low priority policer    : 70
    High priority policer   : 71

---- show platform hardware qfp active infrastructure punt internal-interface ----

Data read from the Punt Server Database

  Punt Path Entry

  QFP index            : 0
  QFP interface handle : 1
  Interface name       : internal0/0/rp:0

  Punt Destination Entry

    Que Information:

    High Priority Que:            : 0x89727C10
    Low Priority Que:             : 0x89727C00
    OCE adjacency is pointing to: : 0x89728400
    Common header version   : 1
    platform header version : 1
    pal header type         : 1

  Punt Interface Configuration

    QFP interface handle       : 1
    platform interface handle  : 65537
    Internal interface type    : 1
    Interface state            : 1
    Input uidb                 : 131071
    Output uidb                : 131071

Data read from QFP DRAM

  Punt Path Dataplane Entry

    Que Information:

    High Priority Que:          : 0x89727C10
    Low Priority Que:           : 0x89727C00
    OCE adjacency pointing to   : 0x89728400
    Fast Failover pointing to   : 0x8971A820
    Common header version   : 1
    platform header version : 1
    pal header type         : 1

  Punt Path Entry

  QFP index            : 0
  QFP interface handle : 2
  Interface name       : internal0/0/rp:1

  Punt Destination Entry

    Que Information:

    High Priority Que:            : 0x89727C30
    Low Priority Que:             : 0x89727C20
    OCE adjacency is pointing to: : 0x89744800
    Common header version   : 1
    platform header version : 1
    pal header type         : 1

  Punt Interface Configuration

    QFP interface handle       : 2
    platform interface handle  : 65538
    Internal interface type    : 1
    Interface state            : 1
    Input uidb                 : 131070
    Output uidb                : 131070

Data read from QFP DRAM

  Punt Path Dataplane Entry

    Que Information:

    High Priority Que:          : 0x89727C30
    Low Priority Que:           : 0x89727C20
    OCE adjacency pointing to   : 0x89744800
    Fast Failover pointing to   : 0x8971A840
    Common header version   : 1
    platform header version : 1
    pal header type         : 1

  Punt Path Entry

  QFP index            : 0
  QFP interface handle : 3
  Interface name       : internal0/0/recycle:0

  Punt Destination Entry

    Que Information:

    High Priority Que:            : 0x89727C40
    Low Priority Que:             : 0x89727C50
    OCE adjacency is pointing to: : 0x89745000
    Common header version   : 1
    platform header version : 1
    pal header type         : 2

  Punt Interface Configuration

    QFP interface handle       : 3
    platform interface handle  : 65539
    Internal interface type    : 7
    Interface state            : 1
    Input uidb                 : 131069
    Output uidb                : 131069

Data read from QFP DRAM

  Punt Path Dataplane Entry

    Que Information:

    High Priority Que:          : 0x89727C40
    Low Priority Que:           : 0x89727C50
    OCE adjacency pointing to   : 0x89745000
    Fast Failover pointing to   : 0x8971A860
    Common header version   : 1
    platform header version : 1
    pal header type         : 2

---- show platform hardware qfp active interface if-name internal0/0/rp:0 ----

General interface information
  Interface Name: internal0/0/rp:0
  Interface state: VALID
  Platform interface handle: 65537
  QFP interface handle: 1
  Rx uidb: 131071
  Tx uidb: 131071
  Channel: 9
Interface Relationships

BGPPA/QPPB interface configuration information
  Ingress: BGPPA/QPPB not configured. flags: 0000
  Egress : BGPPA not configured. flags: 0000

ipv4_input enabled. 
ipv4_output enabled. 
mpls_input enabled. 
mpls_output enabled. 
ipv4_mc_input enabled. 
ipv4_mc_output enabled. 
ipv6_input enabled. 
ipv6_output enabled. 
layer2_input enabled. 
layer2_output enabled. 
ipv6_mc_input enabled. 
ipv6_mc_output enabled. 
ess_switch_upstream enabled. 
ess_switch_downstream enabled. 
ess_ac_input enabled. 
input_layer2_switching enabled. 
output_layer2_switching enabled. 
mpls_input enabled. 
ipv4_sia_input enabled. 
ipv4_sia_output enabled. 
servicewire_input enabled. 
servicewire_output enabled. 

Features Bound to Interface:
 1 GIC FIA state
35 PUNT INJECT DB
25 ipfrag_svr
26 ipreass_svr
27 ipv6reass_svr
Protocol 0 - ipv4_input
FIA handle - CP:0x104b5aa8  DP:0x80481e00
  IPV4V6_INJECT_SBC (M)
  IPV4_INPUT_DST_LOOKUP_ISSUE (M)
  IPV4_INTERNAL_ARL_SANITY (M)
  IPV4_INTERNAL_DST_LOOKUP_CONSUME (M)
  IPV4_INTERNAL_FOR_US (M)
  IPV4_INPUT_LOOKUP_PROCESS (M)
  UPDATE_ICMP_PKT (M)
  INTERNAL_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 1 - ipv4_output
FIA handle - CP:0x104b5a74  DP:0x80482280
  IPV4_INTERNAL_ARL_SANITY (M)
  IPV4_VFR_REFRAG (M)
  IPV4_OUTPUT_DROP_POLICY (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 2 - mpls_input
FIA handle - CP:0x104b5a40  DP:0x80482700
  MPLS_INPUT_LABEL_LOOKUP_ISSUE (M)
  MPLS_INPUT_LABEL_LOOKUP_CONSUME (M)
  MPLS_INPUT_LABEL_LOOKUP_PROCESS (M)
  MPLS_UPDATE_ICMP_PKT (M)
  INTERNAL_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 3 - mpls_output
FIA handle - CP:0x104b5a0c  DP:0x80482b80
  MPLS_OUTPUT_DROP_POLICY (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 4 - ipv4_mc_input
FIA handle - CP:0x104b59d8  DP:0x80483000
  MPASS_SET_IN_VECTOR (M)
  IPV4_MC_INPUT_LOOKUP_ISSUE (M)
  IPV4_INPUT_ARL_SANITY (M)
  IPV4_MC_INTERNAL_LOOKUP_COMPLETE (M)
  IPV4_MC_INPUT_LOOKUP_PROCESS (M)
  IPV4_MC_INPUT_REPLICATION_MODULE (M)
  IPV4_MC_INPUT_POST_REPLICATION_PROCESSING (M)
  INTERNAL_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 5 - ipv4_mc_output
FIA handle - CP:0x104b59a4  DP:0x80483480
  IPV4_INTERNAL_ARL_SANITY (M)
  IPV4_MC_OUTPUT_INTERNAL_INT (M)
  IPV4_OUTPUT_DROP_POLICY (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 6 - ipv6_input
FIA handle - CP:0x104b5970  DP:0x80483900
  IPV4V6_INJECT_SBC (M)
  IPV6_INTERNAL_SANITY_CHECK (M)
  IPV6_INPUT_DST_LOOKUP_ISSUE (M)
  IPV6_INPUT_ARL (M)
  IPV6_INPUT_DST_LOOKUP_CONT (M)
  IPV6_INPUT_DST_LOOKUP_CONSUME (M)
  IPV6_INTERNAL_FOR_US (M)
  IPV6_INPUT_LOOKUP_PROCESS (M)
  UPDATE_ICMP6_PKT (M)
  INTERNAL_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 7 - ipv6_output
FIA handle - CP:0x104b593c  DP:0x80483d80
  IPV6_INTERNAL_SANITY_CHECK (M)
  IPV6_OUTPUT_DROP_POLICY (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 8 - layer2_input
FIA handle - CP:0x104b5b10  DP:0x80481500
  LAYER2_INPUT_LOOKUP_PROCESS (M)
  INTERNAL_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 9 - layer2_output
FIA handle - CP:0x104b5adc  DP:0x80481980
  LAYER2_OUTPUT_DROP_POLICY (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 10 - ipv6_mc_input
FIA handle - CP:0x104b5908  DP:0x80484200
  MPASS_SET_IN_VECTOR (M)
  IPV6_INTERNAL_SANITY_CHECK (M)
  IPV6_MC_INPUT_LOOKUP_ISSUE (M)
  IPV6_INPUT_ARL (M)
  IPV6_MC_INPUT_LOOKUP_COMPLETE (M)
  IPV6_MC_INPUT_LOOKUP_PROCESS (M)
  IPV6_MC_INPUT_REPLICATION_MODULE (M)
  IPV6_MC_INPUT_POST_REPLICATION_PROCESSING (M)
  INTERNAL_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 11 - ipv6_mc_output
FIA handle - CP:0x104b58d4  DP:0x80484680
  IPV6_INTERNAL_SANITY_CHECK (M)
  IPV6_OUTPUT_DROP_POLICY (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 12 - ess_switch_upstream
FIA handle - CP:0x104b58a0  DP:0x80484b00
  ESS_INJECT_PREPARE_ESS (M)
  ESS_ENTER_SWITCHING (M)
Protocol 13 - ess_switch_downstream
FIA handle - CP:0x104b586c  DP:0x80484f80
  ESF_OUTPUT_DROP_POLICY (M)
  ESS_PUNT_ADJUST_FINAL (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 14 - ess_ac_input
FIA handle - CP:0x104b5838  DP:0x80485400
  DEF_IF_DROP_FIA (M)
Protocol 15 - input_layer2_switching
FIA handle - CP:0x104b5804  DP:0x80485880
  DEF_IF_DROP_FIA (M)
Protocol 16 - output_layer2_switching
FIA handle - CP:0x104b57d0  DP:0x80485d00
  LAYER2_OUTPUT_DROP_POLICY (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 17 - mpls_input
FIA handle - CP:0x104b579c  DP:0x80486180
  IPV4_INPUT_SANITY (M)
  IPV4_INPUT_DST_LOOKUP_ISSUE (M)
  IPV4_INPUT_ARL (M)
  IPV4_INTERNAL_DST_LOOKUP_CONSUME (M)
  IPV4_INPUT_FOR_US (M)
  IPV4_INPUT_LOOKUP_PROCESS (M)
  IPV4_INPUT_IPOPTIONS_GOTO_OUTPUT_FEATURE (M)
  IPV4_INPUT_IPOPTIONS_PROCESS (M)
Protocol 18 - ipv4_sia_input
FIA handle - CP:0x104b5768  DP:0x80486600
  DEF_IF_DROP_FIA (M)
Protocol 19 - ipv4_sia_output
FIA handle - CP:0x104b5734  DP:0x80486a80
  DEF_IF_DROP_FIA (M)
Protocol 20 - servicewire_input
FIA handle - CP:0x104b5700  DP:0x80486f00
  DEF_IF_DROP_FIA (M)
Protocol 21 - servicewire_output
FIA handle - CP:0x104b56cc  DP:0x80487380
  DEF_IF_DROP_FIA (M)
---- show platform hardware qfp active interface if-name internal0/0/rp:1 ----

General interface information
  Interface Name: internal0/0/rp:1
  Interface state: VALID
  Platform interface handle: 65538
  QFP interface handle: 2
  Rx uidb: 131070
  Tx uidb: 131070
  Channel: 12
Interface Relationships

BGPPA/QPPB interface configuration information
  Ingress: BGPPA/QPPB not configured. flags: 0000
  Egress : BGPPA not configured. flags: 0000

ipv4_input enabled. 
ipv4_output enabled. 
mpls_input enabled. 
mpls_output enabled. 
ipv4_mc_input enabled. 
ipv4_mc_output enabled. 
ipv6_input enabled. 
ipv6_output enabled. 
layer2_input enabled. 
layer2_output enabled. 
ipv6_mc_input enabled. 
ipv6_mc_output enabled. 
ess_switch_upstream enabled. 
ess_switch_downstream enabled. 
ess_ac_input enabled. 
input_layer2_switching enabled. 
output_layer2_switching enabled. 
mpls_input enabled. 
ipv4_sia_input enabled. 
ipv4_sia_output enabled. 
servicewire_input enabled. 
servicewire_output enabled. 

Features Bound to Interface:
 1 GIC FIA state
35 PUNT INJECT DB
25 ipfrag_svr
26 ipreass_svr
27 ipv6reass_svr
Protocol 0 - ipv4_input
FIA handle - CP:0x104b5aa8  DP:0x80481e00
  IPV4V6_INJECT_SBC (M)
  IPV4_INPUT_DST_LOOKUP_ISSUE (M)
  IPV4_INTERNAL_ARL_SANITY (M)
  IPV4_INTERNAL_DST_LOOKUP_CONSUME (M)
  IPV4_INTERNAL_FOR_US (M)
  IPV4_INPUT_LOOKUP_PROCESS (M)
  UPDATE_ICMP_PKT (M)
  INTERNAL_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 1 - ipv4_output
FIA handle - CP:0x104b5a74  DP:0x80482280
  IPV4_INTERNAL_ARL_SANITY (M)
  IPV4_VFR_REFRAG (M)
  IPV4_OUTPUT_DROP_POLICY (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 2 - mpls_input
FIA handle - CP:0x104b5a40  DP:0x80482700
  MPLS_INPUT_LABEL_LOOKUP_ISSUE (M)
  MPLS_INPUT_LABEL_LOOKUP_CONSUME (M)
  MPLS_INPUT_LABEL_LOOKUP_PROCESS (M)
  MPLS_UPDATE_ICMP_PKT (M)
  INTERNAL_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 3 - mpls_output
FIA handle - CP:0x104b5a0c  DP:0x80482b80
  MPLS_OUTPUT_DROP_POLICY (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 4 - ipv4_mc_input
FIA handle - CP:0x104b59d8  DP:0x80483000
  MPASS_SET_IN_VECTOR (M)
  IPV4_MC_INPUT_LOOKUP_ISSUE (M)
  IPV4_INPUT_ARL_SANITY (M)
  IPV4_MC_INTERNAL_LOOKUP_COMPLETE (M)
  IPV4_MC_INPUT_LOOKUP_PROCESS (M)
  IPV4_MC_INPUT_REPLICATION_MODULE (M)
  IPV4_MC_INPUT_POST_REPLICATION_PROCESSING (M)
  INTERNAL_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 5 - ipv4_mc_output
FIA handle - CP:0x104b59a4  DP:0x80483480
  IPV4_INTERNAL_ARL_SANITY (M)
  IPV4_MC_OUTPUT_INTERNAL_INT (M)
  IPV4_OUTPUT_DROP_POLICY (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 6 - ipv6_input
FIA handle - CP:0x104b5970  DP:0x80483900
  IPV4V6_INJECT_SBC (M)
  IPV6_INTERNAL_SANITY_CHECK (M)
  IPV6_INPUT_DST_LOOKUP_ISSUE (M)
  IPV6_INPUT_ARL (M)
  IPV6_INPUT_DST_LOOKUP_CONT (M)
  IPV6_INPUT_DST_LOOKUP_CONSUME (M)
  IPV6_INTERNAL_FOR_US (M)
  IPV6_INPUT_LOOKUP_PROCESS (M)
  UPDATE_ICMP6_PKT (M)
  INTERNAL_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 7 - ipv6_output
FIA handle - CP:0x104b593c  DP:0x80483d80
  IPV6_INTERNAL_SANITY_CHECK (M)
  IPV6_OUTPUT_DROP_POLICY (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 8 - layer2_input
FIA handle - CP:0x104b5b10  DP:0x80481500
  LAYER2_INPUT_LOOKUP_PROCESS (M)
  INTERNAL_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 9 - layer2_output
FIA handle - CP:0x104b5adc  DP:0x80481980
  LAYER2_OUTPUT_DROP_POLICY (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 10 - ipv6_mc_input
FIA handle - CP:0x104b5908  DP:0x80484200
  MPASS_SET_IN_VECTOR (M)
  IPV6_INTERNAL_SANITY_CHECK (M)
  IPV6_MC_INPUT_LOOKUP_ISSUE (M)
  IPV6_INPUT_ARL (M)
  IPV6_MC_INPUT_LOOKUP_COMPLETE (M)
  IPV6_MC_INPUT_LOOKUP_PROCESS (M)
  IPV6_MC_INPUT_REPLICATION_MODULE (M)
  IPV6_MC_INPUT_POST_REPLICATION_PROCESSING (M)
  INTERNAL_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 11 - ipv6_mc_output
FIA handle - CP:0x104b58d4  DP:0x80484680
  IPV6_INTERNAL_SANITY_CHECK (M)
  IPV6_OUTPUT_DROP_POLICY (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 12 - ess_switch_upstream
FIA handle - CP:0x104b58a0  DP:0x80484b00
  ESS_INJECT_PREPARE_ESS (M)
  ESS_ENTER_SWITCHING (M)
Protocol 13 - ess_switch_downstream
FIA handle - CP:0x104b586c  DP:0x80484f80
  ESF_OUTPUT_DROP_POLICY (M)
  ESS_PUNT_ADJUST_FINAL (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 14 - ess_ac_input
FIA handle - CP:0x104b5838  DP:0x80485400
  DEF_IF_DROP_FIA (M)
Protocol 15 - input_layer2_switching
FIA handle - CP:0x104b5804  DP:0x80485880
  DEF_IF_DROP_FIA (M)
Protocol 16 - output_layer2_switching
FIA handle - CP:0x104b57d0  DP:0x80485d00
  LAYER2_OUTPUT_DROP_POLICY (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 17 - mpls_input
FIA handle - CP:0x104b579c  DP:0x80486180
  IPV4_INPUT_SANITY (M)
  IPV4_INPUT_DST_LOOKUP_ISSUE (M)
  IPV4_INPUT_ARL (M)
  IPV4_INTERNAL_DST_LOOKUP_CONSUME (M)
  IPV4_INPUT_FOR_US (M)
  IPV4_INPUT_LOOKUP_PROCESS (M)
  IPV4_INPUT_IPOPTIONS_GOTO_OUTPUT_FEATURE (M)
  IPV4_INPUT_IPOPTIONS_PROCESS (M)
Protocol 18 - ipv4_sia_input
FIA handle - CP:0x104b5768  DP:0x80486600
  DEF_IF_DROP_FIA (M)
Protocol 19 - ipv4_sia_output
FIA handle - CP:0x104b5734  DP:0x80486a80
  DEF_IF_DROP_FIA (M)
Protocol 20 - servicewire_input
FIA handle - CP:0x104b5700  DP:0x80486f00
  DEF_IF_DROP_FIA (M)
Protocol 21 - servicewire_output
FIA handle - CP:0x104b56cc  DP:0x80487380
  DEF_IF_DROP_FIA (M)
---- show platform hardware qfp active interface if-name internal0/0/recycle:0 ----

General interface information
  Interface Name: internal0/0/recycle:0
  Interface state: VALID
  Platform interface handle: 65539
  QFP interface handle: 3
  Rx uidb: 131069
  Tx uidb: 131069
  Channel: 0
Interface Relationships

BGPPA/QPPB interface configuration information
  Ingress: BGPPA/QPPB not configured. flags: 0000
  Egress : BGPPA not configured. flags: 0000

ipv4_input enabled. 
ipv4_output enabled. 
mpls_input enabled. 
mpls_output enabled. 
ipv4_mc_input enabled. 
ipv4_mc_output enabled. 
ipv6_input enabled. 
ipv6_output enabled. 
layer2_input enabled. 
layer2_output enabled. 
ipv6_mc_input enabled. 
ipv6_mc_output enabled. 
ess_switch_upstream enabled. 
ess_switch_downstream enabled. 
ess_ac_input enabled. 
input_layer2_switching enabled. 
output_layer2_switching enabled. 
mpls_input enabled. 
ipv4_sia_input enabled. 
ipv4_sia_output enabled. 
servicewire_input enabled. 
servicewire_output enabled. 

Features Bound to Interface:
 1 GIC FIA state
35 PUNT INJECT DB
25 ipfrag_svr
26 ipreass_svr
27 ipv6reass_svr
Protocol 0 - ipv4_input
FIA handle - CP:0x104b5aa8  DP:0x80481e00
  IPV4V6_INJECT_SBC (M)
  IPV4_INPUT_DST_LOOKUP_ISSUE (M)
  IPV4_INTERNAL_ARL_SANITY (M)
  IPV4_INTERNAL_DST_LOOKUP_CONSUME (M)
  IPV4_INTERNAL_FOR_US (M)
  IPV4_INPUT_LOOKUP_PROCESS (M)
  UPDATE_ICMP_PKT (M)
  INTERNAL_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 1 - ipv4_output
FIA handle - CP:0x104b5a74  DP:0x80482280
  IPV4_INTERNAL_ARL_SANITY (M)
  IPV4_VFR_REFRAG (M)
  IPV4_OUTPUT_DROP_POLICY (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 2 - mpls_input
FIA handle - CP:0x104b5a40  DP:0x80482700
  MPLS_INPUT_LABEL_LOOKUP_ISSUE (M)
  MPLS_INPUT_LABEL_LOOKUP_CONSUME (M)
  MPLS_INPUT_LABEL_LOOKUP_PROCESS (M)
  MPLS_UPDATE_ICMP_PKT (M)
  INTERNAL_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 3 - mpls_output
FIA handle - CP:0x104b5a0c  DP:0x80482b80
  MPLS_OUTPUT_DROP_POLICY (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 4 - ipv4_mc_input
FIA handle - CP:0x104b59d8  DP:0x80483000
  MPASS_SET_IN_VECTOR (M)
  IPV4_MC_INPUT_LOOKUP_ISSUE (M)
  IPV4_INPUT_ARL_SANITY (M)
  IPV4_MC_INTERNAL_LOOKUP_COMPLETE (M)
  IPV4_MC_INPUT_LOOKUP_PROCESS (M)
  IPV4_MC_INPUT_REPLICATION_MODULE (M)
  IPV4_MC_INPUT_POST_REPLICATION_PROCESSING (M)
  INTERNAL_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 5 - ipv4_mc_output
FIA handle - CP:0x104b59a4  DP:0x80483480
  IPV4_INTERNAL_ARL_SANITY (M)
  IPV4_MC_OUTPUT_INTERNAL_INT (M)
  IPV4_OUTPUT_DROP_POLICY (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 6 - ipv6_input
FIA handle - CP:0x104b5970  DP:0x80483900
  IPV4V6_INJECT_SBC (M)
  IPV6_INTERNAL_SANITY_CHECK (M)
  IPV6_INPUT_DST_LOOKUP_ISSUE (M)
  IPV6_INPUT_ARL (M)
  IPV6_INPUT_DST_LOOKUP_CONT (M)
  IPV6_INPUT_DST_LOOKUP_CONSUME (M)
  IPV6_INTERNAL_FOR_US (M)
  IPV6_INPUT_LOOKUP_PROCESS (M)
  UPDATE_ICMP6_PKT (M)
  INTERNAL_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 7 - ipv6_output
FIA handle - CP:0x104b593c  DP:0x80483d80
  IPV6_INTERNAL_SANITY_CHECK (M)
  IPV6_OUTPUT_DROP_POLICY (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 8 - layer2_input
FIA handle - CP:0x104b5b10  DP:0x80481500
  LAYER2_INPUT_LOOKUP_PROCESS (M)
  INTERNAL_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 9 - layer2_output
FIA handle - CP:0x104b5adc  DP:0x80481980
  LAYER2_OUTPUT_DROP_POLICY (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 10 - ipv6_mc_input
FIA handle - CP:0x104b5908  DP:0x80484200
  MPASS_SET_IN_VECTOR (M)
  IPV6_INTERNAL_SANITY_CHECK (M)
  IPV6_MC_INPUT_LOOKUP_ISSUE (M)
  IPV6_INPUT_ARL (M)
  IPV6_MC_INPUT_LOOKUP_COMPLETE (M)
  IPV6_MC_INPUT_LOOKUP_PROCESS (M)
  IPV6_MC_INPUT_REPLICATION_MODULE (M)
  IPV6_MC_INPUT_POST_REPLICATION_PROCESSING (M)
  INTERNAL_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 11 - ipv6_mc_output
FIA handle - CP:0x104b58d4  DP:0x80484680
  IPV6_INTERNAL_SANITY_CHECK (M)
  IPV6_OUTPUT_DROP_POLICY (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 12 - ess_switch_upstream
FIA handle - CP:0x104b58a0  DP:0x80484b00
  ESS_INJECT_PREPARE_ESS (M)
  ESS_ENTER_SWITCHING (M)
Protocol 13 - ess_switch_downstream
FIA handle - CP:0x104b586c  DP:0x80484f80
  ESF_OUTPUT_DROP_POLICY (M)
  ESS_PUNT_ADJUST_FINAL (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 14 - ess_ac_input
FIA handle - CP:0x104b5838  DP:0x80485400
  DEF_IF_DROP_FIA (M)
Protocol 15 - input_layer2_switching
FIA handle - CP:0x104b5804  DP:0x80485880
  DEF_IF_DROP_FIA (M)
Protocol 16 - output_layer2_switching
FIA handle - CP:0x104b57d0  DP:0x80485d00
  LAYER2_OUTPUT_DROP_POLICY (M)
  INTERNAL_TRANSMIT_PKT (M)
Protocol 17 - mpls_input
FIA handle - CP:0x104b579c  DP:0x80486180
  IPV4_INPUT_SANITY (M)
  IPV4_INPUT_DST_LOOKUP_ISSUE (M)
  IPV4_INPUT_ARL (M)
  IPV4_INTERNAL_DST_LOOKUP_CONSUME (M)
  IPV4_INPUT_FOR_US (M)
  IPV4_INPUT_LOOKUP_PROCESS (M)
  IPV4_INPUT_IPOPTIONS_GOTO_OUTPUT_FEATURE (M)
  IPV4_INPUT_IPOPTIONS_PROCESS (M)
Protocol 18 - ipv4_sia_input
FIA handle - CP:0x104b5768  DP:0x80486600
  DEF_IF_DROP_FIA (M)
Protocol 19 - ipv4_sia_output
FIA handle - CP:0x104b5734  DP:0x80486a80
  DEF_IF_DROP_FIA (M)
Protocol 20 - servicewire_input
FIA handle - CP:0x104b5700  DP:0x80486f00
  DEF_IF_DROP_FIA (M)
Protocol 21 - servicewire_output
FIA handle - CP:0x104b56cc  DP:0x80487380
  DEF_IF_DROP_FIA (M)
---- show platform hardware qfp active interface if-name internal0/0/crypto:0 ----

General interface information
  Interface Name: internal0/0/crypto:0
  Interface state: VALID
  Platform interface handle: 65540
  QFP interface handle: 4
  Rx uidb: 131068
  Tx uidb: 131068
  Channel: 16
Interface Relationships

BGPPA/QPPB interface configuration information
  Ingress: BGPPA/QPPB not configured. flags: 0000
  Egress : BGPPA not configured. flags: 0000

ipv4_input enabled. 
ipv4_output enabled. 
mpls_input enabled. 
mpls_output enabled. 
ipv4_mc_input enabled. 
ipv4_mc_output enabled. 
ipv6_input enabled. 
ipv6_output enabled. 
layer2_input enabled. 
layer2_output enabled. 
ipv6_mc_input enabled. 
ipv6_mc_output enabled. 
ess_switch_upstream enabled. 
ess_switch_downstream enabled. 
ess_ac_input enabled. 
input_layer2_switching enabled. 
output_layer2_switching enabled. 
mpls_input enabled. 
ipv4_sia_input enabled. 
ipv4_sia_output enabled. 
servicewire_input enabled. 
servicewire_output enabled. 

Features Bound to Interface:
 1 GIC FIA state
35 PUNT INJECT DB
25 ipfrag_svr
26 ipreass_svr
27 ipv6reass_svr
Protocol 0 - ipv4_input
FIA handle - CP:0x104b5698  DP:0x80487800
  IPV4_INPUT_DST_LOOKUP_ISSUE (M)
  IPV4_INPUT_ARL_SANITY (M)
  IPV4_INPUT_DST_LOOKUP_CONSUME (M)
  IPV4_INPUT_FOR_US_MARTIAN (M)
  IPV4_INPUT_LOOKUP_PROCESS (M)
  IPV4_INPUT_IPOPTIONS_GOTO_OUTPUT_FEATURE (M)
Protocol 1 - ipv4_output
FIA handle - CP:0x104b5664  DP:0x80487c80
  IPV4_VFR_REFRAG (M)
  IPV4_OUTPUT_L2_REWRITE (M)
  IPV4_OUTPUT_FRAG (M)
  IPV4_OUTPUT_DROP_POLICY (M)
  DEF_IF_DROP_FIA (M)
Protocol 2 - mpls_input
FIA handle - CP:0x104b5630  DP:0x80488100
  MPLS_INPUT_SANITY (M)
  MPLS_INPUT_LABEL_LOOKUP_ISSUE (M)
  MPLS_INPUT_LABEL_LOOKUP_CONSUME (M)
  MPLS_INPUT_LABEL_LOOKUP_PROCESS (M)
  MPLS2IP_TRANSITION_FIA (M)
  MPLS_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 3 - mpls_output
FIA handle - CP:0x104b55fc  DP:0x80488580
  IPV4_VFR_REFRAG (M)
  MPLS_OUTPUT_ADD_LABEL (M)
  MPLS_OUTPUT_L2_REWRITE (M)
  MPLS_OUTPUT_FRAG (M)
  MPLS_OUTPUT_DROP_POLICY (M)
  DEF_IF_DROP_FIA (M)
Protocol 4 - ipv4_mc_input
FIA handle - CP:0x104b55c8  DP:0x80488a00
  MPASS_SET_IN_VECTOR (M)
  IPV4_MC_INPUT_LOOKUP_ISSUE (M)
  IPV4_INPUT_SANITY (M)
  IPV4_INPUT_MARTIAN (M)
  IPV4_INPUT_ARL (M)
  IPV4_MC_INPUT_LOOKUP_COMPLETE (M)
  IPV4_MC_INPUT_LOOKUP_PROCESS (M)
  IPV4_MC_INPUT_REPLICATION_MODULE (M)
  IPV4_MC_INPUT_POST_REPLICATION_PROCESSING (M)
  IPV4_INPUT_IPOPTIONS_GOTO_OUTPUT_FEATURE (M)
Protocol 5 - ipv4_mc_output
FIA handle - CP:0x104b5594  DP:0x80488e80
  MPASS_SET_OUT_VECTOR (M)
  IPV4_VFR_REFRAG (M)
  IPV4_OUTPUT_L2_REWRITE (M)
  IPV4_OUTPUT_FRAG (M)
  IPV4_OUTPUT_DROP_POLICY (M)
  DEF_IF_DROP_FIA (M)
Protocol 6 - ipv6_input
FIA handle - CP:0x104b5560  DP:0x80489300
  IPV6_INPUT_SANITY_CHECK (M)
  IPV6_INPUT_DST_LOOKUP_ISSUE (M)
  IPV6_INPUT_ARL (M)
  IPV6_INPUT_DST_LOOKUP_CONT (M)
  IPV6_INPUT_DST_LOOKUP_CONSUME (M)
  IPV6_INPUT_FOR_US (M)
  IPV6_INPUT_LOOKUP_PROCESS (M)
  IPV6_INPUT_LINK_LOCAL_CHECK (M)
  IPV6_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 7 - ipv6_output
FIA handle - CP:0x104b552c  DP:0x80489780
  IPV6_OUTPUT_L2_REWRITE (M)
  IPV6_OUTPUT_FRAG (M)
  IPV6_OUTPUT_DROP_POLICY (M)
  DEF_IF_DROP_FIA (M)
Protocol 8 - layer2_input
FIA handle - CP:0x104b5b78  DP:0x80480c00
  LAYER2_INPUT_SIA (M)
  LAYER2_INPUT_LOOKUP_PROCESS (M)
  LAYER2_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 9 - layer2_output
FIA handle - CP:0x104b5b44  DP:0x80481080
  LAYER2_OUTPUT_SERVICEWIRE (M)
  LAYER2_OUTPUT_DROP_POLICY (M)
  DEF_IF_DROP_FIA (M)
Protocol 10 - ipv6_mc_input
FIA handle - CP:0x104b54f8  DP:0x80489c00
  MPASS_SET_IN_VECTOR (M)
  IPV6_MC_INPUT_LOOKUP_ISSUE (M)
  IPV6_INPUT_ARL (M)
  IPV6_MC_INPUT_LOOKUP_COMPLETE (M)
  IPV6_MC_INPUT_LOOKUP_PROCESS (M)
  IPV6_MC_INPUT_REPLICATION_MODULE (M)
  IPV6_MC_INPUT_POST_REPLICATION_PROCESSING (M)
  IPV6_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 11 - ipv6_mc_output
FIA handle - CP:0x104b54c4  DP:0x8048a080
  MPASS_SET_OUT_VECTOR (M)
  IPV6_OUTPUT_L2_REWRITE (M)
  IPV6_OUTPUT_DROP_POLICY (M)
  DEF_IF_DROP_FIA (M)
Protocol 12 - ess_switch_upstream
FIA handle - CP:0x104b5490  DP:0x8048a500
  ESF_UPSTREAM_IDLE_TIMEOUT (M)
  ESS_IPSUB_DEFAULT_DROP (M)
Protocol 13 - ess_switch_downstream
FIA handle - CP:0x104b545c  DP:0x8048a980
  ESF_DOWNSTREAM_IDLE_TIMEOUT (M)
  ESS_IPSUB_DEFAULT_DROP (M)
Protocol 14 - ess_ac_input
FIA handle - CP:0x104b5428  DP:0x8048ae00
  DEF_IF_DROP_FIA (M)
Protocol 15 - input_layer2_switching
FIA handle - CP:0x104b53f4  DP:0x8048b280
  LAYER2_INPUT_CONTROL_PKT_CHECK (M)
  LAYER2_SWITCHING_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 16 - output_layer2_switching
FIA handle - CP:0x104b53c0  DP:0x8048b700
  LAYER2_OUTPUT_DROP_POLICY (M)
  DEF_IF_DROP_FIA (M)
Protocol 17 - mpls_input
FIA handle - CP:0x104b538c  DP:0x8048bb80
  IPV4_INPUT_SANITY (M)
  IPV4_INPUT_DST_LOOKUP_ISSUE (M)
  IPV4_INPUT_ARL (M)
  IPV4_INTERNAL_DST_LOOKUP_CONSUME (M)
  IPV4_INPUT_FOR_US (M)
  IPV4_INPUT_LOOKUP_PROCESS (M)
  IPV4_INPUT_IPOPTIONS_GOTO_OUTPUT_FEATURE (M)
  IPV4_INPUT_IPOPTIONS_PROCESS (M)
Protocol 18 - ipv4_sia_input
FIA handle - CP:0x104b5358  DP:0x8048c000
  IPV4_INPUT_DST_LOOKUP_ISSUE (M)
  IPV4_INPUT_ARL_SANITY (M)
  IPV4_INTERNAL_DST_LOOKUP_CONSUME (M)
  IPV4_INPUT_FOR_US_MARTIAN (M)
  SIA_IPV4_INPUT_LOOKUP_PROCESS (M)
  SIA_IPV4_INPUT_GOTO_OUTPUT_FEATURE (M)
Protocol 19 - ipv4_sia_output
FIA handle - CP:0x104b5324  DP:0x8048c480
  IPV4_VFR_REFRAG (M)
  IPV4_SIA_PROCESSING (M)
Protocol 20 - servicewire_input
FIA handle - CP:0x104b52f0  DP:0x8048c900
  IPV4_INPUT_DST_LOOKUP_ISSUE (M)
  IPV4_INPUT_ARL_SANITY (M)
  IPV4_INTERNAL_DST_LOOKUP_CONSUME (M)
  IPV4_INPUT_FOR_US_MARTIAN (M)
  IPV4_INPUT_GOTO_SERVICEWIRE_OUTPUT_FEATURE (M)
Protocol 21 - servicewire_output
FIA handle - CP:0x104b52bc  DP:0x8048cd80
  IPV4_VFR_REFRAG (M)
  IPV4_OUTPUT_SERVICEWIRE (M)
---- show platform hardware qfp active infrastructure uidb internal0/0/rp:0 input config ----

internal0/0/rp:0 uidb_index=131071 cpp_num=0
uidb_entry_input_config_st at 0X89184330
  base.fast.default_q_info *  : 0000000000
  base.fast.stats *           : 0X899FB000
  base.fast.l2_overhead       : 0000000000
  base.fast.min_tu            : 0000000000
  base.fast.max_tu            : 0X00002710
  base.fast.vrf               : 0000000000
  base.fast.port_chnl_idx     : 0000000000
  base.encap                  : 0000000000
  base.opp_uidb               : 0X0001FFFF
  base.group_int_uidb         : 0XFFFFFFFF
  base.drop.drop_block *      : 0X899FCC00
  base.drop.dbg_drop_block *  : 0000000000
  base.drop.parent            : 0X8A114700
  base.drop.drop_class        : 0X00000001
  base.ifindex                : 0000000000
  base.ifname *               : 0X89250020
  base.main_int_uidb          : 0XFFFFFFFF
---- show platform hardware qfp active infrastructure uidb internal0/0/rp:1 input config ----

internal0/0/rp:1 uidb_index=131070 cpp_num=0
uidb_entry_input_config_st at 0X89184660
  base.fast.default_q_info *  : 0000000000
  base.fast.stats *           : 0X899FB080
  base.fast.l2_overhead       : 0000000000
  base.fast.min_tu            : 0000000000
  base.fast.max_tu            : 0X00002710
  base.fast.vrf               : 0000000000
  base.fast.port_chnl_idx     : 0000000000
  base.encap                  : 0000000000
  base.opp_uidb               : 0X0001FFFE
  base.group_int_uidb         : 0XFFFFFFFF
  base.drop.drop_block *      : 0X899FCC90
  base.drop.dbg_drop_block *  : 0000000000
  base.drop.parent            : 0X8A114700
  base.drop.drop_class        : 0X00000001
  base.ifindex                : 0000000000
  base.ifname *               : 0X89250040
  base.main_int_uidb          : 0XFFFFFFFF
---- show platform hardware qfp active infrastructure uidb internal0/0/recycle:0 input config ----

internal0/0/recycle:0 uidb_index=131069 cpp_num=0
uidb_entry_input_config_st at 0X89184990
  base.fast.default_q_info *  : 0000000000
  base.fast.stats *           : 0X899FB100
  base.fast.l2_overhead       : 0000000000
  base.fast.min_tu            : 0000000000
  base.fast.max_tu            : 0X00002710
  base.fast.vrf               : 0000000000
  base.fast.port_chnl_idx     : 0000000000
  base.encap                  : 0000000000
  base.opp_uidb               : 0X0001FFFD
  base.group_int_uidb         : 0XFFFFFFFF
  base.drop.drop_block *      : 0X899FCD20
  base.drop.dbg_drop_block *  : 0000000000
  base.drop.parent            : 0X8A114700
  base.drop.drop_class        : 0X00000001
  base.ifindex                : 0000000000
  base.ifname *               : 0X89250060
  base.main_int_uidb          : 0XFFFFFFFF
---- show platform hardware qfp active infrastructure uidb internal0/0/crypto:0 input config ----

internal0/0/crypto:0 uidb_index=131068 cpp_num=0
uidb_entry_input_config_st at 0X89184CC0
  base.fast.default_q_info *  : 0000000000
  base.fast.stats *           : 0X899FB180
  base.fast.l2_overhead       : 0000000000
  base.fast.min_tu            : 0000000000
  base.fast.max_tu            : 0X00002710
  base.fast.vrf               : 0000000000
  base.fast.port_chnl_idx     : 0000000000
  base.encap                  : 0000000000
  base.opp_uidb               : 0X0001FFFC
  base.group_int_uidb         : 0XFFFFFFFF
  base.drop.drop_block *      : 0X899FCDB0
  base.drop.dbg_drop_block *  : 0000000000
  base.drop.parent            : 0X8A114700
  base.drop.drop_class        : 0X00000001
  base.ifindex                : 0000000000
  base.ifname *               : 0X89250080
  base.main_int_uidb          : 0XFFFFFFFF
---- show platform hardware qfp active infrastructure uidb internal0/0/rp:0 output config ----

internal0/0/rp:0 uidb_index=131071 cpp_num=0
uidb_entry_output_config_st at 0X896582E0
  base.fast.default_q_info *  : 0X89727C00
  base.fast.stats *           : 0X899FE800
  base.fast.l2_overhead       : 0000000000
  base.fast.min_tu            : 0000000000
  base.fast.max_tu            : 0X00002710
  base.fast.vrf               : 0000000000
  base.fast.port_chnl_idx     : 0000000000
  base.encap                  : 0000000000
  base.opp_uidb               : 0X0001FFFF
  base.group_int_uidb         : 0XFFFFFFFF
  base.drop.drop_block *      : 0X89A00400
  base.drop.dbg_drop_block *  : 0000000000
  base.drop.parent            : 0X8A114700
  base.drop.drop_class        : 0X00000001
  base.ifindex                : 0000000000
  base.ifname *               : 0X89710020
  base.main_int_uidb          : 0XFFFFFFFF
---- show platform hardware qfp active infrastructure uidb internal0/0/rp:1 output config ----

internal0/0/rp:1 uidb_index=131070 cpp_num=0
uidb_entry_output_config_st at 0X896585C0
  base.fast.default_q_info *  : 0X89727C20
  base.fast.stats *           : 0X899FE860
  base.fast.l2_overhead       : 0000000000
  base.fast.min_tu            : 0000000000
  base.fast.max_tu            : 0X00002710
  base.fast.vrf               : 0000000000
  base.fast.port_chnl_idx     : 0000000000
  base.encap                  : 0000000000
  base.opp_uidb               : 0X0001FFFE
  base.group_int_uidb         : 0XFFFFFFFF
  base.drop.drop_block *      : 0X89A00490
  base.drop.dbg_drop_block *  : 0000000000
  base.drop.parent            : 0X8A114700
  base.drop.drop_class        : 0X00000001
  base.ifindex                : 0000000000
  base.ifname *               : 0X89710040
  base.main_int_uidb          : 0XFFFFFFFF
---- show platform hardware qfp active infrastructure uidb internal0/0/recycle:0 output config ----

internal0/0/recycle:0 uidb_index=131069 cpp_num=0
uidb_entry_output_config_st at 0X896588A0
  base.fast.default_q_info *  : 0000000000
  base.fast.stats *           : 0X899FE8C0
  base.fast.l2_overhead       : 0000000000
  base.fast.min_tu            : 0000000000
  base.fast.max_tu            : 0X00002710
  base.fast.vrf               : 0000000000
  base.fast.port_chnl_idx     : 0000000000
  base.encap                  : 0000000000
  base.opp_uidb               : 0X0001FFFD
  base.group_int_uidb         : 0XFFFFFFFF
  base.drop.drop_block *      : 0X89A00520
  base.drop.dbg_drop_block *  : 0000000000
  base.drop.parent            : 0X8A114700
  base.drop.drop_class        : 0X00000001
  base.ifindex                : 0000000000
  base.ifname *               : 0X89710060
  base.main_int_uidb          : 0XFFFFFFFF
---- show platform hardware qfp active infrastructure uidb internal0/0/crypto:0 output config ----

internal0/0/crypto:0 uidb_index=131068 cpp_num=0
uidb_entry_output_config_st at 0X89658B80
  base.fast.default_q_info *  : 0X89727C60
  base.fast.stats *           : 0X899FE920
  base.fast.l2_overhead       : 0000000000
  base.fast.min_tu            : 0000000000
  base.fast.max_tu            : 0X00002710
  base.fast.vrf               : 0000000000
  base.fast.port_chnl_idx     : 0000000000
  base.encap                  : 0000000000
  base.opp_uidb               : 0X0001FFFC
  base.group_int_uidb         : 0XFFFFFFFF
  base.drop.drop_block *      : 0X89A005B0
  base.drop.dbg_drop_block *  : 0000000000
  base.drop.parent            : 0X8A114700
  base.drop.drop_class        : 0X00000001
  base.ifindex                : 0000000000
  base.ifname *               : 0X89710080
  base.main_int_uidb          : 0XFFFFFFFF
---- show platform hardware qfp active infrastructure punt statistics interface 1 ----

INTERFACE:

  QFP interface handle      1
  platform interface handle 65537

Per Interface Punt-Inject statistics

  received punt packets      2365102
  transmitted punt packets   28922203
  received inject packets    24936927
  transmitted inject packets 107930

Punt Sub-block Configuration

  ingress QFP index    0 
  egress  QFP index    0 
  QFP interface handle 1 
  ingress subblock pointer 0x8971FC00
  egress subblock pointer  0x8971FC10

Ingress configuration from punt database

  per interface statistics pointer 0x899F9400
  per cause RX statistics pointer  0x899F8C00
  per cause TX statistics pointer  0x899F9000
  platform interface handle        65537

Egress configuration from punt database

  per interface statistics pointer 0x899F9400
  per cause RX statistics pointer  0x899F8C00
  per cause TX statistics pointer  0x899F9000
  platform interface handle        65537

Ingress configuration from QFP DRAM

  per interface statistics pointer 0x899F9400
  per cause RX statistics pointer  0x899F8C00
  per cause TX statistics pointer  0x899F9000
  platform interface handle        65537

Egress configuration from QFP DRAM

  per interface statistics pointer 0x899F9400
  per cause RX statistics pointer  0x899F8C00
  per cause TX statistics pointer  0x899F9000
  platform interface handle        65537

---- show platform hardware qfp active infrastructure punt statistics interface 2 ----

INTERFACE:

  QFP interface handle      2
  platform interface handle 65538

Per Interface Punt-Inject statistics

  received punt packets      0
  transmitted punt packets   0
  received inject packets    0
  transmitted inject packets 0

Punt Sub-block Configuration

  ingress QFP index    0 
  egress  QFP index    0 
  QFP interface handle 2 
  ingress subblock pointer 0x8971FC20
  egress subblock pointer  0x8971FC30

Ingress configuration from punt database

  per interface statistics pointer 0x899F9420
  per cause RX statistics pointer  0x899F8C00
  per cause TX statistics pointer  0x899F9000
  platform interface handle        65538

Egress configuration from punt database

  per interface statistics pointer 0x899F9420
  per cause RX statistics pointer  0x899F8C00
  per cause TX statistics pointer  0x899F9000
  platform interface handle        65538

Ingress configuration from QFP DRAM

  per interface statistics pointer 0x899F9420
  per cause RX statistics pointer  0x899F8C00
  per cause TX statistics pointer  0x899F9000
  platform interface handle        65538

Egress configuration from QFP DRAM

  per interface statistics pointer 0x899F9420
  per cause RX statistics pointer  0x899F8C00
  per cause TX statistics pointer  0x899F9000
  platform interface handle        65538

---- show platform hardware qfp active infrastructure punt statistics interface 3 ----

INTERFACE:

  QFP interface handle      3
  platform interface handle 65539

Per Interface Punt-Inject statistics

  received punt packets      0
  transmitted punt packets   21083469
  received inject packets    21084531
  transmitted inject packets 0

Punt Sub-block Configuration

  ingress QFP index    0 
  egress  QFP index    0 
  QFP interface handle 3 
  ingress subblock pointer 0x8971FC40
  egress subblock pointer  0x8971FC50

Ingress configuration from punt database

  per interface statistics pointer 0x899F9440
  per cause RX statistics pointer  0x899F8C00
  per cause TX statistics pointer  0x899F9000
  platform interface handle        65539

Egress configuration from punt database

  per interface statistics pointer 0x899F9440
  per cause RX statistics pointer  0x899F8C00
  per cause TX statistics pointer  0x899F9000
  platform interface handle        65539

Ingress configuration from QFP DRAM

  per interface statistics pointer 0x899F9440
  per cause RX statistics pointer  0x899F8C00
  per cause TX statistics pointer  0x899F9000
  platform interface handle        65539

Egress configuration from QFP DRAM

  per interface statistics pointer 0x899F9440
  per cause RX statistics pointer  0x899F8C00
  per cause TX statistics pointer  0x899F9000
  platform interface handle        65539

---- show platform hardware qfp active infrastructure punt statistics interface 4 ----

INTERFACE:

  QFP interface handle      4
  platform interface handle 65540

Per Interface Punt-Inject statistics

  received punt packets      0
  transmitted punt packets   0
  received inject packets    0
  transmitted inject packets 0

Punt Sub-block Configuration

  ingress QFP index    0 
  egress  QFP index    0 
  QFP interface handle 4 
  ingress subblock pointer 0x8971FC60
  egress subblock pointer  0x8971FC70

Ingress configuration from punt database

  per interface statistics pointer 0x899F9460
  per cause RX statistics pointer  0x899F8C00
  per cause TX statistics pointer  0x899F9000
  platform interface handle        65540

Egress configuration from punt database

  per interface statistics pointer 0x899F9460
  per cause RX statistics pointer  0x899F8C00
  per cause TX statistics pointer  0x899F9000
  platform interface handle        65540

Ingress configuration from QFP DRAM

  per interface statistics pointer 0x899F9460
  per cause RX statistics pointer  0x899F8C00
  per cause TX statistics pointer  0x899F9000
  platform interface handle        65540

Egress configuration from QFP DRAM

  per interface statistics pointer 0x899F9460
  per cause RX statistics pointer  0x899F8C00
  per cause TX statistics pointer  0x899F9000
  platform interface handle        65540

---- show platform hardware qfp active interface if-name internal0/0/rp:0 statistics ----

Platform Handle 65537
----------------------------------------------------------------
Receive Stats                             Packets        Octets 
----------------------------------------------------------------
  Ipv4                                     208           96767
  Ipv6                                       0               0
  Tag                                        0               0
  McastIpv4                                  0               0
  McastIpv6                                  0               0
  Other                                      2             192

----------------------------------------------------------------
Transmit Stats                            Packets        Octets 
----------------------------------------------------------------
  Ipv4                                     140           15832
  Ipv6                                       0               0
  Tag                                        0               0
  McastIpv4                                  0               0
  McastIpv6                                  0               0
  Other                                      7             424

----------------------------------------------------------------
Input Drop Stats                          Packets        Octets 
----------------------------------------------------------------
  Ingress Drop stats are not enabled on this interface

----------------------------------------------------------------
Output Drop Stats                         Packets        Octets 
----------------------------------------------------------------
  The Egress Drop stats are not enabled on this interface

----------------------------------------------------------------
Drop Stats Summary:
note: 1) these drop stats are only updated when PAL
         reads the interface stats.
      2) the interface stats include the subinterface

Interface                                       Rx Pkts             Tx Pkts
---------------------------------------------------------------------------
internal0/0/rp:0                                  17708                   0

---- show platform hardware qfp active interface if-name internal0/0/rp:1 statistics ----

Platform Handle 65538
----------------------------------------------------------------
Receive Stats                             Packets        Octets 
----------------------------------------------------------------
  Ipv4                                       0               0
  Ipv6                                       0               0
  Tag                                        0               0
  McastIpv4                                  0               0
  McastIpv6                                  0               0
  Other                                      0               0

----------------------------------------------------------------
Transmit Stats                            Packets        Octets 
----------------------------------------------------------------
  Ipv4                                       0               0
  Ipv6                                       0               0
  Tag                                        0               0
  McastIpv4                                  0               0
  McastIpv6                                  0               0
  Other                                      0               0

----------------------------------------------------------------
Input Drop Stats                          Packets        Octets 
----------------------------------------------------------------
  Ingress Drop stats are not enabled on this interface

----------------------------------------------------------------
Output Drop Stats                         Packets        Octets 
----------------------------------------------------------------
  The Egress Drop stats are not enabled on this interface

---- show platform hardware qfp active interface if-name internal0/0/recycle:0 statistics ----

Platform Handle 65539
----------------------------------------------------------------
Receive Stats                             Packets        Octets 
----------------------------------------------------------------
  Ipv4                                      50            4800
  Ipv6                                       0               0
  Tag                                        0               0
  McastIpv4                                  0               0
  McastIpv6                                  0               0
  Other                                      0               0

----------------------------------------------------------------
Transmit Stats                            Packets        Octets 
----------------------------------------------------------------
  Ipv4                                      50            4800
  Ipv6                                       0               0
  Tag                                        0               0
  McastIpv4                                  0               0
  McastIpv6                                  0               0
  Other                                      0               0

----------------------------------------------------------------
Input Drop Stats                          Packets        Octets 
----------------------------------------------------------------
  Ingress Drop stats are not enabled on this interface

----------------------------------------------------------------
Output Drop Stats                         Packets        Octets 
----------------------------------------------------------------
  The Egress Drop stats are not enabled on this interface

----------------------------------------------------------------
Drop Stats Summary:
note: 1) these drop stats are only updated when PAL
         reads the interface stats.
      2) the interface stats include the subinterface

Interface                                       Rx Pkts             Tx Pkts
---------------------------------------------------------------------------
internal0/0/recycle:0                                 1                   0

---- show platform hardware qfp active interface if-name internal0/0/crypto:0 statistics ----

Platform Handle 65540
----------------------------------------------------------------
Receive Stats                             Packets        Octets 
----------------------------------------------------------------
  Ipv4                                       0               0
  Ipv6                                       0               0
  Tag                                        0               0
  McastIpv4                                  0               0
  McastIpv6                                  0               0
  Other                                      0               0

----------------------------------------------------------------
Transmit Stats                            Packets        Octets 
----------------------------------------------------------------
  Ipv4                                       0               0
  Ipv6                                       0               0
  Tag                                        0               0
  McastIpv4                                  0               0
  McastIpv6                                  0               0
  Other                                      0               0

----------------------------------------------------------------
Input Drop Stats                          Packets        Octets 
----------------------------------------------------------------
  Ingress Drop stats are not enabled on this interface

----------------------------------------------------------------
Output Drop Stats                         Packets        Octets 
----------------------------------------------------------------
  The Egress Drop stats are not enabled on this interface

---- show platform hardware qfp active infrastructure punt statistics type per-cause ----

Global Per Cause Statistics

  Number of punt causes =   63 

  Per Punt Cause Statistics
                                                        Packets          Packets
  Counter ID  Punt Cause Name                           Received         Transmitted      
  --------------------------------------------------------------------------------------
  000         Reserved                                  0                0                
  001         MPLS ICMP Can't Fragment                  0                0                
  002         IPv4 Options                              12               0                
  003         Layer2 control and legacy                 300934           300934           
  004         PPP Control                               0                0                
  005         CLNS IS-IS Control                        0                0                
  006         HDLC keepalives                           0                0                
  007         ARP request or response                   463389           463389           
  008         Reverse ARP request or repsonse           55               55               
  009         Frame-relay LMI Control                   0                0                
  010         Incomplete adjacency                      2048             2048             
  011         For-us data                               20590444         20591444         
  012         Mcast Directly Connected Source           0                0                
  013         Mcast IPv4 Options data packet            0                0                
  014         Skip egress processing                    0                0                
  015         MPLS TTL expired                          0                0                
  016         MPLS Reserved label (ie: 0-15)            0                0                
  017         IPv6 Bad hop limit                        0                0                
  018         IPV6 Hop-by-hop Options                   0                0                
  019         Mcast Internal Copy                       0                0                
  020         Generic QFP generated packet              0                0                
  021         RP<->QFP keepalive                        2257173          2257173          
  022         QFP Fwall generated packet                0                0                
  023         Mcast IGMP Unroutable                     0                0                
  024         Glean adjacency                           301127           301127           
  025         Mcast PIM signaling                       0                0                
  026         QFP ICMP generated packet                 21083537         21084538         
  027         ESS session control                       0                0                
  028         ESS data switching back                   0                0                
  029         RP handled ICMP                           431              431              
  030         RP injected For-us data                   0                0                
  031         Punt adjacency                            0                0                
  032         SBC RTP DTMF                              0                0                
  033         Pseudowire VCCV control channel           0                0                
  034         Generic QFP generated packet (keep GPM)   0                0                
  035         Ethernet slow protocol (ie: LACP, OAM)    0                0                
  036         Ethernet OAM Loopback                     0                0                
  037         Egress to Ingress redirect                0                0                
  038         SPA IPC packet                            0                0                
  039         Punt and replicate                        0                0                
  040         PPPoE control                             0                0                
  041         PPPoE session                             0                0                
  042         L2TP control                              0                0                
  043         IP Subscriber control (ie: FSOL, keep...  0                0                
  044         L2TP session                              0                0                
  045         BFD control                               0                0                
  046         MVPN non-RPF signaling packet             0                0                
  047         MVPN PIM signalling packet                0                0                
  048         Mcast punt to RP                          0                0                
  049         SBC generated packet                      0                0                
  050         IPv6 packet                               0                0                
  051         DMVPN NHRP redirect                       0                0                
  052         PFR monitored prefix logging              0                0                
  053         PFR top talkers logging                   0                0                
  054         PFR top talkers application logging       0                0                
  055         For-us control                            4899294          4899294          
  056         RP injected for-us control                0                0                
  057         QFP VTCP generated packet                 0                0                
  058         Layer2 bridge domain packet               0                0                
  059         QFP Stile generated packet                0                0                
  060         IP subnet or broadcast packet             108341           108341           
  061         Ethernet CFM packet                       0                0                
  062         Ethernet CFM notify packet                0                0                


  Number of inject causes = 23

  Per Inject Cause Statistics
                                                        Packets          Packets
  Counter ID  Inject Cause Name                         Received         Transmitted      
  --------------------------------------------------------------------------------------
  000         RESERVED                                  0                0                
  001         L2 control/legacy                         0                0                
  002         QFP destination lookup                    21371637         21353929         
  003         QFP IPv4/v6 nexthop lookup                34               34               
  004         QFP generated packet                      0                0                
  005         QFP <->RP keepalive                       2257173          0                
  006         QFP Fwall generated packet                0                0                
  007         QFP adjacency-id lookup                   640649           640649           
  008         Mcast specific inject packet              0                0                
  009         QFP ICMP generated packet                 21084538         21084537         
  010         QFP/RP->QFP ESS data packet               0                0                
  011         SBC DTMF                                  0                0                
  012         ARP request or response                   667480           667480           
  013         Ethernet OAM loopback packet              0                0                
  014         Ingress redirect packet                   0                0                
  015         PPPoE discovery packet                    0                0                
  016         PPPoE session packet                      0                0                
  017         QFP inject for pp_index lookup            0                0                
  018         QFP inject replicate                      0                0                
  019         QFP inject PIT lookup                     0                0                
  020         SBC generated packets                     0                0                
  021         QFP VTCP generated packet                 0                0                
  022         QFP Stile generated packet                0                0                
---- show platform hardware qfp active infrastructure punt statistics type global-drop ----

Global Drop Statistics

  Number of global drop counters = 21

  Counter ID  Drop Counter Name                         Packets          
  ---------------------------------------------------------------------
  000         INVALID_COUNTER_SELECTED                  0                
  001         INIT_PUNT_INVALID_PUNT_MODE               0                
  002         INIT_PUNT_INVALID_PUNT_CAUSE              0                
  003         INIT_PUNT_INVALID_INJECT_CAUSE            0                
  004         INIT_PUNT_MISSING_FEATURE_HDR_CALLBACK    0                
  005         INIT_PUNT_EXT_PATH_VECTOR_REQUIRED        0                
  006         INIT_PUNT_EXT_PATH_VECTOR_NOT_SUPPORTED   0                
  007         INIT_INJ_INVALID_INJECT_CAUSE             0                
  008         INIT_INJ_MISSING_FEATURE_HDR_CALLBACK     0                
  009         PUNT_INVALID_PUNT_CAUSE                   0                
  010         PUNT_INVALID_COMMON_HDR_VERSION           0                
  011         PUNT_INVALID_PLATFORM_HDR_VERSION         0                
  012         PUNT_PATH_NOT_INITIALIZED                 0                
  013         PUNT_GPM_ALLOC_FAILURE                    0                
  014         PUNT_TRANSITION_FAILURE                   0                
  015         PUNT_DELAYED_PUNT_PKT_SB_NOT_IN_USE       0                
  016         PUNT_CAUSE_GLOBAL_POLICER                 0                
  017         INJ_INVALID_INJECT_CAUSE                  0                
  018         INJ_INVALID_COMMON_HDR_VERSION            0                
  019         INJ_INVALID_PLATFORM_HDR_VERSION          0                
  020         INJ_INVALID_PAL_HDR_FORMAT                0                
---- show platform hardware qfp active infrastructure punt statistics type punt-drop ----

Punt Drop Statistics

  Number of punt causes = 63

  Drop Counter ID   0     Drop Counter Name PUNT_NOT_ENABLED_BY_DATA_PLANE

  Counter ID  Punt Cause Name                           Packets          
  ---------------------------------------------------------------------
  000         Reserved                                  0                
  001         MPLS ICMP Can't Fragment                  0                
  002         IPv4 Options                              0                
  003         Layer2 control and legacy                 0                
  004         PPP Control                               0                
  005         CLNS IS-IS Control                        0                
  006         HDLC keepalives                           0                
  007         ARP request or response                   0                
  008         Reverse ARP request or repsonse           0                
  009         Frame-relay LMI Control                   0                
  010         Incomplete adjacency                      0                
  011         For-us data                               0                
  012         Mcast Directly Connected Source           0                
  013         Mcast IPv4 Options data packet            0                
  014         Skip egress processing                    0                
  015         MPLS TTL expired                          0                
  016         MPLS Reserved label (ie: 0-15)            0                
  017         IPv6 Bad hop limit                        0                
  018         IPV6 Hop-by-hop Options                   0                
  019         Mcast Internal Copy                       0                
  020         Generic QFP generated packet              0                
  021         RP<->QFP keepalive                        0                
  022         QFP Fwall generated packet                0                
  023         Mcast IGMP Unroutable                     0                
  024         Glean adjacency                           0                
  025         Mcast PIM signaling                       0                
  026         QFP ICMP generated packet                 0                
  027         ESS session control                       0                
  028         ESS data switching back                   0                
  029         RP handled ICMP                           0                
  030         RP injected For-us data                   0                
  031         Punt adjacency                            0                
  032         SBC RTP DTMF                              0                
  033         Pseudowire VCCV control channel           0                
  034         Generic QFP generated packet (keep GPM)   0                
  035         Ethernet slow protocol (ie: LACP, OAM)    0                
  036         Ethernet OAM Loopback                     0                
  037         Egress to Ingress redirect                0                
  038         SPA IPC packet                            0                
  039         Punt and replicate                        0                
  040         PPPoE control                             0                
  041         PPPoE session                             0                
  042         L2TP control                              0                
  043         IP Subscriber control (ie: FSOL, keep...  0                
  044         L2TP session                              0                
  045         BFD control                               0                
  046         MVPN non-RPF signaling packet             0                
  047         MVPN PIM signalling packet                0                
  048         Mcast punt to RP                          0                
  049         SBC generated packet                      0                
  050         IPv6 packet                               0                
  051         DMVPN NHRP redirect                       0                
  052         PFR monitored prefix logging              0                
  053         PFR top talkers logging                   0                
  054         PFR top talkers application logging       0                
  055         For-us control                            0                
  056         RP injected for-us control                0                
  057         QFP VTCP generated packet                 0                
  058         Layer2 bridge domain packet               0                
  059         QFP Stile generated packet                0                
  060         IP subnet or broadcast packet             0                
  061         Ethernet CFM packet                       0                
  062         Ethernet CFM notify packet                0                

  Drop Counter ID   1     Drop Counter Name PUNT_NOT_ENABLED_BY_CLIENT

  Counter ID  Punt Cause Name                           Packets          
  ---------------------------------------------------------------------
  000         Reserved                                  0                
  001         MPLS ICMP Can't Fragment                  0                
  002         IPv4 Options                              0                
  003         Layer2 control and legacy                 0                
  004         PPP Control                               0                
  005         CLNS IS-IS Control                        0                
  006         HDLC keepalives                           0                
  007         ARP request or response                   0                
  008         Reverse ARP request or repsonse           0                
  009         Frame-relay LMI Control                   0                
  010         Incomplete adjacency                      0                
  011         For-us data                               0                
  012         Mcast Directly Connected Source           0                
  013         Mcast IPv4 Options data packet            0                
  014         Skip egress processing                    0                
  015         MPLS TTL expired                          0                
  016         MPLS Reserved label (ie: 0-15)            0                
  017         IPv6 Bad hop limit                        0                
  018         IPV6 Hop-by-hop Options                   0                
  019         Mcast Internal Copy                       0                
  020         Generic QFP generated packet              0                
  021         RP<->QFP keepalive                        0                
  022         QFP Fwall generated packet                0                
  023         Mcast IGMP Unroutable                     0                
  024         Glean adjacency                           0                
  025         Mcast PIM signaling                       0                
  026         QFP ICMP generated packet                 0                
  027         ESS session control                       0                
  028         ESS data switching back                   0                
  029         RP handled ICMP                           0                
  030         RP injected For-us data                   0                
  031         Punt adjacency                            0                
  032         SBC RTP DTMF                              0                
  033         Pseudowire VCCV control channel           0                
  034         Generic QFP generated packet (keep GPM)   0                
  035         Ethernet slow protocol (ie: LACP, OAM)    0                
  036         Ethernet OAM Loopback                     0                
  037         Egress to Ingress redirect                0                
  038         SPA IPC packet                            0                
  039         Punt and replicate                        0                
  040         PPPoE control                             0                
  041         PPPoE session                             0                
  042         L2TP control                              0                
  043         IP Subscriber control (ie: FSOL, keep...  0                
  044         L2TP session                              0                
  045         BFD control                               0                
  046         MVPN non-RPF signaling packet             0                
  047         MVPN PIM signalling packet                0                
  048         Mcast punt to RP                          0                
  049         SBC generated packet                      0                
  050         IPv6 packet                               0                
  051         DMVPN NHRP redirect                       0                
  052         PFR monitored prefix logging              0                
  053         PFR top talkers logging                   0                
  054         PFR top talkers application logging       0                
  055         For-us control                            0                
  056         RP injected for-us control                0                
  057         QFP VTCP generated packet                 0                
  058         Layer2 bridge domain packet               0                
  059         QFP Stile generated packet                0                
  060         IP subnet or broadcast packet             0                
  061         Ethernet CFM packet                       0                
  062         Ethernet CFM notify packet                0                

  Drop Counter ID   2     Drop Counter Name PUNT_NULL_INSTANCE

  Counter ID  Punt Cause Name                           Packets          
  ---------------------------------------------------------------------
  000         Reserved                                  0                
  001         MPLS ICMP Can't Fragment                  0                
  002         IPv4 Options                              0                
  003         Layer2 control and legacy                 0                
  004         PPP Control                               0                
  005         CLNS IS-IS Control                        0                
  006         HDLC keepalives                           0                
  007         ARP request or response                   0                
  008         Reverse ARP request or repsonse           0                
  009         Frame-relay LMI Control                   0                
  010         Incomplete adjacency                      0                
  011         For-us data                               0                
  012         Mcast Directly Connected Source           0                
  013         Mcast IPv4 Options data packet            0                
  014         Skip egress processing                    0                
  015         MPLS TTL expired                          0                
  016         MPLS Reserved label (ie: 0-15)            0                
  017         IPv6 Bad hop limit                        0                
  018         IPV6 Hop-by-hop Options                   0                
  019         Mcast Internal Copy                       0                
  020         Generic QFP generated packet              0                
  021         RP<->QFP keepalive                        0                
  022         QFP Fwall generated packet                0                
  023         Mcast IGMP Unroutable                     0                
  024         Glean adjacency                           0                
  025         Mcast PIM signaling                       0                
  026         QFP ICMP generated packet                 0                
  027         ESS session control                       0                
  028         ESS data switching back                   0                
  029         RP handled ICMP                           0                
  030         RP injected For-us data                   0                
  031         Punt adjacency                            0                
  032         SBC RTP DTMF                              0                
  033         Pseudowire VCCV control channel           0                
  034         Generic QFP generated packet (keep GPM)   0                
  035         Ethernet slow protocol (ie: LACP, OAM)    0                
  036         Ethernet OAM Loopback                     0                
  037         Egress to Ingress redirect                0                
  038         SPA IPC packet                            0                
  039         Punt and replicate                        0                
  040         PPPoE control                             0                
  041         PPPoE session                             0                
  042         L2TP control                              0                
  043         IP Subscriber control (ie: FSOL, keep...  0                
  044         L2TP session                              0                
  045         BFD control                               0                
  046         MVPN non-RPF signaling packet             0                
  047         MVPN PIM signalling packet                0                
  048         Mcast punt to RP                          0                
  049         SBC generated packet                      0                
  050         IPv6 packet                               0                
  051         DMVPN NHRP redirect                       0                
  052         PFR monitored prefix logging              0                
  053         PFR top talkers logging                   0                
  054         PFR top talkers application logging       0                
  055         For-us control                            0                
  056         RP injected for-us control                0                
  057         QFP VTCP generated packet                 0                
  058         Layer2 bridge domain packet               0                
  059         QFP Stile generated packet                0                
  060         IP subnet or broadcast packet             0                
  061         Ethernet CFM packet                       0                
  062         Ethernet CFM notify packet                0                

  Drop Counter ID   3     Drop Counter Name PUNT_NULL_PUNT_DEST_INFO

  Counter ID  Punt Cause Name                           Packets          
  ---------------------------------------------------------------------
  000         Reserved                                  0                
  001         MPLS ICMP Can't Fragment                  0                
  002         IPv4 Options                              0                
  003         Layer2 control and legacy                 0                
  004         PPP Control                               0                
  005         CLNS IS-IS Control                        0                
  006         HDLC keepalives                           0                
  007         ARP request or response                   0                
  008         Reverse ARP request or repsonse           0                
  009         Frame-relay LMI Control                   0                
  010         Incomplete adjacency                      0                
  011         For-us data                               0                
  012         Mcast Directly Connected Source           0                
  013         Mcast IPv4 Options data packet            0                
  014         Skip egress processing                    0                
  015         MPLS TTL expired                          0                
  016         MPLS Reserved label (ie: 0-15)            0                
  017         IPv6 Bad hop limit                        0                
  018         IPV6 Hop-by-hop Options                   0                
  019         Mcast Internal Copy                       0                
  020         Generic QFP generated packet              0                
  021         RP<->QFP keepalive                        0                
  022         QFP Fwall generated packet                0                
  023         Mcast IGMP Unroutable                     0                
  024         Glean adjacency                           0                
  025         Mcast PIM signaling                       0                
  026         QFP ICMP generated packet                 0                
  027         ESS session control                       0                
  028         ESS data switching back                   0                
  029         RP handled ICMP                           0                
  030         RP injected For-us data                   0                
  031         Punt adjacency                            0                
  032         SBC RTP DTMF                              0                
  033         Pseudowire VCCV control channel           0                
  034         Generic QFP generated packet (keep GPM)   0                
  035         Ethernet slow protocol (ie: LACP, OAM)    0                
  036         Ethernet OAM Loopback                     0                
  037         Egress to Ingress redirect                0                
  038         SPA IPC packet                            0                
  039         Punt and replicate                        0                
  040         PPPoE control                             0                
  041         PPPoE session                             0                
  042         L2TP control                              0                
  043         IP Subscriber control (ie: FSOL, keep...  0                
  044         L2TP session                              0                
  045         BFD control                               0                
  046         MVPN non-RPF signaling packet             0                
  047         MVPN PIM signalling packet                0                
  048         Mcast punt to RP                          0                
  049         SBC generated packet                      0                
  050         IPv6 packet                               0                
  051         DMVPN NHRP redirect                       0                
  052         PFR monitored prefix logging              0                
  053         PFR top talkers logging                   0                
  054         PFR top talkers application logging       0                
  055         For-us control                            0                
  056         RP injected for-us control                0                
  057         QFP VTCP generated packet                 0                
  058         Layer2 bridge domain packet               0                
  059         QFP Stile generated packet                0                
  060         IP subnet or broadcast packet             0                
  061         Ethernet CFM packet                       0                
  062         Ethernet CFM notify packet                0                

  Drop Counter ID   4     Drop Counter Name PI_PUNT_COPY_AND_RTN_REPLICATE_FAILED

  Counter ID  Punt Cause Name                           Packets          
  ---------------------------------------------------------------------
  000         Reserved                                  0                
  001         MPLS ICMP Can't Fragment                  0                
  002         IPv4 Options                              0                
  003         Layer2 control and legacy                 0                
  004         PPP Control                               0                
  005         CLNS IS-IS Control                        0                
  006         HDLC keepalives                           0                
  007         ARP request or response                   0                
  008         Reverse ARP request or repsonse           0                
  009         Frame-relay LMI Control                   0                
  010         Incomplete adjacency                      0                
  011         For-us data                               0                
  012         Mcast Directly Connected Source           0                
  013         Mcast IPv4 Options data packet            0                
  014         Skip egress processing                    0                
  015         MPLS TTL expired                          0                
  016         MPLS Reserved label (ie: 0-15)            0                
  017         IPv6 Bad hop limit                        0                
  018         IPV6 Hop-by-hop Options                   0                
  019         Mcast Internal Copy                       0                
  020         Generic QFP generated packet              0                
  021         RP<->QFP keepalive                        0                
  022         QFP Fwall generated packet                0                
  023         Mcast IGMP Unroutable                     0                
  024         Glean adjacency                           0                
  025         Mcast PIM signaling                       0                
  026         QFP ICMP generated packet                 0                
  027         ESS session control                       0                
  028         ESS data switching back                   0                
  029         RP handled ICMP                           0                
  030         RP injected For-us data                   0                
  031         Punt adjacency                            0                
  032         SBC RTP DTMF                              0                
  033         Pseudowire VCCV control channel           0                
  034         Generic QFP generated packet (keep GPM)   0                
  035         Ethernet slow protocol (ie: LACP, OAM)    0                
  036         Ethernet OAM Loopback                     0                
  037         Egress to Ingress redirect                0                
  038         SPA IPC packet                            0                
  039         Punt and replicate                        0                
  040         PPPoE control                             0                
  041         PPPoE session                             0                
  042         L2TP control                              0                
  043         IP Subscriber control (ie: FSOL, keep...  0                
  044         L2TP session                              0                
  045         BFD control                               0                
  046         MVPN non-RPF signaling packet             0                
  047         MVPN PIM signalling packet                0                
  048         Mcast punt to RP                          0                
  049         SBC generated packet                      0                
  050         IPv6 packet                               0                
  051         DMVPN NHRP redirect                       0                
  052         PFR monitored prefix logging              0                
  053         PFR top talkers logging                   0                
  054         PFR top talkers application logging       0                
  055         For-us control                            0                
  056         RP injected for-us control                0                
  057         QFP VTCP generated packet                 0                
  058         Layer2 bridge domain packet               0                
  059         QFP Stile generated packet                0                
  060         IP subnet or broadcast packet             0                
  061         Ethernet CFM packet                       0                
  062         Ethernet CFM notify packet                0                

  Drop Counter ID   5     Drop Counter Name PUNT_PLATFORM_HDR_FMT_ERROR

  Counter ID  Punt Cause Name                           Packets          
  ---------------------------------------------------------------------
  000         Reserved                                  0                
  001         MPLS ICMP Can't Fragment                  0                
  002         IPv4 Options                              0                
  003         Layer2 control and legacy                 0                
  004         PPP Control                               0                
  005         CLNS IS-IS Control                        0                
  006         HDLC keepalives                           0                
  007         ARP request or response                   0                
  008         Reverse ARP request or repsonse           0                
  009         Frame-relay LMI Control                   0                
  010         Incomplete adjacency                      0                
  011         For-us data                               0                
  012         Mcast Directly Connected Source           0                
  013         Mcast IPv4 Options data packet            0                
  014         Skip egress processing                    0                
  015         MPLS TTL expired                          0                
  016         MPLS Reserved label (ie: 0-15)            0                
  017         IPv6 Bad hop limit                        0                
  018         IPV6 Hop-by-hop Options                   0                
  019         Mcast Internal Copy                       0                
  020         Generic QFP generated packet              0                
  021         RP<->QFP keepalive                        0                
  022         QFP Fwall generated packet                0                
  023         Mcast IGMP Unroutable                     0                
  024         Glean adjacency                           0                
  025         Mcast PIM signaling                       0                
  026         QFP ICMP generated packet                 0                
  027         ESS session control                       0                
  028         ESS data switching back                   0                
  029         RP handled ICMP                           0                
  030         RP injected For-us data                   0                
  031         Punt adjacency                            0                
  032         SBC RTP DTMF                              0                
  033         Pseudowire VCCV control channel           0                
  034         Generic QFP generated packet (keep GPM)   0                
  035         Ethernet slow protocol (ie: LACP, OAM)    0                
  036         Ethernet OAM Loopback                     0                
  037         Egress to Ingress redirect                0                
  038         SPA IPC packet                            0                
  039         Punt and replicate                        0                
  040         PPPoE control                             0                
  041         PPPoE session                             0                
  042         L2TP control                              0                
  043         IP Subscriber control (ie: FSOL, keep...  0                
  044         L2TP session                              0                
  045         BFD control                               0                
  046         MVPN non-RPF signaling packet             0                
  047         MVPN PIM signalling packet                0                
  048         Mcast punt to RP                          0                
  049         SBC generated packet                      0                
  050         IPv6 packet                               0                
  051         DMVPN NHRP redirect                       0                
  052         PFR monitored prefix logging              0                
  053         PFR top talkers logging                   0                
  054         PFR top talkers application logging       0                
  055         For-us control                            0                
  056         RP injected for-us control                0                
  057         QFP VTCP generated packet                 0                
  058         Layer2 bridge domain packet               0                
  059         QFP Stile generated packet                0                
  060         IP subnet or broadcast packet             0                
  061         Ethernet CFM packet                       0                
  062         Ethernet CFM notify packet                0                

  Drop Counter ID   6     Drop Counter Name PUNT_FEATURE_HDR_FMT_ERROR

  Counter ID  Punt Cause Name                           Packets          
  ---------------------------------------------------------------------
  000         Reserved                                  0                
  001         MPLS ICMP Can't Fragment                  0                
  002         IPv4 Options                              0                
  003         Layer2 control and legacy                 0                
  004         PPP Control                               0                
  005         CLNS IS-IS Control                        0                
  006         HDLC keepalives                           0                
  007         ARP request or response                   0                
  008         Reverse ARP request or repsonse           0                
  009         Frame-relay LMI Control                   0                
  010         Incomplete adjacency                      0                
  011         For-us data                               0                
  012         Mcast Directly Connected Source           0                
  013         Mcast IPv4 Options data packet            0                
  014         Skip egress processing                    0                
  015         MPLS TTL expired                          0                
  016         MPLS Reserved label (ie: 0-15)            0                
  017         IPv6 Bad hop limit                        0                
  018         IPV6 Hop-by-hop Options                   0                
  019         Mcast Internal Copy                       0                
  020         Generic QFP generated packet              0                
  021         RP<->QFP keepalive                        0                
  022         QFP Fwall generated packet                0                
  023         Mcast IGMP Unroutable                     0                
  024         Glean adjacency                           0                
  025         Mcast PIM signaling                       0                
  026         QFP ICMP generated packet                 0                
  027         ESS session control                       0                
  028         ESS data switching back                   0                
  029         RP handled ICMP                           0                
  030         RP injected For-us data                   0                
  031         Punt adjacency                            0                
  032         SBC RTP DTMF                              0                
  033         Pseudowire VCCV control channel           0                
  034         Generic QFP generated packet (keep GPM)   0                
  035         Ethernet slow protocol (ie: LACP, OAM)    0                
  036         Ethernet OAM Loopback                     0                
  037         Egress to Ingress redirect                0                
  038         SPA IPC packet                            0                
  039         Punt and replicate                        0                
  040         PPPoE control                             0                
  041         PPPoE session                             0                
  042         L2TP control                              0                
  043         IP Subscriber control (ie: FSOL, keep...  0                
  044         L2TP session                              0                
  045         BFD control                               0                
  046         MVPN non-RPF signaling packet             0                
  047         MVPN PIM signalling packet                0                
  048         Mcast punt to RP                          0                
  049         SBC generated packet                      0                
  050         IPv6 packet                               0                
  051         DMVPN NHRP redirect                       0                
  052         PFR monitored prefix logging              0                
  053         PFR top talkers logging                   0                
  054         PFR top talkers application logging       0                
  055         For-us control                            0                
  056         RP injected for-us control                0                
  057         QFP VTCP generated packet                 0                
  058         Layer2 bridge domain packet               0                
  059         QFP Stile generated packet                0                
  060         IP subnet or broadcast packet             0                
  061         Ethernet CFM packet                       0                
  062         Ethernet CFM notify packet                0                

  Drop Counter ID   7     Drop Counter Name PUNT_INVALID_PAL_LINK_TYPE

  Counter ID  Punt Cause Name                           Packets          
  ---------------------------------------------------------------------
  000         Reserved                                  0                
  001         MPLS ICMP Can't Fragment                  0                
  002         IPv4 Options                              0                
  003         Layer2 control and legacy                 0                
  004         PPP Control                               0                
  005         CLNS IS-IS Control                        0                
  006         HDLC keepalives                           0                
  007         ARP request or response                   0                
  008         Reverse ARP request or repsonse           0                
  009         Frame-relay LMI Control                   0                
  010         Incomplete adjacency                      0                
  011         For-us data                               0                
  012         Mcast Directly Connected Source           0                
  013         Mcast IPv4 Options data packet            0                
  014         Skip egress processing                    0                
  015         MPLS TTL expired                          0                
  016         MPLS Reserved label (ie: 0-15)            0                
  017         IPv6 Bad hop limit                        0                
  018         IPV6 Hop-by-hop Options                   0                
  019         Mcast Internal Copy                       0                
  020         Generic QFP generated packet              0                
  021         RP<->QFP keepalive                        0                
  022         QFP Fwall generated packet                0                
  023         Mcast IGMP Unroutable                     0                
  024         Glean adjacency                           0                
  025         Mcast PIM signaling                       0                
  026         QFP ICMP generated packet                 0                
  027         ESS session control                       0                
  028         ESS data switching back                   0                
  029         RP handled ICMP                           0                
  030         RP injected For-us data                   0                
  031         Punt adjacency                            0                
  032         SBC RTP DTMF                              0                
  033         Pseudowire VCCV control channel           0                
  034         Generic QFP generated packet (keep GPM)   0                
  035         Ethernet slow protocol (ie: LACP, OAM)    0                
  036         Ethernet OAM Loopback                     0                
  037         Egress to Ingress redirect                0                
  038         SPA IPC packet                            0                
  039         Punt and replicate                        0                
  040         PPPoE control                             0                
  041         PPPoE session                             0                
  042         L2TP control                              0                
  043         IP Subscriber control (ie: FSOL, keep...  0                
  044         L2TP session                              0                
  045         BFD control                               0                
  046         MVPN non-RPF signaling packet             0                
  047         MVPN PIM signalling packet                0                
  048         Mcast punt to RP                          0                
  049         SBC generated packet                      0                
  050         IPv6 packet                               0                
  051         DMVPN NHRP redirect                       0                
  052         PFR monitored prefix logging              0                
  053         PFR top talkers logging                   0                
  054         PFR top talkers application logging       0                
  055         For-us control                            0                
  056         RP injected for-us control                0                
  057         QFP VTCP generated packet                 0                
  058         Layer2 bridge domain packet               0                
  059         QFP Stile generated packet                0                
  060         IP subnet or broadcast packet             0                
  061         Ethernet CFM packet                       0                
  062         Ethernet CFM notify packet                0                

  Drop Counter ID   8     Drop Counter Name PUNT_NULL_PI_UIDB_SB

  Counter ID  Punt Cause Name                           Packets          
  ---------------------------------------------------------------------
  000         Reserved                                  0                
  001         MPLS ICMP Can't Fragment                  0                
  002         IPv4 Options                              0                
  003         Layer2 control and legacy                 0                
  004         PPP Control                               0                
  005         CLNS IS-IS Control                        0                
  006         HDLC keepalives                           0                
  007         ARP request or response                   0                
  008         Reverse ARP request or repsonse           0                
  009         Frame-relay LMI Control                   0                
  010         Incomplete adjacency                      0                
  011         For-us data                               0                
  012         Mcast Directly Connected Source           0                
  013         Mcast IPv4 Options data packet            0                
  014         Skip egress processing                    0                
  015         MPLS TTL expired                          0                
  016         MPLS Reserved label (ie: 0-15)            0                
  017         IPv6 Bad hop limit                        0                
  018         IPV6 Hop-by-hop Options                   0                
  019         Mcast Internal Copy                       0                
  020         Generic QFP generated packet              0                
  021         RP<->QFP keepalive                        0                
  022         QFP Fwall generated packet                0                
  023         Mcast IGMP Unroutable                     0                
  024         Glean adjacency                           0                
  025         Mcast PIM signaling                       0                
  026         QFP ICMP generated packet                 0                
  027         ESS session control                       0                
  028         ESS data switching back                   0                
  029         RP handled ICMP                           0                
  030         RP injected For-us data                   0                
  031         Punt adjacency                            0                
  032         SBC RTP DTMF                              0                
  033         Pseudowire VCCV control channel           0                
  034         Generic QFP generated packet (keep GPM)   0                
  035         Ethernet slow protocol (ie: LACP, OAM)    0                
  036         Ethernet OAM Loopback                     0                
  037         Egress to Ingress redirect                0                
  038         SPA IPC packet                            0                
  039         Punt and replicate                        0                
  040         PPPoE control                             0                
  041         PPPoE session                             0                
  042         L2TP control                              0                
  043         IP Subscriber control (ie: FSOL, keep...  0                
  044         L2TP session                              0                
  045         BFD control                               0                
  046         MVPN non-RPF signaling packet             0                
  047         MVPN PIM signalling packet                0                
  048         Mcast punt to RP                          0                
  049         SBC generated packet                      0                
  050         IPv6 packet                               0                
  051         DMVPN NHRP redirect                       0                
  052         PFR monitored prefix logging              0                
  053         PFR top talkers logging                   0                
  054         PFR top talkers application logging       0                
  055         For-us control                            0                
  056         RP injected for-us control                0                
  057         QFP VTCP generated packet                 0                
  058         Layer2 bridge domain packet               0                
  059         QFP Stile generated packet                0                
  060         IP subnet or broadcast packet             0                
  061         Ethernet CFM packet                       0                
  062         Ethernet CFM notify packet                0                

  Drop Counter ID   9     Drop Counter Name PUNT_NULL_QUEUE_INFO

  Counter ID  Punt Cause Name                           Packets          
  ---------------------------------------------------------------------
  000         Reserved                                  0                
  001         MPLS ICMP Can't Fragment                  0                
  002         IPv4 Options                              0                
  003         Layer2 control and legacy                 0                
  004         PPP Control                               0                
  005         CLNS IS-IS Control                        0                
  006         HDLC keepalives                           0                
  007         ARP request or response                   0                
  008         Reverse ARP request or repsonse           0                
  009         Frame-relay LMI Control                   0                
  010         Incomplete adjacency                      0                
  011         For-us data                               0                
  012         Mcast Directly Connected Source           0                
  013         Mcast IPv4 Options data packet            0                
  014         Skip egress processing                    0                
  015         MPLS TTL expired                          0                
  016         MPLS Reserved label (ie: 0-15)            0                
  017         IPv6 Bad hop limit                        0                
  018         IPV6 Hop-by-hop Options                   0                
  019         Mcast Internal Copy                       0                
  020         Generic QFP generated packet              0                
  021         RP<->QFP keepalive                        0                
  022         QFP Fwall generated packet                0                
  023         Mcast IGMP Unroutable                     0                
  024         Glean adjacency                           0                
  025         Mcast PIM signaling                       0                
  026         QFP ICMP generated packet                 0                
  027         ESS session control                       0                
  028         ESS data switching back                   0                
  029         RP handled ICMP                           0                
  030         RP injected For-us data                   0                
  031         Punt adjacency                            0                
  032         SBC RTP DTMF                              0                
  033         Pseudowire VCCV control channel           0                
  034         Generic QFP generated packet (keep GPM)   0                
  035         Ethernet slow protocol (ie: LACP, OAM)    0                
  036         Ethernet OAM Loopback                     0                
  037         Egress to Ingress redirect                0                
  038         SPA IPC packet                            0                
  039         Punt and replicate                        0                
  040         PPPoE control                             0                
  041         PPPoE session                             0                
  042         L2TP control                              0                
  043         IP Subscriber control (ie: FSOL, keep...  0                
  044         L2TP session                              0                
  045         BFD control                               0                
  046         MVPN non-RPF signaling packet             0                
  047         MVPN PIM signalling packet                0                
  048         Mcast punt to RP                          0                
  049         SBC generated packet                      0                
  050         IPv6 packet                               0                
  051         DMVPN NHRP redirect                       0                
  052         PFR monitored prefix logging              0                
  053         PFR top talkers logging                   0                
  054         PFR top talkers application logging       0                
  055         For-us control                            0                
  056         RP injected for-us control                0                
  057         QFP VTCP generated packet                 0                
  058         Layer2 bridge domain packet               0                
  059         QFP Stile generated packet                0                
  060         IP subnet or broadcast packet             0                
  061         Ethernet CFM packet                       0                
  062         Ethernet CFM notify packet                0                

  Drop Counter ID   10     Drop Counter Name PUNT_NULL_RECYCLE_QUEUE_INFO

  Counter ID  Punt Cause Name                           Packets          
  ---------------------------------------------------------------------
  000         Reserved                                  0                
  001         MPLS ICMP Can't Fragment                  0                
  002         IPv4 Options                              0                
  003         Layer2 control and legacy                 0                
  004         PPP Control                               0                
  005         CLNS IS-IS Control                        0                
  006         HDLC keepalives                           0                
  007         ARP request or response                   0                
  008         Reverse ARP request or repsonse           0                
  009         Frame-relay LMI Control                   0                
  010         Incomplete adjacency                      0                
  011         For-us data                               0                
  012         Mcast Directly Connected Source           0                
  013         Mcast IPv4 Options data packet            0                
  014         Skip egress processing                    0                
  015         MPLS TTL expired                          0                
  016         MPLS Reserved label (ie: 0-15)            0                
  017         IPv6 Bad hop limit                        0                
  018         IPV6 Hop-by-hop Options                   0                
  019         Mcast Internal Copy                       0                
  020         Generic QFP generated packet              0                
  021         RP<->QFP keepalive                        0                
  022         QFP Fwall generated packet                0                
  023         Mcast IGMP Unroutable                     0                
  024         Glean adjacency                           0                
  025         Mcast PIM signaling                       0                
  026         QFP ICMP generated packet                 0                
  027         ESS session control                       0                
  028         ESS data switching back                   0                
  029         RP handled ICMP                           0                
  030         RP injected For-us data                   0                
  031         Punt adjacency                            0                
  032         SBC RTP DTMF                              0                
  033         Pseudowire VCCV control channel           0                
  034         Generic QFP generated packet (keep GPM)   0                
  035         Ethernet slow protocol (ie: LACP, OAM)    0                
  036         Ethernet OAM Loopback                     0                
  037         Egress to Ingress redirect                0                
  038         SPA IPC packet                            0                
  039         Punt and replicate                        0                
  040         PPPoE control                             0                
  041         PPPoE session                             0                
  042         L2TP control                              0                
  043         IP Subscriber control (ie: FSOL, keep...  0                
  044         L2TP session                              0                
  045         BFD control                               0                
  046         MVPN non-RPF signaling packet             0                
  047         MVPN PIM signalling packet                0                
  048         Mcast punt to RP                          0                
  049         SBC generated packet                      0                
  050         IPv6 packet                               0                
  051         DMVPN NHRP redirect                       0                
  052         PFR monitored prefix logging              0                
  053         PFR top talkers logging                   0                
  054         PFR top talkers application logging       0                
  055         For-us control                            0                
  056         RP injected for-us control                0                
  057         QFP VTCP generated packet                 0                
  058         Layer2 bridge domain packet               0                
  059         QFP Stile generated packet                0                
  060         IP subnet or broadcast packet             0                
  061         Ethernet CFM packet                       0                
  062         Ethernet CFM notify packet                0                

  Drop Counter ID   11     Drop Counter Name PUNT_PER_CAUSE_POLICER

  Counter ID  Punt Cause Name                           Packets          
  ---------------------------------------------------------------------
  000         Reserved                                  0                
  001         MPLS ICMP Can't Fragment                  0                
  002         IPv4 Options                              0                
  003         Layer2 control and legacy                 0                
  004         PPP Control                               0                
  005         CLNS IS-IS Control                        0                
  006         HDLC keepalives                           0                
  007         ARP request or response                   0                
  008         Reverse ARP request or repsonse           0                
  009         Frame-relay LMI Control                   0                
  010         Incomplete adjacency                      0                
  011         For-us data                               0                
  012         Mcast Directly Connected Source           0                
  013         Mcast IPv4 Options data packet            0                
  014         Skip egress processing                    0                
  015         MPLS TTL expired                          0                
  016         MPLS Reserved label (ie: 0-15)            0                
  017         IPv6 Bad hop limit                        0                
  018         IPV6 Hop-by-hop Options                   0                
  019         Mcast Internal Copy                       0                
  020         Generic QFP generated packet              0                
  021         RP<->QFP keepalive                        0                
  022         QFP Fwall generated packet                0                
  023         Mcast IGMP Unroutable                     0                
  024         Glean adjacency                           0                
  025         Mcast PIM signaling                       0                
  026         QFP ICMP generated packet                 0                
  027         ESS session control                       0                
  028         ESS data switching back                   0                
  029         RP handled ICMP                           0                
  030         RP injected For-us data                   0                
  031         Punt adjacency                            0                
  032         SBC RTP DTMF                              0                
  033         Pseudowire VCCV control channel           0                
  034         Generic QFP generated packet (keep GPM)   0                
  035         Ethernet slow protocol (ie: LACP, OAM)    0                
  036         Ethernet OAM Loopback                     0                
  037         Egress to Ingress redirect                0                
  038         SPA IPC packet                            0                
  039         Punt and replicate                        0                
  040         PPPoE control                             0                
  041         PPPoE session                             0                
  042         L2TP control                              0                
  043         IP Subscriber control (ie: FSOL, keep...  0                
  044         L2TP session                              0                
  045         BFD control                               0                
  046         MVPN non-RPF signaling packet             0                
  047         MVPN PIM signalling packet                0                
  048         Mcast punt to RP                          0                
  049         SBC generated packet                      0                
  050         IPv6 packet                               0                
  051         DMVPN NHRP redirect                       0                
  052         PFR monitored prefix logging              0                
  053         PFR top talkers logging                   0                
  054         PFR top talkers application logging       0                
  055         For-us control                            0                
  056         RP injected for-us control                0                
  057         QFP VTCP generated packet                 0                
  058         Layer2 bridge domain packet               0                
  059         QFP Stile generated packet                0                
  060         IP subnet or broadcast packet             0                
  061         Ethernet CFM packet                       0                
  062         Ethernet CFM notify packet                0                

  Drop Counter ID   12     Drop Counter Name PUNT_WITH_INTERNAL_IFH

  Counter ID  Punt Cause Name                           Packets          
  ---------------------------------------------------------------------
  000         Reserved                                  0                
  001         MPLS ICMP Can't Fragment                  0                
  002         IPv4 Options                              0                
  003         Layer2 control and legacy                 0                
  004         PPP Control                               0                
  005         CLNS IS-IS Control                        0                
  006         HDLC keepalives                           0                
  007         ARP request or response                   0                
  008         Reverse ARP request or repsonse           0                
  009         Frame-relay LMI Control                   0                
  010         Incomplete adjacency                      0                
  011         For-us data                               0                
  012         Mcast Directly Connected Source           0                
  013         Mcast IPv4 Options data packet            0                
  014         Skip egress processing                    0                
  015         MPLS TTL expired                          0                
  016         MPLS Reserved label (ie: 0-15)            0                
  017         IPv6 Bad hop limit                        0                
  018         IPV6 Hop-by-hop Options                   0                
  019         Mcast Internal Copy                       0                
  020         Generic QFP generated packet              0                
  021         RP<->QFP keepalive                        0                
  022         QFP Fwall generated packet                0                
  023         Mcast IGMP Unroutable                     0                
  024         Glean adjacency                           0                
  025         Mcast PIM signaling                       0                
  026         QFP ICMP generated packet                 0                
  027         ESS session control                       0                
  028         ESS data switching back                   0                
  029         RP handled ICMP                           0                
  030         RP injected For-us data                   0                
  031         Punt adjacency                            0                
  032         SBC RTP DTMF                              0                
  033         Pseudowire VCCV control channel           0                
  034         Generic QFP generated packet (keep GPM)   0                
  035         Ethernet slow protocol (ie: LACP, OAM)    0                
  036         Ethernet OAM Loopback                     0                
  037         Egress to Ingress redirect                0                
  038         SPA IPC packet                            0                
  039         Punt and replicate                        0                
  040         PPPoE control                             0                
  041         PPPoE session                             0                
  042         L2TP control                              0                
  043         IP Subscriber control (ie: FSOL, keep...  0                
  044         L2TP session                              0                
  045         BFD control                               0                
  046         MVPN non-RPF signaling packet             0                
  047         MVPN PIM signalling packet                0                
  048         Mcast punt to RP                          0                
  049         SBC generated packet                      0                
  050         IPv6 packet                               0                
  051         DMVPN NHRP redirect                       0                
  052         PFR monitored prefix logging              0                
  053         PFR top talkers logging                   0                
  054         PFR top talkers application logging       0                
  055         For-us control                            0                
  056         RP injected for-us control                0                
  057         QFP VTCP generated packet                 0                
  058         Layer2 bridge domain packet               0                
  059         QFP Stile generated packet                0                
  060         IP subnet or broadcast packet             0                
  061         Ethernet CFM packet                       0                
  062         Ethernet CFM notify packet                0                

  Drop Counter ID   13     Drop Counter Name PUNT_MALFORMED_PKT

  Counter ID  Punt Cause Name                           Packets          
  ---------------------------------------------------------------------
  000         Reserved                                  0                
  001         MPLS ICMP Can't Fragment                  0                
  002         IPv4 Options                              0                
  003         Layer2 control and legacy                 0                
  004         PPP Control                               0                
  005         CLNS IS-IS Control                        0                
  006         HDLC keepalives                           0                
  007         ARP request or response                   0                
  008         Reverse ARP request or repsonse           0                
  009         Frame-relay LMI Control                   0                
  010         Incomplete adjacency                      0                
  011         For-us data                               0                
  012         Mcast Directly Connected Source           0                
  013         Mcast IPv4 Options data packet            0                
  014         Skip egress processing                    0                
  015         MPLS TTL expired                          0                
  016         MPLS Reserved label (ie: 0-15)            0                
  017         IPv6 Bad hop limit                        0                
  018         IPV6 Hop-by-hop Options                   0                
  019         Mcast Internal Copy                       0                
  020         Generic QFP generated packet              0                
  021         RP<->QFP keepalive                        0                
  022         QFP Fwall generated packet                0                
  023         Mcast IGMP Unroutable                     0                
  024         Glean adjacency                           0                
  025         Mcast PIM signaling                       0                
  026         QFP ICMP generated packet                 0                
  027         ESS session control                       0                
  028         ESS data switching back                   0                
  029         RP handled ICMP                           0                
  030         RP injected For-us data                   0                
  031         Punt adjacency                            0                
  032         SBC RTP DTMF                              0                
  033         Pseudowire VCCV control channel           0                
  034         Generic QFP generated packet (keep GPM)   0                
  035         Ethernet slow protocol (ie: LACP, OAM)    0                
  036         Ethernet OAM Loopback                     0                
  037         Egress to Ingress redirect                0                
  038         SPA IPC packet                            0                
  039         Punt and replicate                        0                
  040         PPPoE control                             0                
  041         PPPoE session                             0                
  042         L2TP control                              0                
  043         IP Subscriber control (ie: FSOL, keep...  0                
  044         L2TP session                              0                
  045         BFD control                               0                
  046         MVPN non-RPF signaling packet             0                
  047         MVPN PIM signalling packet                0                
  048         Mcast punt to RP                          0                
  049         SBC generated packet                      0                
  050         IPv6 packet                               0                
  051         DMVPN NHRP redirect                       0                
  052         PFR monitored prefix logging              0                
  053         PFR top talkers logging                   0                
  054         PFR top talkers application logging       0                
  055         For-us control                            0                
  056         RP injected for-us control                0                
  057         QFP VTCP generated packet                 0                
  058         Layer2 bridge domain packet               0                
  059         QFP Stile generated packet                0                
  060         IP subnet or broadcast packet             0                
  061         Ethernet CFM packet                       0                
  062         Ethernet CFM notify packet                0                
---- show platform hardware qfp active infrastructure punt statistics type inject-drop  ----

Inject Drop Statistics

  Number of inject causes = 23

  Drop Counter ID   0     Drop Counter Name INJECT_NOT_ENABLED_BY_DATA_PLANE

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                

  Drop Counter ID   1     Drop Counter Name INJECT_INVALID_CPP_ID

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                

  Drop Counter ID   2     Drop Counter Name INJECT_INVALID_CPP_EPOCH

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                

  Drop Counter ID   3     Drop Counter Name INJECT_INCONSISTENT_HDR_TYPE

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                

  Drop Counter ID   4     Drop Counter Name INJECT_PACKET_LEN_MISMATCH

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                

  Drop Counter ID   5     Drop Counter Name INJECT_PLATFORM_HDR_PROC_ERROR

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                

  Drop Counter ID   6     Drop Counter Name INJECT_FEATURE_HDR_PROC_ERROR

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                

  Drop Counter ID   7     Drop Counter Name INJECT_INVALID_CPP_LINK_TYPE

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                

  Drop Counter ID   8     Drop Counter Name INJECT_UNSUPPORTED_LINKTYPE

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                

  Drop Counter ID   9     Drop Counter Name INJECT_INVALID_PAL_IF_UIDB

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                

  Drop Counter ID   10     Drop Counter Name INJECT_INVALID_INJECT_IF_UIDB

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                

  Drop Counter ID   11     Drop Counter Name INJECT_INVALID_INJECT_IF_HNDL

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                

  Drop Counter ID   12     Drop Counter Name INJECT_UNEXPECTED_FEATURE_HDR

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                

  Drop Counter ID   13     Drop Counter Name INJECT_DIAG_PACKET_ERR

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                

  Drop Counter ID   14     Drop Counter Name INJECT_NULL_PI_UIDB_SB

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                

  Drop Counter ID   15     Drop Counter Name INJECT_NEXTHOP_SAVE_DSTADDR_ERR

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                

  Drop Counter ID   16     Drop Counter Name INJECT_NEXTHOP_RESTORE_DSTADDR_ERR

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                

  Drop Counter ID   17     Drop Counter Name INJECT_INVALID_PAL_IF_HNDL

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                

  Drop Counter ID   18     Drop Counter Name INJECT_UNEXPECTED_PAL_IF_HNDL

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                

  Drop Counter ID   19     Drop Counter Name INJECT_PREROUTE_ADJ_ID_ERROR

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                

  Drop Counter ID   20     Drop Counter Name INJECT_PREROUTE_PIT_ERROR

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                

  Drop Counter ID   21     Drop Counter Name PUNT_INJECT_WITH_INTERNAL_IFH

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                

  Drop Counter ID   22     Drop Counter Name INJECT_MALFORMED_PKT

  Counter ID  Inject Cause Name                         Packets          
  ---------------------------------------------------------------------
  000         RESERVED                                  0                
  001         L2 control/legacy                         0                
  002         QFP destination lookup                    0                
  003         QFP IPv4/v6 nexthop lookup                0                
  004         QFP generated packet                      0                
  005         QFP <->RP keepalive                       0                
  006         QFP Fwall generated packet                0                
  007         QFP adjacency-id lookup                   0                
  008         Mcast specific inject packet              0                
  009         QFP ICMP generated packet                 0                
  010         QFP/RP->QFP ESS data packet               0                
  011         SBC DTMF                                  0                
  012         ARP request or response                   0                
  013         Ethernet OAM loopback packet              0                
  014         Ingress redirect packet                   0                
  015         PPPoE discovery packet                    0                
  016         PPPoE session packet                      0                
  017         QFP inject for pp_index lookup            0                
  018         QFP inject replicate                      0                
  019         QFP inject PIT lookup                     0                
  020         SBC generated packets                     0                
  021         QFP VTCP generated packet                 0                
  022         QFP Stile generated packet                0                
---- show platform hardware qfp active statistics drop  ----

-------------------------------------------------------------------------
Global Drop Stats                         Packets                  Octets  
-------------------------------------------------------------------------
Disabled                                   159376                46756346  
Icmp                                          420                  589305  
IpTtlExceeded                            12025905              1250865267  
Ipv4Martian                                559645                80108145  
Ipv4NoAdj                                  272665                20791202  
Ipv4NoRoute                                    81                    7497  
Ipv4Unclassified                            35216                 3315203  
UnconfiguredIpv6Fia                             6                     492  
Unresolved                                 302166                61425204  
---- show platform hardware qfp active system state ----

CPP HA client processes registered (6 of 6)
  cpp_ha : Initialized
  cpp_cdm : Initialized
  cpp_driver0 : Initialized
  cpp_sp : Initialized
  cpp_cp : Initialized
  FMAN-FP : Initialized
Platform State: curr=ACTIVE_SOLO next=ACTIVE_SOLO
HA State: CPP=0 dir=BOTH Role: curr=ACTIVE_SOLO next=ACTIVE_SOLO
Client State: ENABLE
Image: /tmp/sw/fp/0/0/fp/mount/usr/cpp/bin/qfp-ucode-esp10
Ucode dir: /auto/mcpbuilds6/release/03.02.00.S/BLD-03.02.00.S/cpp/dp/obj/mcp 
Image: mcp 
HW: CPP10 
Ucode name: qfp-ucode-esp10 
Built by: mcpre 
Host: mcp-bld-lnx-114 
Time: Mon Nov 22 10:56:08 2010 
Component: cpp/dp xe32_throttle/69 
Load Cnt: 1 Time: Aug 10, 2014 08:31:29
Active Threads: 0-159
Fault Manager Flags:
    ignore_fault:          FALSE
    ignore_stuck_thread:   FALSE
    crashdump_in_progress: FALSE
---- show platform hardware qfp active datapath infrastructure callback basic ----

callback heartbeat 220776984
callback called 0
callback added 0
callback removed 0
callback overlap execution counter 0
callback out of static memory counter 0
callback element index 0
dlist head 0 tail 0 count 0
---- show platform hardware qfp active datapath infrastructure time basic ----

Time Information
timers active 19
timers popped 0
timers new thread started 127666334
timer events received 127666334
sysup time -762531234
heartbeat expected seq# 0x0
time hb searial 0
time hb errors 0
---- show platform hardware qfp active infrastructure exmem statistics ----

QFP exmem statistics

Type: Name: IRAM, CPP: 0
  Total: 134217728
  InUse: 5979136
  Free: 127401984
  Free protected: 836608
  Free unprotected: 0
  Total Free: 128238592
  Lowest free water mark: 128238592
  Largest free block: 99521536
Type: Name: DRAM, CPP: 0
  Total: 402653184
  InUse: 141382656
  Free: 253231104
  Free protected: 7071744
  Free unprotected: 967680
  Total Free: 261270528
  Lowest free water mark: 260484096
  Largest free block: 259404800
Type: Name: SRAM, CPP: 0
  Total: 32768
  InUse: 12288
  Free: 20480
  Free protected: 0
  Free unprotected: 0
  Total Free: 20480
  Lowest free water mark: 20480
  Largest free block: 20480
Type: Name: BQS_PQS, CPP: 0
  Total: 204800
  InUse: 16386
  Free: 188414
  Free protected: 0
  Free unprotected: 0
  Total Free: 188414
  Lowest free water mark: 188414
  Largest free block: 188414
Type: Name: BQS_MINP, CPP: 0
  Total: 16384
  InUse: 4097
  Free: 12287
  Free protected: 0
  Free unprotected: 0
  Total Free: 12287
  Lowest free water mark: 12287
  Largest free block: 12287
Type: Name: BQS_MAXP, CPP: 0
  Total: 8192
  InUse: 1025
  Free: 7167
  Free protected: 0
  Free unprotected: 0
  Total Free: 7167
  Lowest free water mark: 7167
  Largest free block: 7167
Type: Name: BQS_EXSP, CPP: 0
  Total: 4096
  InUse: 1025
  Free: 3071
  Free protected: 0
  Free unprotected: 0
  Total Free: 3071
  Lowest free water mark: 3071
  Largest free block: 3071
---- show platform hardware qfp active infrastructure exmem information  ----

Type: Name: IRAM, CPP: 0, initialized: Yes
  Epoch: 0, attr: True, fallback: IRAM
  block: size: 1024, count: 131072, offset: 0, next allocation: 0
  table: size: 20640
  low mem threshold: 127506432
  alloc failures: 0
  reserved size: 0
    exclude range: address: 0x02000000, bytes: 1141760   , flags: 0x00000001
    exclude range: address: 0x00000000, bytes: 4721664   , flags: 0x00000001
  page: count: 256, units: 512, attribute: 1
    next allocation: attribute: 0        , index:     0
    next allocation: attribute: 0x1      , index:  4724
Type: Name: DRAM, CPP: 0, initialized: Yes
  Epoch: 0, attr: True, fallback: IRAM
  block: size: 1024, count: 393216, offset: 0, next allocation: 0
  table: size: 61600
  low mem threshold: 510026752
  alloc failures: 0
  reserved size: 0
    exclude range: address: 0x02000000, bytes: 19486720  , flags: 0x00000002
    exclude range: address: 0x0215b400, bytes: 0         , flags: 0x00000002
    exclude range: address: 0x02000000, bytes: 0         , flags: 0x00000001
    exclude range: address: 0x00000000, bytes: 11534336  , flags: 0x00000002
  page: count: 768, units: 512, attribute: 1
    next allocation: attribute: 0        , index: 91123
    next allocation: attribute: 0x1      , index: 147712
Type: Name: GSRAM, CPP: 0, initialized: Yes
  Epoch: 0, attr: True, fallback: GSRAM
  block: size: 128, count: 256, offset: 0, next allocation: 0
  table: size: 1216
  low mem threshold: 31104
  alloc failures: 0
  reserved size: 0
    exclude range: address: 0x00000000, bytes: 12288     , flags: 0x00000002
    exclude range: address: 0x00000000, bytes: 0         , flags: 0x00000002
  page: count: 64, units: 4, attribute: 1
    next allocation: attribute: 0        , index:     0
    next allocation: attribute: 0x1      , index:     0
Type: Name: PQS, CPP: 0, initialized: Yes
  Epoch: 0, attr: False, fallback: PQS
  block: size: 1, count: 204800, offset: 0, next allocation: 16386
  table: size: 25732
  low mem threshold: 194560
  alloc failures: 0
  reserved size: 2
Type: Name: MINPROF, CPP: 0, initialized: Yes
  Epoch: 0, attr: False, fallback: MINPROF
  block: size: 1, count: 16384, offset: 0, next allocation: 4097
  table: size: 2180
  low mem threshold: 15564
  alloc failures: 0
  reserved size: 1
Type: Name: MAXPROF, CPP: 0, initialized: Yes
  Epoch: 0, attr: False, fallback: MAXPROF
  block: size: 1, count: 8192, offset: 0, next allocation: 1025
  table: size: 1156
  low mem threshold: 7782
  alloc failures: 0
  reserved size: 1
Type: Name: EXSPROF, CPP: 0, initialized: Yes
  Epoch: 0, attr: False, fallback: EXSPROF
  block: size: 1, count: 4096, offset: 0, next allocation: 1025
  table: size: 644
  low mem threshold: 3891
  alloc failures: 0
  reserved size: 1
---- show platform hardware qfp active feature acl control ----

Stats Poll Period: 0
Stats Entry Size: 16
Ha Init: 1
Fm Ready: 0
IPv4 Logging Threshold: 2147483647
IPv4 Logging Interval: 0
IPv6 Logging Threshold: 350000
IPv6 Logging Interval: 0
Maximum Aces Per Acl: 81920
Stats Update size: 200
Maximum Entries: 0
Maximum Entries per Classifier: 0
Result Bit Size: 0
Result Start Bit Pos: 0
Maximum Profiles: 0
Maximum Blocks per Profile: 0
Device Select: 0
Maximum Tree Depth: 0
Dimention: 0
Number Cuts: 0
---- show platform hardware qfp active feature acl tree  ----

ACL Tree Root 0x1011e580
---- show platform hardware qfp active feature tunnel state  ----

Server state:
  num QFP complexes: 1  num CPPs: 1
  num IPv4/GRE P2P hash buckets: 2000
  num IPv4/GRE MP hash buckets: 2000
  num IPv6 hash buckets: 2000
  num configured tunnels: 0
Operations:
  interface create 0  delete 0
  uIDB subblock alloc 0  free 0
  hash element alloc 0  free 0
---- show platform hardware qfp active feature erspan state ----

ERSPAN State:
  Status    : Waiting for Bind
  Complexes : 1
  CPPs      : 1
Capabilities: (not available)
System Statistics:
  DROP src session replica  :                  0 /                  0
  DROP term session replica :                  0 /                  0
  DROP receive malformed    :                  0 /                  0
  DROP receive invalid ID   :                  0 /                  0
  DROP recycle queue full   :                  0 /                  0
  DROP no GPM memory        :                  0 /                  0
  DROP no channel memory    :                  0 /                  0
Client Debug Config:
  Enabled: Info, Warn
Data Path Debug Config:
  0x00000000

---- show platform hardware qfp active feature erspan session summary  ----

% Error: ERSPAN client (show): ERSPAN is not active
---- show platform hardware qfp active feature ess state  ----

ESS State:
  Number of QFPs: 1
  Number of QFP Complexes: 1
  Max interfaces: 131072
  Max sessions: 32768
  Max IP sessions: 32768
  Max L2TP sessions: 65536
  Max PPPOE sessions: 32768
  Max PPPOA sessions: 32768
  Max AC sessions: 32768
  Current number of segments: 0
  Current number of sessions: 0
  Current number of TC flow: 0
  Current number of evsi: 0
  Conditional Debugging: 0x00000000
  smc_chan_h: 0x10046300

QFP Number 0:
  ipc_conn: 0x101c0c70
  mdm_h: 0x0eb3b338
  uidb_conn: 0x104a3e10
  encap_info_chunk_h: 0x801d2980
  encaps_chunk_h: 0x801d2a88
  drop_config_chunk_h: 0x801d2b90

ESS Message Counter:
  Type                  Request          Reply (OK)       Reply (Error)    
  -----------------------------------------------------------------------
  Stats Register        6                6                0                
  (a) Register          1                1                0                
  (a) Encap Enable      14               14               0                
  (a) Feat Register     1                1                0                
---- show platform hardware qfp active bqs 0 opm statistics channel all ----


BQS OPM Channel Statistics

Chan   GoodPkts  GoodBytes    BadPkts   BadBytes

 0 - 0000000000 0000000000 0000000000 0000000000
 1 - 0000000000 0000000000 0000000000 0000000000
 2 - 0000000000 0000000000 0000000000 0000000000
 3 - 0000000000 0000000000 0000000000 0000000000
 4 - b02f5196c5 3da391d525 0000000000 0000000000
 5 - 0000000000 0000000000 0000000000 0000000000
 6 - db7abab3e9 c243691daf 0000000000 0000000000
 7 - 0000000000 0000000000 0000000000 0000000000
 8 - 0000000000 0000000000 0000000000 0000000000
 9 - 0000000000 0000000000 0000000000 0000000000
10 - 0000000000 0000000000 0000000000 0000000000
11 - 0000798a55 00320fda64 0000000000 0000000000
12 - 00013fcfcb 00d9652502 0000000000 0000000000
13 - 0000000018 0000000480 0000000000 0000000000
14 - 0000000000 0000000000 0000000000 0000000000
15 - 0000000000 0000000000 0000000000 0000000000
16 - 0000000000 0000000000 0000000000 0000000000
17 - 0000000000 0000000000 0000000000 0000000000
18 - 0000000000 0000000000 0000000000 0000000000
19 - 0000de5de4 00d4fee3bc 0000000000 0000000000
20 - 0000000000 0000000000 0000000000 0000000000
21 - 0000000000 0000000000 0000000000 0000000000
22 - 0000000000 0000000000 0000000000 0000000000
23 - 0000000000 0000000000 0000000000 0000000000
24 - 0000000000 0000000000 0000000000 0000000000
25 - 0000000000 0000000000 0000000000 0000000000
26 - 0000000000 0000000000 0000000000 0000000000
27 - 000000060f 0000a8cfdc 0000000000 0000000000
28 - 0000000000 0000000000 0000000000 0000000000
29 - 0000000000 0000000000 0000000000 0000000000
30 - 0000000000 0000000000 0000000000 0000000000
31 - 0000000000 0000000000 0000000000 0000000000
32 - 14dcad70a4 9e02b98ff2 0000000000 0000000000
33 - 00397da3a0 0649bde580 0000000000 0000000000
34 - 0000000000 0000000000 0000000000 0000000000
35 - 0000000000 0000000000 0000000000 0000000000
36 - 0000000000 0000000000 0000000000 0000000000
37 - 0000000000 0000000000 0000000000 0000000000
38 - 0000000000 0000000000 0000000000 0000000000
39 - 0000000000 0000000000 0000000000 0000000000
40 - 0000000000 0000000000 0000000000 0000000000
41 - 0000000000 0000000000 0000000000 0000000000
42 - 0000000000 0000000000 0000000000 0000000000
43 - 0000000000 0000000000 0000000000 0000000000
44 - 0000000000 0000000000 0000000000 0000000000
45 - 0000000000 0000000000 0000000000 0000000000
46 - 0000000000 0000000000 0000000000 0000000000
47 - 0000000000 0000000000 0000000000 0000000000
48 - 0000000000 0000000000 0000000000 0000000000
49 - 0000000000 0000000000 0000000000 0000000000
50 - 0000000000 0000000000 0000000000 0000000000
51 - 0000000000 0000000000 0000000000 0000000000
52 - 0000000000 0000000000 0000000000 0000000000
53 - 0000000000 0000000000 0000000000 0000000000
54 - 0000000000 0000000000 0000000000 0000000000
55 - 0000000000 0000000000 0000000000 0000000000
56 - 000000048e 00000185e0 0000000000 0000000000
57 - 0000000000 0000000000 0000000000 0000000000
58 - 0000000000 0000000000 0000000000 0000000000
59 - 0000000000 0000000000 0000000000 0000000000
60 - 000000048e 00009ffc12 0000000000 0000000000
 0-55: OPM Channels
56-59: Metapacket/Recycle Pools 0-3
   60: Reassembled Packets Sent to QED
---- show platform hardware qfp active bqs 0 opm mapping  ----


BQS OPM Channel Mapping

Chan     Name                          Interface      LogicalChannel

 0       CC3 Low                       SPI1            0             
 1       CC3 Hi                        SPI1            1             
 2       CC2 Low                       SPI1            2             
 3       CC2 Hi                        SPI1            3             
 4       CC1 Low                       SPI1            4             
 5       CC1 Hi                        SPI1            5             
 6       CC0 Low                       SPI1            6             
 7       CC0 Hi                        SPI1            7             
 8       Diag Loopback                 SPI1            8             
 9       RP1 Low                       SPI0            0             
10       RP1 Hi                        SPI0            1             
11       RP0 Low                       SPI0            2             
12       RP0 Hi                        SPI0            3             
13       Peer-FP Low                   SPI0            4             
14       Peer-FP Hi                    SPI0            5             
15       Nitrox Low                    SPI0            6             
16       Nitrox Hi                     SPI0            7             
17       HT Pkt Low                    HT              0             
18       HT Pkt Hi                     HT              1             
19       HT IPC Low                    HT              2             
20       HT IPC Hi                     HT              3             
21       Unmapped                      
22       Unmapped                      
23       Unmapped                      
24       Unmapped                      
25       Unmapped                      
26       Unmapped                      
27       HighNormal                    GPM             7             
28       HighPriority                  GPM             6             
29       LowNormal                     GPM            11             
30       LowPriority                   GPM            10             
31       InternalTrafficHiChannel      GPM            12             
32       InternalTrafficLoChannel      GPM            13             
33       AttnTrafficHiChannel          GPM            14             
34       MetaPktTrafficChannel         GPM            15             
35       Unmapped                      
36       Unmapped                      
37       Unmapped                      
38       Unmapped                      
39       Unmapped                      
40       Unmapped                      
41       Unmapped                      
42       Unmapped                      
43       Unmapped                      
44       Unmapped                      
45       Unmapped                      
46       Unmapped                      
47       Unmapped                      
48       Unmapped                      
49       Unmapped                      
50       Unmapped                      
51       Unmapped                      
52       Unmapped                      
53       Unmapped                      
54       Unmapped                      
55*      Drain Low                     GPM             0             
 * - indicates the drain mode bit is set for this channel
---- show platform hardware qfp active bqs 0 ipm interface statistics  ----


BQS IPM Interface Statistics

           Packets               Bytes

                       SPI0

GOOD  00000000017c8369     0000000104000fe0
DROP6 0000000000000000     0000000000000000
DROP7 0000000000000000     0000000000000000

                       SPI1

GOOD  0000018baa62fa16     0004e1f26123c059
DROP6 0000000000000000     0000000000000000
DROP7 0000000000000000     0000000000000000

                        HT

GOOD  0000000000be2624     0000000025eba6f0
DROP6 0000000000000000     0000000000000000
DROP7 0000000000000000     0000000000000000
---- show platform hardware qfp active feature ipfrag global ----

Fragmented packet count: 0
Fragments(L3) count: 0
Fragments(L2) count: 0
Fragmentation failure count: 0
Reassembly dgrams count: 0
Reassembly dgram rx count: 0
Reassembly dropped count: 0
Reassembly overlap count: 0
Reassembly overwrite count: 0
Reassembly timeout count: 0
VFR dgrams count: 0
VFR dgram rx count: 0
VFR dropped count: 0
VFR overlap count: 0
VFR overwrite count: 0
VFR timeout count: 0
VFR refrag dgrams count: 0
VFR refrag frags count: 0
VFR refrag drops count: 0
VFR current dgram count: 0
VFR current frag  count: 0
IPv6 Fragmented packet count: 0
IPv6 Fragments(L3) count: 0
IPv6 Fragments(L2) count: 0
IPv6 Fragmentation failure count: 0
IPv6 Reassembly dgrams count: 0
IPv6 Reassembly dgram rx count: 0
IPv6 Reassembly dropped count: 0
IPv6 Reassembly overlap count: 0
IPv6 Reassembly overwrite count: 0
IPv6 Reassembly timeout count: 0
---- show bootlog FP active ----

Reserving 64MB of memory at 32MB for crashkernel (System RAM: 2048MB)
Using MPC85xx ADS machine description
Memory CAM mapping: CAM0=256Mb, CAM1=256Mb, CAM2=256Mb residual: 0Mb
Linux version 2.6.27.45 (mcpre@mcp-bld-lnx-114) (gcc version 4.2.1) #1 Mon Nov 22 13:23:29 PST 2010
Found initrd at 0xc0a03000:0xc17301dd
Found legacy serial port 0 for /soc8548@fbf00000/serial@4500
  mem=fbf04500, taddr=fbf04500, irq=0, clk=400000000, speed=0
Found legacy serial port 1 for /soc8548@fbf00000/serial@4600
  mem=fbf04600, taddr=fbf04600, irq=0, clk=400000000, speed=0
bootparam mstpbtp = 00000000
bootparam mstpPHY = 00000000
ioremap: return ffbff000 - virt ffbff000 phys 80000000 size 1000 flags 2ad
ioremap: return ffbfe000 - virt ffbfe000 phys fbfe0000 size 1000 flags 2ad
ASR:bdtype 20 20 subtype 1 mstp_svr 803a0221 mask  f0  != 10
ioremap: return ffafe000 - virt ffafe000 phys 81000000 size 100000 flags 2ad
mcp_ccfp_reset() removed
mcp: FP FpRstCntrl reset scooby 
ioremap: return ffafd000 - virt ffafd000 phys fbf08000 size 1000 flags 2ad
Found FSL PCI host bridge at 0x00000000fbf08000. Firmware bus number: 0->255
PCI host bridge /pci@fbf08000 (primary) ranges:
 MEM 0x00000000a8000000..0x00000000a8000fff -> 0x00000000a8000000 
  IO 0x00000000a8001000..0x00000000a8002fff -> 0x0000000000000000
ioremap: return ffafb000 - virt ffafb000 phys a8000000 size 2000 flags 2ad
ioremap: return ffafa000 - virt ffafa000 phys fbf08000 size 1000 flags 2ad
ioremap: return ffaf9000 - virt ffaf9000 phys fbf00000 size 1000 flags 2ad
MCP mcp85xx_setup_hose(): FP early mod lawar4 8000000d
ioremap: return ffaf8000 - virt ffaf8000 phys fbf0b000 size 1000 flags 2ad
ioremap: return ffab8000 - virt ffab8000 phys fbf40000 size 40000 flags 2ad
Top of RAM: 0x80000000, Total RAM: 0x80000000
Memory hole size: 0MB
Zone PFN ranges:
  DMA      0x00000000 -> 0x00030000
  Normal   0x00030000 -> 0x00030000
  HighMem  0x00030000 -> 0x00080000
Movable zone start PFN for each node
early_node_map[1] active PFN ranges
    0: 0x00000000 -> 0x00080000
On node 0 totalpages: 524288
free_area_init_node: node 0, pgdat c042fa98, node_mem_map c6000000
  DMA zone: 195072 pages, LIFO batch:31
  HighMem zone: 325120 pages, LIFO batch:31
Built 1 zonelists in Zone order, mobility grouping on.  Total pages: 520192
Kernel command line: root=/dev/ram rw console=ttyS0,9600  SR_BOOT=tftp:base_fp_00.pkg
ioremap: return ffab7000 - virt ffab7000 phys fbf41000 size 1000 flags 2ad
ioremap: return ffab5100 - virt ffab5000 phys fbf41100 size 2000 flags 2ad
ioremap: return ffab4000 - virt ffab4000 phys fbf60000 size 1000 flags 2ad
ioremap: return ffab2000 - virt ffab2000 phys fbf50000 size 2000 flags 2ad
mpic: Setting up MPIC " OpenPIC  " version 1.2 at fbf40000, max 1 CPUs
mpic: ISU size: 256, shift: 8, mask: ff
mpic: Initializing for 256 sources
PID hash table entries: 4096 (order: 12, 16384 bytes)
time_init: decrementer frequency = 50.000000 MHz
time_init: processor frequency   = 800.000000 MHz
clocksource: timebase mult[5000000] shift[22] registered
clockevent: decrementer mult[ccc] shift[16] cpu[0]
Console: colour dummy device 80x25
Dentry cache hash table entries: 131072 (order: 7, 524288 bytes)
Inode-cache hash table entries: 65536 (order: 6, 262144 bytes)
ASR1000: using mcp_memrsv_fp
High memory: 1310720k
Memory: 1986284k/2097152k available (4136k kernel code, 109948k reserved, 160k data, 253k bss, 180k init)
SLUB: Genslabs=12, HWalign=32, Order=0-3, MinObjects=0, CPUs=1, Nodes=1
Calibrating delay loop... 99.84 BogoMIPS (lpj=49920)
Mount-cache hash table entries: 512
net_namespace: 792 bytes
NET: Registered protocol family 16
ioremap: return f10000b0 - virt f1000000 phys fbfe00b0 size 1000 flags 2ad
PCI: Probing PCI hardware
PCI: Scanning bus 0000:00
pci 0000:00:11.0: found [177d/0002] class 001000 header type 00
PCI: 0000:00:11.0 reg 10 io port: [0, ff]
PCI: 0000:00:11.0 reg 18 io port: [0, ff]
pci 0000:00:11.0: calling pcibios_fixup_resources+0x0/0x110
PCI: Fixups for bus 0000:00
PCI: Bus scan for 0000:00 returning with max=00
pci 0000:00:11.0: BAR 0: got res [0x1000-0x10ff] bus [0x1000-0x10ff] flags 0x20020101
pci 0000:00:11.0: BAR 0: moved to bus [0x1000-0x10ff] flags 0x20101
pci 0000:00:11.0: BAR 2: got res [0x1400-0x14ff] bus [0x1400-0x14ff] flags 0x20020101
pci 0000:00:11.0: BAR 2: moved to bus [0x1400-0x14ff] flags 0x20101
bus: 00 index 0 io port: [0, 1fff]
bus: 00 index 1 mmio: [a8000000, a8000fff]
ASR1000: htm init
ASR: reserved 01000000 from e9000000 or e9000000 virt 29000000 29000000 for htm. rsvpag 1000  start c6520000 end c653ffe0
SCSI subsystem initialized
libata version 3.00 loaded.
usbcore: registered new interface driver usbfs
usbcore: registered new interface driver hub
usbcore: registered new device driver usb
Switched to high resolution mode on CPU 0
NET: Registered protocol family 2
IP route cache hash table entries: 32768 (order: 5, 131072 bytes)
TCP established hash table entries: 131072 (order: 8, 1048576 bytes)
TCP bind hash table entries: 65536 (order: 8, 1310720 bytes)
TCP: Hash tables configured (established 131072 bind 65536)
TCP reno registered
NET: Registered protocol family 1
checking if image is initramfs... it is
Freeing initrd memory: 13492k freed
ioremap: return f1002500 - virt f1002000 phys fbf04500 size 1000 flags 2ad
ioremap: return f1004600 - virt f1004000 phys fbf04600 size 1000 flags 2ad
setup_kcore: restrict size=3fffffff
highmem bounce pool size: 64 pages
JFFS2 version 2.2. (NAND) B) 2001-2006 Red Hat, Inc.
msgmni has been set to 1347
io scheduler noop registered
io scheduler anticipatory registered
io scheduler deadline registered
io scheduler cfq registered (default)
pci 0000:00:11.0: calling quirk_cardbus_legacy+0x0/0x60
pci 0000:00:11.0: calling quirk_usb_early_handoff+0x0/0x510
Generic non-volatile memory driver v1.1
Serial: 8250/16550 driver2 ports, IRQ sharing enabled
serial8250.0: ttyS0 at MMIO 0xfbf04500 (irq = 42) is a 16550A
console [ttyS0] enabled
serial8250.0: ttyS1 at MMIO 0xfbf04600 (irq = 42) is a 16550A
brd: module loaded
loop: module loaded
nbd: registered device at major 43
ioremap: return f1062520 - virt f1062000 phys fbf24520 size 1000 flags 2ad
Gianfar MII Bus: probed
ioremap: return f1064000 - virt f1064000 phys fbf24000 size 1000 flags 2ad
eth0: Gianfar Ethernet Controller Version 1.2, 00:00:02:00:00:00
eth0: Running with NAPI enabled
eth0: 256/256 RX/TX BD ring size
ioremap: return f1066000 - virt f1066000 phys fbf25000 size 1000 flags 2ad
eth1: Gianfar Ethernet Controller Version 1.2, 00:00:02:00:00:01
eth1: Running with NAPI enabled
eth1: 256/256 RX/TX BD ring size
ioremap: return f1068000 - virt f1068000 phys fbf26000 size 1000 flags 2ad
eth2: Gianfar Ethernet Controller Version 1.2, 00:00:00:00:00:00
eth2: Running with NAPI enabled
eth2: 256/256 RX/TX BD ring size
MCP: phy 1 feat 000002ff supported 000002f0 advert 000002f0
MCP: phy 2 feat 000002ff supported 000002f0 advert 000002f0
st: Version 20080504, fixed bufsize 32768, s/g segs 256
Driver 'st' needs updating - please use bus_type methods
Driver 'sd' needs updating - please use bus_type methods
Driver 'sr' needs updating - please use bus_type methods
physmap platform flash device: 01000000 at ff000000
ioremap: return f1080000 - virt f1080000 phys ff000000 size 1000000 flags 2ad
physmap-flash.0: Found 1 x16 devices at 0x0 in 16-bit bank
 Intel/Sharp Extended Query Table at 0x0031
Using buffer write method
cfi_cmdset_0001: Erase suspend on write enabled
erase region 0: offset=0x0,size=0x20000,blocks=128
cmdlinepart partition parsing not available
RedBoot partition parsing not available
Using physmap partition information
Creating 6 MTD partitions on "physmap-flash.0":
0x00000000-0x00a00000 : "Crashdump"
0x00a00000-0x00c00000 : "OBFL Data"
0x00c00000-0x00c20000 : "NVRAM Backup"
0x00c20000-0x00e00000 : "Upgrade Boot Rom"
0x00e00000-0x00e20000 : "NVRAM"
0x00e20000-0x01000000 : "Running Boot Rom"
ohci_hcd: 2006 August 04 USB 1.1 'Open' Host Controller (OHCI) Driver
Initializing USB Mass Storage driver...
usbcore: registered new interface driver usb-storage
USB Mass Storage support registered.
ioremap: return f106a000 - virt f106a000 phys fbf03000 size 1000 flags 2ad
rtc-ds1307: probe of 0-00---- show bootlog FP standby ----

This chassis cannot have a standby Embedded-Service-Processor
---- show bootlog RP active  ----

Reserving 64MB of memory at 32MB for crashkernel (System RAM: 4031MB)
Using MPC85xx ADS machine description
Memory CAM mapping: CAM0=256Mb, CAM1=256Mb, CAM2=256Mb residual: 0Mb
Linux version 2.6.27.45 (mcpre@mcp-bld-lnx-114) (gcc version 4.2.1) #1 Mon Nov 22 13:23:29 PST 2010
Found initrd at 0xc0a03000:0xc17301dd
Found legacy serial port 0 for /soc8548@fbf00000/serial@4500
  mem=fbf04500, taddr=fbf04500, irq=0, clk=400000000, speed=0
Found legacy serial port 1 for /soc8548@fbf00000/serial@4600
  mem=fbf04600, taddr=fbf04600, irq=0, clk=400000000, speed=0
bootparam mstpbtp = 00000000
bootparam mstpPHY = 00000000
ioremap: return ffbff000 - virt ffbff000 phys 80000000 size 1000 flags 2ad
ioremap: return ffbfe000 - virt ffbfe000 phys fbfe0000 size 1000 flags 2ad
ASR:bdtype 10 10 subtype 0 mstp_svr 80390021 mask  f0  != 10
mcp: mcp_rp_reset() enabling phy's/switch.
mcp: RP RpDevRstCntrl reset to 2a36000
ioremap: return ffbfd000 - virt ffbfd000 phys fbf08000 size 1000 flags 2ad
ASR: bus arbiter at 0, offset 46 value 5000
Found FSL PCI host bridge at 0x00000000fbf08000. Firmware bus number: 0->255
PCI host bridge /pci@fbf08000 (primary) ranges:
 MEM 0x00000000a8000000..0x00000000a83fffff -> 0x00000000a8000000 
  IO 0x00000000a8400000..0x00000000a87fffff -> 0x0000000000000000
ioremap: return ff7fd000 - virt ff7fd000 phys a8400000 size 400000 flags 2ad
ioremap: return ff7fc000 - virt ff7fc000 phys fbf08000 size 1000 flags 2ad
ioremap: return ff7fb000 - virt ff7fb000 phys fbf09000 size 1000 flags 2ad
ASR: bus arbiter at 0, offset 46 value 5000
Found FSL PCI host bridge at 0x00000000fbf09000. Firmware bus number: 0->255
PCI host bridge /pci@fbf09000 (primary) ranges:
 MEM 0x00000000a8800000..0x00000000a8bfffff -> 0x00000000a8800000 
  IO 0x00000000a8c00000..0x00000000a8ffffff -> 0x0000000000000000
ioremap: return ff3fb000 - virt ff3fb000 phys a8c00000 size 400000 flags 2ad
ioremap: return ff3fa000 - virt ff3fa000 phys fbf09000 size 1000 flags 2ad
ioremap: return ff3f9000 - virt ff3f9000 phys fbf00000 size 1000 flags 2ad
MCP mcp85xx_setup_hose(): RP early mod lawar3 80200014
ioremap: return ff3f8000 - virt ff3f8000 phys fbf0b000 size 1000 flags 2ad
ioremap: return ff3b8000 - virt ff3b8000 phys fbf40000 size 40000 flags 2ad
Top of RAM: 0xfbf00000, Total RAM: 0xfbf00000
Memory hole size: 0MB
Zone PFN ranges:
  DMA      0x00000000 -> 0x00030000
  Normal   0x00030000 -> 0x00030000
  HighMem  0x00030000 -> 0x000fbf00
Movable zone start PFN for each node
early_node_map[1] active PFN ranges
    0: 0x00000000 -> 0x000fbf00
On node 0 totalpages: 1031936
free_area_init_node: node 0, pgdat c042fa98, node_mem_map d188a000
  DMA zone: 195072 pages, LIFO batch:31
  HighMem zone: 828802 pages, LIFO batch:31
Built 1 zonelists in Zone order, mobility grouping on.  Total pages: 1023874
Kernel command line: root=/dev/ram rw console=ttyS2,9600 max_loop=64  SR_BOOT=bootflash:/asr1000rp1-advipservices.03.02.00.S.151-1.S.bin
ioremap: return ff3b7000 - virt ff3b7000 phys fbf41000 size 1000 flags 2ad
ioremap: return ff3b5100 - virt ff3b5000 phys fbf41100 size 2000 flags 2ad
ioremap: return ff3b4000 - virt ff3b4000 phys fbf60000 size 1000 flags 2ad
ioremap: return ff3b2000 - virt ff3b2000 phys fbf50000 size 2000 flags 2ad
mpic: Setting up MPIC " OpenPIC  " version 1.2 at fbf40000, max 1 CPUs
mpic: ISU size: 256, shift: 8, mask: ff
mpic: Initializing for 256 sources
PID hash table entries: 4096 (order: 12, 16384 bytes)
time_init: decrementer frequency = 50.000000 MHz
time_init: processor frequency   = 1400.000000 MHz
clocksource: timebase mult[5000000] shift[22] registered
clockevent: decrementer mult[ccc] shift[16] cpu[0]
Console: colour dummy device 80x25
Dentry cache hash table entries: 131072 (order: 7, 524288 bytes)
Inode-cache hash table entries: 65536 (order: 6, 262144 bytes)
ASR1000: resv 0x80000000 - 0x88000000 
ASR1000: resv 0x90000000 - 0x90010000 
ASR1000: resv 0xa8000000 - 0xa8800000 
ASR1000: resv 0xa8800000 - 0xa9000000 
ASR1000: resv 0xc0000000 - 0xc0201000 
High memory: 3191740k
Memory: 3662184k/4127744k available (4136k kernel code, 464432k reserved, 160k data, 253k bss, 180k init)
SLUB: Genslabs=12, HWalign=32, Order=0-3, MinObjects=0, CPUs=1, Nodes=1
Calibrating delay loop... 99.84 BogoMIPS (lpj=49920)
Mount-cache hash table entries: 512
net_namespace: 792 bytes
NET: Registered protocol family 16
ioremap: return f10000b0 - virt f1000000 phys fbfe00b0 size 1000 flags 2ad
PCI: Probing PCI hardware
PCI: Scanning bus 0000:00
pci 0000:00:12.0: found [11ab/6041] class 000100 header type 00
PCI: 0000:00:12.0 reg 10 64bit mmio: [14000000, 140fffff]
PCI: 0000:00:12.0 reg 18 io port: [0, ff]
pci 0000:00:12.0: calling pcibios_fixup_resources+0x0/0x110
pci 0000:00:12.0: calling mstp_mv_fixup+0x0/0x60
Found device 11ab:6041 at pdev e804c800
PCI: Fixups for bus 0000:00
PCI: Bus scan for 0000:00 returning with max=00
PCI: Scanning bus 0001:01
pci 0001:01:00.0: found [1057/0012] class 000b20 header type 00
PCI: 0001:01:00.0 reg 10 32bit mmio: [fbf00000, fbffffff]
PCI: 0001:01:00.0 reg 14 32bit mmio: [0, 7fffffff]
PCI: 0001:01:00.0 reg 18 64bit mmio: [0, ffffffff]
pci 0001:01:00.0: calling fixup_hide_host_resource_fsl+0x0/0x90
pci 0001:01:00.0: calling pcibios_fixup_resources+0x0/0x110
pci 0001:01:11.0: found [1033/0035] class 000c03 header type 00
PCI: 0001:01:11.0 reg 10 32bit mmio: [0, fff]
pci 0001:01:11.0: calling pcibios_fixup_resources+0x0/0x110
pci 0001:01:11.0: calling mstp_nec_fixup+0x0/0x200
Found device 1033:35 at pdev e804d800
pci 0001:01:11.0: supports D1
pci 0001:01:11.0: supports D2
pci 0001:01:11.0: PME# supported from D0 D1 D2 D3hot
pci 0001:01:11.0: PME# disabled
pci 0001:01:11.1: found [1033/0035] class 000c03 header type 00
PCI: 0001:01:11.1 reg 10 32bit mmio: [0, fff]
pci 0001:01:11.1: calling pcibios_fixup_resources+0x0/0x110
pci 0001:01:11.1: calling mstp_nec_fixup+0x0/0x200
Found device 1033:35 at pdev e804e000
pci 0001:01:11.1: supports D1
pci 0001:01:11.1: supports D2
pci 0001:01:11.1: PME# supported from D0 D1 D2 D3hot
pci 0001:01:11.1: PME# disabled
pci 0001:01:11.2: found [1033/00e0] class 000c03 header type 00
PCI: 0001:01:11.2 reg 10 32bit mmio: [0, ff]
pci 0001:01:11.2: calling pcibios_fixup_resources+0x0/0x110
pci 0001:01:11.2: calling mstp_nec_fixup+0x0/0x200
Found device 1033:e0 at pdev e804e800
pci 0001:01:11.2: supports D1
pci 0001:01:11.2: supports D2
pci 0001:01:11.2: PME# supported from D0 D1 D2 D3hot
pci 0001:01:11.2: PME# disabled
PCI: Fixups for bus 0001:01
PCI: Bus scan for 0001:01 returning with max=01
PCI: Cannot allocate resource region 0 of device 0000:00:12.0, will remap
pci 0000:00:12.0: BAR 0: got res [0xa8000000-0xa80fffff] bus [0xa8000000-0xa80fffff] flags 0x20020204
pci 0000:00:12.0: BAR 0: moved to bus [0xa8000000-0xa80fffff] flags 0x20204
pci 0000:00:12.0: BAR 2: got res [0x402000-0x4020ff] bus [0x0-0xff] flags 0x20020101
pci 0000:00:12.0: BAR 2: moved to bus [0x0-0xff] flags 0x20101
pci 0001:01:11.0: BAR 0: got res [0xa8800000-0xa8800fff] bus [0xa8800000-0xa8800fff] flags 0x20020200
pci 0001:01:11.0: BAR 0: moved to bus [0xa8800000-0xa8800fff] flags 0x20200
pci 0001:01:11.1: BAR 0: got res [0xa8801000-0xa8801fff] bus [0xa8801000-0xa8801fff] flags 0x20020200
pci 0001:01:11.1: BAR 0: moved to bus [0xa8801000-0xa8801fff] flags 0x20200
pci 0001:01:11.2: BAR 0: got res [0xa8802000-0xa88020ff] bus [0xa8802000-0xa88020ff] flags 0x20020200
pci 0001:01:11.2: BAR 0: moved to bus [0xa8802000-0xa88020ff] flags 0x20200
bus: 00 index 0 io port: [402000, 801fff]
bus: 00 index 1 mmio: [a8000000, a83fffff]
bus: 01 index 0 io port: [0, 3fffff]
bus: 01 index 1 mmio: [a8800000, a8bfffff]
ASR1000: htm init
ASR: IOSXE_DUAL_IOS not found.
ASR reserved region2 0 phys 0 for 63a000
ASR: reserved 0063a000 from e8800000 or e8800000 virt 28800000 28800000 for htm. rsvpag 63a  start d1d9a000 end d1da6720
SCSI subsystem initialized
libata version 3.00 loaded.
usbcore: registered new interface driver usbfs
usbcore: registered new interface driver hub
usbcore: registered new device driver usb
NET: Registered protocol family 2
Switched to high resolution mode on CPU 0
IP route cache hash table entries: 32768 (order: 5, 131072 bytes)
TCP established---- show bootlog RP standby  ----

This chassis cannot have a standby Route-Processor
---- show platform software diagnostic chassis-manager R0 cpld  ----

Chassis Manager Diagnostics - CPLD:

Location  Flags     Flags string                      
----------------------------------------------------
R0/0      0x3       Present Ready                     
R1/0      0         Not Present                       
F0/0      0x7       Present Ready Packet Ready        
F1/0      0         Not Present                       
0/0       0x3       Present Ready                     
1/0       0x3       Present Ready                     
2/0       0         Not Present                       
3/0       0         Not Present                       
4/0       0         Not Present                       
5/0       0         Not Present                       
---- show platform software diagnostic chassis-manager R0 status  ----

Chassis Manager Diagnostics - Status:
------------------------------------

Dual IOS mode        : False
Inventory all SIP OK : True
Inventory all ESP OK : True
Process restart      : True

State Machine States:
R0 : s_master_standalone
R1 : s_master_idle
F0 : s_fp_standalone
F1 : s_fp_not_present
0  : s_cc_active
1  : s_cc_active
2  : s_cc_not_present

RP Switch Statistics - CM-RP:
----------------------------

Switchover IOS initiated     : False
FRU all sync done            : False
FRU sync timer expired       : False
---- show platform software diagnostic chassis-manager R1 cpld  ----

This chassis cannot have a Route-Processor at slot 1
---- show platform software diagnostic chassis-manager R1 status  ----

This chassis cannot have a Route-Processor at slot 1
---- show platform software mount R0 brief ----

Mount point: rootfs
  Type     : rootfs
  Location : /
  Options  : rw

Mount point: tmpfs
  Type     : tmpfs
  Location : /tmp
  Options  : rw,size=2757744k,nr_inodes=121312

Mount point: proc
  Type     : proc
  Location : /proc
  Options  : rw

Mount point: sysfs
  Type     : sysfs
  Location : /sys
  Options  : rw

Mount point: none
  Type     : tmpfs
  Location : /dev
  Options  : rw,size=1838492k,nr_inodes=121312,mode=755

Mount point: /dev/bootflash1
  Type     : ext2
  Location : /bootflash
  Options  : rw,errors=continue

Mount point: /dev/loop1
  Type     : iso9660
  Location : /tmp/sw/mount/asr1000rp1-rpbase.03.02.00.S.151-1.S.pkg
  Options  : ro

Mount point: /dev/loop2
  Type     : iso9660
  Location : /tmp/sw/mount/asr1000rp1-rpcontrol.03.02.00.S.151-1.S.pkg
  Options  : ro

Mount point: /dev/loop3
  Type     : iso9660
  Location : /tmp/sw/mount/asr1000rp1-rpios-advipservices.03.02.00.S.151-1.S.pkg
  Options  : ro

Mount point: /dev/loop4
  Type     : iso9660
  Location : /tmp/sw/mount/asr1000rp1-rpaccess.03.02.00.S.151-1.S.pkg
  Options  : ro

Mount point: /dev/loop5
  Type     : iso9660
  Location : /tmp/sw/mount/asr1000rp1-espbase.03.02.00.S.151-1.S.pkg
  Options  : ro

Mount point: /dev/loop6
  Type     : iso9660
  Location : /tmp/sw/mount/asr1000rp1-sipbase.03.02.00.S.151-1.S.pkg
  Options  : ro

Mount point: /dev/loop7
  Type     : iso9660
  Location : /tmp/sw/mount/asr1000rp1-sipspa.03.02.00.S.151-1.S.pkg
  Options  : ro

Mount point: none
  Type     : tmpfs
  Location : /dev
  Options  : rw

Mount point: /proc/bus/usb
  Type     : usbfs
  Location : /proc/bus/usb
  Options  : rw

Mount point: /dev/mtdblock1
  Type     : jffs2
  Location : /obfl
  Options  : rw,noatime,nodiratime

Mount point: /etc/auto.vol
  Type     : autofs
  Location : /vol
  Options  : rw,fd=5,pgrp=14313,timeout=60,minproto=5,maxproto=5,indirect

Mount point: /dev/harddisk1
  Type     : ext2
  Location : /vol/harddisk
  Options  : rw,noatime,nodiratime,errors=continue

---- show platform software mount R1 brief ----

This chassis cannot have a Route-Processor at slot 1
---- show platform software ipc queue-based chassis-manager R0 connection  ----

Name: -iosd_to_chassis_mgr
  Number    : 0
  Mode      : reader
  Created on: 08/10/14 08:31:44
  Enqueued  : 0, Errors 0
  Dequeued  : 895155, Errors 0

---- show platform software ipc queue-based chassis-manager R1 connection  ----

This chassis cannot have a Route-Processor at slot 1
---- show platform software ipc queue-based forwarding-manager R0 connection  ----

Name: -fman-log-bay0-peer0
  Number    : 0
  Mode      : writer
  Created on: 08/10/14 08:31:47
  Enqueued  : 2047962, Errors 0
  Dequeued  : 0, Errors 0

Name: -fman-log-bay0-peer0
  Number    : 1
  Mode      : reader
  Created on: 08/10/14 08:31:47
  Enqueued  : 0, Errors 0
  Dequeued  : 2047962, Errors 0

Name: -iosd_to_forwarding_mgr
  Number    : 2
  Mode      : reader
  Created on: 08/10/14 08:31:47
  Enqueued  : 0, Errors 0
  Dequeued  : 12481351, Errors 0

---- show platform software ipc queue-based forwarding-manager R1 connection  ----

This chassis cannot have a Route-Processor at slot 1
---- show platform software ipc queue-based interface-manager R0 connection  ----

Name: -iosd_to_interface_mgr
  Number    : 0
  Mode      : reader
  Created on: 08/10/14 08:31:49
  Enqueued  : 0, Errors 0
  Dequeued  : 751551, Errors 0

---- show platform software ipc queue-based interface-manager R1 connection  ----

This chassis cannot have a Route-Processor at slot 1
---- show platform software ipc stream-based chassis-manager 0 connection  ----

Number: 0, created: 1407645091
Type: local IPC, origin: listen
Channel information: /tmp/cc/lipc/chassis_mgr_socket, note: 

Number: 1, created: 1407645091
Type: remote IPC, origin: listen
Channel information: listen port: 2603, note: 

Number: 2, created: 1407645096
Type: remote IPC, origin: connect
Channel information: 10.0.1.0, note: 

Number: 3, created: 1407645101
Type: remote IPC, origin: connect
Channel information: 10.0.1.0, note: uipeer uplink to slot 0

Number: 4, created: 1407645104
Type: local IPC, origin: accept
Channel information: /tmp/cc/lipc/chassis_mgr_socket, note: 

Number: 5, created: 1407645108
Type: local IPC, origin: accept
Channel information: /tmp/cc/lipc/chassis_mgr_socket, note: 

Number: 6, created: 1412160889
Type: remote IPC, origin: accept
Channel information: 10.0.1.0, note: uipeer downlink

---- show platform software ipc stream-based chassis-manager 0 manager  ----

Manager: uipeer command manager, number: 1, created: 1407645091
Managed connections: 1, write pool buffers: 15, maximum: 32

Manager: uipeer sman manager, number: 2, created: 1407645091
Managed connections: 1, write pool buffers: 16, maximum: 32

---- show platform software ipc stream-based chassis-manager 1 connection  ----

Number: 0, created: 1407645056
Type: local IPC, origin: listen
Channel information: /tmp/cc/lipc/chassis_mgr_socket, note: 

Number: 1, created: 1407645057
Type: remote IPC, origin: listen
Channel information: listen port: 2604, note: 

Number: 2, created: 1407645061
Type: remote IPC, origin: connect
Channel information: 10.0.1.0, note: 

Number: 4, created: 1407645073
Type: local IPC, origin: accept
Channel information: /tmp/cc/lipc/chassis_mgr_socket, note: 

Number: 7, created: 1407645097
Type: remote IPC, origin: connect
Channel information: 10.0.1.0, note: uipeer uplink to slot 0

Number: 8, created: 1412160889
Type: remote IPC, origin: accept
Channel information: 10.0.1.0, note: uipeer downlink

---- show platform software ipc stream-based chassis-manager 1 manager  ----

Manager: uipeer command manager, number: 1, created: 1407645057
Managed connections: 1, write pool buffers: 15, maximum: 32

Manager: uipeer sman manager, number: 2, created: 1407645057
Managed connections: 1, write pool buffers: 16, maximum: 32

---- show platform software ipc stream-based chassis-manager 2 connection  ----

This chassis cannot have a SPA-Inter-Processor at slot 2
---- show platform software ipc stream-based chassis-manager 2 manager  ----

This chassis cannot have a SPA-Inter-Processor at slot 2
---- show platform software ipc stream-based chassis-manager F0 connection  ----

Number: 0, created: 1407645063
Type: remote IPC, origin: listen
Channel information: listen port: 2502, note: 

Number: 1, created: 1407645063
Type: remote IPC, origin: connect
Channel information: 10.0.1.0, note: 

Number: 2, created: 1407645071
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_ha_mgr_socket, note: 

Number: 3, created: 1407645071
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_ha_mgr_socket, note: 

Number: 6, created: 1407645093
Type: remote IPC, origin: connect
Channel information: 10.0.1.0, note: uipeer uplink to slot 0

Number: 7, created: 1412160890
Type: remote IPC, origin: accept
Channel information: 10.0.1.0, note: uipeer downlink

---- show platform software ipc stream-based chassis-manager F0 manager  ----

Manager: uipeer command manager, number: 1, created: 1407645063
Managed connections: 1, write pool buffers: 15, maximum: 32

Manager: uipeer sman manager, number: 2, created: 1407645063
Managed connections: 1, write pool buffers: 16, maximum: 32

Manager: CM-FP BIPC Manager, number: 3, created: 1407645063
Managed connections: 1, write pool buffers: 256, maximum: 256

---- show platform software ipc stream-based chassis-manager F1 connection  ----

This chassis cannot have an Embedded-Service-Processor at slot 1
---- show platform software ipc stream-based chassis-manager F1 manager  ----

This chassis cannot have an Embedded-Service-Processor at slot 1
---- show platform software ipc stream-based chassis-manager R0 connection  ----

Number: 0, created: 1407645050
Type: local IPC, origin: listen
Channel information: /tmp/rp/lipc/chassis_mgr_socket, note: 

Number: 1, created: 1407645050
Type: remote IPC, origin: listen
Channel information: listen port: 2000, note: 

Number: 2, created: 1407645050
Type: remote IPC, origin: listen
Channel information: listen port: 2402, note: 

Number: 4, created: 1407645061
Type: remote IPC, origin: accept
Channel information: 10.0.3.1, note: 

Number: 5, created: 1407645063
Type: remote IPC, origin: accept
Channel information: 10.0.2.0, note: 

Number: 9, created: 1407645096
Type: remote IPC, origin: accept
Channel information: 10.0.3.0, note: 

Number: 10, created: 1407645100
Type: remote IPC, origin: connect
Channel information: 10.0.1.0, note: uipeer uplink to slot 0

Number: 11, created: 1407645104
Type: local IPC, origin: accept
Channel information: /tmp/rp/lipc/chassis_mgr_socket, note: 

Number: 15, created: 1412160891
Type: remote IPC, origin: accept
Channel information: 10.0.1.0, note: uipeer downlink

---- show platform software ipc stream-based chassis-manager R0 manager  ----

Manager: CM-RP BIPC Manager, number: 1, created: 1407645050
Managed connections: 4, write pool buffers: 16, maximum: 256

Manager: uipeer command manager, number: 2, created: 1407645050
Managed connections: 1, write pool buffers: 15, maximum: 32

Manager: uipeer sman manager, number: 3, created: 1407645050
Managed connections: 1, write pool buffers: 16, maximum: 32

---- show platform software ipc stream-based chassis-manager R1 connection  ----

This chassis cannot have a Route-Processor at slot 1
---- show platform software ipc stream-based chassis-manager R1 manager  ----

This chassis cannot have a Route-Processor at slot 1
---- show platform software ipc stream-based forwarding-manager F0 connection  ----

Number: 0, created: 1407645082
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_ha_mgr_socket, note: 

Number: 1, created: 1407645082
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_ha_mgr_socket, note: 

Number: 4, created: 1407645083
Type: remote IPC, origin: listen
Channel information: listen port: 2506, note: 

Number: 5, created: 1407645083
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 6, created: 1407645083
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 7, created: 1407645083
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 8, created: 1407645083
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 9, created: 1407645083
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 10, created: 1407645083
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 11, created: 1407645083
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_drv0_socket, note: 

Number: 12, created: 1407645083
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_drv_ipc0_socket, note: 

Number: 13, created: 1407645083
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_drv_ipc0_socket, note: 

Number: 28, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 29, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 30, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 31, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 32, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 33, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 34, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 35, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 36, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 37, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 38, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 39, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 40, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 41, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 42, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 43, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 44, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 45, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 46, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 47, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 48, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 49, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 50, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 51, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 52, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 53, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 54, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 55, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 56, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 57, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 58, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 59, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 60, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 61, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 62, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 63, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 64, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 65, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 66, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 67, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 68, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 69, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 70, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 71, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 72, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 73, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 74, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 75, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 76, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 77, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 78, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 79, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 80, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 81, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 82, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 83, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 84, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 85, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 86, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 87, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 88, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 89, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 90, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 91, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 92, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 93, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 94, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 95, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 96, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 97, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 98, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 99, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 100, created: 1407645090
Type: local IPC, origin: listen
Channel information: /tmp/fp/lipc/fman_fp_socket, note: 

Number: 101, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 102, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 103, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 104, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 105, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 106, created: 1407645090
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 107, created: 1407645091
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 108, created: 1407645091
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 109, created: 1407645091
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 110, created: 1407645091
Type: local IPC, origin: connect
Channel information: /tmp/fp/lipc/cpp_cp_socket, note: 

Number: 115, created: 1407645093
Type: remote IPC, origin: connect
Channel information: 10.0.1.0, note: uipeer uplink to slot 0

Number: 146, created: 1407645107
Type: remote IPC, origin: connect
Channel information: 10.0.1.0, note: 

Number: 147, created: 1407645107
Type: remote IPC, origin: connect
Channel information: 10.0.1.0, note: 

Number: 148, created: 1407645107
Type: remote IPC, origin: connect
Channel information: 10.0.1.0, note: 

Number: 153, created: 1407645111
Type: remote IPC, origin: connect
Channel information: 10.0.1.0, note: 

Number: 154, created: 1407645111
Type: remote IPC, origin: connect
Channel information: 10.0.1.0, note: 

Number: 155, created: 1412160891
Type: remote IPC, origin: accept
Channel information: 10.0.1.0, note: uipeer downlink

---- show platform software ipc stream-based forwarding-manager F0 manager  ----

Manager: uipeer command manager, number: 1, created: 1407645083
Managed connections: 1, write pool buffers: 15, maximum: 32

Manager: uipeer sman manager, number: 2, created: 1407645083
Managed connections: 1, write pool buffers: 16, maximum: 32

---- show platform software ipc stream-based forwarding-manager F1 connection  ----

This chassis cannot have an Embedded-Service-Processor at slot 1
---- show platform software ipc stream-based forwarding-manager F1 manager  ----

This chassis cannot have an Embedded-Service-Processor at slot 1
---- show platform software ipc stream-based forwarding-manager R0 connection  ----

Number: 0, created: 1407645059
Type: remote IPC, origin: listen
Channel information: listen port: 2406, note: 

Number: 1, created: 1407645060
Type: local IPC, origin: listen
Channel information: /tmp/rp/lipc/forwarding_mgr_socket, note: 

Number: 2, created: 1407645060
Type: remote IPC, origin: listen
Channel information: listen port: 2001, note: 

Number: 3, created: 1407645060
Type: remote IPC, origin: listen
Channel information: listen port: 2004, note: 

Number: 4, created: 1407645060
Type: remote IPC, origin: listen
Channel information: listen port: 2006, note: 

Number: 8, created: 1407645099
Type: remote IPC, origin: connect
Channel information: 10.0.1.0, note: uipeer uplink to slot 0

Number: 9, created: 1407645107
Type: remote IPC, origin: accept
Channel information: 10.0.2.0, note: 

Number: 10, created: 1407645107
Type: remote IPC, origin: accept
Channel information: 10.0.2.0, note: 

Number: 11, created: 1407645107
Type: remote IPC, origin: accept
Channel information: 10.0.2.0, note: 

Number: 12, created: 1407645109
Type: local IPC, origin: accept
Channel information: /tmp/rp/lipc/forwarding_mgr_socket, note: 

Number: 14, created: 1412160893
Type: remote IPC, origin: accept
Channel information: 10.0.1.0, note: uipeer downlink

---- show platform software ipc stream-based forwarding-manager R0 manager  ----

Manager: uipeer command manager, number: 1, created: 1407645059
Managed connections: 1, write pool buffers: 15, maximum: 32

Manager: uipeer sman manager, number: 2, created: 1407645059
Managed connections: 1, write pool buffers: 16, maximum: 32

---- show platform software ipc stream-based forwarding-manager R1 connection  ----

This chassis cannot have a Route-Processor at slot 1
---- show platform software ipc stream-based forwarding-manager R1 manager  ----

This chassis cannot have a Route-Processor at slot 1
---- show platform software ipc stream-based host-manager 0 connection  ----

Number: 0, created: 1407645093
Type: remote IPC, origin: listen
Channel information: listen port: 2606, note: 

Number: 1, created: 1407645103
Type: remote IPC, origin: connect
Channel information: 10.0.1.0, note: uipeer uplink to slot 0

Number: 2, created: 1412160893
Type: remote IPC, origin: accept
Channel information: 10.0.1.0, note: uipeer downlink

---- show platform software ipc stream-based host-manager 0 manager  ----

Manager: uipeer command manager, number: 1, created: 1407645093
Managed connections: 1, write pool buffers: 15, maximum: 32

Manager: uipeer sman manager, number: 2, created: 1407645093
Managed connections: 1, write pool buffers: 16, maximum: 32

---- show platform software ipc stream-based host-manager 1 connection  ----

Number: 0, created: 1407645058
Type: remote IPC, origin: listen
Channel information: listen port: 2607, note: 

Number: 4, created: 1407645098
Type: remote IPC, origin: connect
Channel information: 10.0.1.0, note: uipeer uplink to slot 0

Number: 5, created: 1412160894
Type: remote IPC, origin: accept
Channel information: 10.0.1.0, note: uipeer downlink

---- show platform software ipc stream-based host-manager 1 manager  ----

Manager: uipeer command manager, number: 1, created: 1407645058
Managed connections: 1, write pool buffers: 15, maximum: 32

Manager: uipeer sman manager, number: 2, created: 1407645058
Managed connections: 1, write pool buffers: 16, maximum: 32

---- show platform software ipc stream-based host-manager 2 connection  ----

This chassis cannot have a SPA-Inter-Processor at slot 2
---- show platform software ipc stream-based host-manager 2 manager  ----

This chassis cannot have a SPA-Inter-Processor at slot 2
---- show platform software ipc stream-based host-manager F0 connection  ----

Number: 0, created: 1407645076
Type: remote IPC, origin: listen
Channel information: listen port: 2508, note: 

Number: 2, created: 1407645096
Type: remote IPC, origin: connect
Channel information: 10.0.1.0, note: uipeer uplink to slot 0

Number: 4, created: 1412160895
Type: remote IPC, origin: accept
Channel information: 10.0.1.0, note: uipeer downlink

---- show platform software ipc stream-based host-manager F0 manager  ----

Manager: uipeer command manager, number: 1, created: 1407645076
Managed connections: 1, write pool buffers: 15, maximum: 32

Manager: uipeer sman manager, number: 2, created: 1407645076
Managed connections: 1, write pool buffers: 16, maximum: 32

---- show platform software ipc stream-based host-manager F1 connection  ----

This chassis cannot have an Embedded-Service-Processor at slot 1
---- show platform software ipc stream-based host-manager F1 manager  ----

This chassis cannot have an Embedded-Service-Processor at slot 1
---- show platform software ipc stream-based host-manager R0 connection  ----

Number: 0, created: 1407645056
Type: remote IPC, origin: listen
Channel information: listen port: 2408, note: 

Number: 4, created: 1407645096
Type: remote IPC, origin: connect
Channel information: 10.0.1.0, note: uipeer uplink to slot 0

Number: 9, created: 1412160848
Type: remote IPC, origin: accept
Channel information: 10.0.1.0, note: uipeer downlink

Number: 14, created: 1412160895
Type: remote IPC, origin: accept
Channel information: 10.0.1.0, note: uipeer downlink

---- show platform software ipc stream-based host-manager R0 manager  ----

Manager: uipeer command manager, number: 1, created: 1407645056
Managed connections: 2, write pool buffers: 15, maximum: 32

Manager: uipeer sman manager, number: 2, created: 1407645056
Managed connections: 1, write pool buffers: 16, maximum: 32

---- show platform software ipc stream-based host-manager R1 connection  ----

This chassis cannot have a Route-Processor at slot 1
---- show platform software ipc stream-based shell-manager R0 connection  ----

Number: 0, created: 1407645092
Type: local IPC, origin: listen
Channel information: /tmp/rp/lipc/shell_mgr_bshell_serv_socket, note: 

Number: 1, created: 1407645092
Type: remote IPC, origin: listen
Channel information: listen port: 2007, note: uipeer ripc listener

Number: 2, created: 1407645092
Type: local IPC, origin: listen
Channel information: /tmp/rp/lipc/shell_mgr_ui_serv_socket, note: uipeer lipc listener

Number: 3, created: 1407645092
Type: remote IPC, origin: listen
Channel information: listen port: 2404, note: 

Number: 4, created: 1407645092
Type: local IPC, origin: listen
Channel information: /tmp/rp/lipc/shell_mgr_iosd_socket, note: IOSd lipc listener

Number: 5, created: 1407645093
Type: remote IPC, origin: accept
Channel information: 10.0.2.0, note: F0:0

Number: 6, created: 1407645093
Type: remote IPC, origin: accept
Channel information: 10.0.1.0, note: R0:0

Number: 7, created: 1407645093
Type: remote IPC, origin: accept
Channel information: 10.0.2.0, note: F0:0

Number: 8, created: 1407645093
Type: remote IPC, origin: accept
Channel information: 10.0.2.0, note: F0:0

Number: 9, created: 1407645093
Type: remote IPC, origin: accept
Channel information: 10.0.2.0, note: F0:0

Number: 10, created: 1407645093
Type: remote IPC, origin: accept
Channel information: 10.0.3.1, note: 1:0

Number: 11, created: 1407645094
Type: remote IPC, origin: accept
Channel information: 10.0.2.0, note: F0:0

Number: 12, created: 1407645096
Type: remote IPC, origin: accept
Channel information: 10.0.2.0, note: F0:0

Number: 13, created: 1407645096
Type: remote IPC, origin: accept
Channel information: 10.0.1.0, note: R0:0

Number: 14, created: 1407645097
Type: remote IPC, origin: accept
Channel information: 10.0.2.0, note: F0:0

Number: 15, created: 1407645097
Type: remote IPC, origin: accept
Channel information: 10.0.3.1, note: 1:0

Number: 16, created: 1407645098
Type: remote IPC, origin: accept
Channel information: 10.0.3.1, note: 1:0

Number: 17, created: 1407645098
Type: remote IPC, origin: accept
Channel information: 10.0.2.0, note: F0:0

Number: 18, created: 1407645099
Type: remote IPC, origin: accept
Channel information: 10.0.1.0, note: R0:0

Number: 19, created: 1407645099
Type: remote IPC, origin: accept
Channel information: 10.0.3.1, note: 1:0

Number: 20, created: 1407645099
Type: remote IPC, origin: accept
Channel information: 10.0.1.0, note: R0:0

Number: 21, created: 1407645100
Type: remote IPC, origin: accept
Channel information: 10.0.3.1, note: 1:0

Number: 22, created: 1407645100
Type: remote IPC, origin: accept
Channel information: 10.0.1.0, note: R0:0

Number: 23, created: 1407645100
Type: remote IPC, origin: accept
Channel information: 10.0.1.0, note: R0:0

Number: 24, created: 1407645100
Type: remote IPC, origin: accept
Channel information: 10.0.2.0, note: F0:0

Number: 25, created: 1407645101
Type: remote IPC, origin: accept
Channel information: 10.0.3.1, note: 1:0

Number: 26, created: 1407645101
Type: remote IPC, origin: accept
Channel information: 10.0.1.0, note: R0:0

Number: 27, created: 1407645102
Type: remote IPC, origin: accept
Channel information: 10.0.3.0, note: 0:0

Number: 28, created: 1407645102
Type: remote IPC, origin: connect
Channel information: 10.0.1.0, note: uipeer uplink to slot 0

Number: 29, created: 1407645102
Type: remote IPC, origin: accept
Channel information: 10.0.1.0, note: R0:0

Number: 30, created: 1407645103
Type: remote IPC, origin: accept
Channel information: 10.0.3.0, note: 0:0

Number: 31, created: 1407645104
Type: remote IPC, origin: accept
Channel information: 10.0.3.0, note: 0:0

Number: 32, created: 1407645104
Type: remote IPC, origin: accept
Channel information: 10.0.3.0, note: 0:0

Number: 33, created: 1407645106
Type: remote IPC, origin: accept
Channel information: 10.0.3.0, note: 0:0

Number: 41, created: 1407645110
Type: local IPC, origin: accept
Channel information: /tmp/rp/lipc/shell_mgr_iosd_socket, note: R0:0

Number: 42, created: 1407645110
Type: local IPC, origin: accept
Channel information: /tmp/rp/lipc/shell_mgr_bshell_serv_socket, note: connection from bshell

Number: 43, created: 1407645110
Type: local IPC, origin: accept
Channel information: /tmp/rp/lipc/shell_mgr_bshell_serv_socket, note: connection from bshell

Number: 44, created: 1407645110
Type: local IPC, origin: accept
Channel information: /tmp/rp/lipc/shell_mgr_bshell_serv_socket, note: connection from bshell

Number: 45, created: 1407645110
Type: local IPC, origin: accept
Channel information: /tmp/rp/lipc/shell_mgr_bshell_serv_socket, note: connection from bshell

Number: 52, created: 1407645112
Type: local IPC, origin: accept
Channel information: /tmp/rp/lipc/shell_mgr_bshell_serv_socket, note: connection from bshell

Number: 53, created: 1407645112
Type: local IPC, origin: accept
Channel information: /tmp/rp/lipc/shell_mgr_bshell_serv_socket, note: connection from bshell

Number: 54, created: 1407645112
Type: local IPC, origin: accept
Channel information: /tmp/rp/lipc/shell_mgr_bshell_serv_socket, note: connection from bshell

Number: 55, created: 1407645112
Type: local IPC, origin: accept
Channel information: /tmp/rp/lipc/shell_mgr_bshell_serv_socket, note: connection from bshell

Number: 56, created: 1407645114
Type: remote IPC, origin: accept
Channel information: 10.0.1.0, note: R0:0

Number: 57, created: 1407645114
Type: remote IPC, origin: accept
Channel information: 10.0.3.0, note: 0:0

Number: 58, created: 1407645119
Type: remote IPC, origin: accept
Channel information: 10.0.3.0, note: 0:0

Number: 63, created: 1412160848
Type: remote IPC, origin: connect
Channel information: 10.0.1.0, note: command connection to hman-ui-R0-0:hman-ui-p:0x11278c48-loc:R0:0-ipc:RIPC

Number: 64, created: 1412160848
Type: local IPC, origin: accept
Channel information: /tmp/rp/lipc/shell_mgr_bshell_serv_socket, note: connection from bshell

Number: 137, created: 1412160896
Type: remote IPC, origin: connect
Channel information: 10.0.1.0, note: command connection to sman-ui-R0-0:sman-ui-p:0x10827ec8-loc:R0:0-ipc:RIPC

Number: 138, created: 1412160896
Type: remote IPC, origin: accept
Channel information: 10.0.1.0, note: uipeer downlink

---- show platform software ipc stream-based shell-manager R0 manager  ----

Manager: bshell manager, number: 1, created: 1407645092
Managed connections: 9, write pool buffers: 512, maximum: 512

Manager: uipeer server manager, number: 2, created: 1407645092
Managed connections: 31, write pool buffers: 256, maximum: 256

Manager: uipeer command manager, number: 3, created: 1407645092
Managed connections: 1, write pool buffers: 15, maximum: 32

Manager: uipeer sman manager, number: 4, created: 1407645092
Managed connections: 1, write pool buffers: 16, maximum: 32

Manager: outbound connections manager, number: 5, created: 1407645092
Managed connections: 2, write pool buffers: 256, maximum: 256

Manager: IOSd conn manager, number: 6, created: 1407645092
Managed connections: 1, write pool buffers: 256, maximum: 256

---- show platform software mount 0  ----

Filesystem                 Used  Available Use % Mounted on                     
rootfs                        0          0     - /                              
tmpfs                    124572     205996   38% /tmp                           
proc                          0          0     - /proc                          
sysfs                         0          0     - /sys                           
none                        532     224356    1% /dev                           
/dev/loop1                25776          0  100% /tmp/sw/cc/0/0/cc/mount        
none                        532     224356    1% /dev                           
/proc/bus/usb                 0          0     - /proc/bus/usb                  
/dev/mtdblock1              480       1568   24% /obfl                          
/etc/auto.misc                0          0     - /misc1                         
/dev/loop2                 4394       2524   64% /mnt/firmware                  
10.0.1.0:/misc/scrat    1255712   35185760    4% /misc1/scratch0                
---- show platform software mount 1  ----

Filesystem                 Used  Available Use % Mounted on                     
rootfs                        0          0     - /                              
tmpfs                    124328     206240   38% /tmp                           
proc                          0          0     - /proc                          
sysfs                         0          0     - /sys                           
none                        532     224356    1% /dev                           
/dev/loop1                25776          0  100% /tmp/sw/cc/1/0/cc/mount        
none                        532     224356    1% /dev                           
/proc/bus/usb                 0          0     - /proc/bus/usb                  
/dev/mtdblock1              448       1600   22% /obfl                          
/etc/auto.misc                0          0     - /misc1                         
/dev/loop2                 4394       2524   64% /mnt/firmware                  
---- show platform software mount 2  ----

This chassis cannot have a SPA-Inter-Processor at slot 2
---- show platform software mount F0  ----

Filesystem                 Used  Available Use % Mounted on                     
rootfs                        0          0     - /                              
tmpfs                    104980    1395680    7% /tmp                           
proc                          0          0     - /proc                          
sysfs                         0          0     - /sys                           
none                      24324     980624    3% /dev                           
/dev/loop1                51400          0  100% /tmp/sw/fp/0/0/fp/mount        
none                      24324     980624    3% /dev                           
/proc/bus/usb                 0          0     - /proc/bus/usb                  
/dev/mtdblock1              500       1548   25% /obfl                          
/etc/auto.misc                0          0     - /misc1                         
---- show platform software mount F1  ----

This chassis cannot have an Embedded-Service-Processor at slot 1
---- show platform software mount R0  ----

Filesystem                 Used  Available Use % Mounted on                     
rootfs                        0          0     - /                              
tmpfs                    841080    1916664   31% /tmp                           
proc                          0          0     - /proc                          
sysfs                         0          0     - /sys                           
none                       3728    1933760    1% /dev                           
/dev/bootflash1          309176     567148   36% /bootflash                     
/dev/loop1                18292          0  100% /tmp/sw/mount/asr1000rp1-rpbas 
/dev/loop2                26490          0  100% /tmp/sw/mount/asr1000rp1-rpcon 
/dev/loop3                56946          0  100% /tmp/sw/mount/asr1000rp1-rpios 
/dev/loop4                24346          0  100% /tmp/sw/mount/asr1000rp1-rpacc 
/dev/loop5                51400          0  100% /tmp/sw/mount/asr1000rp1-espba 
/dev/loop6                25776          0  100% /tmp/sw/mount/asr1000rp1-sipba 
/dev/loop7                36466          0  100% /tmp/sw/mount/asr1000rp1-sipsp 
none                       3728    1933760    1% /dev                           
/proc/bus/usb                 0          0     - /proc/bus/usb                  
/dev/mtdblock1              492       1556   25% /obfl                          
/etc/auto.vol                 0          0     - /vol                           
/dev/harddisk1          1255692   35185744    4% /vol/harddisk                  
---- show platform software mount R1  ----

This chassis cannot have a Route-Processor at slot 1
---- show platform software peer chassis-manager 0  ----

Peers

Peer          Location  Births  Deaths  PIn       POut      EPIn      EPOut     
------------------------------------------------------------------------------
Chassis RP    R0/0      0       0       0         0         0         0         
SPA driver    0/0       0       0       0         0         0         0         
SPA driver    0/3       0       0       0         0         0         0         
---- show platform software peer chassis-manager 1  ----

Peers

Peer          Location  Births  Deaths  PIn       POut      EPIn      EPOut     
------------------------------------------------------------------------------
Chassis RP    R0/0      0       0       0         0         0         0         
SPA driver    1/3       0       0       0         0         0         0         
---- show platform software peer chassis-manager 2  ----

This chassis cannot have a SPA-Inter-Processor at slot 2
---- show platform software peer chassis-manager F0  ----

Connection to RP: Connected
  QFP role: Active
  QFP flags: Asic-Ready, Config-Ready, Packet-Ready, Started, Config-Done
---- show platform software peer chassis-manager F1  ----

This chassis cannot have an Embedded-Service-Processor at slot 1
---- show platform software peer chassis-manager R0  ----

Peers

Peer          Location  Births  Deaths  PIn       POut      EPIn      EPOut     
------------------------------------------------------------------------------
Chassis ESP   F0        1       0       0         0         0         0         
Chassis SIP   0         1       0       0         0         0         0         
Chassis SIP   1         1       0       0         0         0         0         
IOSD          R0/0      1       0       0         0         0         0         
---- show platform software peer chassis-manager R1  ----

This chassis cannot have a Route-Processor at slot 1
---- show platform software peer forwarding-manager F0  ----


FP slot: 0, FP role: Active
Number of RP FMAN resyncs: 0, Current epoch: 0
Init Complete: Yes, Configuration State: Ready
Config objects: 513313, Need updates: 0, Ready for download: 0

Master RP Slot: 0, Bay: 0
RP FMAN Channel (Download): Connected, Read-selected
RP FMAN Channel (Upstream): Connected, Read-selected
RP FMAN IOSD Channel (Upstream): Connected, Read-selected
IOSD Stats Channel: Connected, Read-selected
IOSD Data Channel: Connected, Read-selected

RP FMAN Channel (Upstream) Sender Information

  Number of senders: 1
  Number of channel back-pressure: 0

  Sender Information

    Sender: IPSEC fmrp
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 0, Free Pool Packets: 10


RP FMAN-IOSd Channel (Upstream) Information

    Number of senders: 1
    Number of channel back-pressure: 0
    Is back-pressured: No, IPC-LOG send context created: Yes

  IPC log context Information

    Peer name: fman-ipc-log-slot0-bay0
    State: Connected
    Has IPC-LOG: Yes, Connected to peer cnt: 1
    Log is back-pressured: No, Log back-pressured cnt: 0
    Pending ACK Request buffer: 0
    Cached msg cnt: 0, Total cached msg cnt: 0

      IPC Log internal stats:
      Send Seq: 0, Recv Seq: 0, Msgs Sent: 0, Msgs Recovered: 0

  Sender Information

    Sender: IPSEC iosd
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 0, Free Pool Packets: 10


IOSD Stats Channel Sender Information

  Number of senders: 29
  Number of channel back-pressure: 0

  Sender Information

    Sender: Interface stats
      Tx Packets: 453419, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 500
      Packed Messages: 1806284, Free Pool Packets: 10

    Sender: FW stats
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 0, Free Pool Packets: 10

    Sender: NAT stats
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 200
      Packed Messages: 0, Free Pool Packets: 10

    Sender: MLP stats
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 0, Free Pool Packets: 10

    Sender: IP option stats
      Tx Packets: 451578, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 10
      Packed Messages: 451578, Free Pool Packets: 10

    Sender: PBR stats
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 0, Free Pool Packets: 10

    Sender: NAT64 stats
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 0, Free Pool Packets: 10

    Sender: Proc stats
      Tx Packets: 903153, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 1806306, Free Pool Packets: 10

    Sender: BGPPA stats
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 10
      Packed Messages: 0, Free Pool Packets: 10

    Sender: Frag stats
      Tx Packets: 13, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 25, Free Pool Packets: 10

    Sender: SMI stats
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 0, Free Pool Packets: 10

    Sender: CEF stats
      Tx Packets: 451575, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 451575, Free Pool Packets: 10

    Sender: ACL stats
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 0, Free Pool Packets: 10

    Sender: uRPF stats
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 0, Free Pool Packets: 10

    Sender: NF stats
      Tx Packets: 451581, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 903162, Free Pool Packets: 10

    Sender: QOS stats
      Tx Packets: 375702, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 1200
      Packed Messages: 751404, Free Pool Packets: 10

    Sender: FPM stats
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 500
      Packed Messages: 0, Free Pool Packets: 10

    Sender: IPHC stats
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 0, Free Pool Packets: 10

    Sender: STILE stats
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 10
      Packed Messages: 0, Free Pool Packets: 10

    Sender: IPSEC stats
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 0, Free Pool Packets: 10

    Sender: ICMP stats
      Tx Packets: 451578, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 10
      Packed Messages: 451578, Free Pool Packets: 10

    Sender: ICMP6 stats
      Tx Packets: 451578, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 10
      Packed Messages: 451578, Free Pool Packets: 10

    Sender: WCCP stats
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 0, Free Pool Packets: 10

    Sender: LI stats
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 0, Free Pool Packets: 10

    Sender: QFP MIB stats
      Tx Packets: 903217, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 1806303, Free Pool Packets: 10

    Sender: ESS stats
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 0, Free Pool Packets: 10

    Sender: ESS isg accounting
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 0, Free Pool Packets: 10

    Sender: ISG DRL
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 0, Free Pool Packets: 10

    Sender: ESS IPv6 accounting
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 0, Free Pool Packets: 10

IOSD Data Channel Sender Information

  Number of senders: 8
  Number of channel back-pressure: 0

  Sender Information

    Sender: Interface deletion
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 500
      Packed Messages: 0, Free Pool Packets: 10

    Sender: NAT data
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 200
      Packed Messages: 0, Free Pool Packets: 10

    Sender: RG data
      Tx Packets: 1, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 1, Free Pool Packets: 10

    Sender: SBC
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 250
      Packed Messages: 0, Free Pool Packets: 10

    Sender: ESS async events
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 1000
      Packed Messages: 0, Free Pool Packets: 10

    Sender: SSLVPN data
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 200
      Packed Messages: 0, Free Pool Packets: 10

    Sender: FNF IOSd
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 200
      Packed Messages: 0, Free Pool Packets: 10

    Sender: IPSEC data
      Tx Packets: 0, Failed Packets: 0
      Queued Packets: 0, Maximum Queued Packets: 50
      Packed Messages: 0, Free Pool Packets: 10

---- show platform software peer forwarding-manager F1  ----

This chassis cannot have an Embedded-Service-Processor at slot 1
---- show platform software peer forwarding-manager R0  ----


IOSD Connection Information:

  State: Connected, Read-selected
  MQIPC Connections: 1, Failures: 47
    12481362 packets received (0 dropped), 1141173972 bytes
    Read attempts: 1591999, Yields: 3
  BIPC Connection State: Ready
    Accepted: 1, Rejected: 0, Closed: 0, Backpressures: 0
    0 packets sent, 0 bytes

FP Peers Information:

  Slot: 0
  Peer state: connected
    OM ID: 0, Download attempts: 1591843
      Complete: 1583507, Yields: 0, Spurious: 8334
      IPC Back-Pressure: 0, IPC-Log Back-Pressure: 2
    Back-Pressure asserted for IPC: 0, IPC-Log: 8
    Number of FP FMAN peer connection expected: 3
    Number of FP FMAN online msg received: 1
    Config IPC Context:
      State: Connected, Read-selected
      BIPC Handle: 0x10478ed8, BIPC FD: 16, Peer Context: 0x1048b280
      Tx Packets: 2047965, Messages: 8909502, ACKs: 418668
      Rx Packets: 418669, Bytes: 18421432

      IPC Log:
        Send Seq: 25452, Recv Seq: 25452, Msgs Sent: 0, Msgs Recovered: 0

    Upstream FMRP IPC Context:
      State: Connected, Read-selected
      BIPC Handle: 0x1049d658, BIPC FD: 18, Peer Context: 0x1048b280
      Rx Packets: 0, Bytes: 0

    Upstream FMRP-IOSd IPC Context:
      State: Connected, Read-selected
      BIPC Handle: 0x1048b358, BIPC FD: 17, Peer Context: 0x1048b280
      Rx Packets: 0, Bytes: 0
      Rx ACK Requests: 0, Tx ACK Responses: 0


---- show platform software peer forwarding-manager R1  ----

This chassis cannot have a Route-Processor at slot 1
---- show platform software peer interface-manager 0  ----

Interface Manager Active Peers

Peer: RP
  Fru         : Route-Processor
  Slot        : 0         Bay          : 0      
  Registered  : Peer is connected
  Births      : 1         Deaths       : 0      
  Messages In : 676385    Messages Out : 20279273   Errors: 0
  Errors In   : 0         Errors Out   : 0      
  IPC Alloc   : 18442590   IPC Free     : 18442590
  NoSpc Count : 10
  NoSpc State : Peer IPC is clear
  CurrQ Depth : 0       
  Ack Req Sent: 1836683   Ack Resp Recv: 1836683
  Ack Req Recv: 75764     Ack Resp Sent: 75764  

Peer: SPA:0:0
  Fru         : SIP-Inter-Processor
  Slot        : 0         Bay          : 0      
  Registered  : Peer is connected
  Births      : 1         Deaths       : 0      
  Messages In : 13059142   Messages Out : 601218    Errors: 0
  Errors In   : 0         Errors Out   : 0      
  IPC Alloc   : 601218    IPC Free     : 601218 
  NoSpc Count : 0
  NoSpc State : Peer IPC is clear
  CurrQ Depth : 0       
  Ack Req Sent: 0         Ack Resp Recv: 0      
  Ack Req Recv: 0         Ack Resp Sent: 0      

Peer: SPA:0:3
  Fru         : SIP-Inter-Processor
  Slot        : 0         Bay          : 3      
  Registered  : Peer is connected
  Births      : 1         Deaths       : 0      
  Messages In : 3501421   Messages Out : 75169     Errors: 0
  Errors In   : 0         Errors Out   : 0      
  IPC Alloc   : 75169     IPC Free     : 75169  
  NoSpc Count : 0
  NoSpc State : Peer IPC is clear
  CurrQ Depth : 0       
  Ack Req Sent: 0         Ack Resp Recv: 0      
  Ack Req Recv: 0         Ack Resp Sent: 0      

---- show platform software peer interface-manager 1  ----

Interface Manager Active Peers

Peer: RP
  Fru         : Route-Processor
  Slot        : 0         Bay          : 0      
  Registered  : Peer is connected
  Births      : 1         Deaths       : 0      
  Messages In : 75166     Messages Out : 5516942   Errors: 0
  Errors In   : 0         Errors Out   : 0      
  IPC Alloc   : 4931333   IPC Free     : 4931333
  NoSpc Count : 0
  NoSpc State : Peer IPC is clear
  CurrQ Depth : 0       
  Ack Req Sent: 585609    Ack Resp Recv: 585609 
  Ack Req Recv: 75141     Ack Resp Sent: 75141  

Peer: SPA:1:3
  Fru         : SIP-Inter-Processor
  Slot        : 1         Bay          : 3      
  Registered  : Peer is connected
  Births      : 1         Deaths       : 0      
  Messages In : 3049909   Messages Out : 75167     Errors: 0
  Errors In   : 0         Errors Out   : 0      
  IPC Alloc   : 75167     IPC Free     : 75167  
  NoSpc Count : 0
  NoSpc State : Peer IPC is clear
  CurrQ Depth : 0       
  Ack Req Sent: 0         Ack Resp Recv: 0      
  Ack Req Recv: 0         Ack Resp Sent: 0      

---- show platform software peer interface-manager 2  ----

This chassis cannot have a SPA-Inter-Processor at slot 2
---- show platform software peer interface-manager R0  ----

Interface Manager Peers Status

Peer: ios_rp_iosd_slot_0
  Fru: Route-Processor, Slot: 0
  Registered  : Peer is registered
  Births      : 1         Deaths       : 0      
  Messages In : 751552    Messages Out : 25029205
  Errors In   : 0         Errors Out   : 0      
  NoSpc Count : 0
  NoSpc State : Peer is clear
  CurrQ Depth : 0         MaxQ Depth   : 0      
  Ack Req Sent: 0         Ack Resp Recv: 0      
  Ack Req Recv: 0         Ack Resp Sent: 0      
  Acks in Q   : 0         Ack Resp Pend: 0      
  Recovered   : 0
  Cache State : Peer is clear

Peer: interface-manager_rp_cc_slot_0
  Fru: SIP-Inter-Processor, Slot: 0
  Registered  : Peer is registered
  Births      : 1         Deaths       : 0      
  Messages In : 20279274   Messages Out : 2588834
  Errors In   : 0         Errors Out   : 0      
  NoSpc Count : 0
  NoSpc State : Peer is clear
  CurrQ Depth : 0         MaxQ Depth   : 14     
  Ack Req Sent: 75764     Ack Resp Recv: 75764  
  Ack Req Recv: 1836683   Ack Resp Sent: 1836683
  Acks in Q   : 0         Ack Resp Pend: 0      
  Recovered   : 0
  Cache State : Peer is clear

Peer: interface-manager_rp_cc_slot_1
  Fru: SIP-Inter-Processor, Slot: 1
  Registered  : Peer is registered
  Births      : 1         Deaths       : 0      
  Messages In : 5516942   Messages Out : 735918 
  Errors In   : 0         Errors Out   : 0      
  NoSpc Count : 0
  NoSpc State : Peer is clear
  CurrQ Depth : 0         MaxQ Depth   : 11     
  Ack Req Sent: 75141     Ack Resp Recv: 75141  
  Ack Req Recv: 585609    Ack Resp Sent: 585609 
  Acks in Q   : 0         Ack Resp Pend: 0      
  Recovered   : 0
  Cache State : Peer is clear

---- show platform software peer interface-manager R1  ----

This chassis cannot have a Route-Processor at slot 1
---- show platform software peer shell-manager  ----

Peer: cpp-sp-ui
  Role: active, process ID: 6441, instance: F0-0:cpp-sp-ui
  Connected: 2014-08-10 04:31:33, updated: 2014-08-10 04:31:33
  Uplink: remote IPC, from: F0/0
  Downlink: remote IPC, from: F0/0

Peer: psd-ui
  Role: active, process ID: 27614, instance: R0-0:psd-ui
  Connected: 2014-08-10 04:31:33, updated: 2014-08-10 04:31:33
  Uplink: remote IPC, from: R0/0
  Downlink: remote IPC, from: R0/0

Peer: fman-ui
  Role: active, process ID: 6802, instance: F0-0:fman-ui
  Connected: 2014-08-10 04:31:33, updated: 2014-08-10 04:31:33
  Uplink: remote IPC, from: F0/0
  Downlink: remote IPC, from: F0/0

Peer: cman-ui
  Role: active, process ID: 5443, instance: F0-0:cman-ui
  Connected: 2014-08-10 04:31:33, updated: 2014-08-10 04:31:33
  Uplink: remote IPC, from: F0/0
  Downlink: remote IPC, from: F0/0

Peer: cpp-ui
  Role: active, process ID: 5882, instance: F0-0:cpp-ui
  Connected: 2014-08-10 04:31:33, updated: 2014-08-10 04:31:33
  Uplink: remote IPC, from: F0/0
  Downlink: remote IPC, from: F0/0

Peer: iosd-ui
  Role: active, process ID: 7043, instance: 1-3:iosd-ui
  Connected: 2014-08-10 04:31:33, updated: 2014-08-10 04:31:33
  Uplink: remote IPC, from: 1/3
  Downlink: remote IPC, from: 1/3

Peer: emd-ui
  Role: active, process ID: 6625, instance: F0-0:emd-ui
  Connected: 2014-08-10 04:31:34, updated: 2014-08-10 04:31:34
  Uplink: remote IPC, from: F0/0
  Downlink: remote IPC, from: F0/0

Peer: hman-ui
  Role: active, process ID: 6992, instance: F0-0:hman-ui
  Connected: 2014-08-10 04:31:36, updated: 2014-08-10 04:31:36
  Uplink: remote IPC, from: F0/0
  Downlink: remote IPC, from: F0/0

Peer: hman-ui
  Role: active, process ID: 24425, instance: R0-0:hman-ui
  Connected: 2014-08-10 04:31:36, updated: 2014-08-10 04:31:36
  Uplink: remote IPC, from: R0/0
  Downlink: remote IPC, from: R0/0

Peer: plog-ui
  Role: active, process ID: 7117, instance: F0-0:plog-ui
  Connected: 2014-08-10 04:31:37, updated: 2014-08-10 04:31:37
  Uplink: remote IPC, from: F0/0
  Downlink: remote IPC, from: F0/0

Peer: cman-ui
  Role: active, process ID: 5344, instance: 1-0:cman-ui
  Connected: 2014-08-10 04:31:37, updated: 2014-08-10 04:31:37
  Uplink: remote IPC, from: 1/0
  Downlink: remote IPC, from: 1/0

Peer: emd-ui
  Role: active, process ID: 5568, instance: 1-0:emd-ui
  Connected: 2014-08-10 04:31:38, updated: 2014-08-10 04:31:38
  Uplink: remote IPC, from: 1/0
  Downlink: remote IPC, from: 1/0

Peer: cpp-driver-ui
  Role: active, process ID: 6083, instance: F0-0:cpp-driver-ui
  Connected: 2014-08-10 04:31:38, updated: 2014-08-10 04:31:38
  Uplink: remote IPC, from: F0/0
  Downlink: remote IPC, from: F0/0

Peer: iman-ui
  Role: active, process ID: 24882, instance: R0-0:iman-ui
  Connected: 2014-08-10 04:31:39, updated: 2014-08-10 04:31:39
  Uplink: remote IPC, from: R0/0
  Downlink: remote IPC, from: R0/0

Peer: hman-ui
  Role: active, process ID: 5770, instance: 1-0:hman-ui
  Connected: 2014-08-10 04:31:39, updated: 2014-08-10 04:31:39
  Uplink: remote IPC, from: 1/0
  Downlink: remote IPC, from: 1/0

Peer: fman-ui
  Role: active, process ID: 23659, instance: R0-0:fman-ui
  Connected: 2014-08-10 04:31:39, updated: 2014-08-10 04:31:39
  Uplink: remote IPC, from: R0/0
  Downlink: remote IPC, from: R0/0

Peer: iman-ui
  Role: active, process ID: 5913, instance: 1-0:iman-ui
  Connected: 2014-08-10 04:31:40, updated: 2014-08-10 04:31:40
  Uplink: remote IPC, from: 1/0
  Downlink: remote IPC, from: 1/0

Peer: cman-ui
  Role: active, process ID: 22776, instance: R0-0:cman-ui
  Connected: 2014-08-10 04:31:40, updated: 2014-08-10 04:31:40
  Uplink: remote IPC, from: R0/0
  Downlink: remote IPC, from: R0/0

Peer: plog-ui
  Role: active, process ID: 27079, instance: R0-0:plog-ui
  Connected: 2014-08-10 04:31:40, updated: 2014-08-10 04:31:40
  Uplink: remote IPC, from: R0/0
  Downlink: remote IPC, from: R0/0

Peer: cpp-ha-ui
  Role: active, process ID: 6253, instance: F0-0:cpp-ha-ui
  Connected: 2014-08-10 04:31:40, updated: 2014-08-10 04:31:40
  Uplink: remote IPC, from: F0/0
  Downlink: remote IPC, from: F0/0

Peer: plog-ui
  Role: active, process ID: 6271, instance: 1-0:plog-ui
  Connected: 2014-08-10 04:31:41, updated: 2014-08-10 04:31:41
  Uplink: remote IPC, from: 1/0
  Downlink: remote IPC, from: 1/0

Peer: emd-ui
  Role: active, process ID: 23140, instance: R0-0:emd-ui
  Connected: 2014-08-10 04:31:41, updated: 2014-08-10 04:31:41
  Uplink: remote IPC, from: R0/0
  Downlink: remote IPC, from: R0/0

Peer: cman-ui
  Role: active, process ID: 5340, instance: 0-0:cman-ui
  Connected: 2014-08-10 04:31:42, updated: 2014-08-10 04:31:42
  Uplink: remote IPC, from: 0/0
  Downlink: remote IPC, from: 0/0

Peer: sman-ui
  Role: active, process ID: 28347, instance: R0-0:sman-ui
  Connected: 2014-08-10 04:31:42, updated: 2014-08-10 04:31:42
  Uplink: remote IPC, from: R0/0
  Downlink: remote IPC, from: R0/0

Peer: emd-ui
  Role: active, process ID: 5568, instance: 0-0:emd-ui
  Connected: 2014-08-10 04:31:43, updated: 2014-08-10 04:31:43
  Uplink: remote IPC, from: 0/0
  Downlink: remote IPC, from: 0/0

Peer: hman-ui
  Role: active, process ID: 5780, instance: 0-0:hman-ui
  Connected: 2014-08-10 04:31:44, updated: 2014-08-10 04:31:44
  Uplink: remote IPC, from: 0/0
  Downlink: remote IPC, from: 0/0

Peer: iman-ui
  Role: active, process ID: 5913, instance: 0-0:iman-ui
  Connected: 2014-08-10 04:31:44, updated: 2014-08-10 04:31:44
  Uplink: remote IPC, from: 0/0
  Downlink: remote IPC, from: 0/0

Peer: plog-ui
  Role: active, process ID: 6271, instance: 0-0:plog-ui
  Connected: 2014-08-10 04:31:46, updated: 2014-08-10 04:31:46
  Uplink: remote IPC, from: 0/0
  Downlink: remote IPC, from: 0/0

Peer: iosd-ui
  Role: active, process ID: 25737, instance: R0-0:iosd-ui
  Connected: 2014-08-10 04:31:54, updated: 2014-08-10 04:31:54
  Uplink: remote IPC, from: R0/0
  Downlink: remote IPC, from: R0/0

Peer: iosd-ui
  Role: active, process ID: 7099, instance: 0-0:iosd-ui
  Connected: 2014-08-10 04:31:54, updated: 2014-08-10 04:31:54
  Uplink: remote IPC, from: 0/0
  Downlink: remote IPC, from: 0/0

Peer: iosd-ui
  Role: active, process ID: 7489, instance: 0-3:iosd-ui
  Connected: 2014-08-10 04:31:59, updated: 2014-08-10 04:31:59
  Uplink: remote IPC, from: 0/3
  Downlink: remote IPC, from: 0/3

---- show platform software peer shell-manager brief  ----

  Peer             Role        Pid     Downlink  Uplink  Time        
  -----------------------------------------------------------------
  cman-ui          active      5443    F0/0      F0/0    4515810     
  cman-ui          active      5344    1/0       1/0     4515806     
  cman-ui          active      22776   R0/0      R0/0    4515803     
  cman-ui          active      5340    0/0       0/0     4515801     
  cpp-driver-ui    active      6083    F0/0      F0/0    4515805     
  cpp-ha-ui        active      6253    F0/0      F0/0    4515803     
  cpp-sp-ui        active      6441    F0/0      F0/0    4515810     
  cpp-ui           active      5882    F0/0      F0/0    4515810     
  emd-ui           active      6625    F0/0      F0/0    4515809     
  emd-ui           active      5568    1/0       1/0     4515805     
  emd-ui           active      23140   R0/0      R0/0    4515802     
  emd-ui           active      5568    0/0       0/0     4515800     
  fman-ui          active      6802    F0/0      F0/0    4515810     
  fman-ui          active      23659   R0/0      R0/0    4515804     
  hman-ui          active      6992    F0/0      F0/0    4515807     
  hman-ui          active      24425   R0/0      R0/0    4515807     
  hman-ui          active      5770    1/0       1/0     4515804     
  hman-ui          active      5780    0/0       0/0     4515799     
  iman-ui          active      24882   R0/0      R0/0    4515804     
  iman-ui          active      5913    1/0       1/0     4515803     
  iman-ui          active      5913    0/0       0/0     4515799     
  iosd-ui          active      7043    1/3       1/3     4515810     
  iosd-ui          active      25737   R0/0      R0/0    4515789     
  iosd-ui          active      7099    0/0       0/0     4515789     
  iosd-ui          active      7489    0/3       0/3     4515784     
  plog-ui          active      7117    F0/0      F0/0    4515806     
  plog-ui          active      27079   R0/0      R0/0    4515803     
  plog-ui          active      6271    1/0       1/0     4515802     
  plog-ui          active      6271    0/0       0/0     4515797     
  psd-ui           active      27614   R0/0      R0/0    4515810     
  sman-ui          active      28347   R0/0      R0/0    4515801     
---- show platform software process environment host-manager 0  ----

Name                            Value                                           
------------------------------------------------------------------------------
TRACEKEY                        1#eda6d098171a07eee7988e541e33e3e5              
BINOS_FRU_BASE_PKG              cc                                              
BINOS_BAY_LOCAL                 0                                               
BINOS_CONF_DIR                  /usr/binos/conf                                 
CONSOLE                         /dev/console                                    
PROCESS_FRU                     cc                                              
BINOS_BTRACE_FILE_PATH          /tmp/cc/trace                                   
SLOT                            0                                               
CPP_BIN_DIR                     /usr/cpp/bin/cc                                 
ROMMON_BINFOVER                 5                                               
TERM                            linux                                           
BOARD_TYPE                      CC                                              
BINOS_SLOT                      0                                               
BINOS_FRU                       cc                                              
BINOS_BASE_DIR                  /tmp/cc                                         
MQIPC_PREFIX_NAME                                                               
REAL_MGMTE_DEV                  eth2                                            
BINOS_BAY                       0                                               
USER                            root                                            
HOLD_INTERVAL                   1800                                            
PROC_SCOREBOARD_BKTRACE_FILE    /tmp/cc/process/hman%cc_0_0/hman%cc_0_0.bac...  
CPP_STARTUP_FILE                /tmp/cc/cpp_startup_complete                    
LD_LIBRARY_PATH                 /tmp/sw/cc/0/0/cc/mount/usr/lib/:/tmp/sw/cc...  
PMAN_SH_BTRACE_LEVEL            NOTICE                                          
INIT_VERSION                    sysvinit-2.85                                   
BINOS_CHASFS_ROOT               /tmp/cc/chasfs                                  
BINOS_NVRAM_DIR                 /config                                         
ROMMON_PS1                      rommon _ _                                      
ROMMON_TFTP_FILE                base_cc_00.pkg                                  
PROCESS_SLOT                    0                                               
SW_FRU_BASE                     /tmp/sw/cc/0/0/cc/mount                         
PVP_SH_BTRACE_LEVEL             NOTICE                                          
CPP_STARTUP_WAIT                120                                             
PLATFORM_TYPE                   mcp                                             
RUNLEVEL                        3                                               
runlevel                        3                                               
BINOS_CMRP_TFTP_PORT            69                                              
PWD                             /                                               
BINOS_CMRP_IMAGE_ROOT           /tftp                                           
CPP_CONF_DIR                    /usr/cpp/conf                                   
BINOS_RAMFS_DIR                 /tmp                                            
BOARD_SUBTYPE                   10G                                             
PREVLEVEL                       N                                               
previous                        N                                               
BINOS_TDLDB_PATH                /tmp/cc/tdldb                                   
SR_BOOT                         tftp:base_cc_00.pkg                             
LOGFILE                         /tmp/cc/pvp_log                                 
GMON_OUT_PREFIX                 /harddisk/hman                                  
SHLVL                           4                                               
HOME                            /                                               
SR_BAY_IS_GLOBAL                1                                               
PROCESS_BAY                     0                                               
HOLD_FAILURES                   2                                               
PROCESS                         hman                                            
BINOS_BIN_DIR                   /usr/binos/bin/cc                               
TEST_DIR                        /usr/binos/conf                                 
BINOS_BTRACE_LEVEL              NOTICE                                          
BINOS_CHASSIS_XML               /usr/binos/conf/chassis.xml                     
PROCESS_ARGUMENTS                                                               
LOGDIR                          /tmp/cc                                         
PROF_DIR                        /harddisk                                       
FRU                             cc                                              
BINOS_SLOT_LOCAL                0                                               
BAY                             0                                               
BINOS_LIPC_PATH                 /tmp/cc/lipc                                    
ROMMON_VERSION                  12.2(33r)XNC                                    
BINOS_FRU_LOCAL                 BINOS_FRU_CC                                    
NETIO_NETMAP                    /usr/binos/bin/cc/NETMAP                        
RESOLVED_PROCESS                /tmp/sw/cc/0/0/cc/mount/usr/binos/bin/hman      
_                               /tmp/sw/cc/0/0/cc/mount/usr/binos/bin/hman      
---- show platform software process environment host-manager 1  ----

Name                            Value                                           
------------------------------------------------------------------------------
TRACEKEY                        1#eda6d098171a07eee7988e541e33e3e5              
BINOS_FRU_BASE_PKG              cc                                              
BINOS_BAY_LOCAL                 0                                               
BINOS_CONF_DIR                  /usr/binos/conf                                 
CONSOLE                         /dev/console                                    
PROCESS_FRU                     cc                                              
BINOS_BTRACE_FILE_PATH          /tmp/cc/trace                                   
SLOT                            1                                               
CPP_BIN_DIR                     /usr/cpp/bin/cc                                 
ROMMON_BINFOVER                 5                                               
TERM                            linux                                           
BOARD_TYPE                      CC                                              
BINOS_SLOT                      1                                               
BINOS_FRU                       cc                                              
BINOS_BASE_DIR                  /tmp/cc                                         
MQIPC_PREFIX_NAME                                                               
REAL_MGMTE_DEV                  eth2                                            
BINOS_BAY                       0                                               
USER                            root                                            
HOLD_INTERVAL                   1800                                            
PROC_SCOREBOARD_BKTRACE_FILE    /tmp/cc/process/hman%cc_1_0/hman%cc_1_0.bac...  
CPP_STARTUP_FILE                /tmp/cc/cpp_startup_complete                    
LD_LIBRARY_PATH                 /tmp/sw/cc/1/0/cc/mount/usr/lib/:/tmp/sw/cc...  
PMAN_SH_BTRACE_LEVEL            NOTICE                                          
INIT_VERSION                    sysvinit-2.85                                   
BINOS_CHASFS_ROOT               /tmp/cc/chasfs                                  
BINOS_NVRAM_DIR                 /config                                         
ROMMON_PS1                      rommon _ _                                      
ROMMON_TFTP_FILE                base_cc_01.pkg                                  
PROCESS_SLOT                    1                                               
SW_FRU_BASE                     /tmp/sw/cc/1/0/cc/mount                         
PVP_SH_BTRACE_LEVEL             NOTICE                                          
CPP_STARTUP_WAIT                120                                             
PLATFORM_TYPE                   mcp                                             
RUNLEVEL                        3                                               
runlevel                        3                                               
BINOS_CMRP_TFTP_PORT            69                                              
PWD                             /                                               
BINOS_CMRP_IMAGE_ROOT           /tftp                                           
CPP_CONF_DIR                    /usr/cpp/conf                                   
BINOS_RAMFS_DIR                 /tmp                                            
BOARD_SUBTYPE                   10G                                             
PREVLEVEL                       N                                               
previous                        N                                               
BINOS_TDLDB_PATH                /tmp/cc/tdldb                                   
SR_BOOT                         tftp:base_cc_01.pkg                             
LOGFILE                         /tmp/cc/pvp_log                                 
GMON_OUT_PREFIX                 /harddisk/hman                                  
SHLVL                           4                                               
HOME                            /                                               
SR_BAY_IS_GLOBAL                1                                               
PROCESS_BAY                     0                                               
HOLD_FAILURES                   2                                               
PROCESS                         hman                                            
BINOS_BIN_DIR                   /usr/binos/bin/cc                               
TEST_DIR                        /usr/binos/conf                                 
BINOS_BTRACE_LEVEL              NOTICE                                          
BINOS_CHASSIS_XML               /usr/binos/conf/chassis.xml                     
PROCESS_ARGUMENTS                                                               
LOGDIR                          /tmp/cc                                         
PROF_DIR                        /harddisk                                       
FRU                             cc                                              
BINOS_SLOT_LOCAL                1                                               
BAY                             0                                               
BINOS_LIPC_PATH                 /tmp/cc/lipc                                    
ROMMON_VERSION                  12.2(33r)XNC                                    
BINOS_FRU_LOCAL                 BINOS_FRU_CC                                    
NETIO_NETMAP                    /usr/binos/bin/cc/NETMAP                        
RESOLVED_PROCESS                /tmp/sw/cc/1/0/cc/mount/usr/binos/bin/hman      
_                               /tmp/sw/cc/1/0/cc/mount/usr/binos/bin/hman      
---- show platform software process environment host-manager 2  ----

This chassis cannot have a SPA-Inter-Processor at slot 2
---- show platform software process environment host-manager F0  ----

Name                            Value                                           
------------------------------------------------------------------------------
TRACEKEY                        1#eda6d098171a07eee7988e541e33e3e5              
BINOS_FRU_BASE_PKG              fp                                              
BINOS_BAY_LOCAL                 0                                               
BINOS_CONF_DIR                  /usr/binos/conf                                 
CONSOLE                         /dev/console                                    
PROCESS_FRU                     fp                                              
BINOS_BTRACE_FILE_PATH          /tmp/fp/trace                                   
SLOT                            0                                               
CPP_BIN_DIR                     /usr/cpp/bin/fp                                 
ROMMON_BINFOVER                 5                                               
TERM                            linux                                           
BOARD_TYPE                      FP                                              
BINOS_SLOT                      0                                               
BINOS_FRU                       fp                                              
BINOS_BASE_DIR                  /tmp/fp                                         
MQIPC_PREFIX_NAME                                                               
REAL_MGMTE_DEV                  eth2                                            
BINOS_BAY                       0                                               
USER                            root                                            
HOLD_INTERVAL                   1800                                            
PROC_SCOREBOARD_BKTRACE_FILE    /tmp/fp/process/hman%fp_0_0/hman%fp_0_0.bac...  
CPP_STARTUP_FILE                /tmp/fp/cpp_startup_complete                    
LD_LIBRARY_PATH                 /tmp/sw/fp/0/0/fp/mount/usr/lib/:/tmp/sw/fp...  
PMAN_SH_BTRACE_LEVEL            NOTICE                                          
INIT_VERSION                    sysvinit-2.85                                   
BINOS_CHASFS_ROOT               /tmp/fp/chasfs                                  
BINOS_NVRAM_DIR                 /config                                         
ROMMON_PS1                      rommon _ _                                      
ROMMON_TFTP_FILE                base_fp_00.pkg                                  
PROCESS_SLOT                    0                                               
SW_FRU_BASE                     /tmp/sw/fp/0/0/fp/mount                         
PVP_SH_BTRACE_LEVEL             NOTICE                                          
CPP_STARTUP_WAIT                120                                             
PLATFORM_TYPE                   mcp                                             
RUNLEVEL                        3                                               
runlevel                        3                                               
BINOS_CMRP_TFTP_PORT            69                                              
PWD                             /                                               
FMANFP_ENABLE_EC                0                                               
BINOS_CMRP_IMAGE_ROOT           /tftp                                           
CPP_CONF_DIR                    /usr/cpp/conf                                   
BINOS_RAMFS_DIR                 /tmp                                            
BOARD_SUBTYPE                   10G                                             
PREVLEVEL                       N                                               
previous                        N                                               
BINOS_TDLDB_PATH                /tmp/fp/tdldb                                   
SR_BOOT                         tftp:base_fp_00.pkg                             
LOGFILE                         /tmp/fp/pvp_log                                 
GMON_OUT_PREFIX                 /harddisk/hman                                  
SHLVL                           4                                               
HOME                            /                                               
SR_BAY_IS_GLOBAL                1                                               
PROCESS_BAY                     0                                               
HOLD_FAILURES                   2                                               
PROCESS                         hman                                            
BINOS_BIN_DIR                   /usr/binos/bin/fp                               
TEST_DIR                        /usr/binos/conf                                 
BINOS_BTRACE_LEVEL              NOTICE                                          
BINOS_CHASSIS_XML               /usr/binos/conf/chassis.xml                     
PROCESS_ARGUMENTS                                                               
FMANFP_ENABLE_SPIID             0                                               
LOGDIR                          /tmp/fp                                         
PROF_DIR                        /harddisk                                       
FRU                             fp                                              
BINOS_SLOT_LOCAL                0                                               
BAY                             0                                               
BINOS_LIPC_PATH                 /tmp/fp/lipc                                    
ROMMON_VERSION                  12.2(33r)XNC                                    
BINOS_FRU_LOCAL                 BINOS_FRU_FP                                    
NETIO_NETMAP                    /usr/binos/bin/fp/NETMAP                        
RESOLVED_PROCESS                /tmp/sw/fp/0/0/fp/mount/usr/binos/bin/hman      
_                               /tmp/sw/fp/0/0/fp/mount/usr/binos/bin/hman      
---- show platform software process environment host-manager F1  ----

This chassis cannot have an Embedded-Service-Processor at slot 1
---- show platform software process environment host-manager R0  ----

Name                            Value                                           
------------------------------------------------------------------------------
TRACEKEY                        1#eda6d098171a07eee7988e541e33e3e5              
BINOS_FRU_BASE_PKG              rp_base                                         
BINOS_BAY_LOCAL                 0                                               
BINOS_CONF_DIR                  /usr/binos/conf                                 
CONSOLE                         /dev/tty0                                       
PROCESS_FRU                     rp                                              
BINOS_BTRACE_FILE_PATH          /tmp/rp/trace                                   
SLOT                            0                                               
CPP_BIN_DIR                     /usr/cpp/bin/rp                                 
ROMMON_BINFOVER                 5                                               
TERM                            linux                                           
BOARD_TYPE                      RP                                              
ROMMON_BOOT                                                                     
BINOS_SLOT                      0                                               
BINOS_FRU                       rp                                              
BINOS_BASE_DIR                  /tmp/rp                                         
MQIPC_PREFIX_NAME                                                               
REAL_MGMTE_DEV                  eth2                                            
BINOS_BAY                       0                                               
USER                            root                                            
HOLD_INTERVAL                   1800                                            
PROC_SCOREBOARD_BKTRACE_FILE    /tmp/rp/process/hman%rp_0_0/hman%rp_0_0.bac...  
CPP_STARTUP_FILE                /tmp/rp/cpp_startup_complete                    
LD_LIBRARY_PATH                 /tmp/sw/rp/0/0/rp_daemons/mount/usr/lib/:/t...  
PMAN_SH_BTRACE_LEVEL            NOTICE                                          
ROMMON_RET_2_RCALTS                                                             
INIT_VERSION                    sysvinit-2.85                                   
BINOS_CHASFS_ROOT               /tmp/rp/chasfs                                  
BINOS_NVRAM_DIR                 /config                                         
ROMMON_PS1                      rommon _ _                                      
PROCESS_SLOT                    0                                               
SW_FRU_BASE                     /tmp/sw/rp/0/0/rp_daemons/mount                 
PVP_SH_BTRACE_LEVEL             NOTICE                                          
ROMMON_BSI                      0                                               
CPP_STARTUP_WAIT                120                                             
PLATFORM_TYPE                   mcp                                             
ROMMON_MCP_STARTUP_TRACEFLAGS   00000000:00000000                               
RUNLEVEL                        3                                               
runlevel                        3                                               
BINOS_CMRP_TFTP_PORT            69                                              
PWD                             /                                               
BINOS_CMRP_IMAGE_ROOT           /tftp                                           
CPP_CONF_DIR                    /usr/cpp/conf                                   
BINOS_RAMFS_DIR                 /tmp                                            
BOARD_SUBTYPE                   RP1                                             
ROMMON_RANDOM_NUM               328656945                                       
ROMMON_RET_2_RTS                11:02:21 MSK Wed Nov 20 2013                    
PREVLEVEL                       2                                               
previous                        2                                               
BINOS_TDLDB_PATH                /tmp/rp/tdldb                                   
BINOS_DUAL_IOS_CAPABLE          1                                               
SR_BOOT                         bootflash:/asr1000rp1-advipservices.03.02.0...  
LOGFILE                         /tmp/rp/pvp_log                                 
GMON_OUT_PREFIX                 /harddisk/hman                                  
SHLVL                           4                                               
HOME                            /                                               
SR_BAY_IS_GLOBAL                1                                               
PROCESS_BAY                     0                                               
HOLD_FAILURES                   2                                               
PROCESS                         hman                                            
BINOS_BIN_DIR                   /usr/binos/bin/rp                               
TEST_DIR                        /usr/binos/conf                                 
BINOS_BTRACE_LEVEL              NOTICE                                          
BINOS_CHASSIS_XML               /usr/binos/conf/chassis.xml                     
PROCESS_ARGUMENTS               -c                                              
LOGDIR                          /tmp/rp                                         
PROF_DIR                        /harddisk                                       
FRU                             rp                                              
BINOS_SLOT_LOCAL                0                                               
BAY                             0                                               
BINOS_LIPC_PATH                 /tmp/rp/lipc                                    
ROMMON_VERSION                  12.2(33r)XNC                                    
BINOS_FRU_LOCAL                 BINOS_FRU_RP                                    
BINOS_DUAL_IOS_REQUESTED        0                                               
NETIO_NETMAP                    /usr/binos/bin/rp/NETMAP                        
RESOLVED_PROCESS                /tmp/sw/mount/asr1000rp1-rpcontrol.03.02.00...  
_                               /tmp/sw/mount/asr1000rp1-rpcontrol.03.02.00...  
---- show platform software process environment host-manager R1  ----

This chassis cannot have a Route-Processor at slot 1
---- show platform software process environment shell-manager RP active  ----

Name                            Value                                           
------------------------------------------------------------------------------
TRACEKEY                        1#847981e229515040c6113eb4df9c1414              
BINOS_FRU_BASE_PKG              rp_base                                         
BINOS_BAY_LOCAL                 0                                               
BINOS_CONF_DIR                  /usr/binos/conf                                 
CONSOLE                         /dev/tty0                                       
PROCESS_FRU                     rp                                              
BINOS_BTRACE_FILE_PATH          /tmp/rp/trace                                   
SLOT                            0                                               
CPP_BIN_DIR                     /usr/cpp/bin/rp                                 
ROMMON_BINFOVER                 5                                               
TERM                            linux                                           
BOARD_TYPE                      RP                                              
ROMMON_BOOT                                                                     
BINOS_SLOT                      0                                               
BINOS_FRU                       rp                                              
BINOS_BASE_DIR                  /tmp/rp                                         
MQIPC_PREFIX_NAME                                                               
IOSD_NVRAM_DIR                  /config                                         
REAL_MGMTE_DEV                  eth2                                            
BINOS_BAY                       0                                               
USER                            root                                            
HOLD_INTERVAL                   1800                                            
PROC_SCOREBOARD_BKTRACE_FILE    /tmp/rp/process/smand%rp_0_0/smand%rp_0_0.b...  
CPP_STARTUP_FILE                /tmp/rp/cpp_startup_complete                    
LD_LIBRARY_PATH                 /tmp/sw/rp/0/0/rp_daemons/mount/usr/lib/:/t...  
PMAN_SH_BTRACE_LEVEL            NOTICE                                          
ROMMON_RET_2_RCALTS                                                             
INIT_VERSION                    sysvinit-2.85                                   
BINOS_CHASFS_ROOT               /tmp/rp/chasfs                                  
BINOS_NVRAM_DIR                 /config                                         
ROMMON_PS1                      rommon _ _                                      
PROCESS_SLOT                    0                                               
SW_FRU_BASE                     /tmp/sw/rp/0/0/rp_daemons/mount                 
PVP_SH_BTRACE_LEVEL             NOTICE                                          
ROMMON_BSI                      0                                               
CPP_STARTUP_WAIT                120                                             
PLATFORM_TYPE                   mcp                                             
ROMMON_MCP_STARTUP_TRACEFLAGS   00000000:00000000                               
RUNLEVEL                        3                                               
runlevel                        3                                               
BINOS_CMRP_TFTP_PORT            69                                              
REAL_AUX                        /dev/ttyS1                                      
PWD                             /                                               
BINOS_CMRP_IMAGE_ROOT           /tftp                                           
CPP_CONF_DIR                    /usr/cpp/conf                                   
BINOS_RAMFS_DIR                 /tmp                                            
BOARD_SUBTYPE                   RP1                                             
ROMMON_RANDOM_NUM               328656945                                       
ROMMON_RET_2_RTS                11:02:21 MSK Wed Nov 20 2013                    
PREVLEVEL                       2                                               
previous                        2                                               
BINOS_TDLDB_PATH                /tmp/rp/tdldb                                   
BINOS_DUAL_IOS_CAPABLE          1                                               
SR_BOOT                         bootflash:/asr1000rp1-advipservices.03.02.0...  
LOGFILE                         /tmp/rp/pvp_log                                 
GMON_OUT_PREFIX                 /harddisk/smand                                 
SHLVL                           4                                               
HOME                            /                                               
SR_BAY_IS_GLOBAL                1                                               
PROCESS_BAY                     0                                               
HOLD_FAILURES                   2                                               
PROCESS                         smand                                           
BINOS_BIN_DIR                   /usr/binos/bin/rp                               
TEST_DIR                        /usr/binos/conf                                 
BINOS_BTRACE_LEVEL              NOTICE                                          
BINOS_CHASSIS_XML               /usr/binos/conf/chassis.xml                     
PROCESS_ARGUMENTS               -i /tmp/sw/rp/0/0/rp_daemons/mount/usr/bino...  
LOGDIR                          /tmp/rp                                         
PROF_DIR                        /harddisk                                       
FRU                             rp                                              
IOSD_MEMORY_MB                  1800                                            
BINOS_SLOT_LOCAL                0                                               
REAL_CONSOLE                    /dev/ttyS0                                      
BAY                             0                                               
BINOS_LIPC_PATH                 /tmp/rp/lipc                                    
ROMMON_VERSION                  12.2(33r)XNC                                    
BINOS_FRU_LOCAL                 BINOS_FRU_RP                                    
BINOS_DUAL_IOS_REQUESTED        0                                               
NETIO_NETMAP                    /usr/binos/bin/rp/NETMAP                        
RESOLVED_PROCESS                /tmp/sw/mount/asr1000rp1-rpcontrol.03.02.00...  
_                               /tmp/sw/mount/asr1000rp1-rpcontrol.03.02.00...  
LUA_CPATH                       /tmp/sw/rp/local/0/rp_daemons/mount/usr/bin...  
LUA_PATH                        /tmp/sw/rp/local/0/rp_daemons/mount/lua/?.lua   
---- show platform software process list 0  ----

Name                     Pid    PPid  Group Id  Status    Priority  Size        
------------------------------------------------------------------------------
init                       1       0         1  S               20  2207744     
kthreadd                   2       0         0  S               15  0           
ksoftirqd/0                3       2         0  S               15  0           
watchdog/0                 4       2         0  S       4294967196  0           
events/0                   5       2         0  S               15  0           
khelper                    6       2         0  S               15  0           
netns                      9       2         0  S               15  0           
kblockd/0                 55       2         0  S               15  0           
ata/0                     62       2         0  S               15  0           
ata_aux                   63       2         0  S               15  0           
khubd                     69       2         0  S               15  0           
kseriod                   72       2         0  S               15  0           
pdflush                  117       2         0  S               20  0           
pdflush                  118       2         0  S               20  0           
kswapd0                  119       2         0  S               15  0           
aio/0                    171       2         0  S               15  0           
mtdblockd                878       2         0  S               15  0           
rpciod/0                1783       2         0  S               15  0           
nfsiod                  1789       2         0  S               15  0           
loop0                   1826       2         0  S                0  0           
portmap                 1871       1      1871  S               20  2297856     
loop1                   1910       2         0  S                0  0           
udevd                   2621       1      2621  S               16  2187264     
jffs2_gcd_mtd1          3507       2         0  S               30  0           
klogd                   3839       1      3839  S               20  1941504     
automount               3869       1      3869  S               20  40095744    
xinetd                  3887       1      3887  S               20  3567616     
xinetd                  3889       1      3889  S               20  3567616     
scansta                 4073       2         0  S               15  0           
loop2                   4082       2         0  S                0  0           
pvp.sh                  4587       1      4586  S               20  4423680     
rotee                   4634       1      4633  S               20  8515584     
inotifywait             4667    4587      4586  S               20  2117632     
pman.sh                 4727    4587      4586  S               14  4321280     
rotee                   4819       1      4818  S               20  8519680     
pman.sh                 4877    4587      4586  S               14  4325376     
agetty                  4883       1      4883  S               20  1933312     
mcp_chvrf.sh            4889       1      4889  S               20  3244032     
issu_switchover         4899       1      4899  S               20  5120000     
xinetd                  4903    4889      4889  S               20  3567616     
oom.sh                  4904       1      4904  S               20  3624960     
btrace_rotate.s         5068    4727      5068  S               20  4096000     
rotee                   5070       1      5069  S               20  8519680     
rotee                   5116       1      5115  S               20  8515584     
oom.sh                  5155    4904      5155  S               20  3735552     
rotee                   5175       1      5174  S               20  8515584     
pman.sh                 5177    4587      4586  S               14  4325376     
rotee                   5292       1      5291  S               20  8519680     
cmcc                    5340    4877      5340  S               20  32419840    
rotee                   5347       1      5346  S               20  8519680     
pman.sh                 5404    4587      4586  S               14  4325376     
emd                     5568    5177      5568  S               20  21008384    
rotee                   5576       1      5575  S               20  8519680     
pman.sh                 5633    4587      4586  S               14  4325376     
rotee                   5777       1      5776  S               20  8519680     
hman                    5780    5404      5780  R               20  17522688    
imccd                   5913    5633      5913  S               20  19111936    
pman.sh                 6060    4587      4586  S               14  4325376     
rotee                   6143       1      6142  S               20  8519680     
plogd                   6271    6060      6271  S               20  16822272    
inotifywait             6346    4899      4899  S               20  2113536     
pman.sh                 6883    4587      4586  S               14  4317184     
rotee                   6968       1      6967  S               20  8519680     
mcpcc-lc-ms             7099    6883      7099  S               20  127381504   
pman.sh                 7332    4587      4586  S               14  4317184     
rotee                   7419       1      7418  S               20  8519680     
mcpcc-lc-ms             7489    7332      7489  S               20  127381504   
sntp                   13373       1     13373  S               20  3153920     
sleep                  14115    5155      5155  S               20  3272704     
lockd                  14127       2         0  S               15  0           
inotifywait            14224    5068     14224  S               20  2113536     
---- show platform software process list 0 summary  ----

Total number of processes: 71
  Running          : 2
  Sleeping         : 69
  Disk sleeping    : 0
  Zombies          : 0
  Stopped          : 0
  Paging           : 0

  Up time          : 4515850
  Idle time        : 136265
  User time        : 5272255
  Kernel time      : 2946570

  Virtual memory   : 596836352
  Pages resident   : 48711
  Major page faults: 41
  Minor page faults: 424393513

  Architecture     : ppc
  Memory (kB)
    Physical       : 524288
    Total          : 449776
    Used           : 377676
    Free           : 72100
    Active         : 157472
    Inactive       : 108768
    Inact-dirty    : 0
    Inact-clean    : 0
    Dirty          : 0
    AnonPages      : 82392
    Bounce         : 0
    Cached         : 173160
    Commit Limit   : 224888
    Committed As   : 313928
    High Total     : 0
    High Free      : 0
    Low Total      : 449776
    Low Free       : 72100
    Mapped         : 32248
    NFS Unstable   : 0
    Page Tables    : 1916
    Slab           : 93356
    VMmalloc Chunk : 456008
    VMmalloc Total : 503512
    VMmalloc Used  : 46408
    Writeback      : 0

  Swap (kB)
    Total          : 0
    Used           : 0
    Free           : 0
    Cached         : 0

  Buffers (kB)     : 10688

  Load Average
    1-Min          : 0.00
    5-Min          : 0.00
    15-Min         : 0.00
---- show platform software process list 1  ----

Name                     Pid    PPid  Group Id  Status    Priority  Size        
------------------------------------------------------------------------------
init                       1       0         1  S               20  2207744     
kthreadd                   2       0         0  S               15  0           
ksoftirqd/0                3       2         0  S               15  0           
watchdog/0                 4       2         0  S       4294967196  0           
events/0                   5       2         0  S               15  0           
khelper                    6       2         0  S               15  0           
netns                      9       2         0  S               15  0           
kblockd/0                 55       2         0  S               15  0           
ata/0                     62       2         0  S               15  0           
ata_aux                   63       2         0  S               15  0           
khubd                     69       2         0  S               15  0           
kseriod                   72       2         0  S               15  0           
pdflush                  117       2         0  S               20  0           
pdflush                  118       2         0  S               20  0           
kswapd0                  119       2         0  S               15  0           
aio/0                    171       2         0  S               15  0           
mtdblockd                878       2         0  S               15  0           
rpciod/0                1783       2         0  S               15  0           
nfsiod                  1789       2         0  S               15  0           
loop0                   1826       2         0  S                0  0           
portmap                 1871       1      1871  S               20  2297856     
loop1                   1910       2         0  S                0  0           
udevd                   2621       1      2621  S               16  2187264     
jffs2_gcd_mtd1          3507       2         0  S               30  0           
klogd                   3839       1      3839  S               20  1941504     
automount               3869       1      3869  S               20  40095744    
xinetd                  3887       1      3887  S               20  3567616     
xinetd                  3889       1      3889  S               20  3567616     
scansta                 4073       2         0  S               15  0           
loop2                   4082       2         0  S                0  0           
pvp.sh                  4587       1      4586  S               20  4407296     
rotee                   4634       1      4633  S               20  8515584     
inotifywait             4667    4587      4586  S               20  2117632     
pman.sh                 4727    4587      4586  S               14  4321280     
rotee                   4820       1      4819  S               20  8519680     
pman.sh                 4880    4587      4586  S               14  4325376     
agetty                  4884       1      4884  S               20  1933312     
mcp_chvrf.sh            4890       1      4890  S               20  3244032     
issu_switchover         4901       1      4901  S               20  5120000     
xinetd                  4903    4890      4890  S               20  3567616     
oom.sh                  4906       1      4906  S               20  3624960     
btrace_rotate.s         5047    4727      5047  S               20  4091904     
rotee                   5081       1      5080  S               20  8519680     
rotee                   5118       1      5117  S               20  8515584     
oom.sh                  5156    4906      5156  S               20  3735552     
rotee                   5178       1      5177  S               20  8515584     
pman.sh                 5181    4587      4586  S               14  4325376     
rotee                   5274       1      5273  S               20  8519680     
cmcc                    5344    4880      5344  S               20  32342016    
rotee                   5346       1      5345  S               20  8519680     
pman.sh                 5405    4587      4586  S               14  4325376     
emd                     5568    5181      5568  S               20  21008384    
rotee                   5570       1      5569  S               20  8519680     
pman.sh                 5635    4587      4586  S               14  4325376     
hman                    5770    5405      5770  R               20  17522688    
rotee                   5781       1      5780  S               20  8519680     
imccd                   5913    5635      5913  S               20  18984960    
pman.sh                 6059    4587      4586  S               14  4325376     
rotee                   6141       1      6140  S               20  8519680     
plogd                   6271    6059      6271  S               20  16822272    
inotifywait             6338    4901      4901  S               20  2113536     
pman.sh                 6887    4587      4586  S               14  4317184     
rotee                   6972       1      6971  S               20  8519680     
mcpcc-lc-ms             7043    6887      7043  S               20  127377408   
sntp                   11388       1     11388  S               20  3153920     
sleep                  23899    5156      5156  S               20  3272704     
inotifywait            24094    5047     24094  S               20  2113536     
---- show platform software process list 1 summary  ----

Total number of processes: 67
  Running          : 2
  Sleeping         : 65
  Disk sleeping    : 0
  Zombies          : 0
  Stopped          : 0
  Paging           : 0

  Up time          : 4515885
  Idle time        : 149943
  User time        : 2572519
  Kernel time      : 2679223

  Virtual memory   : 456388608
  Pages resident   : 36350
  Major page faults: 41
  Minor page faults: 405404241

  Architecture     : ppc
  Memory (kB)
    Physical       : 524288
    Total          : 449776
    Used           : 353116
    Free           : 96660
    Active         : 133376
    Inactive       : 108584
    Inact-dirty    : 0
    Inact-clean    : 0
    Dirty          : 0
    AnonPages      : 58352
    Bounce         : 0
    Cached         : 172920
    Commit Limit   : 224888
    Committed As   : 258572
    High Total     : 0
    High Free      : 0
    Low Total      : 449776
    Low Free       : 96660
    Mapped         : 32184
    NFS Unstable   : 0
    Page Tables    : 1632
    Slab           : 93016
    VMmalloc Chunk : 456008
    VMmalloc Total : 503512
    VMmalloc Used  : 46408
    Writeback      : 0

  Swap (kB)
    Total          : 0
    Used           : 0
    Free           : 0
    Cached         : 0

  Buffers (kB)     : 10688

  Load Average
    1-Min          : 0.00
    5-Min          : 0.00
    15-Min         : 0.00
---- show platform software process list 2  ----

This chassis cannot have a SPA-Inter-Processor at slot 2
---- show platform software process list 2 summary  ----

This chassis cannot have a SPA-Inter-Processor at slot 2
---- show platform software process list F0  ----

Name                     Pid    PPid  Group Id  Status    Priority  Size        
------------------------------------------------------------------------------
init                       1       0         1  S               20  2207744     
kthreadd                   2       0         0  S               15  0           
ksoftirqd/0                3       2         0  S               15  0           
watchdog/0                 4       2         0  S       4294967196  0           
events/0                   5       2         0  S               15  0           
khelper                    6       2         0  S               15  0           
netns                      9       2         0  S               15  0           
kblockd/0                 57       2         0  S               15  0           
ata/0                     64       2         0  S               15  0           
ata_aux                   65       2         0  S               15  0           
khubd                     71       2         0  S               15  0           
kseriod                   74       2         0  S               15  0           
pdflush                  119       2         0  S               20  0           
pdflush                  120       2         0  S               20  0           
kswapd0                  121       2         0  S               15  0           
aio/0                    173       2         0  S               15  0           
sleep                    709    5228      5228  S               20  3272704     
inotifywait              833    5191       833  S               20  2113536     
mtdblockd                880       2         0  S               15  0           
rpciod/0                1788       2         0  S               15  0           
nfsiod                  1794       2         0  S               15  0           
loop0                   1831       2         0  S                0  0           
portmap                 1876       1      1876  S               20  2297856     
loop1                   1915       2         0  S                0  0           
udevd                   2612       1      2612  S               16  2187264     
jffs2_gcd_mtd1          3501       2         0  S               30  0           
klogd                   3798       1      3798  S               20  1941504     
automount               3828       1      3828  S               20  40095744    
xinetd                  3846       1      3846  S               20  3567616     
xinetd                  3848       1      3848  S               20  3567616     
cavium                  4007       2         0  R               20  0           
scansta                 4059       2         0  S               15  0           
pvp.sh                  4667       1      4666  S               20  4386816     
rotee                   4714       1      4713  S               20  8515584     
inotifywait             4751    4667      4666  S               20  2117632     
pman.sh                 4809    4667      4666  S               14  4333568     
rotee                   4907       1      4906  S               20  8519680     
pman.sh                 4957    4667      4666  S               14  4333568     
agetty                  4959       1      4959  S               20  1933312     
mcp_chvrf.sh            4964       1      4964  S               20  3244032     
issu_switchover         4974       1      4974  S               20  5120000     
xinetd                  4976    4964      4964  S               20  3567616     
oom.sh                  4980       1      4980  S               20  3624960     
rotee                   5142       1      5141  S               20  8519680     
rotee                   5190       1      5189  S               20  8515584     
btrace_rotate.s         5191    4809      5191  S               20  4489216     
oom.sh                  5228    4980      5228  S               20  4128768     
rotee                   5248       1      5247  S               20  8515584     
pman.sh                 5249    4667      4666  S               14  4333568     
rotee                   5397       1      5396  S               20  8519680     
rotee                   5424       1      5423  S               20  8519680     
cman_fp                 5443    4957      5443  R               20  399437824   
pman.sh                 5484    4667      4666  S               14  4333568     
rotee                   5647       1      5646  S               20  8519680     
cpp_cdm_svr             5676    5249      5676  S               20  390160384   
pman.sh                 5725    4667      4666  S               14  4333568     
rotee                   5876       1      5875  S               20  8519680     
cpp_cp_svr              5882    5484      5882  S               20  646115328   
pman.sh                 5921    4667      4666  S               14  4333568     
inotifywait             5942    4974      4974  S               20  2113536     
rotee                   6053       1      6052  S               20  8519680     
cpp_driver              6083    5725      6083  S               20  720818176   
pman.sh                 6106    4667      4666  S               14  4333568     
rotee                   6238       1      6237  S               20  8519680     
cpp_ha_top_leve         6253    5921      6253  S               20  396304384   
pman.sh                 6287    4667      4666  S               14  4333568     
rotee                   6420       1      6419  S               20  8519680     
cpp_sp_svr              6441    6106      6441  S               20  421265408   
pman.sh                 6469    4667      4666  S               14  4333568     
rotee                   6605       1      6604  S               20  8519680     
emd                     6625    6287      6625  S               20  21172224    
pman.sh                 6649    4667      4666  S               14  4333568     
rotee                   6783       1      6782  S               20  8519680     
fman_fp_image           6802    6469      6802  R               20  750284800   
pman.sh                 6832    4667      4666  S               14  4333568     
rotee                   6963       1      6962  S               20  8519680     
hman                    6992    6649      6992  R               20  17518592    
plogd                   7117    6832      7117  S               20  16822272    
sntp                   15441       1     15441  S               20  3153920     
---- show platform software process list F0 summary  ----

Total number of processes: 79
  Running          : 2
  Sleeping         : 77
  Disk sleeping    : 0
  Zombies          : 0
  Stopped          : 0
  Paging           : 0

  Up time          : 4515882
  Idle time        : 126870
  User time        : 2491080
  Kernel time      : 3566034

  Virtual memory   : 4054482944
  Pages resident   : 135547
  Major page faults: 702
  Minor page faults: 457923964

  Architecture     : ppc
  Memory (kB)
    Physical       : 2097152
    Total          : 2009900
    Used           : 829336
    Free           : 1180564
    Active         : 472416
    Inactive       : 180260
    Inact-dirty    : 0
    Inact-clean    : 0
    Dirty          : 0
    AnonPages      : 383832
    Bounce         : 0
    Cached         : 240756
    Commit Limit   : 1004948
    Committed As   : 3124932
    High Total     : 1310720
    High Free      : 669724
    Low Total      : 699180
    Low Free       : 510840
    Mapped         : 69580
    NFS Unstable   : 0
    Page Tables    : 4176
    Slab           : 70432
    VMmalloc Chunk : 201776
    VMmalloc Total : 240328
    VMmalloc Used  : 38100
    Writeback      : 0

  Swap (kB)
    Total          : 0
    Used           : 0
    Free           : 0
    Cached         : 0

  Buffers (kB)     : 28088

  Load Average
    1-Min          : 0.00
    5-Min          : 0.00
    15-Min         : 0.00
---- show platform software process list F1  ----

This chassis cannot have an Embedded-Service-Processor at slot 1
---- show platform software process list F1 summary  ----

This chassis cannot have an Embedded-Service-Processor at slot 1
---- show platform software process list R0  ----

Name                     Pid    PPid  Group Id  Status    Priority  Size        
------------------------------------------------------------------------------
init                       1       0         1  S               20  2207744     
kthreadd                   2       0         0  S               15  0           
ksoftirqd/0                3       2         0  S               15  0           
watchdog/0                 4       2         0  S       4294967196  0           
events/0                   5       2         0  S               15  0           
khelper                    6       2         0  S               15  0           
netns                      9       2         0  S               15  0           
kblockd/0                 62       2         0  S               15  0           
ata/0                     69       2         0  S               15  0           
ata_aux                   70       2         0  S               15  0           
khubd                     76       2         0  S               15  0           
kseriod                   79       2         0  S               15  0           
pdflush                  124       2         0  S               20  0           
pdflush                  125       2         0  S               20  0           
kswapd0                  126       2         0  S               15  0           
aio/0                    178       2         0  S               15  0           
rotee                    387       1       386  S               20  8515584     
rotee                    400       1       399  S               20  8515584     
rotee                    420       1       419  S               20  8515584     
rotee                    424       1       423  S               20  8515584     
oom.sh                   441   32654       441  S               20  4636672     
inotifywait              445   32648       445  S               20  2113536     
inotifywait              459   32660       459  S               20  2113536     
mtdblockd               1011       2         0  S               15  0           
scsi_eh_0               1077       2         0  S               15  0           
usb-storage             1078       2         0  S               15  0           
scsi_eh_1               1092       2         0  S               15  0           
scsi_eh_2               1093       2         0  S               15  0           
scsi_eh_3               1094       2         0  S               15  0           
scsi_eh_4               1095       2         0  S               15  0           
mcp-rtc-wq              1112       2         0  S               15  0           
rpciod/0                2218       2         0  S               15  0           
nfsiod                  2224       2         0  S               15  0           
loop0                   2263       2         0  S                0  0           
portmap                 2386       1      2386  S               20  2297856     
loop1                   2440       2         0  S                0  0           
loop2                   2477       2         0  S                0  0           
loop3                   2514       2         0  S                0  0           
loop4                   2551       2         0  S                0  0           
loop5                   2660       2         0  S                0  0           
loop6                   2697       2         0  S                0  0           
loop7                   2770       2         0  S                0  0           
sleep                  10881   26557     26557  S               20  3272704     
sleep                  11282     441       441  S               20  3272704     
bexec.sh               11444   24425     24425  S               20  3289088     
mcp_chvrf.sh           11448   11444     24425  S               20  3256320     
mcp_tech_suppor        11449   11448     24425  S               20  3358720     
bshell.sh              11460   11449     24425  S               20  4030464     
bshell                 11589   11460     11589  S               20  13393920    
udevd                  12641       1     12641  S               16  2187264     
jffs2_gcd_mtd1         13825       2         0  S               30  0           
auxport.sh             14191       1     14191  S               20  3231744     
reflector.sh           14212       1     14212  S               20  4476928     
droputil.sh            14218       1     14218  S               20  4489216     
automount              14313       1     14313  S               20  27344896    
sleep                  14326   28706     28706  S               20  3272704     
sleep                  14330   32657     14330  S               20  3272704     
xinetd                 14345       1     14345  S               20  3567616     
xinetd                 14347       1     14347  S               20  3567616     
lockd                  14366       2         0  S               15  0           
nfsd                   14368       2         0  S               15  0           
nfsd                   14369       2         0  S               15  0           
nfsd                   14370       2         0  S               15  0           
nfsd                   14371       2         0  S               15  0           
nfsd                   14372       2         0  S               15  0           
nfsd                   14373       2         0  S               15  0           
nfsd                   14374       2         0  S               15  0           
nfsd                   14375       2         0  S               15  0           
rpc.mountd             14378       1     14378  S               20  2363392     
btrace_rotate.s        14423   22445     22445  R               20  5025792     
ls                     14424   14423     22445  Z               20  0           
lsmpi-refill           14466       2         0  S               15  0           
lsmpi-xmit             14467       2         0  S               15  0           
lsmpi-rx               14468       2         0  R               15  0           
rotee                  15327       1     15326  S               20  8515584     
rotee                  15329       1     15328  S               20  8515584     
inotifywait            15390   14218     15390  S               20  2117632     
inotifywait            15399   14212     15399  S               20  2117632     
klogd                  21345       1     21345  S               20  1941504     
pvp.sh                 21356       1     21355  S               20  4419584     
rotee                  21403       1     21402  S               20  8515584     
inotifywait            21521   21356     21355  S               20  2117632     
pman.sh                21589   21356     21355  S               14  4358144     
rotee                  21674       1     21673  S               20  8519680     
pman.sh                21730   21356     21355  S               14  4341760     
rotee                  21876       1     21875  S               20  8519680     
pman.sh                21987   21356     21355  S               14  4341760     
rotee                  22173       1     22172  S               20  8519680     
pman.sh                22330   21356     21355  S               14  4345856     
btrace_rotate.s        22445   21589     22445  R               20  5025792     
rotee                  22566       1     22565  S               20  8519680     
rotee                  22724       1     22723  S               20  8519680     
cmand                  22776   21730     22776  S               20  28893184    
pman.sh                22877   21356     21355  S               14  4341760     
emd                    23140   21987     23140  S               20  20819968    
rotee                  23185       1     23184  S               20  8519680     
pman.sh                23404   21356     21355  S               14  4341760     
fman_rp                23659   22330     23659  S               20  338321408   
rotee                  23697       1     23696  S               20  8519680     
pman.sh                24315   21356     21355  S               14  4345856     
hman                   24425   22877     24425  R               20  17723392    
rotee                  24589       1     24588  S               20  8519680     
imand                  24882   23404     24882  S               20  28155904    
pman.sh                25021   21356     21355  S               14  4358144     
rotee                  25298       1     25297  S               20  8519680     
pman.sh                25467   21356     21355  S               14  4345856     
linux_iosd-imag        25737   24315     25737  R               20  1999187968  
rotee                  25757       1     25756  S               20  8519680     
pman.sh                25947   21356     21355  S               14  4345856     
rotee                  26215       1     26214  S               20  8519680     
sleep                  26544   14191     14191  S               20  3272704     
periodic.sh            26557   25021     26557  S               20  4984832     
pman.sh                26752   21356     21355  S               14  4349952     
rotee                  26901       1     26900  S               20  8519680     
plogd                  27079   25467     27079  S               20  17350656    
rotee                  27132       1     27131  S               20  8519680     
pman.sh                27358   21356     21355  S               14  4358144     
psd                    27614   25947     27614  S               20  21151744    
rotee                  27660       1     27659  S               20  8519680     
smand                  28347   26752     28347  R               20  100012032   
sort_files_by_i        28706   27358     28706  S               20  4308992     
mcp_chvrf.sh           32641       1     32641  S               20  3244032     
mcp_chvrf.sh           32643       1     32643  S               20  3244032     
xinetd                 32645   32641     32641  S               20  3567616     
sntp                   32646       1     32646  S               20  3149824     
xinetd                 32647   32643     32643  S               20  3567616     
rollback_timer.        32648       1     32648  S               20  3657728     
oom.sh                 32654       1     32654  S               20  3624960     
chasync.sh             32657       1     32657  S               20  5099520     
iptbl.sh               32660       1     32660  S               20  4026368     
---- show platform software process list R0 summary  ----

Total number of processes: 130
  Running          : 5
  Sleeping         : 124
  Disk sleeping    : 0
  Zombies          : 1
  Stopped          : 0
  Paging           : 0

  Up time          : 4515993
  Idle time        : 4220787
  User time        : 35258463
  Kernel time      : 7717167

  Virtual memory   : 2976378880
  Pages resident   : 357067
  Major page faults: 1788
  Minor page faults: 1002644076

  Architecture     : ppc
  Memory (kB)
    Physical       : 4127744
    Total          : 3874976
    Used           : 2303232
    Free           : 1571744
    Active         : 1312216
    Inactive       : 896360
    Inact-dirty    : 0
    Inact-clean    : 0
    Dirty          : 20
    AnonPages      : 887516
    Bounce         : 0
    Cached         : 1214740
    Commit Limit   : 1937488
    Committed As   : 2796208
    High Total     : 3191740
    High Free      : 1082024
    Low Total      : 683236
    Low Free       : 489720
    Mapped         : 428936
    NFS Unstable   : 0
    Page Tables    : 5352
    Slab           : 63880
    VMmalloc Chunk : 207172
    VMmalloc Total : 233160
    VMmalloc Used  : 25308
    Writeback      : 0

  Swap (kB)
    Total          : 0
    Used           : 0
    Free           : 0
    Cached         : 0

  Buffers (kB)     : 106320

  Load Average
    1-Min          : 1.88
    5-Min          : 0.63
    15-Min         : 0.27
---- show platform software process list R1  ----

This chassis cannot have a Route-Processor at slot 1
---- show platform software process list R1 summary  ----

This chassis cannot have a Route-Processor at slot 1
---- request platform software trace rotate all ----




------------------ show interfaces ------------------


GigabitEthernet0/0/0 is administratively down, line protocol is down 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6c00 (bia b414.8901.6c00)
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is unknown media type
  output flow-control is unsupported, input flow-control is unsupported
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 1 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0/0/1 is up, line protocol is up 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6c01 (bia b414.8901.6c01)
  Description: CTD-S6 Gi2/18 RETN-3kanal
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is LX
  output flow-control is on, input flow-control is on
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 00:00:21, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     9121353 packets input, 777968511 bytes, 0 no buffer
     Received 455171 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 714759 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 2 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0/0/2 is down, line protocol is down 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6cc2 (bia b414.8901.6c02)
  Description: CTD-S6 Gi2/9 (Po3) INET
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is SX
  output flow-control is on, input flow-control is on
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 2 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0/0/3 is down, line protocol is down 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6cc2 (bia b414.8901.6c03)
  Description: CTD-S6 Gi2/13 (Po3) INET
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is LX
  output flow-control is on, input flow-control is on
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 2 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0/0/4 is down, line protocol is down 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6cc2 (bia b414.8901.6c04)
  Description: CTD-S6 Gi2/15 (Po3) INET
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is LX
  output flow-control is on, input flow-control is on
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 2 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0/0/5 is administratively down, line protocol is down 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6c05 (bia b414.8901.6c05)
  Description: #RETN-INTERNET1 Uplink
  Internet address is 87.245.241.134/30
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is unknown media type
  output flow-control is unsupported, input flow-control is unsupported
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 1 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0/0/6 is administratively down, line protocol is down 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6c06 (bia b414.8901.6c06)
  Description: #CTD-S6 Gi2/17 RETN-INET-2kanal
  Internet address is 87.245.241.146/30
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is unknown media type
  output flow-control is unsupported, input flow-control is unsupported
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 1 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0/0/7 is down, line protocol is down 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6c07 (bia b414.8901.6c07)
  Description: #BEELINE-INTERNET Uplink
  Internet address is 87.229.223.118/30
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is BX10U
  output flow-control is on, input flow-control is on
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 2 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
TenGigabitEthernet0/3/0 is up, line protocol is up 
  Hardware is SPA-1X10GE-L-V2, address is b414.8901.6c30 (bia b414.8901.6c30)
  Description: #to Catalyst4900
  MTU 1500 bytes, BW 10000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 48/255, rxload 26/255
  Encapsulation 802.1Q Virtual LAN, Vlan ID  1., loopback not set
  Keepalive not supported 
  Full Duplex, 10000Mbps, link type is force-up, media type is 10GBase-LR
  output flow-control is on, input flow-control is on
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 00:00:03, output 00:00:03, output hang never
  Last clearing of "show interface" counters 01:13:42
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 1022046000 bits/sec, 239929 packets/sec
  30 second output rate 1910080000 bits/sec, 256116 packets/sec
     1003582170 packets input, 546590534844 bytes, 0 no buffer
     Received 73 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     6090 input errors, 5797 CRC, 291 frame, 0 overrun, 0 ignored
     0 watchdog, 4624 multicast, 0 pause input
     1056630239 packets output, 973245448785 bytes, 0 underruns
     0 output errors, 0 collisions, 0 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
TenGigabitEthernet0/3/0.13 is up, line protocol is up 
  Hardware is SPA-1X10GE-L-V2, address is b414.8901.6c30 (bia b414.8901.6c30)
  Description: #OSPF-link
  Internet address is 81.20.192.52/28
  MTU 1500 bytes, BW 10000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 48/255, rxload 26/255
  Encapsulation 802.1Q Virtual LAN, Vlan ID  13.
  ARP type: ARPA, ARP Timeout 04:00:00
  Keepalive not supported 
  Last clearing of "show interface" counters never
TenGigabitEthernet0/3/0.1042 is administratively down, line protocol is down 
  Hardware is SPA-1X10GE-L-V2, address is b414.8901.6c30 (bia b414.8901.6c30)
  Description: #Bigtelecom
  Internet address is 81.20.192.149/30
  MTU 1500 bytes, BW 307200 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 48/255, rxload 26/255
  Encapsulation 802.1Q Virtual LAN, Vlan ID  1042.
  ARP type: ARPA, ARP Timeout 04:00:00
  Keepalive not supported 
  Last clearing of "show interface" counters never
TenGigabitEthernet1/3/0 is up, line protocol is up 
  Hardware is SPA-1X10GE-L-V2, address is b414.8901.6c70 (bia b414.8901.6c70)
  Description: #Megafon
  Internet address is 78.25.66.222/30
  MTU 1500 bytes, BW 10000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 25/255, rxload 48/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 10000Mbps, link type is force-up, media type is 10GBase-ER
  output flow-control is on, input flow-control is on
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 00:10:53, output 00:10:53, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 1903005000 bits/sec, 256125 packets/sec
  30 second output rate 1013127000 bits/sec, 239918 packets/sec
     942583062453 packets input, 946778176537588 bytes, 0 no buffer
     Received 3753 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     11 input errors, 0 CRC, 11 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     756714097653 packets output, 417254438868269 bytes, 0 underruns
     0 output errors, 0 collisions, 2 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0 is up, line protocol is up 
  Hardware is RP management port, address is b414.8901.6c80 (bia b414.8901.6c80)
  Description: #mngt27 to CTD-S0 Fa0/8
  Internet address is 192.168.121.31/24
  MTU 1500 bytes, BW 100000 Kbit/sec, DLY 100 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive set (10 sec)
  Full Duplex, 100Mbps, link type is auto, media type is RJ45
  output flow-control is unsupported, input flow-control is unsupported
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 00:00:25, output 00:00:10, output hang never
  Last clearing of "show interface" counters 1w6d
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     430102 packets input, 59594636 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     325197 packets output, 59942667 bytes, 0 underruns
     0 output errors, 0 collisions, 0 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
Loopback0 is up, line protocol is up 
  Hardware is Loopback
  Description: # Interface for Tunnel endpoint, IP/MPLS and BGP exchanges
  Internet address is 81.20.192.75/32
  MTU 1514 bytes, BW 8000000 Kbit/sec, DLY 5000 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation LOOPBACK, loopback not set
  Keepalive set (10 sec)
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/0 (size/max)
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 0 interface resets
     0 unknown protocol drops
     0 output buffer failures, 0 output buffers swapped out
Port-channel3 is administratively down, line protocol is down 
  Hardware is GEChannel, address is b414.8901.6cc2 (bia b414.8901.6cc2)
  Description: #CTD-S6 Po3 802.1q INET
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation 802.1Q Virtual LAN, Vlan ID  1., loopback not set
  Keepalive set (10 sec)
  ARP type: ARPA, ARP Timeout 04:00:00
    No. of active members in this channel: 0 
    No. of PF_JUMBO supported members in this channel : 3
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/0/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/0 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 0 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
Port-channel3.13 is administratively down, line protocol is down 
  Hardware is GEChannel, address is b414.8901.6cc2 (bia b414.8901.6cc2)
  Description: OSPF-link 120 #pheonix 20.05.2011
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation 802.1Q Virtual LAN, Vlan ID  13.
  ARP type: ARPA, ARP Timeout 04:00:00
  Keepalive set (10 sec)
  Last clearing of "show interface" counters never

------------------ show interfaces ------------------


GigabitEthernet0/0/0 is administratively down, line protocol is down 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6c00 (bia b414.8901.6c00)
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is unknown media type
  output flow-control is unsupported, input flow-control is unsupported
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 1 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0/0/1 is up, line protocol is up 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6c01 (bia b414.8901.6c01)
  Description: CTD-S6 Gi2/18 RETN-3kanal
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is LX
  output flow-control is on, input flow-control is on
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 00:00:24, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     9121353 packets input, 777968511 bytes, 0 no buffer
     Received 455171 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 714759 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 2 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0/0/2 is down, line protocol is down 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6cc2 (bia b414.8901.6c02)
  Description: CTD-S6 Gi2/9 (Po3) INET
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is SX
  output flow-control is on, input flow-control is on
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 2 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0/0/3 is down, line protocol is down 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6cc2 (bia b414.8901.6c03)
  Description: CTD-S6 Gi2/13 (Po3) INET
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is LX
  output flow-control is on, input flow-control is on
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 2 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0/0/4 is down, line protocol is down 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6cc2 (bia b414.8901.6c04)
  Description: CTD-S6 Gi2/15 (Po3) INET
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is LX
  output flow-control is on, input flow-control is on
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 2 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0/0/5 is administratively down, line protocol is down 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6c05 (bia b414.8901.6c05)
  Description: #RETN-INTERNET1 Uplink
  Internet address is 87.245.241.134/30
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is unknown media type
  output flow-control is unsupported, input flow-control is unsupported
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 1 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0/0/6 is administratively down, line protocol is down 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6c06 (bia b414.8901.6c06)
  Description: #CTD-S6 Gi2/17 RETN-INET-2kanal
  Internet address is 87.245.241.146/30
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is unknown media type
  output flow-control is unsupported, input flow-control is unsupported
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 1 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0/0/7 is down, line protocol is down 
  Hardware is SPA-8X1GE-V2, address is b414.8901.6c07 (bia b414.8901.6c07)
  Description: #BEELINE-INTERNET Uplink
  Internet address is 87.229.223.118/30
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 1000Mbps, link type is auto, media type is BX10U
  output flow-control is on, input flow-control is on
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 2 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
TenGigabitEthernet0/3/0 is up, line protocol is up 
  Hardware is SPA-1X10GE-L-V2, address is b414.8901.6c30 (bia b414.8901.6c30)
  Description: #to Catalyst4900
  MTU 1500 bytes, BW 10000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 48/255, rxload 26/255
  Encapsulation 802.1Q Virtual LAN, Vlan ID  1., loopback not set
  Keepalive not supported 
  Full Duplex, 10000Mbps, link type is force-up, media type is 10GBase-LR
  output flow-control is on, input flow-control is on
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 00:00:06, output 00:00:06, output hang never
  Last clearing of "show interface" counters 01:13:45
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 1022046000 bits/sec, 239929 packets/sec
  30 second output rate 1910080000 bits/sec, 256116 packets/sec
     1003582170 packets input, 546590534844 bytes, 0 no buffer
     Received 73 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     6090 input errors, 5797 CRC, 291 frame, 0 overrun, 0 ignored
     0 watchdog, 4624 multicast, 0 pause input
     1056630239 packets output, 973245448785 bytes, 0 underruns
     0 output errors, 0 collisions, 0 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
TenGigabitEthernet0/3/0.13 is up, line protocol is up 
  Hardware is SPA-1X10GE-L-V2, address is b414.8901.6c30 (bia b414.8901.6c30)
  Description: #OSPF-link
  Internet address is 81.20.192.52/28
  MTU 1500 bytes, BW 10000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 48/255, rxload 26/255
  Encapsulation 802.1Q Virtual LAN, Vlan ID  13.
  ARP type: ARPA, ARP Timeout 04:00:00
  Keepalive not supported 
  Last clearing of "show interface" counters never
TenGigabitEthernet0/3/0.1042 is administratively down, line protocol is down 
  Hardware is SPA-1X10GE-L-V2, address is b414.8901.6c30 (bia b414.8901.6c30)
  Description: #Bigtelecom
  Internet address is 81.20.192.149/30
  MTU 1500 bytes, BW 307200 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 48/255, rxload 26/255
  Encapsulation 802.1Q Virtual LAN, Vlan ID  1042.
  ARP type: ARPA, ARP Timeout 04:00:00
  Keepalive not supported 
  Last clearing of "show interface" counters never
TenGigabitEthernet1/3/0 is up, line protocol is up 
  Hardware is SPA-1X10GE-L-V2, address is b414.8901.6c70 (bia b414.8901.6c70)
  Description: #Megafon
  Internet address is 78.25.66.222/30
  MTU 1500 bytes, BW 10000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 25/255, rxload 48/255
  Encapsulation ARPA, loopback not set
  Keepalive not supported 
  Full Duplex, 10000Mbps, link type is force-up, media type is 10GBase-ER
  output flow-control is on, input flow-control is on
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 00:10:56, output 00:10:56, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/375/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 1903005000 bits/sec, 256125 packets/sec
  30 second output rate 1013127000 bits/sec, 239918 packets/sec
     942583062453 packets input, 946778176537588 bytes, 0 no buffer
     Received 3753 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     11 input errors, 0 CRC, 11 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     756714097653 packets output, 417254438868269 bytes, 0 underruns
     0 output errors, 0 collisions, 2 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
GigabitEthernet0 is up, line protocol is up 
  Hardware is RP management port, address is b414.8901.6c80 (bia b414.8901.6c80)
  Description: #mngt27 to CTD-S0 Fa0/8
  Internet address is 192.168.121.31/24
  MTU 1500 bytes, BW 100000 Kbit/sec, DLY 100 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive set (10 sec)
  Full Duplex, 100Mbps, link type is auto, media type is RJ45
  output flow-control is unsupported, input flow-control is unsupported
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 00:00:28, output 00:00:13, output hang never
  Last clearing of "show interface" counters 1w6d
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     430102 packets input, 59594636 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     325197 packets output, 59942667 bytes, 0 underruns
     0 output errors, 0 collisions, 0 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
Loopback0 is up, line protocol is up 
  Hardware is Loopback
  Description: # Interface for Tunnel endpoint, IP/MPLS and BGP exchanges
  Internet address is 81.20.192.75/32
  MTU 1514 bytes, BW 8000000 Kbit/sec, DLY 5000 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation LOOPBACK, loopback not set
  Keepalive set (10 sec)
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/0 (size/max)
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 0 interface resets
     0 unknown protocol drops
     0 output buffer failures, 0 output buffers swapped out
Port-channel3 is administratively down, line protocol is down 
  Hardware is GEChannel, address is b414.8901.6cc2 (bia b414.8901.6cc2)
  Description: #CTD-S6 Po3 802.1q INET
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation 802.1Q Virtual LAN, Vlan ID  1., loopback not set
  Keepalive set (10 sec)
  ARP type: ARPA, ARP Timeout 04:00:00
    No. of active members in this channel: 0 
    No. of PF_JUMBO supported members in this channel : 3
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/0/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/0 (size/max)
  30 second input rate 0 bits/sec, 0 packets/sec
  30 second output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     0 packets output, 0 bytes, 0 underruns
     0 output errors, 0 collisions, 0 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out
Port-channel3.13 is administratively down, line protocol is down 
  Hardware is GEChannel, address is b414.8901.6cc2 (bia b414.8901.6cc2)
  Description: OSPF-link 120 #pheonix 20.05.2011
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation 802.1Q Virtual LAN, Vlan ID  13.
  ARP type: ARPA, ARP Timeout 04:00:00
  Keepalive set (10 sec)
  Last clearing of "show interface" counters never

------------------ show environment all ------------------


Sensor List:  Environmental Monitoring 
 Sensor           Location          State             Reading
 V1: VMA          1                 Normal            1098 mV
 V1: VMB          1                 Normal            1196 mV
 V1: VMC          1                 Normal            1499 mV
 V1: VMD          1                 Normal            1796 mV
 V1: VME          1                 Normal            2495 mV
 V1: VMF          1                 Normal            3295 mV
 V1: 12v          1                 Normal            11909 mV
 V1: VDD          1                 Normal            3286 mV
 V1: GP1          1                 Normal            747 mV
 V1: GP2          1                 Normal            900 mV
 V2: VMB          1                 Normal            1196 mV
 V2: 12v          1                 Normal            11909 mV
 V2: VDD          1                 Normal            3291 mV
 V2: GP2          1                 Normal            903 mV
 Temp: Left       1                 Normal            24 Celsius
 Temp: Center     1                 Normal            26 Celsius
 Temp: Asic1      1                 Normal            40 Celsius
 Temp: Right      1                 Normal            24 Celsius
 V1: VMA          F0                Normal            1796 mV
 V1: VMB          F0                Normal            1196 mV
 V1: VMC          F0                Normal            1201 mV
 V1: VMD          F0                Normal            1098 mV
 V1: VME          F0                Normal            996 mV
 V1: 12v          F0                Normal            11879 mV
 V1: VDD          F0                Normal            3286 mV
 V1: GP1          F0                Normal            900 mV
 V2: VMA          F0                Normal            3291 mV
 V2: VMB          F0                Normal            2495 mV
 V2: VMC          F0                Normal            1499 mV
 V2: VMD          F0                Normal            1098 mV
 V2: VME          F0                Normal            996 mV
 V2: VMF          F0                Normal            1000 mV
 V2: 12v          F0                Normal            11850 mV
 V2: VDD          F0                Normal            3286 mV
 V2: GP1          F0                Normal            749 mV
 Temp: Inlet      F0                Normal            24 Celsius
 Temp: Asic1      F0                Normal            33 Celsius
 Temp: Exhaust1   F0                Normal            31 Celsius
 Temp: Exhaust2   F0                Normal            31 Celsius
 Temp: Asic2      F0                Normal            29 Celsius
 V1: VMA          0                 Normal            1098 mV
 V1: VMB          0                 Normal            1196 mV
 V1: VMC          0                 Normal            1499 mV
 V1: VMD          0                 Normal            1796 mV
 V1: VME          0                 Normal            2490 mV
 V1: VMF          0                 Normal            3291 mV
 V1: 12v          0                 Normal            11894 mV
 V1: VDD          0                 Normal            3286 mV
 V1: GP1          0                 Normal            751 mV
 V1: GP2          0                 Normal            900 mV
 V2: VMB          0                 Normal            1201 mV
 V2: 12v          0                 Normal            11894 mV
 V2: VDD          0                 Normal            3281 mV
 V2: GP2          0                 Normal            900 mV
 Temp: Left       0                 Normal            23 Celsius
 Temp: Center     0                 Normal            25 Celsius
 Temp: Asic1      0                 Normal            34 Celsius
 Temp: Right      0                 Normal            23 Celsius
 PEM Iout         P0                Normal            21 A
 PEM Vout         P0                Normal            12 V AC
 PEM Vin          P0                Normal            206 V AC
 Temp: PEM        P0                Normal            31 Celsius
 Temp: FC         P0                Fan Speed 65%     18 Celsius
 PEM Iout         P1                Normal            1 A
 PEM Vout         P1                Normal            0 V AC
 PEM Vin          P1                Normal            223 V AC
 Temp: PEM        P1                Normal            25 Celsius
 Temp: FC         P1                Fan Speed 65%     18 Celsius
 V1: VMA          R0                Normal            1108 mV
 V1: VMB          R0                Normal            3315 mV
 V1: VMC          R0                Normal            2514 mV
 V1: VMD          R0                Normal            1806 mV
 V1: VME          R0                Normal            1508 mV
 V1: VMF          R0                Normal            1210 mV
 V1: 12v          R0                Normal            11938 mV
 V1: VDD          R0                Normal            3271 mV
 V1: GP1          R0                Normal            908 mV
 V1: GP2          R0                Normal            1267 mV
 Temp: CPU        R0                Normal            25 Celsius
 Temp: Outlet     R0                Normal            24 Celsius
 Temp: Inlet      R0                Normal            18 Celsius
 Temp: Asic1      R0                Normal            25 Celsius



------------------ show logging ------------------


Syslog logging: enabled (0 messages dropped, 14 messages rate-limited, 0 flushes, 0 overruns, xml disabled, filtering disabled)

No Active Message Discriminator.



No Inactive Message Discriminator.


    Console logging: level debugging, 4792 messages logged, xml disabled,
                     filtering disabled
    Monitor logging: level debugging, 0 messages logged, xml disabled,
                     filtering disabled
    Buffer logging:  level debugging, 4805 messages logged, xml disabled,
                    filtering disabled
    Exception Logging: size (4096 bytes)
    Count and timestamp logging messages: disabled
    Persistent logging: disabled

No active filter modules.

    Trap logging: level notifications, 4762 message lines logged
        Logging to 192.168.121.26  (udp port 514, audit disabled,
              link up),
              25 message lines logged, 
              0 message lines rate-limited, 
              0 message lines dropped-by-MD, 
              xml disabled, sequence number disabled
              filtering disabled
        Logging to 81.20.196.53  (udp port 514, audit disabled,
              link up),
              15 message lines logged, 
              0 message lines rate-limited, 
              0 message lines dropped-by-MD, 
              xml disabled, sequence number disabled
              filtering disabled

Log Buffer (32768 bytes):
logy base removed from session  Peer closed the session
Sep  3 18:25:56: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:26:05: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:26:12: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:26:25: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:26:35: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:26:44: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:26:50: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:27:01: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:27:11: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:27:20: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:27:30: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:27:44: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:27:53: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:28:06: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:28:15: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:28:23: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:28:31: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:28:44: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:28:51: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:28:59: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:29:11: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:29:24: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:29:36: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:29:49: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:30:01: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:30:11: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:30:24: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:30:31: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:30:37: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:30:50: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:30:57: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:31:06: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:31:20: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:31:31: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:31:38: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:31:51: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:32:03: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:32:11: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:32:26: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:32:32: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:32:41: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:32:52: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:33:05: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:33:15: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:33:22: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:33:30: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:33:39: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:33:47: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:33:58: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:34:09: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:34:18: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:34:30: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:34:42: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:34:52: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:35:02: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:35:12: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:35:25: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:35:33: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:35:42: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:35:49: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:35:59: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:36:09: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:36:21: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:36:32: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:36:46: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:36:57: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:37:10: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:37:21: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:37:32: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:37:45: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:37:56: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:38:06: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:38:16: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:38:26: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:38:33: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:38:40: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:38:48: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:38:59: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:39:12: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:39:22: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:39:35: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:39:45: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:39:58: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:40:07: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:40:17: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:40:25: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:40:33: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:40:42: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:40:52: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:40:59: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:41:12: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:41:24: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:41:32: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:41:42: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:41:49: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:42:00: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:42:07: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:42:15: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:42:21: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:42:32: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:42:45: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:42:56: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:43:03: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:43:14: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:43:26: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:43:36: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:43:45: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:43:57: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:44:06: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:44:14: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:44:20: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:44:26: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:44:40: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:44:48: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:45:00: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:45:11: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:45:21: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:45:34: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:45:43: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:45:54: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:46:08: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:46:21: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:46:32: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:46:41: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:46:49: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:46:59: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:47:12: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:47:24: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:47:39: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:47:45: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:47:55: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:48:06: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:48:18: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:48:31: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:48:41: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:48:53: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:49:00: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:49:08: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:49:21: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:49:34: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:49:47: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:49:57: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:50:04: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:50:13: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:50:27: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:50:39: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:50:53: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:51:02: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:51:12: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:51:20: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:51:29: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:51:42: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:51:52: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:52:00: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:52:11: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:52:20: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:52:32: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:52:39: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:52:53: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:53:06: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:53:16: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:53:28: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:53:35: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:53:42: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:53:50: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:54:01: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:54:10: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:54:22: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:54:28: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:54:39: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:54:51: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:54:59: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:55:09: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:55:19: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:55:27: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:55:38: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:55:51: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:56:01: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:56:12: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:56:25: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:56:34: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:56:47: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:56:54: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:57:01: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:57:08: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:57:22: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:57:34: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:57:46: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:57:54: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:58:05: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:58:18: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:58:31: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:58:43: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:58:55: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:59:01: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:59:08: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:59:21: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:59:29: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:59:37: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 18:59:51: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 19:00:03: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 19:00:13: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 19:00:19: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 19:00:31: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 19:00:39: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep  3 19:00:46: %BGP_SESSION-5-ADJCHANGE: neighbor 81.20.192.150 IPv4 Unicast topology base removed from session  Peer closed the session
Sep 12 16:10:35: %SYS-5-CONFIG_I: Configured from console by garry on vty0 (81.20.192.32)
Sep 13 00:45:54: %SYS-6-EXEC_EXPIRE_TIMER: (tty 2 (81.20.192.32)) exec-timeout timer expired for user garry
Sep 16 14:16:57: %SYS-6-LOGGINGHOST_STARTSTOP: Logging to host 192.168.121.17 port 514 stopped - CLI initiated
Sep 16 14:17:08: %SYS-5-CONFIG_I: Configured from console by garry on vty0 (81.20.192.32)
Sep 16 14:17:09: %SYS-6-LOGGINGHOST_STARTSTOP: Logging to host 192.168.121.26 port 514 started - CLI initiated
Sep 17 01:15:30: %SYS-6-EXEC_EXPIRE_TIMER: (tty 2 (81.20.192.32)) exec-timeout timer expired for user garry
Sep 17 04:01:01: %SYS-4-SNMP_WRITENET: SNMP WriteNet request. Writing current configuration to 192.168.121.1
Sep 18 04:01:01: %SYS-4-SNMP_WRITENET: SNMP WriteNet request. Writing current configuration to 192.168.121.1
Sep 18 10:32:09: %SYS-5-PRIV_AUTH_FAIL: Authentication to privilege level 15 failed by garry on vty0 (81.20.192.32)
Sep 18 10:33:33: %SYS-5-CONFIG_I: Configured from console by garry on vty0 (81.20.192.32)
Sep 18 10:33:39: %SYS-6-LOGGINGHOST_STARTSTOP: Logging to host 81.20.196.53 port 514 started - reconnection
Sep 18 10:33:44: %SYS-6-LOGGINGHOST_STARTSTOP: Logging to host 192.168.121.26 port 514 started - reconnection
Sep 18 10:35:15: %CLEAR-5-COUNTERS: Clear counter on interface GigabitEthernet0 by garry on vty0 (81.20.192.32)
Sep 18 10:37:34: %CLEAR-5-COUNTERS: Clear counter on interface GigabitEthernet0 by garry on vty0 (81.20.192.32)
Sep 18 14:41:59: %SYS-6-LOGGINGHOST_STARTSTOP: Logging to host 81.20.196.53 port 514 stopped - CLI initiated
Sep 18 14:42:15: %SYS-5-CONFIG_I: Configured from console by garry on vty0 (81.20.192.32)
Sep 18 14:42:16: %SYS-6-LOGGINGHOST_STARTSTOP: Logging to host 192.168.121.1 port 514 started - CLI initiated
Sep 18 14:42:24: %CLEAR-5-COUNTERS: Clear counter on interface GigabitEthernet0 by garry on vty0 (81.20.192.32)
Sep 18 14:43:21: %CLEAR-5-COUNTERS: Clear counter on interface GigabitEthernet0 by garry on vty0 (81.20.192.32)
Sep 18 15:02:43: %SYS-6-LOGGINGHOST_STARTSTOP: Logging to host 192.168.121.1 port 514 stopped - CLI initiated
Sep 18 15:02:46: %SYS-5-CONFIG_I: Configured from console by garry on vty0 (81.20.192.32)
Sep 18 15:02:47: %SYS-6-LOGGINGHOST_STARTSTOP: Logging to host 81.20.196.53 port 514 started - CLI initiated
Sep 18 23:02:47: %SYS-6-EXEC_EXPIRE_TIMER: (tty 2 (81.20.192.32)) exec-timeout timer expired for user garry
Sep 19 04:01:01: %SYS-4-SNMP_WRITENET: SNMP WriteNet request. Writing current configuration to 192.168.121.1
Sep 20 04:01:01: %SYS-4-SNMP_WRITENET: SNMP WriteNet request. Writing current configuration to 192.168.121.1
Sep 21 04:01:01: %SYS-4-SNMP_WRITENET: SNMP WriteNet request. Writing current configuration to 192.168.121.1
Sep 22 04:01:01: %SYS-4-SNMP_WRITENET: SNMP WriteNet request. Writing current configuration to 192.168.121.1
Sep 23 04:01:01: %SYS-4-SNMP_WRITENET: SNMP WriteNet request. Writing current configuration to 192.168.121.1
Sep 24 04:01:01: %SYS-4-SNMP_WRITENET: SNMP WriteNet request. Writing current configuration to 192.168.121.1
Sep 24 20:59:22: %SYS-6-EXEC_EXPIRE_TIMER: (tty 2 (192.168.121.1)) exec-timeout timer expired for user garry
Sep 25 04:01:01: %SYS-4-SNMP_WRITENET: SNMP WriteNet request. Writing current configuration to 192.168.121.1
Sep 26 04:01:01: %SYS-4-SNMP_WRITENET: SNMP WriteNet request. Writing current configuration to 192.168.121.1
Sep 27 04:01:01: %SYS-4-SNMP_WRITENET: SNMP WriteNet request. Writing current configuration to 192.168.121.1
Sep 28 04:01:02: %SYS-4-SNMP_WRITENET: SNMP WriteNet request. Writing current configuration to 192.168.121.1
Sep 29 04:01:01: %SYS-4-SNMP_WRITENET: SNMP WriteNet request. Writing current configuration to 192.168.121.1
Sep 30 04:01:02: %SYS-4-SNMP_WRITENET: SNMP WriteNet request. Writing current configuration to 192.168.121.1
Oct  1 04:01:01: %SYS-4-SNMP_WRITENET: SNMP WriteNet request. Writing current configuration to 192.168.121.1
Oct  1 13:41:29: %CLEAR-5-COUNTERS: Clear counter on interface TenGigabitEthernet0/3/0 by garry on vty0 (81.20.192.32)




sh environment temperature

------------------ show hw-module subslot all sensors ----------
```
