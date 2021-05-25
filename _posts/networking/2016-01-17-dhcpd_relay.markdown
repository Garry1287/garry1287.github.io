---
layout: post
title:  "dhcpd_relay"
date:   2016-01-17 05:18:20 +0300
categories: Networking
tags: Networking
---

# dhcpd_relay
Jul 20 14:21:15 garry dhcpd: DHCPDISCOVER from 00:00:00:44:bb:aa via 192.168.113.201
Jul 20 14:21:16 garry dhcpd: DHCPOFFER on 192.168.113.32 to 00:00:00:44:bb:aa (Se06) via 192.168.113.201
Jul 20 14:21:16 garry dhcpd: DHCPREQUEST for 192.168.113.32 (192.168.113.1) from 00:00:00:44:bb:aa (Se06) via 192.168.113.201
Jul 20 14:21:16 garry dhcpd: DHCPACK on 192.168.113.32 to 00:00:00:44:bb:aa (Se06) via 192.168.113.201





Jul 20 16:55:05 ruby dhcpd: DHCPDISCOVER from 00:0d:56:7d:6e:66 via 172.20.134.129
Jul 20 16:55:06 ruby dhcpd: DHCPOFFER on 172.20.134.152 to 00:0d:56:7d:6e:66 (Bayer) via 172.20.134.129
Jul 20 16:55:06 ruby dhcpd: DHCPREQUEST for 172.20.134.152 (81.20.192.6) from 00:0d:56:7d:6e:66 (Bayer) via 172.20.134.129
Jul 20 16:55:06 ruby dhcpd: DHCPACK on 172.20.134.152 to 00:0d:56:7d:6e:66 (Bayer) via 172.20.134.129

Раздаваемая сетка и ip свитча(релея) в одной подсети
попробовать ещё вместе с  ip helper address
ip адрес серевера сделать другим, чтобы проверить работу релея.



config dhcp_relay delete ipif System 192.168.113.1


CODE
interface GigabitEthernet9/10
switchport
switchport trunk encapsulation dot1q
switchport trunk allowed vlan 425,459-466,468-470 // список виланов, подаваемых к юзерам
switchport mode trunk
no ip address


Логика:
CODE
interface Vlan425
ip unnumbered Loopback123321

Виланов делаем потребное количество, на всех один лупбэк
CODE
interface Loopback123321
ip address 192.168.1.254 255.255.255.0
no ip redirects

На юзера пишем роутинг
CODE
ip route 192.168.1.1 255.255.255.255 vlan425


Код
interface Vlan100
ip address 10.32.X.X 255.255.240.0
ip helper-address 10.32.X.Y
no ip redirects
ip local-proxy-arp

vlan filter BLOCK_LAN vlan-list 100

vlan access-map BLOCK_LAN 10
action drop
match ip address 101
vlan access-map BLOCK_LAN 20
action forward

! блокировка нежелательного трафика
access-list 101 permit tcp any any eq 135
access-list 101 permit tcp any any eq 139
access-list 101 permit tcp any any eq 445
...
! отключение абонентов
access-list 101 permit ip 10.32.Y.Y 255.255.255.255 any
...
! все остальное разрешить
access-list 101 deny   ip any any



02 0A 00 00 AC 14 8C 01 0C 00 00 00

spanning-tree mst configuration
instance 1 vlan 60

switchport trunk allowed vlan add 60


Jul 22 12:17:29 garry dhcpd: send_packet: Network is unreachable
Jul 22 12:17:29 garry dhcpd: send_packet: please consult README file regarding broadcast address.




config dhcp_local_relay vlan vlanid 601 state enable


interface GigabitEthernet0/0.899
 description #RAPSOIL #garry 12.08.2010
 encapsulation dot1Q 899
 ip unnumbered Loopback5
 no ip proxy-arp
 rate-limit input 1024000 192000 384000 conform-action transmit exceed-action drop
 rate-limit output 1024000 192000 384000 conform-action transmit exceed-action drop
 no cdp enable
end


Value: 020C020A0000AC148C010C000000
Agent Remote ID: 020A0000AC148C010C000000

Value: 020C020A0000AC148C010C000000
Agent Remote ID: 020A0000AC148C010C000000




Agent Remote ID: 02 0A 00 00 AC148C010C000000



Agent Remote ID: 020A0000AC148C010C000000
Agent Remote ID: 020A0000AC148C010C000000

Jul 23 12:34:29 garry dhcpd: DHCPRELEASE of 0.0.0.0 from 00:1d:60:d7:68:79 via 172.20.140.1 (not found)
Jul 23 12:34:29 garry dhcpd: DHCPRELEASE of 0.0.0.0 from 00:1d:60:d7:68:79 via 192.168.113.201 (not found)
Jul 23 12:34:30 garry dhcpd: DHCPDISCOVER from 00:1d:60:d7:68:79 via 192.168.113.201: network 192.168.113/24: no free leases
Jul 23 12:34:30 garry dhcpd: DHCPDISCOVER from 00:1d:60:d7:68:79 via 172.20.140.1
Jul 23 12:34:30 garry dhcpd: DHCPOFFER on 172.20.140.208 to 00:1d:60:d7:68:79 (Se06) via 172.20.140.1
Jul 23 12:34:31 garry dhcpd: DHCPREQUEST for 172.20.140.208 (192.168.113.1) from 00:1d:60:d7:68:79 (Se06) via 172.20.140.1
Jul 23 12:34:31 garry dhcpd: DHCPACK on 172.20.140.208 to 00:1d:60:d7:68:79 (Se06) via 172.20.140.1
Jul 23 12:34:31 garry dhcpd: DHCPREQUEST for 172.20.140.208 (172.20.140.1) from 00:1d:60:d7:68:79 (Se06) via 192.168.113.201: ignored (not authoritative).



create iproute default 192.168.113.1 1


config ipif System vlan mng ipaddress 192.168.113.201/24 state enable



config ipif System vlan mng ipaddress 192.168.113.201/24 state disable
config ipif System vlan abonent1 ipaddress 172.20.140.254/24 state enable
delete iproute default
create iproute default 172.20.140.1 1


disable dhcp_relay                                                              
config dhcp_relay hops 4 time 0                                                 
config dhcp_relay option_82 state enable                                        
config dhcp_relay option_82 check disable                                       
config dhcp_relay option_82 policy replace                                      
config dhcp_relay option_82 remote_id default                                   
config dhcp_relay option_60 state disable                                       
config dhcp_relay option_60 default mode drop                                   
config dhcp_relay option_61 state disable                                       
config dhcp_relay option_61 default drop                                        
config dhcp_relay add ipif System <<ip адрес ISG>>                                 
                                                                                
# DHCP_LOCAL_RELAY                                                              
                                                                                
disable dhcp_local_relay                                                        
config dhcp_local_relay vlan vlanid 500 state enable                            
config dhcp_local_relay option_82 ports 1-26 policy keep


config dhcp_local_relay vlan vlanid 22 state enable



CO-6k01(config)#monitor session 1 source interface fastEthernet 3/12
CO-6k01(config)#monitor session 1 destination interface fastEthernet 3/13

monitor session 1 source interface Gi2/9
monitor session 1 destination interface Gi2/10
monitor session 1 filter packet-type good rx























aaa authentication login default local
aaa authentication ppp default group radius
aaa authorization network default group radius
aaa accounting update periodic 15
aaa accounting network default start-stop group radius
!


vpdn-group 1
! Default PPTP VPDN group
 description # PPTP endpoint for physical clients
 accept-dialin
  protocol pptp
  virtual-template 1

interface GigabitEthernet0/0
 no ip address
 ip flow ingress
 ip route-cache policy
 load-interval 30
 duplex full
 speed auto
 media-type rj45
!

interface GigabitEthernet0/0.10
 description #Uplink to PSi Network
 encapsulation dot1Q 10
 ip address 81.20.192.14 255.255.255.224
 ip flow ingress
 ip nat outside
 ip ospf cost 10
 mpls netflow egress
 mpls ip
 no cdp enable
!







interface Virtual-Template1
 description # PPTP virtual template (CHAP authentication)
 mtu 1492
 ip unnumbered GigabitEthernet0/0.10
 no ip proxy-arp
 ip flow ingress
 ip nat inside
 ppp authentication ms-chap ms-chap-v2
!


radius-server host 81.20.192.6 auth-port 1645 acct-port 1646 non-standard
radius-server retransmit 10
radius-server timeout 10
radius-server key 7 111D1C16031B050B557878
radius-server vsa send accounting
radius-server vsa send authentication










aaa authentication login default local
aaa authorization exec default local


Паша

aaa authentication login default local
aaa authentication ppp default local
aaa authorization network default if-authenticated local
aaa session-id common

vpdn enable
!
vpdn-group 1
! Default PPTP VPDN group
 description # PPTP test
 accept-dialin
  protocol pptp
  virtual-template 1




interface Virtual-Template1
 ip unnumbered Loopback1
 no ip proxy-arp
 ip route-cache flow
 peer default ip address pool MY
 ppp mtu adaptive
 ppp authentication pap callin
 ppp direction callin

ip local pool MY 81.20.199.6


!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!!!!!!!!!!!!!!!!!!!!!!!!!!!
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!!!!!!!!!!!!!!!!!!!!!!!!!!!
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!!!!!!!!!!!!!!!!!!!!!!!!!!!
!!!!!!!!!!!!!!!!!!!!!!!!!!!




ip dhcp snooping information option format remote-id ---- global configuration command, and enter the 
ip dhcp snooping vlan information option format-type circuit-id string -----------interface configuration command, the switch uses these formats. 


no ip dhcp relay information check
ip dhcp relay information policy {drop | keep | replace


ip dhcp relay override giaddr link-selection
