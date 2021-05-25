---
layout: post
title:  "dlink-rstp"
date:   2015-12-16 00:39:36 +0300
categories: dlink
tags: dlink
---

# dlink-rstp

Пример Манежа

DSG3627


 config stp version rstp
 config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 3 fbpdu disable hellotime 2 lbd enable lbd_recover_timer 60
 config stp priority 4096 instance_id 0 
 config stp mst_config_id name 00:22:B0:30:E9:00 revision_level 0
 
 config stp ports 1-8 externalCost auto  edge false p2p auto state enable lbd disable
 config stp mst_ports 1-27 instance_id 0 internalCost auto priority 128
config stp ports 1-8 fbpdu enable
 config stp ports 9-27 externalCost auto  edge true p2p auto state disable lbd disable
config stp ports 9-27 fbpdu disable
enable stp


3200
# STP
                                                                               
config stp version rstp
config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 6 fbpdu enable hellotime 2
config stp priority 32768 instance_id 0 
config stp mst_config_id name 1C:BD:B9:64:94:60 revision_level 0
config stp ports 1-24 externalCost auto edge true p2p auto state disable
config stp mst_ports 1-28 instance_id 0 internalCost auto priority 128
config stp ports 1-24 fbpdu disable
config stp ports 1-24 restricted_role true
config stp ports 1-24 restricted_tcn true
config stp ports 25-28 externalCost auto edge false p2p auto state enable
config stp ports 25-28 fbpdu enable
config stp ports 25-28 restricted_role false
config stp ports 25-28 restricted_tcn false
enable stp


Конфиг 13 район









config stp version rstp
config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 6 fbpdu enable hellotime 2
config stp priority 32768 instance_id 0 
config stp mst_config_id name 1C:BD:B9:64:94:60 revision_level 0
config stp ports 1-24 externalCost auto edge true p2p auto state disable
config stp mst_ports 1-28 instance_id 0 internalCost auto priority 128
config stp ports 1-24 fbpdu disable
config stp ports 1-24 restricted_role true
config stp ports 1-24 restricted_tcn true
config stp ports 25-28 externalCost auto edge false p2p auto state enable
config stp ports 25-28 fbpdu enable
config stp ports 25-28 restricted_role false
config stp ports 25-28 restricted_tcn false
enable stp





192.168.124.39

192.168.124.39



5 кольцо ОК

6 кольцо 2 последних не видно
ул.Ильича 18		6.4.1	192.168.124.37	1c-7e-e5-6d-49-20	PVZ82B7000490	6	1:6,2:6
ул.Волгоградская 5		6.5.1	192.168.124.38	1c-7e-e5-6d-4b-60	PVZ82B7000430	6	1:6,2:6

7 OK, obratny poradok


Не видно в 8
Жуковского 5		8.5.1	192.168.124.48	1c-7e-e5-6d-58-40	PVZ82B7000004	8	1:8,2:8


9 ок. но обратный порядок



vlan 21
 name CDE-RADIO-MGMT
!
vlan 22
 name CDE-MGMT
!
vlan 23
 name WIMAX-MGMT

vlan 155
 name OEZ-CHSZ-INET

vlan 129
 name Novikova-INET-VoIp

vlan 168
 name VNC_TEC2

vlan 176
 name Bist_INET-VoIP

!
vlan 178
 name Borino(JKH)-INET
                                                                                                                                                
vlan 579
 name Kondi-BSR-nlmk-INET                                                                                                                                                         

vlan 610
 name OEZ-TP-INET-VOIP
!
vlan 611
 name CHKINGDOM-ROSSIA-IPVPN

vlan 625
 name Liter(OEZ)-INET
                                                                                                                                                    
vlan 626
 name INET_BEKARD

vlan 803
 name LGEK-VPN
                                                                                                                                 
                                                                                                                                                             
vlan 817
 name STINOL

vlan 2024
 name city-bank-psi

vlan 3012
 name UVSK-2

vlan 3021
 name RemEnMet-L-INET


vlan 3032
 name Grazhd_pripasy_VOIP

vlan 3065
 name Lapina-Kamennoe-INET


vlan 3071
 name Anisimov
!
vlan 3073
 name PPT-Lipetsk

vlan 3082
 name Bekard-2-OEZ
                                                                                                                               
vlan 3997
 name pppoe_nlmk
                                                                                                                                                           
vlan 4007
 name KMN-VPN


 switchport trunk allowed vlan add 21-23,129,154,155,158,159,161,168,176,178,579
 switchport trunk allowed vlan add 608-612,625,626,803,817,953,954,2024,3012
 switchport trunk allowed vlan add 3021,3032,3064,3065,3071,3073,3082,3997,4007


  

config stp version rstp
config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 3 fbpdu disable hellotime 2 lbd enable lbd_recover_timer 60 nni_bpdu_addr dot1ad
config stp priority 4096 instance_id 0 
config stp mst_config_id name 00:22:B0:2B:64:00 revision_level 0
enable stp
config stp ports 1:1-1:20 externalCost auto  edge false p2p auto state enable restricted_role false restricted_tcn false lbd disable
config stp mst_ports 1:1-1:25 instance_id 0 internalCost auto priority 128
config stp ports 1:1-1:20 fbpdu enable
config stp ports 1:12-1:25 externalCost auto  edge true p2p auto state disable restricted_role false restricted_tcn false lbd disable
config stp ports 1:12-1:25 fbpdu disable

config stp ports 2:1-2:20 externalCost auto  edge false p2p auto state enable restricted_role false restricted_tcn false lbd disable
config stp mst_ports 2:1-2:25 instance_id 0 internalCost auto priority 128
config stp ports 2:1-2:20 fbpdu enable

config stp ports 2:12-2:25 externalCost auto  edge true p2p auto state disable restricted_role false restricted_tcn false lbd disable
config stp ports 2:12-2:25 fbpdu disable


map-class frame-relay policy768K
 frame-relay cir 768000
 frame-relay mincir 768000
!









495 747 51 41(42) Владимир Жаркий
20
24 порт агрегатор НЛМК
сфп со стороны

113.244
120.188 (24 порт)

ЛКБ Канал в Магнитагорск

top
left
right

											<div id="veryTopLeft">
												<jdoc:include type="modules" name="topleft" style="xhtml"/>
											</div>
											<div id="veryTopRight">
												<jdoc:include type="modules" name="topright" style="xhtml"/>
											</div>







                                                                    
config stp version rstp
enable stp                                                      
config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 6 fbpdu enable hellotime 2
config stp priority 32768 instance_id 0                                                   
config stp ports 1-24 externalCost auto edge true p2p auto state disable       
config stp mst_ports 1-28 instance_id 0 internalCost auto priority 128
config stp ports 1-24 fbpdu disable                                            
config stp ports 1-24 restricted_role true                                     
config stp ports 1-24 restricted_tcn true                                      
config stp ports 25-28 externalCost auto edge false p2p auto state enable      
config stp ports 25-28 fbpdu enable                                            
config stp ports 25-28 restricted_role false   








 config stp version rstp                                                        
 config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 3 fbpdu disable hellotime 2 lbd enable lbd_recover_timer 60
 config stp priority 16384 instance_id 0 
enable stp













                                                                                
 config stp version rstp                                                        
 config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 3 fbpdu disable hellotime 2 lbd enable lbd_recover_timer 60
 config stp priority 4096 instance_id 0                                        
 config stp mst_config_id name 00:22:B0:1B:EC:00 revision_level 0               
 enable stp                                                                     
 config stp ports 9-27 externalCost auto  edge false p2p auto state enable lbd disable
 config stp mst_ports 1-27 instance_id 0 internalCost auto priority 128         
config stp ports 1-20,22-24 fbpdu enable                                        
 config stp ports 21 externalCost auto  edge true p2p auto state disable lbd disable
config stp ports 21,25-27 fbpdu disable                                         
                                           
config stp priority 4096 instance_id 0
config stp ports 1-4 externalCost auto  edge true p2p auto state disable lbd disable 
config stp ports 9-27 externalCost auto edge true p2p auto state disable lbd disable
 config stp ports 5-8 externalCost auto  edge false p2p auto state enable lbd disable
config stp ports 5-8 fbpdu enable 


config stp ports 21 externalCost auto edge true p2p auto state disable lbd disable
config stp ports 1-20 externalCost auto edge false p2p auto state enable lbd disable
config stp ports 22-23 fbpdu enable

config stp ports 1-20 externalCost auto edge false p2p auto state enable lbd disable
config stp ports 22-24 externalCost auto edge false p2p auto state enable lbd disable

config stp ports 1-20 fbpdu enable
config stp ports 22-24 fbpdu enable





ip vrf vpn-sovintel-zenit
 description #VPN Sovintel Zenit
 rd 20866:413
 route-target export 20866:413
 route-target import 20866:413


interface GigabitEthernet0/0.2002
 description #IPVPN Sovintel-Zenit - Zenit-Side  #garry 07.06.2011
 encapsulation dot1Q 2002
 ip vrf forwarding vpn-sovintel-zenit
 ip address 192.168.229.105 255.255.255.252
 rate-limit input 512000 96000 192000 conform-action transmit exceed-action drop
 rate-limit output 512000 96000 192000 conform-action transmit exceed-action drop
 no cdp enable
end

  redistribute connected
  redistribute static

router bgp 20866
address-family ipv4 vrf vpn-sovintel-zenit









access-list 57 permit 192.168.113.1
access-list 57 permit 81.20.192.0 0.0.0.127
access-list 57 deny   any


snmp-server community public RO 57
snmp-server community Sh73ah91Kld RW 57
snmp-server ifindex persist
snmp-server contact bav@sc.ru
snmp-server enable traps snmp authentication linkdown linkup coldstart warmstart
snmp-server enable traps tty
snmp-server enable traps entity
snmp-server enable traps frame-relay
snmp-server enable traps frame-relay subif
snmp-server host 81.20.192.33 version 2c public 


interface GigabitEthernet0/0/2.51
 encapsulation dot1Q 51
 ip address 81.20.199.241 255.255.255.248
 service-policy type control ISG-CUSTOMERS-POLICY
 ip subscriber l2-connected
  initiator dhcp class-aware

interface GigabitEthernet0/0/2.51
 encapsulation dot1Q 1951 second-dot1q 51
 ip address 81.20.199.241 255.255.255.248
 service-policy type control ISG-CUSTOMERS-POLICY
 ip subscriber l2-connected
  initiator dhcp class-aware



ip route vrf sovintel-kredit-evropabank 0.0.0.0 0.0.0.0 10.128.2.14
ip route vrf sovintel-kredit-evropabank 10.126.138.0 255.255.255.0 10.128.2.17
ip route vrf sovintel-kredit-evropabank 10.128.64.0 255.255.255.0 10.128.2.17






001f.c644.7e3b
1C-BD-B9-65-FB-60
1cbdb965fb60
000400330001:00061cbdb965fb60

class-map type traffic match-any 20480
 match access-group input 195
 match access-group output 195

policy-map type service 20480
 200 class type traffic 20480
  accounting aaa list ISG-AUTH-1
  police input 2048000 384000 768000
  police output 2048000 384000 768000





class-map type traffic match-any 8096
 match access-group input 195
 match access-group output 195

policy-map type service 8096
 200 class type traffic 8096
  accounting aaa list ISG-AUTH-1
  police input 8192000 1536000 3072000
  police output 8192000 1536000 3072000






route-map ISG-nat permit 10
 description #PPTP NAT redirection
 match ip address 31
 set ip next-hop 81.20.192.11


access-list 31 remark NAT:packet redirect
access-list 31 permit 10.100.0.0 0.0.31.255


snmp-server community public RO 57
snmp-server community Sh73ah91Kld RW 57
snmp-server ifindex persist
snmp-server location CTD-S6
snmp-server contact bav@sc.ru
snmp-server enable traps snmp authentication linkdown linkup coldstart warmstart
snmp-server enable traps tty
snmp-server enable traps bgp
snmp-server enable traps entity
snmp-server enable traps frame-relay
snmp-server enable traps frame-relay subif
snmp-server enable traps mpls ldp
snmp-server enable traps mpls traffic-eng
snmp-server enable traps mpls vpn
snmp-server host 81.20.192.33 version 2c public 

ntp clock-period 17180286
ntp access-group peer 30
ntp server 81.20.192.19 prefer


access-list 57 permit 192.168.113.1
access-list 57 permit 81.20.192.0 0.0.0.127
access-list 57 deny   any


logging facility local6
logging 81.20.192.19




ip address 172.28.0.1 255.255.255.0
access-list 31 remark NAT:packet redirect
access-list 31 permit 172.20.252.0 0.0.0.255



-A POSTROUTING -s 192.168.1.0/24 -o vlan10 -j SNAT --to-source 81.20.198.190 




conf t
interface GigabitEthernet0/0/2.195153
  encapsulation dot1Q 1951 second-dot1q 53
  ip unnumbered Loopback1
  service-policy type control ISG-CUSTOMERS-POLICY
  ip subscriber l2-connected
    initiator dhcp class-aware
end



 description #Pool Public Address
 ip address 81.20.199.241 255.255.255.248


privilege interface level 5 description
privilege interface level 5 ip
privilege interface level 5 ip address
privilege interface level 5 service-policy
privilege interface level 5 ip unnumbered
privilege interface level 5 no ip unnumbered
privilege interface level 5 encapsulation
privilege interface level 5 initiator dhcp class-aware
privilege configure level 5 interface
privilege exec level 5 configure terminal
privilege exec level 5 show running-config
privilege exec level 5 show interface
privilege exec level 5 write memory
privilege exec level 5 show




 encapsulation dot1Q 1951 second-dot1q 52
 ip unnumbered Loopback2
 service-policy type control ISG-CUSTOMERS-POLICY
 ip subscriber l2-connected
  initiator dhcp class-aware


bill
private


description Zyxel-Voip-Test
 encapsulation dot1Q 130
 ip address 192.168.130.177 255.255.255.252
 ip verify unicast reverse-path
 ip flow ingress
 ip flow egress
 rate-limit input 296000 57000 114000 conform-action transmit exceed-action drop
 rate-limit output 296000 57000 114000 conform-action transmit exceed-action drop
 no snmp trap link-status
 no cdp enable


access-list 11 permit 172.20.252.0 0.0.0.255
access-list 11 deny   any


ip nat inside source list 11 interface Loopback0 overload

interface Loopback0
 description # NAT interface
 ip address 81.20.196.107 255.255.255.255
end


ip dhcp pool private
 network 172.20.96.0 255.255.224.0
 dns-server 81.20.192.16 
 default-router 172.20.96.1 
 lease 0 2

81.20.192.49

route-map pptp-nat permit 10
 description #PPTP NAT redirection
 match ip address 31
 set ip next-hop 192.168.200.1

access-list 31 permit 172.20.252.0 0.0.0.255
access-list 31 deny   any

ip prefix-list no-sc-local-distribution seq 2 deny 172.20.96.0/19


ip policy route-map pptp-nat



ip route vrf tusom-vpn 0.0.0.0 0.0.0.0 10.255.246.109
ip route vrf tusom-vpn 10.129.200.0 255.255.255.0 10.255.250.109







interface GigabitEthernet0/1.1021
 description PPTP-NAT-Server
 encapsulation dot1Q 1021
 ip address 192.168.200.3 255.255.255.248
 ip flow ingress
end


router ospf 200
 router-id 192.168.200.4
 log-adjacency-changes
 redistribute connected subnets route-map redist_bras_int
 passive-interface default
 no passive-interface GigabitEthernet0/0/2.1021
 network 192.168.200.0 0.0.0.7 area 0.0.0.1
 distribute-list route-map dist_bras_int in



!         
route-map redist_bras_int permit 10
 match ip address 31
!         
route-map dist_bras_int permit 10
 match ip address 32
!   

access-list 31 remark PPTP:packet redirect
access-list 31 permit 172.20.96.0 0.0.31.255
access-list 31 deny   any
access-list 32 deny   any


-A forward_ext -d 81.20.192.0/20 -i vlan10 -o vlan1021 -m state --state RELATED,ESTABLISHED -j ACCEPT
-A forward_ext -d 81.20.192.0/20 -i vlan10 -o vlan11 -m state --state RELATED,ESTABLISHED -j ACCEPT
-A forward_ext -d 81.20.192.0/20 -i vlan10 -o eth0 -m state --state RELATED,ESTABLISHED -j ACCEPT
-A forward_ext -d 81.20.192.0/20 -i vlan10 -o eth1 -m state --state RELATED,ESTABLISHED -j ACCEPT
-A forward_ext -d 172.20.96.0/19 -i vlan10 -o vlan1021 -m state --state RELATED,ESTABLISHED -j ACCEPT
-A forward_ext -d 172.20.96.0/19 -i vlan10 -o vlan11 -m state --state RELATED,ESTABLISHED -j ACCEPT
-A forward_ext -d 172.20.96.0/19 -i vlan10 -o eth0 -m state --state RELATED,ESTABLISHED -j ACCEPT
-A forward_ext -d 172.20.96.0/19 -i vlan10 -o eth1 -m state --state RELATED,ESTABLISHED -j ACCEPT



-A forward_int -s 81.20.192.0/20 -i vlan1021 -o vlan10 -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT
-A forward_int -s 81.20.192.0/20 -i vlan11 -o vlan10 -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT
-A forward_int -s 81.20.192.0/20 -i eth0 -o vlan10 -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT
-A forward_int -s 81.20.192.0/20 -i eth1 -o vlan10 -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT
-A forward_int -s 172.20.96.0/19 -i vlan1021 -o vlan10 -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT
-A forward_int -s 172.20.96.0/19 -i vlan11 -o vlan10 -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT
-A forward_int -s 172.20.96.0/19 -i eth0 -o vlan10 -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT
-A forward_int -s 172.20.96.0/19 -i eth1 -o vlan10 -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT




/bin/sh /root/iptables.sh


#!/bin/bash
/usr/sbin/iptables-restore < /root/work/ipts_work_last

access-list 56 permit 172.19.5.200
access-list 56 deny   any
access-list 57 permit 10.192.10.190
access-list 57 deny   any
!
!
n snmp-server community KrE98DsVf RO 56
snmp-server community Sh73ah91Kld RW 57
snmp-server ifindex persist
snmp-server contact a.bukreev@promsvyaz.ru










ip route 0.0.0.0 0.0.0.0 81.20.192.11
iptables -t nat -A POSTROUTING -s 172.20.252.0/24 -o vlan10 -j SNAT --to-source 81.20.198.190






router ospf 110
 router-id 81.20.192.51
 limit retransmissions non-dc disable
 redistribute connected metric 1 subnets
 redistribute static metric 1 subnets
 passive-interface default
 no passive-interface GigabitEthernet0/0/2.13
 no passive-interface GigabitEthernet0/0/2.2022
 network 81.20.192.48 0.0.0.15 area 0
 network 81.20.192.112 0.0.0.3 area 0
 distribute-list prefix no-sc-local-distribution out





ip vrf rtk-psi-gazbank
 description #GazEnergoPromBank-IPVPN
 rd 20866:302
 route-target export 20866:3020
 route-target import 20866:3020
 maximum routes 500 100



interface GigabitEthernet0/0.770
 description # GazEnergoPromBank IPVPN (RTK) # Woland 13.01.2009
 encapsulation dot1Q 770
 ip vrf forwarding rtk-psi-gazbank
 ip address 10.19.251.6 255.255.255.252
 ip flow ingress
 rate-limit input 2048000 386000 776000 conform-action transmit exceed-action drop
 rate-limit output 2048000 386000 776000 conform-action transmit exceed-action drop
 no cdp enable
!

 address-family ipv4 vrf rtk-psi-gazbank
  redistribute connected
  redistribute static
  default-information originate
  no synchronization
 exit-address-family


interface GigabitEthernet0/0.774
 encapsulation dot1Q 774
 ip vrf forwarding rtk-psi-gazbank
 ip address 10.19.251.1 255.255.255.252
 ip flow ingress
 rate-limit input 2048000 386000 776000 conform-action transmit exceed-action drop
 rate-limit output 2048000 386000 776000 conform-action transmit exceed-action drop
 no cdp enable





 address-family ipv4 vrf alpha-zegelya
 redistribute connected
 redistribute static
 neighbor 172.26.24.141 remote-as 64543
 neighbor 172.26.24.141 activate
 neighbor 172.26.24.145 remote-as 65007
 neighbor 172.26.24.145 activate
 no auto-summary
 no synchronization
 exit-address-family



ip vrf rtk-psi-gazbank
 description #GazEnergoPromBank-IPVPN
 rd 20866:302
 route-target export 20866:3020
 route-target import 20866:3020
 maximum routes 500 100


 address-family ipv4 vrf rtk-psi-gazbank
  redistribute connected
  redistribute static
  default-information originate
  no synchronization
 exit-address-family




 address-family ipv4 vrf rtk-psi-gazbank
  redistribute connected
  redistribute static
   no synchronization
 exit-address-family




ip vrf rtk-psi-gazbank
 description #GazEnergoPromBank-IPVPN
 rd 20866:302
 route-target export 20866:3020
 route-target import 20866:3020
 maximum routes 500 100









ip vrf rtk-psi-abrossia
 description #AB Rossia VPN #It was GazEnergoPromBank
 rd 20866:317
 route-target export 20866:3170
 route-target import 20866:3170
 maximum routes 500 100


interface GigabitEthernet0/0.801
 description # AB Rossia VPN #GazEnergoPromBank IPVPN (RTK) # garry 30.09.2011
 encapsulation dot1Q 801
 ip vrf forwarding rtk-psi-abrossia
 ip address 10.19.251.14 255.255.255.252
 ip flow ingress
 rate-limit input 2048000 386000 776000 conform-action transmit exceed-action drop
 rate-limit output 2048000 386000 776000 conform-action transmit exceed-action drop
 no cdp enable

 address-family ipv4 vrf rtk-psi-abrossia
  redistribute connected
  redistribute static
  default-information originate
  no synchronization
 exit-address-family

ip route vrf rtk-psi-abrossia 0.0.0.0 0.0.0.0 10.19.251.13







ip vrf rtk-psi-abrossia
 description #AB Rossia VPN #It was GazEnergoPromBank
 rd 20866:317
 route-target export 20866:3170
 route-target import 20866:3170
 maximum routes 500 100



interface FastEthernet0/0.2004
 description #AB Rossia #Gazenergobank
 encapsulation dot1Q 2004
 ip vrf forwarding rtk-psi-abrossia
 ip address 10.19.251.9 255.255.255.252
 ip flow ingress
 no cdp enable

 address-family ipv4 vrf rtk-psi-abrossia
 redistribute connected
 redistribute static
 default-information originate
 no auto-summary
 no synchronization
 exit-address-family
 



1C-BD-B9-65-FA-E0
1cbdb965fae0











Jun 15 08:29:13.954: DHCPD: checking for expired ldhcp binding 
Jun 15 08:29:24.104: DHCPD: dhcpd_lookup_route: host = 172.20.96.3
Jun 15 08:29:24.104: DHCPD: dhcpd_lookup_route: index = 219
Jun 15 08:29:24.104: DHCPD: Binding output intf GigabitEthernet0/0/2.13 is updated to GigabitEthernet0/0/2.51
Jun 15 08:29:24.104: DHCPD: dhcpd_lookup_route: host = 172.20.96.3
Jun 15 08:29:24.104: DHCPD: dhcpd_lookup_route: index = 219
Jun 15 08:29:24.104:  DHCPD: Deleting existing route to host 172.20.96.3
Jun 15 08:29:24.104: DHCPD: dhcpd_delete_route: index = 219
Jun 15 08:29:24.104: DHCPD: dhcpd_create_and_hash_route: host = 172.20.96.3
Jun 15 08:29:24.104: DHCPD: dhcpd_create_and_hash_route index = 219
Jun 15 08:29:24.104: DHCPD: dhcpd_add_route: lease = 7107 
Jun 15 08:29:24.104: DHCPD: input i/f override GigabitEthernet0/0/2.51 for client
Jun 15 08:29:24.108: DHCPD: dhcpd_lookup_route: host = 172.20.96.3
Jun 15 08:29:24.108: DHCPD: dhcpd_lookup_route: index = 219
Jun 15 08:29:24.108: DHCPD: Binding output intf GigabitEthernet0/0/2.51 is updated to GigabitEthernet0/0/2.13
Jun 15 08:29:24.108: DHCPD: dhcpd_lookup_route: host = 172.20.96.3
Jun 15 08:29:24.108: DHCPD: dhcpd_lookup_route: index = 219
Jun 15 08:29:24.108:  DHCPD: Deleting existing route to host 172.20.96.3
Jun 15 08:29:24.108: DHCPD: dhcpd_delete_route: index = 219
Jun 15 08:29:24.108: DHCPD: dhcpd_create_and_hash_route: host = 172.20.96.3
Jun 15 08:29:24.108: DHCPD: dhcpd_create_and_hash_route index = 219
Jun 15 08:29:24.108: DHCPD: dhcpd_add_route: lease = 7107 
Jun 15 08:29:24.108: DHCPD: input i/f override GigabitEthernet0/0/2.13 for client
Jun 15 08:29:24.108: DHCPD: unicast BOOTREPLY output i/f override GigabitEthernet0/0/2.13
Jun 15 08:29:35.491: DHCPD: dhcpd_lookup_route: host = 172.20.96.3
Jun 15 08:29:35.491: DHCPD: dhcpd_lookup_route: index = 219
Jun 15 08:29:35.491: DHCPD: Binding output intf GigabitEthernet0/0/2.13 is updated to GigabitEthernet0/0/2.51
Jun 15 08:29:35.491: DHCPD: dhcpd_lookup_route: host = 172.20.96.3
Jun 15 08:29:35.491: DHCPD: dhcpd_lookup_route: index = 219
Jun 15 08:29:35.491:  DHCPD: Deleting existing route to host 172.20.96.3
Jun 15 08:29:35.491: DHCPD: dhcpd_delete_route: index = 219
Jun 15 08:29:35.491: DHCPD: dhcpd_create_and_hash_route: host = 172.20.96.3
Jun 15 08:29:35.492: DHCPD: dhcpd_create_and_hash_route index = 219
Jun 15 08:29:35.492: DHCPD: dhcpd_add_route: lease = 7096 
Jun 15 08:29:35.492: DHCPD: input i/f override GigabitEthernet0/0/2.51 for client
Jun 15 08:29:35.492: DHCPD: Sending notification of TERMINATION:
Jun 15 08:29:35.492:  DHCPD: address 172.20.96.3 mask 255.255.224.0
Jun 15 08:29:35.492:  DHCPD: reason flags: RELEASE 
Jun 15 08:29:35.492:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:35.492:   DHCPD: lease time remaining (secs) = 7096
Jun 15 08:29:35.492:   DHCPD: interface = GigabitEthernet0/0/2.51
Jun 15 08:29:35.494: DHCPD: dhcpd_lookup_route: host = 172.20.96.3
Jun 15 08:29:35.494: DHCPD: dhcpd_lookup_route: index = 219
Jun 15 08:29:35.494: DHCPD: dhcpd_delete_route: index = 219
Jun 15 08:29:35.494: DHCPD: returned 172.20.96.3 to address pool private.
Jun 15 08:29:35.494: DHCPD: Received DHCPRELEASE on UNNUM-IF
Jun 15 08:29:35.494: DHCPD: dhcpd_lookup_route: host = 172.20.96.3
Jun 15 08:29:35.494: DHCPD: dhcpd_lookup_route: index = 219
Jun 15 08:29:35.494: DHCPD: Route block NOT found for 172.20.96.3
Jun 15 08:29:35.503: DHCPD: there is no pool for 192.168.120.104.
Jun 15 08:29:41.194: DHCPD: Sending notification of DISCOVER:
Jun 15 08:29:41.194:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:41.194:   DHCPD: remote id 00061cbdb965fb60
Jun 15 08:29:41.194:   DHCPD: circuit id 000400330001
Jun 15 08:29:41.194:   DHCPD: interface = GigabitEthernet0/0/2.51
Jun 15 08:29:41.194:   DHCPD: class id 4d53465420352e30
Jun 15 08:29:41.194: DHCPD: Sending notification of DISCOVER:
Jun 15 08:29:41.194:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:41.194:   DHCPD: remote id 00061cbdb965fb60
Jun 15 08:29:41.194:   DHCPD: circuit id 000400330001
Jun 15 08:29:41.194:   DHCPD: interface = GigabitEthernet0/0/2.51
Jun 15 08:29:41.194:   DHCPD: class id 4d53465420352e30
Jun 15 08:29:41.197: DHCPD: input i/f override GigabitEthernet0/0/2.13 for client
Jun 15 08:29:41.197: DHCPD: Sending notification of DISCOVER:
Jun 15 08:29:41.197:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:41.197:   DHCPD: giaddr = 192.168.120.104
Jun 15 08:29:41.197:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 15 08:29:41.197:   DHCPD: class id 4d53465420352e30
Jun 15 08:29:41.197: DHCPD: Sending notification of DISCOVER:
Jun 15 08:29:41.197:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:41.197:   DHCPD: giaddr = 192.168.120.104
Jun 15 08:29:41.197:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 15 08:29:41.197:   DHCPD: class id 4d53465420352e30
Jun 15 08:29:41.197: DHCPD: No internally specified class returned
Jun 15 08:29:41.197: DHCPD: there is no address pool for 192.168.120.104.
Jun 15 08:29:41.197: DHCPD: Sending notification of ASSIGNMENT FAILURE:
Jun 15 08:29:41.197:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:41.197:   DHCPD: remote id 020a00005114c0330200000d
Jun 15 08:29:41.197:   DHCPD: giaddr = 192.168.120.104
Jun 15 08:29:41.197:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 15 08:29:41.197:   DHCPD: class id 4d53465420352e30
Jun 15 08:29:41.197: DHCPD: Sending notification of ASSIGNMENT_FAILURE:
Jun 15 08:29:41.197:  DHCPD: due to: NO POOL
Jun 15 08:29:41.197:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:41.197:   DHCPD: remote id 020a00005114c0330200000d
Jun 15 08:29:41.197:   DHCPD: giaddr = 192.168.120.104
Jun 15 08:29:41.197:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 15 08:29:41.197:   DHCPD: class id 4d53465420352e30
Jun 15 08:29:44.179: DHCPD: input i/f override GigabitEthernet0/0/2.51 for client
Jun 15 08:29:44.180: DHCPD: Sending notification of DISCOVER:
Jun 15 08:29:44.180:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:44.180:   DHCPD: remote id 00061cbdb965fb60
Jun 15 08:29:44.180:   DHCPD: circuit id 000400330001
Jun 15 08:29:44.180:   DHCPD: interface = GigabitEthernet0/0/2.51
Jun 15 08:29:44.180:   DHCPD: class id 4d53465420352e30
Jun 15 08:29:44.180: DHCPD: Sending notification of DISCOVER:
Jun 15 08:29:44.180:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:44.180:   DHCPD: remote id 00061cbdb965fb60
Jun 15 08:29:44.180:   DHCPD: circuit id 000400330001
Jun 15 08:29:44.180:   DHCPD: interface = GigabitEthernet0/0/2.51
Jun 15 08:29:44.180:   DHCPD: class id 4d53465420352e30
Jun 15 08:29:44.180: DHCPD: No internally specified class returned
Jun 15 08:29:44.180: DHCPD: client requests 172.20.96.3.
Jun 15 08:29:44.180: DHCPD: Adding binding to radix tree (172.20.96.3)
Jun 15 08:29:44.180: DHCPD: Adding binding to hash tree
Jun 15 08:29:44.180: DHCPD: assigned IP address 172.20.96.3 to client 0188.ae1d.8393.53.
Jun 15 08:29:44.181: DHCPD: input i/f override GigabitEthernet0/0/2.13 for client
Jun 15 08:29:44.181: DHCPD: Sending notification of DISCOVER:
Jun 15 08:29:44.181:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:44.181:   DHCPD: giaddr = 192.168.120.104
Jun 15 08:29:44.181:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 15 08:29:44.181:   DHCPD: class id 4d53465420352e30
Jun 15 08:29:44.181: DHCPD: Sending notification of DISCOVER:
Jun 15 08:29:44.181:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:44.181:   DHCPD: giaddr = 192.168.120.104
Jun 15 08:29:44.181:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 15 08:29:44.181:   DHCPD: class id 4d53465420352e30
Jun 15 08:29:44.181: DHCPD: No internally specified class returned
Jun 15 08:29:44.181: DHCPD: there is no address pool for 192.168.120.104.
Jun 15 08:29:44.181: DHCPD: Sending notification of ASSIGNMENT FAILURE:
Jun 15 08:29:44.181:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:44.181:   DHCPD: remote id 020a00005114c0330200000d
Jun 15 08:29:44.181:   DHCPD: giaddr = 192.168.120.104
Jun 15 08:29:44.181:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 15 08:29:44.181:   DHCPD: class id 4d53465420352e30
Jun 15 08:29:44.181: DHCPD: Sending notification of ASSIGNMENT_FAILURE:
Jun 15 08:29:44.181:  DHCPD: due to: NO POOL
Jun 15 08:29:44.181:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:44.181:   DHCPD: remote id 020a00005114c0330200000d
Jun 15 08:29:44.181:   DHCPD: giaddr = 192.168.120.104
Jun 15 08:29:44.181:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 15 08:29:44.181:   DHCPD: class id 4d53465420352e30
Jun 15 08:29:46.179: DHCPD: Sending notification of DISCOVER:
Jun 15 08:29:46.179:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:46.179:   DHCPD: remote id 00061cbdb965fb60
Jun 15 08:29:46.179:   DHCPD: circuit id 000400330001
Jun 15 08:29:46.179:   DHCPD: interface = GigabitEthernet0/0/2.51
Jun 15 08:29:46.179:   DHCPD: class id 4d53465420352e30
Jun 15 08:29:46.180: DHCPD: Found previous server binding
Jun 15 08:29:46.180: DHCPD: requested address 172.20.96.3 has already been assigned.
Jun 15 08:29:46.180: DHCPD: DHCPOFFER notify setup address 172.20.96.3 mask 255.255.224.0
Jun 15 08:29:46.184: DHCPD: Callback for workspace (ID=0xA6000040)
Jun 15 08:29:46.184: DHCPD: Callback: switching path now setup for client 0188.ae1d.8393.53
Jun 15 08:29:46.184: DHCPD: Sending notification of DISCOVER:
Jun 15 08:29:46.184:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:46.184:   DHCPD: remote id 00061cbdb965fb60
Jun 15 08:29:46.184:   DHCPD: circuit id 000400330001
Jun 15 08:29:46.184:   DHCPD: interface = GigabitEthernet0/0/2.51
Jun 15 08:29:46.184:   DHCPD: class id 4d53465420352e30
Jun 15 08:29:46.184: DHCPD: Found previous server binding
Jun 15 08:29:46.184: DHCPD: requested address 172.20.96.3 has already been assigned.
Jun 15 08:29:46.184: DHCPD: unicast BOOTREPLY output i/f override GigabitEthernet0/0/2.13
Jun 15 08:29:52.179: DHCPD: dhcpd_lookup_route: host = 172.20.96.3
Jun 15 08:29:52.180: DHCPD: dhcpd_lookup_route: index = 219
Jun 15 08:29:52.180: DHCPD: Unable to locate route for 172.20.96.3 
Jun 15 08:29:52.180: DHCPD: input i/f override GigabitEthernet0/0/2.51 for client
Jun 15 08:29:52.180: DHCPD: Sending notification of DISCOVER:
Jun 15 08:29:52.180:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:52.180:   DHCPD: remote id 00061cbdb965fb60
Jun 15 08:29:52.180:   DHCPD: circuit id 000400330001
Jun 15 08:29:52.180:   DHCPD: interface = GigabitEthernet0/0/2.51
Jun 15 08:29:52.180:   DHCPD: class id 4d53465420352e30
Jun 15 08:29:52.180: DHCPD: Sending notification of DISCOVER:
Jun 15 08:29:52.180:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:52.180:   DHCPD: remote id 00061cbdb965fb60
Jun 15 08:29:52.180:   DHCPD: circuit id 000400330001
Jun 15 08:29:52.180:   DHCPD: interface = GigabitEthernet0/0/2.51
Jun 15 08:29:52.180:   DHCPD: class id 4d53465420352e30
Jun 15 08:29:52.180: DHCPD: No internally specified class returned
Jun 15 08:29:52.180: DHCPD: Found previous server binding
Jun 15 08:29:52.180: DHCPD: requested address 172.20.96.3 has already been assigned.
Jun 15 08:29:52.180: DHCPD: DHCPOFFER notify setup address 172.20.96.3 mask 255.255.224.0
Jun 15 08:29:52.181: DHCPD: Callback for workspace (ID=0xC7000041)
Jun 15 08:29:52.181: DHCPD: Callback: switching path now setup for client 0188.ae1d.8393.53
Jun 15 08:29:52.181: DHCPD: Sending notification of DISCOVER:
Jun 15 08:29:52.181:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:52.181:   DHCPD: remote id 00061cbdb965fb60
Jun 15 08:29:52.181:   DHCPD: circuit id 000400330001
Jun 15 08:29:52.181:   DHCPD: interface = GigabitEthernet0/0/2.51
Jun 15 08:29:52.181:   DHCPD: class id 4d53465420352e30
Jun 15 08:29:52.181: DHCPD: Found previous server binding
Jun 15 08:29:52.181: DHCPD: requested address 172.20.96.3 has already been assigned.
Jun 15 08:29:52.181: DHCPD: unicast BOOTREPLY output i/f override GigabitEthernet0/0/2.51
Jun 15 08:29:52.182: DHCPD: dhcpd_lookup_route: host = 172.20.96.3
Jun 15 08:29:52.182: DHCPD: dhcpd_lookup_route: index = 219
Jun 15 08:29:52.182: DHCPD: Unable to locate route for 172.20.96.3 
Jun 15 08:29:52.182: DHCPD: input i/f override GigabitEthernet0/0/2.13 for client
Jun 15 08:29:52.182: DHCPD: Sending notification of DISCOVER:
Jun 15 08:29:52.182:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:52.182:   DHCPD: giaddr = 192.168.120.104
Jun 15 08:29:52.183:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 15 08:29:52.183:   DHCPD: class id 4d53465420352e30
Jun 15 08:29:52.183: DHCPD: Sending notification of DISCOVER:
Jun 15 08:29:52.183:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:52.183:   DHCPD: giaddr = 192.168.120.104
Jun 15 08:29:52.183:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 15 08:29:52.183:   DHCPD: class id 4d53465420352e30
Jun 15 08:29:52.183: DHCPD: No internally specified class returned
Jun 15 08:29:52.183: DHCPD: there is no address pool for 192.168.120.104.
Jun 15 08:29:52.183: DHCPD: Sending notification of ASSIGNMENT FAILURE:
Jun 15 08:29:52.183:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:52.183:   DHCPD: remote id 020a00005114c0330200000d
Jun 15 08:29:52.183:   DHCPD: giaddr = 192.168.120.104
Jun 15 08:29:52.183:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 15 08:29:52.183:   DHCPD: class id 4d53465420352e30
Jun 15 08:29:52.183: DHCPD: Sending notification of ASSIGNMENT_FAILURE:
Jun 15 08:29:52.183:  DHCPD: due to: NO POOL
Jun 15 08:29:52.183:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:52.183:   DHCPD: remote id 020a00005114c0330200000d
Jun 15 08:29:52.183:   DHCPD: giaddr = 192.168.120.104
Jun 15 08:29:52.183:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 15 08:29:52.183:   DHCPD: class id 4d53465420352e30
Jun 15 08:29:52.191: DHCPD: dhcpd_lookup_route: host = 172.20.96.3
Jun 15 08:29:52.191: DHCPD: dhcpd_lookup_route: index = 219
Jun 15 08:29:52.191: DHCPD: Unable to locate route for 172.20.96.3 
Jun 15 08:29:52.191: DHCPD: input i/f override GigabitEthernet0/0/2.51 for client
Jun 15 08:29:52.191: DHCPD: Sending notification of ASSIGNMENT:
Jun 15 08:29:52.191:  DHCPD: address 172.20.96.3 mask 255.255.224.0
Jun 15 08:29:52.191:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:52.191:   DHCPD: remote id 00061cbdb965fb60
Jun 15 08:29:52.191:   DHCPD: circuit id 000400330001
Jun 15 08:29:52.191:   DHCPD: lease time remaining (secs) = 7200
Jun 15 08:29:52.191:   DHCPD: interface = GigabitEthernet0/0/2.51
Jun 15 08:29:52.192: DHCPD: Updating DPM hdl in DHCP binding for 172.20.96.3 
Jun 15 08:29:52.192:  DHCPD: lease time = 7200
Jun 15 08:29:52.192: DHCPD: dhcpd_lookup_route: host = 172.20.96.3
Jun 15 08:29:52.192: DHCPD: dhcpd_lookup_route: index = 219
Jun 15 08:29:52.192: DHCPD: dhcpd_create_and_hash_route: host = 172.20.96.3
Jun 15 08:29:52.192: DHCPD: dhcpd_create_and_hash_route index = 219
Jun 15 08:29:52.192: DHCPD: dhcpd_add_route: lease = 7200 
Jun 15 08:29:52.192: DHCPD: unicast BOOTREPLY output i/f override GigabitEthernet0/0/2.51
Jun 15 08:29:52.195: DHCPD: dhcpd_lookup_route: host = 172.20.96.3
Jun 15 08:29:52.195: DHCPD: dhcpd_lookup_route: index = 219
Jun 15 08:29:52.195: DHCPD: Binding output intf GigabitEthernet0/0/2.51 is updated to GigabitEthernet0/0/2.13
Jun 15 08:29:52.195: DHCPD: dhcpd_lookup_route: host = 172.20.96.3
Jun 15 08:29:52.195: DHCPD: dhcpd_lookup_route: index = 219
Jun 15 08:29:52.195:  DHCPD: Deleting existing route to host 172.20.96.3
Jun 15 08:29:52.195: DHCPD: dhcpd_delete_route: index = 219
Jun 15 08:29:52.196: DHCPD: dhcpd_create_and_hash_route: host = 172.20.96.3
Jun 15 08:29:52.196: DHCPD: dhcpd_create_and_hash_route index = 219
Jun 15 08:29:52.196: DHCPD: dhcpd_add_route: lease = 7200 
Jun 15 08:29:52.196: DHCPD: input i/f override GigabitEthernet0/0/2.13 for client
Jun 15 08:29:52.196: DHCPD: Sending notification of ASSIGNMENT:
Jun 15 08:29:52.196:  DHCPD: address 172.20.96.3 mask 255.255.224.0
Jun 15 08:29:52.196:   DHCPD: htype 1 chaddr 88ae.1d83.9353
Jun 15 08:29:52.196:   DHCPD: remote id 00061cbdb965fb60
Jun 15 08:29:52.196:   DHCPD: circuit id 000400330001
Jun 15 08:29:52.196:   DHCPD: lease time remaining (secs) = 7200
Jun 15 08:29:52.196:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 15 08:29:52.196: DHCPD: Updating DPM hdl in DHCP binding for 172.20.96.3 
Jun 15 08:29:52.196: DHCPD: unicast BOOTREPLY output i/f override GigabitEthernet0/0/2.13


Jun 16 12:57:23.228: DHCPD: Sending notification of DISCOVER:
Jun 16 12:57:23.228:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 12:57:23.228:   DHCPD: remote id 00061cbdb965fae0
Jun 16 12:57:23.228:   DHCPD: circuit id 000400340002
Jun 16 12:57:23.228:   DHCPD: giaddr = 192.168.120.105
Jun 16 12:57:23.228:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 12:57:23.228:   DHCPD: class id 4d53465420352e30
Jun 16 12:57:23.228: DHCPD: there is no address pool for 192.168.120.105.
Jun 16 12:57:23.228: DHCPD: Sending notification of ASSIGNMENT FAILURE:
Jun 16 12:57:23.228:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 12:57:23.228:   DHCPD: remote id 020a00005114c0330200000d
Jun 16 12:57:23.228:   DHCPD: giaddr = 192.168.120.105







108   0000-00-00 00:00:39 Safeguard Engine enters NORMAL mode
107   0000-00-00 00:00:37 System cold start
106   0000-00-00 00:00:34 Safeguard Engine enters EXHAUSTED mode
105   0000-00-00 00:00:32 Port 26 link up, 1000Mbps  FULL duplex
104   0000-00-00 00:00:32 Port 25 link up, 1000Mbps  FULL duplex

108   0000-00-00 00:00:39 Safeguard Engine enters NORMAL mode
107   0000-00-00 00:00:37 System cold start
106   0000-00-00 00:00:34 Safeguard Engine enters EXHAUSTED mode
105   0000-00-00 00:00:32 Port 26 link up, 1000Mbps  FULL duplex
104   0000-00-00 00:00:32 Port 25 link up, 1000Mbps  FULL duplex
103   2011-06-24 10:45:47 Topology changed (Instance:0 port:25)
102   2011-06-22 17:17:03 Topology changed (Instance:0 port:25)
101   2011-06-22 15:17:07 Topology changed (Instance:0 port:25)
100   2011-06-22 15:15:47 Topology changed (Instance:0 port:25)
99    2011-06-22 15:13:39 Topology changed (Instance:0 port:25)                
98    2011-06-22 15:12:49 Topology changed (Instance:0 port:25)
97    2011-06-22 14:44:19 Topology changed (Instance:0 port:25)
96    2011-06-20 16:18:29 Topology changed (Instance:0 port:25)
95    2011-06-20 13:44:46 Topology changed (Instance:0 port:25)
94    2011-06-20 13:35:35 Topology changed (Instance:0 port:25)
93    2011-06-17 18:41:51 Topology changed (Instance:0 port:25)
92    2011-06-17 18:24:51 Topology changed (Instance:0 port:25)
91    2011-06-17 18:24:39 Topology changed (Instance:0 port:25)
90    2011-06-17 18:24:02 Topology changed (Instance:0 port:25)
89    2011-06-17 18:23:17 Topology changed (Instance:0 port:25)
88    2011-06-17 18:22:39 Topology changed (Instance:0 port:25)
87    2011-06-17 18:12:09 Topology changed (Instance:0 port:25)
86    2011-06-17 18:12:06 Topology changed (Instance:0 port:25)
85    2011-06-16 20:49:53 Topology changed (Instance:0 port:26)
84    2011-06-16 20:26:53 Topology changed (Instance:0 port:26)
83    2011-06-15 16:09:38 Topology changed (Instance:0 port:26)
82    2011-06-11 18:10:21 Topology changed (Instance:0 port:26)
81    2011-06-10 17:34:38 Topology changed (Instance:0 port:26)
80    2011-06-09 10:57:41 Topology changed (Instance:0 port:26)
79    2011-06-09 10:55:45 Topology changed (Instance:0 port:26)
78    2011-06-08 15:59:53 Topology changed (Instance:0 port:26)
77    2011-06-08 15:22:39 Topology changed (Instance:0 port:26)                
76    2011-06-08 11:57:33 Topology changed (Instance:0 port:26)
75    2011-06-08 11:38:11 Topology changed (Instance:0 port:26)
74    2011-06-07 10:15:47 Topology changed (Instance:0 port:26)
73    2011-06-07 10:14:08 Topology changed (Instance:0 port:26)
72    2011-06-07 10:13:45 Topology changed (Instance:0 port:26)
71    2011-06-07 10:07:55 Topology changed (Instance:0 port:25)









115   0000-00-00 00:00:40 Safeguard Engine enters NORMAL mode
114   0000-00-00 00:00:38 System cold start
113   0000-00-00 00:00:35 Safeguard Engine enters EXHAUSTED mode
112   0000-00-00 00:00:33 Port 26 link up, 1000Mbps  FULL duplex
111   0000-00-00 00:00:33 Port 25 link up, 1000Mbps  FULL duplex
110   2011-06-24 10:45:47 Topology changed (Instance:0 port:25)




current
disable stp
config stp version rstp
config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 6 fbpdu enable hellotime 2
config stp priority 32768 instance_id 0 
config stp mst_config_id name 1C:BD:B9:64:94:60 revision_level 0
config stp ports 1-24 externalCost auto edge true p2p auto state disable
config stp mst_ports 1-28 instance_id 0 internalCost auto priority 128
config stp ports 1-24 fbpdu disable
config stp ports 1-24 restricted_role true                                     
config stp ports 1-24 restricted_tcn true
config stp ports 25-28 externalCost auto edge false p2p auto state enable
config stp ports 25-28 fbpdu enable
config stp ports 25-28 restricted_role false
config stp ports 25-28 restricted_tcn false







in-nvram
enable stp
config stp version rstp
config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 6 fbpdu enable hellotime 2
config stp priority 32768 instance_id 0 
config stp mst_config_id name 1C:BD:B9:64:94:60 revision_level 0
config stp ports 1-24 externalCost auto edge true p2p auto state disable
config stp mst_ports 1-28 instance_id 0 internalCost auto priority 128
config stp ports 1-24 fbpdu disable
config stp ports 1-24 restricted_role true
config stp ports 1-24 restricted_tcn true
config stp ports 25-28 externalCost auto edge false p2p auto state enable
config stp ports 25-28 fbpdu enable
config stp ports 25-28 restricted_role false
config stp ports 25-28 restricted_tcn false







config stp ports 1-24 restricted_role true
config stp ports 1-24 restricted_tcn true

download firmware_fromTFTP 10.90.90.1 DES-3200R_1.50.B010.had image_id 1
download cfg_fromTFTP 10.90.90.1 /3/AdmMakarova30-311.conf


logging trap debugging
logging facility local6
logging 192.168.113.1

DES-3200-28:5#sh vlan Lisenko.E.A.Pravda66.19
Command: show vlan Lisenko.E.A.Pravda66.19



vlan 214
name Lesnoy-dom-nlmk


spanning-tree vlan 214

spanning-tree mst configuration
instance 1 vlan 214






vlan 861
name BOST-MPLS

spanning-tree vlan 861
spanning-tree mst configuration
instance 1 vlan 861




vlan 862
name BOST-INET

spanning-tree vlan 862
spanning-tree mst configuration
instance 1 vlan 862

switchport trunk allowed vlan add 861
switchport trunk allowed vlan add 214
switchport trunk allowed vlan add 862


create vlan TEMP-BOST-LG-MGMT tag 899
config vlan TEMP-BOST-LG-MGMT add tagged 22,25

create vlan BOST-MPLS tag 861
config vlan BOST-MPLS add tagged 22,25

create vlan BOST-INET tag 862
config vlan BOST-INET add tagged 22,25

create vlan Lesnoy-dom-nlmk tag 214
config vlan Lesnoy-dom-nlmk add tagged 22,25




lease 172.28.17.187 {
  starts 2 2011/08/09 18:45:19;
  ends 2 2011/08/09 18:47:19;
  cltt 2 2011/08/09 18:45:19;
  binding state free;
  hardware ethernet 5c:d9:98:bd:5e:d5;
  uid "\001\\\331\230\275^\325";
  client-hostname "home-b4cccf12c9";


5C-D9-98-BD-5E-D5


lease 172.28.17.182 {
  starts 3 2011/08/10 06:20:11;
  ends 3 2011/08/10 06:30:11;
  tstp 3 2011/08/10 06:30:11;
  cltt 3 2011/08/10 06:20:11;
  binding state free;
  hardware ethernet 1c:75:08:27:4a:af;
  uid "\001\034u\010'J\257";






VID             : 2386        VLAN Name       : Lisenko.E.A.Pravda66.19
VLAN Type       : Static      Advertisement   : Disabled
Member Ports    : 16,25-28            
Static Ports    : 16,25-28            
Current Tagged Ports   : 25-28               
Current Untagged Ports : 16                  
Static Tagged Ports    : 25-28               
Static Untagged Ports  : 16                  
Forbidden Ports        : 


config traffic control  1-27 broadcast enable multicast enable unicast disable action drop threshold 81920 countdown 5 time_interval 5

username='00040075000A:000634080437c630'
username='00040079000A:0006f07d682cdce0'



iptables -t nat -A PREROUTING -s 81.20.192.57/32 -d 81.20.192.19/32 -p tcp -m tcp --dport 15210 -j DNAT --to-destination 192.168.1.30:1521
iptables -t nat -A PREROUTING -s 81.20.192.6/32 -d 81.20.192.19/32 -p tcp -m tcp --dport 15211 -j DNAT --to-destination 192.168.1.30:1521 






config sntp primary 192.168.113.1 secondary 81.20.192.19 poll-interval 720 








config ports 27 state disable


config traffic control_trap both
config traffic control 1-28 broadcast enable multicast enable unicast disable action drop threshold 64 countdown 5 time_interval 5



                                                                                
 config stp version rstp                                                        
 config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 3 fbpdu disable hellotime 2 lbd enable lbd_recover_timer 60
 config stp priority 4096 instance_id 0                                        
 config stp mst_config_id name 00:22:B0:1B:EC:00 revision_level 0               
 enable stp                                                                     
 config stp ports 9-16 externalCost auto  edge false p2p auto state enable lbd disable
    
config stp ports 9-16 fbpdu enable                                        
 config stp ports 1-8, 16-25 externalCost auto  edge true p2p auto state disable lbd disable
config stp ports 1-8, 16-25 fbpdu disable                                         
                                           
config stp priority 4096 instance_id 0
config stp ports 1-4 externalCost auto  edge true p2p auto state disable lbd disable 
config stp ports 9-27 externalCost auto edge true p2p auto state disable lbd disable
 config stp ports 5-8 externalCost auto  edge false p2p auto state enable lbd disable
config stp ports 5-8 fbpdu enable 


config stp ports 21 externalCost auto edge true p2p auto state disable lbd disable
config stp ports 1-20 externalCost auto edge false p2p auto state enable lbd disable
config stp ports 22-23 fbpdu enable

config stp ports 1-20 externalCost auto edge false p2p auto state enable lbd disable
config stp ports 22-24 externalCost auto edge false p2p auto state enable lbd disable

config stp ports 1-20 fbpdu enable
config stp ports 22-24 fbpdu enable


