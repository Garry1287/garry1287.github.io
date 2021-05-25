---
layout: post
title:  "UNISPRINT-KLG-C0"
date:   2016-06-18 12:38:22 +0300
categories: zavod
tags: zavod
---

# UNISPRINT-KLG-C0
version 12.4
service timestamps debug datetime msec
service timestamps log datetime msec
service password-encryption
!
hostname UNISPRINT-KLG-C0
!
boot-start-marker
boot system flash c2800nm-spservicesk9-mz.124-19.bin
boot-end-marker
!
enable secret 5 $1$Qi2F$ohOVXShpHwqYpB66FrIVE.
!
aaa new-model
!
!
aaa authentication login default local
!
aaa session-id common
!
!
ip cef
!
!
ip vrf connect-amds-voip
 description # AMDS VoIP Service
 rd 20866:405
 route-target export 20866:4050
 route-target import 20866:4050
!
ip vrf equant-diksi-kaluga-lm
 description # VPN L3 for Equant (Diksi Kaluga)
 rd 20866:403
 route-target export 20866:4030
 route-target import 20866:4030
!
ip vrf unisprint-mgmt
 description # Unisprint mgmt
 rd 20866:401
 route-target export 20866:4010
 route-target import 20866:4010
!
mpls label protocol ldp
!
voice-card 0
 no dspfarm
!
!
!
!
!
!
!
!
!
!
!
!
!
!
username hd password 7 012303167C1E0B1F73
username pheonix password 7 091A1B00161518
username garry password 7 000F1A0220410E5757126B
!
!
!
!
!
interface Loopback0
 description # MPLS & BGP exchanges
 ip address 192.168.91.3 255.255.255.255
!
interface GigabitEthernet0/0
 no ip address
 duplex auto
 speed auto
!
interface GigabitEthernet0/0.10
 description # Mgmt interface
 encapsulation dot1Q 10
 ip vrf forwarding unisprint-mgmt
 ip address 192.168.10.1 255.255.255.0
!
interface GigabitEthernet0/0.145
 description # Diksi IPVPN
 bandwidth 5120
 encapsulation dot1Q 145
 ip vrf forwarding equant-diksi-kaluga-lm
 ip address 172.16.202.94 255.255.255.252
 rate-limit input 5120000 960000 1920000 conform-action transmit exceed-action drop
 rate-limit output 5120000 960000 1920000 conform-action transmit exceed-action drop
 no cdp enable
!
interface GigabitEthernet0/0.148
 description # AMDS VoIP Service (Connect)
 encapsulation dot1Q 148
 ip vrf forwarding connect-amds-voip
 ip address 10.255.9.1 255.255.255.248
 no cdp enable
!
interface GigabitEthernet0/0.456
 description # Uplink to UNISPRINT-M9-C0
 encapsulation dot1Q 456
 ip address 192.168.90.6 255.255.255.252
 mpls ip
!
interface GigabitEthernet0/1
 no ip address
 shutdown
 duplex auto
 speed auto
!
router bgp 20866
 bgp router-id 192.168.90.6
 no bgp default ipv4-unicast
 bgp log-neighbor-changes
 neighbor 192.168.90.5 remote-as 20866
 neighbor 192.168.90.5 update-source GigabitEthernet0/0.456
 neighbor 192.168.91.2 remote-as 20866
 neighbor 192.168.91.2 update-source Loopback0
 !
 address-family vpnv4
  neighbor 192.168.90.5 activate
  neighbor 192.168.90.5 send-community both
  neighbor 192.168.91.2 activate
  neighbor 192.168.91.2 send-community both
 exit-address-family
 !
 address-family ipv4 vrf unisprint-mgmt
  redistribute connected
  redistribute static
  no synchronization
 exit-address-family
 !
 address-family ipv4 vrf equant-diksi-kaluga-lm
  redistribute connected
  no synchronization
 exit-address-family
 !
 address-family ipv4 vrf connect-amds-voip
  redistribute connected
  no synchronization
 exit-address-family
!
ip forward-protocol nd
ip route 192.168.90.0 255.255.255.0 192.168.90.5
ip route 192.168.91.1 255.255.255.255 192.168.90.5
ip route 192.168.91.2 255.255.255.255 192.168.90.5
!
!
ip http server
no ip http secure-server
!
access-list 57 permit 192.168.8.2
access-list 57 deny   any
snmp-server community Sh73ah91Kld RW 57
snmp-server location kaluga-c0
snmp-server contact ibd@sc.ru
snmp-server enable traps tty
!
mpls ldp router-id GigabitEthernet0/0.456
!
!
control-plane
!
!
!
!
!
!
!
!
!
line con 0
line aux 0
line vty 0 4
 exec-timeout 0 0
line vty 5 15
 exec-timeout 0 0
!
scheduler allocate 20000 1000
!
end
