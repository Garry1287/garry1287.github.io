---
layout: post
title:  "mikrotik-mpls"
date:   2015-06-30 14:42:10 +0300
categories: mikrotik
tags: mikrotik
---

# mikrotik-mpls

interface bridge add name=loopback
ip address add address=81.20.192.68/32 interface=loopback


routing ospf network add network=81.20.193.92/30 area=backbone



nlmk-vpn                         20866:101 


psi-lkb-vpn                      20866:161



ip vrf cust-one
 rd 1.1.1.1:111
 route-target export 1.1.1.1:111
 route-target import 1.1.1.1:111
 exit





ip vrf nlmk-vpn
 description ### IPVPN NLMK @ LES POP
 rd 20866:101
 route-target export 20866:1010
 route-target import 20866:1010
 maximum routes 500 100



#Создаём VRF
ip vrf nlmk-vpn
 description ### IPVPN NLMK @ LES POP
 rd 20866:101
 route-target export 20866:1010
 route-target import 20866:1010
 maximum routes 500 100



ip route vrf add disabled=no routing-mark=nlmk-vpn route-distinguisher=20866:101 \
    export-route-targets=20866:1010 import-route-targets=20866:1010 interfaces=ether3-nlmk

#Настройка mpls
mpls ldp set enabled=yes transport-address=81.20.192.68 lsr-id=81.20.192.68
mpls ldp interface add interface=ether1-gateway




#Созддаём BGP

/routing bgp instance
set default as=20866 redistribute-connected=yes redistribute-static=yes router-id=81.20.192.68
add as=20866 client-to-client-reflection=no name=nlmk redistribute-connected=yes redistribute-static=yes router-id=10.192.10.6 routing-table=nlmk-vpn
/routing bgp instance vrf
add redistribute-connected=yes redistribute-other-bgp=yes redistribute-static=yes routing-mark=nlmk-vpn
add redistribute-connected=yes redistribute-static=yes routing-mark=psi-lkb-vpn
/routing bgp peer
add address-families=vpnv4 name=peer1 remote-address=81.20.192.66 remote-as=20866 update-source=loopback
add address-families=vpnv4 name=peer2 remote-address=81.20.192.67 remote-as=20866 update-source=loopback
add address-families=vpnv4 name=peer3 remote-address=81.20.192.70 remote-as=20866 update-source=loopback
add address-families=vpnv4 name=peer4 remote-address=81.20.192.71 remote-as=20866 update-source=loopback
add address-families=vpnv4 name=peer5 remote-address=81.20.192.72 remote-as=20866 update-source=loopback
add address-families=vpnv4 name=peer6 remote-address=81.20.192.76 remote-as=20866 update-source=loopback
add address-families=vpnv4 name=peer7 remote-address=81.20.192.77 remote-as=20866 update-source=loopback
add address-families=vpnv4 name=peer8 remote-address=81.20.192.78 remote-as=20866 update-source=loopback
add address-families=vpnv4 name=peer9 remote-address=81.20.192.79 remote-as=20866 update-source=loopback
add address-families=vpnv4 name=peer10 remote-address=81.20.192.74 remote-as=20866 update-source=loopback
add instance=nlmk name=peer11 remote-address=10.192.10.5 remote-as=65055 update-source=ether3-nlmk









router bgp 20866
 neighbor 81.20.192.68 remote-as 20866
 neighbor 81.20.192.68 update-source Loopback0


address-family vpnv4

 neighbor 81.20.192.68 activate
 neighbor 81.20.192.68 send-community extended



LKB IPVPN



ip route vrf add disabled=no routing-mark=psi-lkb-vpn route-distinguisher=20866:161 \
    export-route-targets=20866:1610 import-route-targets=20866:1610 interfaces=ether4-lkb


Для НЛМК

routing bgp peer add remote-address=10.192.10.5 remote-as=65055 address-families=vpnv4 \
    update-source=ether3-nlmk






Нормальная статья по L3VPN
[http://wiki.mikrotik.com/wiki/Manual:Virtual_Routing_and_Forwarding](http://wiki.mikrotik.com/wiki/Manual:Virtual_Routing_and_Forwarding)














VPLS
[http://netwild.ru/vpls/](http://netwild.ru/vpls/)

VPWS(EoMPLS) point-to-point (P2P)
EoMPLS - это точка-точка  L2circuit (он же — CrossConnect Circuit в реализации Juniper),
	VPWS (l2circuit) — the channel a point point (it are pseudo-wire).
	[http://wiki.mikrotik.com/wiki/Manual:EoMPLS_vs_Cisco](http://wiki.mikrotik.com/wiki/Manual:EoMPLS_vs_Cisco)

VPLS -  организация псевдоканалов осуществляется с помощью многоточечных соединений (P2M) 
VPLS — the multidrop channel, for the client looked as the virtual "blunt" switch which is transparently pass any packets.
Для VPLS cisco использует свои фичи, отличающиеся от общепризнанных
      [http://wiki.mikrotik.com/wiki/Manual:Cisco_VPLS](http://wiki.mikrotik.com/wiki/Manual:Cisco_VPLS)
      [http://www.cisco.com/c/en/us/td/docs/ios-xml/ios/mp_l2_vpns/configuration/xe-3s/mp-l2-vpns-xe-3s-book/vpls-auto-bgp-xe.html](http://www.cisco.com/c/en/us/td/docs/ios-xml/ios/mp_l2_vpns/configuration/xe-3s/mp-l2-vpns-xe-3s-book/vpls-auto-bgp-xe.html)
      [http://www.cisco.com/c/en/us/support/docs/ios-nx-os-software/virtual-private-lan-services-vpls/116121-tech-vpls-bgp-00.html#anc26](http://www.cisco.com/c/en/us/support/docs/ios-nx-os-software/virtual-private-lan-services-vpls/116121-tech-vpls-bgp-00.html#anc26)

VPLS бывает 2 видов
  - LDP based  (это то, что настроил я)
     [http://wiki.mikrotik.com/wiki/Manual:MPLSVPLS#Configuring_VPLS](http://wiki.mikrotik.com/wiki/Manual:MPLSVPLS#Configuring_VPLS)
      
  - BGP based  
	  L2VPN Address Family?
    [http://wiki.mikrotik.com/wiki/Manual:BGP_based_VPLS](http://wiki.mikrotik.com/wiki/Manual:BGP_based_VPLS)
    [http://www.cisco.com/c/en/us/td/docs/ios-xml/ios/iproute_bgp/configuration/xe-3s/irg-xe-3s-book/irg-vpls-bgp-sig.html](http://www.cisco.com/c/en/us/td/docs/ios-xml/ios/iproute_bgp/configuration/xe-3s/irg-xe-3s-book/irg-vpls-bgp-sig.html)

      В первую очередь я бы хотел рассмотреть «классическую», с точки зрения Juniper, реализацию VPLS с использованием BGP сигнализации (RFC 4761).
	С точки зрения control plane это мало чем отличается от обычного L3VPN — здесь также используются Route Distinguisher и Route Target,
	а в качестве address family указывается l2vpn.
      Для начала нужно настроить сам протокол BGP. Так как для корректной работы iBGP необходима полная связность внутри сети, я использовал
      P1 и P2 в качестве route-reflector, для упрощения конфигурации.

[https://www.cisco.com/application/pdf/en/us/guest/tech/tk891/c1482/ccmigration_09186a00801ed3ea.pdf](https://www.cisco.com/application/pdf/en/us/guest/tech/tk891/c1482/ccmigration_09186a00801ed3ea.pdf)
[http://sysmagazine.com/posts/169103/](http://sysmagazine.com/posts/169103/)

Особенности CISCO и Mikrotik VPLS
[http://wiki.mikrotik.com/wiki/Manual:Cisco_VPLS](http://wiki.mikrotik.com/wiki/Manual:Cisco_VPLS)

LDP или BGP сигнализация
[http://www.opennet.ru/docs/RUS/mpls/vplssig.html](http://www.opennet.ru/docs/RUS/mpls/vplssig.html)


[http://www.cisco.com/c/en/us/td/docs/ios-xml/ios/mp_l2_vpns/configuration/15-s/mp-l2-vpns-15-s-book/mp-any-transport.html#GUID-80FE4D78-C445-4970-9DB1-43349F91AB15](http://www.cisco.com/c/en/us/td/docs/ios-xml/ios/mp_l2_vpns/configuration/15-s/mp-l2-vpns-15-s-book/mp-any-transport.html#GUID-80FE4D78-C445-4970-9DB1-43349F91AB15)
[http://cisco-lab.by/study/articles/1299-mpls-vpn-atom-eompls.html](http://cisco-lab.by/study/articles/1299-mpls-vpn-atom-eompls.html)



Делал по этому
[http://wiki.mikrotik.com/wiki/Manual:EoMPLS_vs_Cisco](http://wiki.mikrotik.com/wiki/Manual:EoMPLS_vs_Cisco)
[http://habrahabr.ru/post/64073/](http://habrahabr.ru/post/64073/)
[https://ccieblog.co.uk/mpls/eompls](https://ccieblog.co.uk/mpls/eompls)




K9-C0(config-subif)#xconnect 81.20.192.68 165 ?
  encapsulation  Data encapsulation method
  pw-class       Pseudowire-class to use for encapsulation and protocol configuration

K9-C0(config-subif)#xconnect 81.20.192.68 165 en
K9-C0(config-subif)#xconnect 81.20.192.68 165 encapsulation ?
  l2tpv3  Use L2TPv3 encapsulation
  mpls    Use MPLS encapsulation








/interface vpls add name=A1toA2 remote-peer=9.9.9.5 mac-address=00:00:00:00:00:a1 vpls-id=10 disabled=no
/interface vpls add name=A1toA3 remote-peer=9.9.9.4 mac-address=00:00:00:00:00:a1 vpls-id=10 disabled=no
/interface vpls add name=B1toB2 remote-peer=9.9.9.5 mac-address=00:00:00:00:00:b1 vpls-id=11 disabled=no



/interface bridge add name=B
/interface bridge port add bridge=B interface=ether1
/interface bridge port add bridge=B interface=B1toB2









/interface vpls
add advertised-l2mtu=1526 cisco-style=yes cisco-style-id=5 disabled=no l2mtu=1526 \
name=junos-l2circuit remote-peer=172.19.238.33
/interface bridge port
add bridge=vpn interface=eth5
add bridge=vpn interface=junos-l2circuit horizon=1


/interface vpls
add advertised-l2mtu=1526 cisco-style=yes cisco-style-id=5 disabled=no l2mtu=1526 \
name=junos-l2circuit remote-peer=172.19.238.33

interface vpls add name=vpls1 disabled=no remote-peer=9.9.9.1 \
	    cisco-style=yes cisco-style-id=111;



What line cards are those? ES-cards?

I run VPLS to SIP-600 without problems, but I do it as if it was EoMPLS.

Configuration:

MikroTik:

Code: Select all
/interface vpls
add name="VC001231234" remote-peer=198.18.1.2 cisco-style=yes cisco-style-id=1231234 pw-type=raw-ethernet

(bridge to VLAN interface or whatever

Cisco

Code: Select all
vlan 1234
 name "VC001231234"
!
interface vlan 1234
 description Cust: Customer (edge1/VC001231234)
 no ip address
 xconnect 198.18.1.1 1231234 encapsulation mpls
!

This basically terminates the xconnect on a SVI. On the SIP, I can then put it in a VRF or I can put it on a switchport.




     



Hello. I've just made a Cisco's xconnect to signal with Extreme's VPWS! 

Find the CISCO configuration below:
#
pseudowire-class PW_CLASS 
 encapsulation mpls
 interworking ethernet
#
interface GigabitEthernet0/3.666 encapsulation dot1Q 666
 xconnect Z.Z.Z.Z 666 pw-class PW_CLASS
  remote circuit id 666
#















Статус нормального подключения 

interface vpls monitor vpls-voip once 
       remote-label: 51
        local-label: 24
      remote-status: 
          transport: 81.20.192.67/32
  transport-nexthop: 81.20.193.93
     imposed-labels: 51


/routing ospf instance
set [ find default=yes ] redistribute-connected=as-type-1 redistribute-static=as-type-1 router-id=81.20.192.68
/routing ospf interface
add interface=ether1-gateway network-type=broadcast
/routing ospf network
add area=backbone network=81.20.193.92/30



 0 R   name="vpls-voip" mtu=1500 l2mtu=1500 mac-address=02:F7:A0:A8:2C:E8 arp=enabled disable-running-check=no remote-peer=81.20.192.67 cisco-style=yes cisco-style-id=165 advertised-l2mtu=1500 
       pw-type=tagged-ethernet use-control-word=default 



interface bridge print 
Flags: X - disabled, R - running 
 0  R name="loopback" mtu=auto actual-mtu=1500 l2mtu=65535 arp=enabled mac-address=00:00:00:00:00:00 protocol-mode=rstp priority=0x8000 auto-mac=yes admin-mac=00:00:00:00:00:00 max-message-age=20s 
      forward-delay=15s transmit-hold-count=6 ageing-time=5m 

 1  R name="voice-bridge" mtu=auto actual-mtu=1500 l2mtu=1500 arp=enabled mac-address=E4:8D:8C:AD:2E:71 protocol-mode=rstp priority=0x8000 auto-mac=yes admin-mac=00:00:00:00:00:00 max-message-age=20s 
      forward-delay=15s transmit-hold-count=6 ageing-time=5m 



C другой стороны

 interface vpls monitor vpls-voip once 
       remote-label: 51
        local-label: 24
      remote-status: 
          transport: 81.20.192.67/32
  transport-nexthop: 81.20.193.93
     imposed-labels: 51



/routing ospf instance
set [ find default=yes ] redistribute-connected=as-type-1 redistribute-static=as-type-1 router-id=81.20.192.68
/routing ospf interface
add interface=ether1-gateway network-type=broadcast
/routing ospf network
add area=backbone network=81.20.193.92/30




Flags: X - disabled, R - running, D - dynamic, B - bgp-signaled, C - cisco-bgp-signaled 
 0 R   name="vpls-voip" mtu=1500 l2mtu=1500 mac-address=02:F7:A0:A8:2C:E8 arp=enabled disable-running-check=no remote-peer=81.20.192.67 cisco-style=yes cisco-style-id=165 advertised-l2mtu=1500 
       pw-type=tagged-ethernet use-control-word=default 




# oct/22/2015 19:15:45 by RouterOS 6.32.2
# software id = 3A69-VFDW
#
/interface bridge
add name=loopback
add name=voice-bridge
/interface bridge port
add bridge=voice-bridge interface=ether5-slave-local
add bridge=voice-bridge interface=vpls-voip














OSPF настроить как STUB



O - OSPF,
IA - OSPF inter area 
N1 - OSPF NSSA external type 1,
N2 - OSPF NSSA external type 2
E1 - OSPF external type 1,
E2 - OSPF external type 2


router ospf 10
  network 203.250.15.0 0.0.0.255 area 0.0.0.2
  network 203.250.14.0 0.0.0.255 area 0
  area 0.0.0.2 stub



/routing ospf area add name=area1 area-id=1.1.1.1 type=stub inject-summary-lsa=yes
/routing ospf network 
add network=10.0.1.0/24 area=area1





forward all в нужном vrf



Тест комбината

router bgp 65055
 bgp router-id 10.192.10.5
 bgp log-neighbor-changes
 neighbor 10.192.10.5 remote-as 20866

 !
 address-family ipv4
  network 10.6.10.4 mask 255.255.255.252
  neighbor 10.192.10.5 activate
 exit-address-family
!

[http://www.stubarea51.com/2015/11/09/cisco-to-mikrotik-command-translation-bgp/](http://www.stubarea51.com/2015/11/09/cisco-to-mikrotik-command-translation-bgp/)
