---
layout: post
title:  "UNISPRINT-M9-C0"
date:   2015-05-01 20:07:13 +0300
categories: zavod
tags: zavod
---

# UNISPRINT-M9-C0
version 12.4
service timestamps debug datetime msec
service timestamps log datetime msec
service password-encryption
!
hostname UNISPRINT-M9-C0
!
boot-start-marker
boot-end-marker
!
enable secret 5 $1$fQDY$96n6eufwCoHt/dfciXKOj0
!
aaa new-model
!
!
aaa authentication login default local
!
aaa session-id common
!
resource policy
!
ip subnet-zero
ip cef
!
!
!
!
ip vrf comstar-dm-voronezh-lm
 description # VPN L3 LM for Comstar (DM Voronezh)
 rd 20866:404
 route-target export 20866:4040
 route-target import 20866:4040
!
ip vrf connect-ipvpn
 description # Connect IPVPN
 rd 20866:402
 route-target export 20866:4020
 route-target import 20866:4020
!
ip vrf connect-voip
 description # Connect VoIP IPVPN
 rd 20866:405
 route-target export 20866:4050
 route-target import 20866:4050
!
ip vrf equant-diksi-kaluga-lm
 description # VPN L3 LM for Equant (Diksi Kaluga)
 rd 20866:403
 route-target export 20866:4030
 route-target import 20866:4030
!
ip vrf rtk-tlg-kamov
 description # VPN Kamov (Rostelecom - Telegraph)
 rd 20866:406
!
ip vrf sucden-vpn
 description # VPN for Sucden (via Equant)
 rd 20866:407
 route-target export 20866:4070
 route-target import 20866:4070
!
ip vrf unisprint-mgmt
 description # Unisprint mgmt
 rd 20866:401
 route-target export 20866:4010
 route-target import 20866:4010
!
no ip domain lookup
mpls label protocol ldp
mpls ldp router-id GigabitEthernet0/0.457
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
!
username hd password 7 11391C173007061C56
username pheonix password 7 06505A28435E06
username garry password 7 0831435C0612544F45
!
!
!
!
interface Loopback0
 description # MPLS & BGP exchanges
 ip address 192.168.91.1 255.255.255.255
!
interface GigabitEthernet0/0
 description # 802.1q multiplexed interface
 no ip address
 ip route-cache flow
 load-interval 30
 duplex auto
 speed auto
 media-type rj45
 no negotiation auto
!
interface GigabitEthernet0/0.10
 description # Mgmt interface
 encapsulation dot1Q 10
 ip vrf forwarding unisprint-mgmt
 ip address 192.168.9.1 255.255.255.0
 no snmp trap link-status
!
interface GigabitEthernet0/0.101
 description # Link to Sucden for IPVPN service # Paul # 09.07.2009
 bandwidth 2048
 encapsulation dot1Q 101
 ip vrf forwarding sucden-vpn
 no snmp trap link-status
 no cdp enable
!
interface GigabitEthernet0/0.250
 description # Link to Comstar for DM Voronezh # Woland 06.11.2008
 bandwidth 2048
 encapsulation dot1Q 250
 ip vrf forwarding comstar-dm-voronezh-lm
 ip address 192.168.13.50 255.255.255.240
 rate-limit input 2048000 384000 768000 conform-action transmit exceed-action drop
 rate-limit output 2048000 384000 768000 conform-action transmit exceed-action drop
 no snmp trap link-status
 mpls netflow egress
 no cdp enable
!
interface GigabitEthernet0/0.455
 description # Downlink to Voronezh 2Mbps via StartTelecom # Woland 06.11.2008
 bandwidth 2048
 encapsulation dot1Q 455
 ip vrf forwarding comstar-dm-voronezh-lm
 ip address 192.168.13.25 255.255.255.252
 rate-limit input 2048000 384000 768000 conform-action transmit exceed-action drop
 rate-limit output 2048000 384000 768000 conform-action transmit exceed-action drop
 no snmp trap link-status
 mpls netflow egress
 no cdp enable
!
interface GigabitEthernet0/0.456
 description # Downlink to Kaluga 5Mbps # Paul 29.10.2008
 encapsulation dot1Q 456
 ip address 192.168.90.5 255.255.255.252
 no snmp trap link-status
 mpls netflow egress
 mpls ip
 no cdp enable
!
interface GigabitEthernet0/0.457
 description # Link to Lipetsk CDE-C2 via StartTelecom (MPLS/IP)
 encapsulation dot1Q 457
 ip address 192.168.90.1 255.255.255.252
 no snmp trap link-status
 mpls netflow egress
 mpls ip
!
interface GigabitEthernet0/0.458
 description # Connect IPVPN (Tver)
 bandwidth 256
 encapsulation dot1Q 458
 ip vrf forwarding connect-ipvpn
 ip address 10.65.15.1 255.255.255.252
 rate-limit input 256000 48000 96000 conform-action transmit exceed-action drop
 rate-limit output 256000 48000 96000 conform-action transmit exceed-action drop
 no snmp trap link-status
 mpls netflow egress
 no cdp enable
!
interface GigabitEthernet0/0.459
 description # Connect IPVPN (Voronezh)
 bandwidth 256
 encapsulation dot1Q 459
 ip vrf forwarding connect-ipvpn
 ip address 10.65.4.1 255.255.255.252
 rate-limit input 256000 48000 96000 conform-action transmit exceed-action drop
 rate-limit output 256000 48000 96000 conform-action transmit exceed-action drop
 no snmp trap link-status
 mpls netflow egress
 no cdp enable
!
interface GigabitEthernet0/0.460
 description # Connect IPVPN (Vladimir)
 bandwidth 256
 encapsulation dot1Q 460
 ip vrf forwarding connect-ipvpn
 ip address 10.65.5.1 255.255.255.252
 rate-limit input 256000 48000 96000 conform-action transmit exceed-action drop
 rate-limit output 256000 48000 96000 conform-action transmit exceed-action drop
 no snmp trap link-status
 mpls netflow egress
 no cdp enable
!
interface GigabitEthernet0/0.461
 description # Connect IPVPN (Belgorod)
 bandwidth 256
 encapsulation dot1Q 461
 ip vrf forwarding connect-ipvpn
 ip address 10.65.2.1 255.255.255.252
 rate-limit input 256000 48000 96000 conform-action transmit exceed-action drop
 rate-limit output 256000 48000 96000 conform-action transmit exceed-action drop
 no snmp trap link-status
 mpls netflow egress
 no cdp enable
!
interface GigabitEthernet0/0.462
 description # Connect IPVPN (Kursk)
 bandwidth 256
 encapsulation dot1Q 462
 ip vrf forwarding connect-ipvpn
 ip address 10.65.9.1 255.255.255.252
 rate-limit input 256000 48000 96000 conform-action transmit exceed-action drop
 rate-limit output 256000 48000 96000 conform-action transmit exceed-action drop
 no snmp trap link-status
 mpls netflow egress
 no cdp enable
!
interface GigabitEthernet0/0.463
 description # Connect IPVPN (Orel)
 bandwidth 256
 encapsulation dot1Q 463
 ip vrf forwarding connect-ipvpn
 ip address 10.65.11.1 255.255.255.252
 rate-limit input 256000 48000 96000 conform-action transmit exceed-action drop
 rate-limit output 256000 48000 96000 conform-action transmit exceed-action drop
 no snmp trap link-status
 mpls netflow egress
 no cdp enable
!
interface GigabitEthernet0/0.464
 description # Connect IPVPN (Bryansk)
 bandwidth 256
 encapsulation dot1Q 464
 ip vrf forwarding connect-ipvpn
 ip address 10.65.3.1 255.255.255.252
 rate-limit input 256000 48000 96000 conform-action transmit exceed-action drop
 rate-limit output 256000 48000 96000 conform-action transmit exceed-action drop
 no snmp trap link-status
 mpls netflow egress
 no cdp enable
!
interface GigabitEthernet0/0.465
 description # Connect IPVPN (Smolensk)
 bandwidth 256
 encapsulation dot1Q 465
 ip vrf forwarding connect-ipvpn
 ip address 10.65.13.1 255.255.255.252
 rate-limit input 256000 48000 96000 conform-action transmit exceed-action drop
 rate-limit output 256000 48000 96000 conform-action transmit exceed-action drop
 no snmp trap link-status
 mpls netflow egress
 no cdp enable
!
interface GigabitEthernet0/0.466
 description # Connect IPVPN (Tambov)
 bandwidth 256
 encapsulation dot1Q 466
 ip vrf forwarding connect-ipvpn
 ip address 10.65.14.1 255.255.255.252
 rate-limit input 256000 48000 96000 conform-action transmit exceed-action drop
 rate-limit output 256000 48000 96000 conform-action transmit exceed-action drop
 no snmp trap link-status
 mpls netflow egress
 no cdp enable
!
interface GigabitEthernet0/0.467
 description # Connect IPVPN (Tula)
 bandwidth 256
 encapsulation dot1Q 467
 ip vrf forwarding connect-ipvpn
 ip address 10.65.16.1 255.255.255.252
 rate-limit input 256000 48000 96000 conform-action transmit exceed-action drop
 rate-limit output 256000 48000 96000 conform-action transmit exceed-action drop
 no snmp trap link-status
 mpls netflow egress
 no cdp enable
!
interface GigabitEthernet0/0.468
 description # Connect IPVPN (Kaluga)
 bandwidth 256
 encapsulation dot1Q 468
 ip vrf forwarding connect-ipvpn
 ip address 10.65.7.1 255.255.255.252
 rate-limit input 256000 48000 96000 conform-action transmit exceed-action drop
 rate-limit output 256000 48000 96000 conform-action transmit exceed-action drop
 no snmp trap link-status
 mpls netflow egress
 no cdp enable
!
interface GigabitEthernet0/0.469
 description # Connect IPVPN (Ryazan)
 bandwidth 256
 encapsulation dot1Q 469
 ip vrf forwarding connect-ipvpn
 ip address 10.65.12.1 255.255.255.252
 rate-limit input 256000 48000 96000 conform-action transmit exceed-action drop
 rate-limit output 256000 48000 96000 conform-action transmit exceed-action drop
 no snmp trap link-status
 mpls netflow egress
 no cdp enable
!
interface GigabitEthernet0/0.470
 description # Connect IPVPN (Ivanovo)
 bandwidth 256
 encapsulation dot1Q 470
 ip vrf forwarding connect-ipvpn
 ip address 10.65.6.1 255.255.255.252
 rate-limit input 256000 48000 96000 conform-action transmit exceed-action drop
 rate-limit output 256000 48000 96000 conform-action transmit exceed-action drop
 no snmp trap link-status
 mpls netflow egress
 no cdp enable
!
interface GigabitEthernet0/0.471
 description # Connect IPVPN (Kostroma)
 bandwidth 256
 encapsulation dot1Q 471
 ip vrf forwarding connect-ipvpn
 ip address 10.65.8.1 255.255.255.252
 rate-limit input 256000 48000 96000 conform-action transmit exceed-action drop
 rate-limit output 256000 48000 96000 conform-action transmit exceed-action drop
 no snmp trap link-status
 mpls netflow egress
 no cdp enable
!
interface GigabitEthernet0/0.472
 description # Connect IPVPN (Yaroslavl)
 bandwidth 256
 encapsulation dot1Q 472
 ip vrf forwarding connect-ipvpn
 ip address 10.65.17.1 255.255.255.252
 rate-limit input 256000 48000 96000 conform-action transmit exceed-action drop
 rate-limit output 256000 48000 96000 conform-action transmit exceed-action drop
 no snmp trap link-status
 mpls netflow egress
 no cdp enable
!
interface GigabitEthernet0/0.473
 description # Connect IPVPN (Moscow)
 bandwidth 1024
 encapsulation dot1Q 473
 ip vrf forwarding connect-ipvpn
 ip address 10.129.1.1 255.255.255.252
 rate-limit input 1024000 192000 384000 conform-action transmit exceed-action drop
 rate-limit output 1024000 192000 384000 conform-action transmit exceed-action drop
 no snmp trap link-status
 mpls netflow egress
 no cdp enable
!
interface GigabitEthernet0/0.483
 description # Connect VoIP
 encapsulation dot1Q 483
 ip vrf forwarding connect-voip
 ip address 10.34.0.10 255.255.255.252
 no snmp trap link-status
!
interface GigabitEthernet0/0.499
 description # SUCDEN VPN (via Equant) # Paul # 09.07.2009
 encapsulation dot1Q 499
 ip vrf forwarding sucden-vpn
 ip address 172.16.97.217 255.255.255.252
 no snmp trap link-status
 no cdp enable
!
interface GigabitEthernet0/0.500
 description # Link to Equant for Diksi Kaluga # Paul 30.10.2008
 bandwidth 5000
 encapsulation dot1Q 500
 ip vrf forwarding equant-diksi-kaluga-lm
 ip address 172.16.202.89 255.255.255.252
 rate-limit input 5120000 960000 1920000 conform-action transmit exceed-action drop
 rate-limit output 5120000 960000 1920000 conform-action transmit exceed-action drop
 no snmp trap link-status
 mpls netflow egress
 no cdp enable
!
interface GigabitEthernet0/0.817
 description # VPN Kamov - Rostelecom side
 bandwidth 10240
 encapsulation dot1Q 817
 ip vrf forwarding rtk-tlg-kamov
 ip address 188.128.0.234 255.255.255.252
 rate-limit input 10240000 1920000 3840000 conform-action transmit exceed-action drop
 rate-limit output 10240000 1920000 3840000 conform-action transmit exceed-action drop
 no snmp trap link-status
 no cdp enable
!
interface GigabitEthernet0/0.3517
 description # VPN Kamov - Telegraph side
 bandwidth 10240
 encapsulation dot1Q 3517
 ip vrf forwarding rtk-tlg-kamov
 ip address 188.128.2.37 255.255.255.252
 rate-limit input 10240000 1920000 3840000 conform-action transmit exceed-action drop
 rate-limit output 10240000 1920000 3840000 conform-action transmit exceed-action drop
 no snmp trap link-status
 no cdp enable
!
interface GigabitEthernet0/1
 no ip address
 shutdown
 duplex auto
 speed auto
 media-type rj45
 negotiation auto
!
router bgp 20866
 bgp router-id 192.168.90.1
 no bgp default ipv4-unicast
 bgp log-neighbor-changes
 neighbor 192.168.90.2 remote-as 20866
 neighbor 192.168.90.2 update-source GigabitEthernet0/0.457
 neighbor 192.168.90.6 remote-as 20866
 neighbor 192.168.90.6 update-source GigabitEthernet0/0.456
 !
 address-family vpnv4
 neighbor 192.168.90.2 activate
 neighbor 192.168.90.2 send-community extended
 neighbor 192.168.90.6 activate
 neighbor 192.168.90.6 send-community both
 exit-address-family
 !
 address-family ipv4 vrf unisprint-mgmt
 redistribute connected
 redistribute static
 no auto-summary
 no synchronization
 exit-address-family
 !
 address-family ipv4 vrf sucden-vpn
 no auto-summary
 no synchronization
 exit-address-family
 !
 address-family ipv4 vrf rtk-tlg-kamov
 no auto-summary
 no synchronization
 exit-address-family
 !
 address-family ipv4 vrf equant-diksi-kaluga-lm
 redistribute connected
 redistribute static
 default-information originate
 no auto-summary
 no synchronization
 exit-address-family
 !
 address-family ipv4 vrf connect-voip
 redistribute connected
 redistribute static
 no auto-summary
 no synchronization
 exit-address-family
 !
 address-family ipv4 vrf connect-ipvpn
 redistribute connected
 redistribute static
 default-information originate
 no auto-summary
 no synchronization
 exit-address-family
 !
 address-family ipv4 vrf comstar-dm-voronezh-lm
 no auto-summary
 no synchronization
 exit-address-family
!
ip classless
ip route 81.20.192.74 255.255.255.255 192.168.90.2
ip route 192.168.91.2 255.255.255.255 192.168.90.2
ip route 192.168.91.3 255.255.255.255 192.168.90.6
ip route vrf connect-ipvpn 0.0.0.0 0.0.0.0 10.129.1.2
ip route vrf connect-ipvpn 10.1.2.0 255.255.255.0 10.65.2.2
ip route vrf connect-ipvpn 10.1.3.0 255.255.255.0 10.65.3.2
ip route vrf connect-ipvpn 10.1.4.0 255.255.255.0 10.65.4.2
ip route vrf connect-ipvpn 10.1.5.0 255.255.255.0 10.65.5.2
ip route vrf connect-ipvpn 10.1.6.0 255.255.255.0 10.65.6.2
ip route vrf connect-ipvpn 10.1.7.0 255.255.255.0 10.65.7.2
ip route vrf connect-ipvpn 10.1.8.0 255.255.255.0 10.65.8.2
ip route vrf connect-ipvpn 10.1.9.0 255.255.255.0 10.65.9.2
ip route vrf connect-ipvpn 10.1.11.0 255.255.255.0 10.65.11.2
ip route vrf connect-ipvpn 10.1.12.0 255.255.255.0 10.65.12.2
ip route vrf connect-ipvpn 10.1.13.0 255.255.255.0 10.65.13.2
ip route vrf connect-ipvpn 10.1.14.0 255.255.255.0 10.65.14.2
ip route vrf connect-ipvpn 10.1.15.0 255.255.255.0 10.65.15.2
ip route vrf connect-ipvpn 10.1.16.0 255.255.255.0 10.65.16.2
ip route vrf connect-ipvpn 10.1.17.0 255.255.255.0 10.65.17.2
ip route vrf equant-diksi-kaluga-lm 0.0.0.0 0.0.0.0 172.16.202.90
ip route vrf connect-voip 217.174.180.0 255.255.255.192 10.34.0.9
ip route vrf connect-voip 217.174.181.0 255.255.255.192 10.34.0.9
ip route vrf rtk-tlg-kamov 0.0.0.0 0.0.0.0 188.128.0.233
ip route vrf rtk-tlg-kamov 188.128.122.96 255.255.255.248 188.128.2.38
ip route vrf sucden-vpn 10.0.48.0 255.255.255.0 172.16.97.218
ip route vrf sucden-vpn 172.16.48.0 255.255.255.0 172.16.97.218
!
ip flow-export source GigabitEthernet0/0.10
ip flow-export version 5 origin-as
ip flow-aggregation cache prefix
 cache entries 16384
 export destination 192.168.1.135 8008
 mask source minimum 24
 mask destination minimum 20
 enabled
!
ip flow-aggregation cache as-tos
 cache entries 16384
 export destination 192.168.1.135 8009
 enabled
!
!
no ip http server
no ip http secure-server
!
snmp-server community public RO 57
snmp-server community Sh73ah91Kld RW 57
snmp-server ifindex persist
snmp-server location M9
snmp-server contact woland@sc.ru
snmp-server enable traps snmp authentication linkdown linkup coldstart warmstart
snmp-server enable traps tty
snmp-server enable traps bgp
snmp-server enable traps entity
snmp-server enable traps frame-relay
snmp-server enable traps frame-relay subif
snmp-server enable traps mpls ldp
snmp-server enable traps mpls traffic-eng
snmp-server enable traps mpls vpn
snmp-server host 192.168.1.11 version 2c public
snmp-server host 192.168.1.135 version 2c public
!
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
 stopbits 1
line aux 0
 stopbits 1
line vty 0 4
 exec-timeout 0 0
line vty 5 15
 exec-timeout 0 0
!
scheduler allocate 20000 1000
!
end
