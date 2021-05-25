---
layout: post
title:  "plan-maksi"
date:   2012-11-10 05:21:49 +0400
categories: zavod
tags: zavod
---

# plan-maksi
1.Перекроссировать СтартТелекомовский аплинк на Се1 (Starttelecom-ce0)
2.Подготовить 2 порта на Maksi-s0 под ASA failover (eth1 порты) - использует 65 влан
11 порт под stk ASA
12 порт по sov ASA


Current configuration : 200 bytes
!
interface FastEthernet0/1
 description # Link to Maxi_group-CE0
 switchport trunk allowed vlan 11,12,16-18,65,72
 switchport mode trunk
 switchport nonegotiate
 load-interval 30
 no cdp enable
end

Maxi_Group-S0#sh run int Fa0/11
Building configuration...

Current configuration : 200 bytes
!
interface FastEthernet0/11
 description #Link to ASA-stk-Active
 switchport trunk allowed vlan 11,12,16-18,65,72
 switchport mode trunk
 switchport nonegotiate
 load-interval 30
 no cdp enable
end

Maxi_Group-S0#sh run int Fa0/12  
Building configuration...

Current configuration : 200 bytes
!
interface FastEthernet0/12
 description #Link to ASA-sov-Stanby
 switchport trunk allowed vlan 11,12,16-18,65,72
 switchport mode trunk
 switchport nonegotiate
 load-interval 30
 no cdp enable
end


interface FastEthernet0/2
 description # Link to Maxi_group-C0
 switchport trunk allowed vlan 10,11,13-16,65,72
 switchport mode trunk
 switchport nonegotiate
 load-interval 30
 no cdp enable
end





3.На Asa failover завести новый стык с CO взамен 10.98.254.4/30. Влан 11 меняем на  65. 10.98.254.64/29
10.98.254.65 - на С0 10.98.254.66 на ASA1, 10.98.254.67 stanby

Maxi-C0
conf t
interface FastEthernet0/0.65
 description # Link to Maxi_Group-CE0
 encapsulation dot1Q 65
 ip address 10.98.254.65 255.255.255.248

router ospf 109
  network 10.98.254.64 0.0.0.7 area 0
  no passive-interface FastEthernet0/0.65


ASA
interface Ethernet0/1.65
 vlan 65
 nameif vlan65
 security-level 100
 ip address 10.98.254.66 255.255.255.248 standby 10.98.254.67 
 ospf cost 100

mtu vlan65 1500

access-list vlan65_access_in extended permit ip any any 
access-list vlan65_access_in extended permit tcp any any 
access-list vlan65_access_in extended permit udp any any 

access-group vlan65_access_in in interface vlan65


4. 72 влан сделать вместо 16 влана (maxi video) 10.98.254.72/29, 73 для CO 74,75 ASA

interface FastEthernet0/0.16
 description # Video-conferenece Link to Maxi_Group-CE0
 encapsulation dot1Q 16
 ip vrf forwarding mg-video
 ip address 10.98.254.18 255.255.255.252


conf t
interface FastEthernet0/0.72
 description # Video-conferenece Link to Maxi_Group-CE0 New
 encapsulation dot1Q 72
 ip vrf forwarding mg-video
 ip address 10.98.254.73 255.255.255.248

router ospf 110 vrf mg-video
 

Asa
interface Ethernet0/1.72
 vlan 72
 nameif vlan72
 security-level 100
 ip address 10.98.254.74 255.255.255.248 standby 10.98.254.75  
 ospf cost 100

mtu vlan72 1500
access-group outside_access_in in interface vlan72


5. Прописать на ASA 2 дополнительные сети

network 10.98.254.74 255.255.255.248 area 0
network 10.98.254.66 255.255.255.248 area 0

router ospf 110
 router-id 10.98.99.9
 network 10.98.99.8 255.255.255.248 area 0
 area 0       
 log-adj-changes
 redistribute connected metric 1 metric-type 1 subnets
 redistribute static metric 1 metric-type 1 subnets
!             

6. Все готово к переводу
  Сначала на Maxi-Ce0 меняем адрес 10.98.0.1 на 10.98.0.253
  Говоирим Мишке
  Кроссируем порты Асы в maxi-s0 (11,12 порт)
  Заходим по 10.98.0.253 через новый стык
  Убираем BGP и OSPF совсем
  
  
11 оставляем на время как mngt
12 оставляем c другим адресом
16 оставляем на время
18 убираем



7. Переставляем плату совинтеловскую из Ce0 в sov-ce0 и поднимаем bgp на sov-ce0
8. Вуаля должно работать
9. Удалить 16 и 11 влан










Bgp сессия
Из второго слота выдернуть плату, которая идёт в аплинк билайна
В нулевом  - идёт в АТС


controller E1 0/0/0
 pri-group timeslots 1-31
 description # Link to PBX
!         
controller E1 0/2/0
 framing NO-CRC4 
 channel-group 0 timeslots 1-31
 description # Uplink to NLMK IPVPN via Golden-Telecom
!         
!         
class-map match-any REAL-TIME
 match ip precedence 5 
class-map match-any PREMIUM
 match ip precedence 3 
!         
!         
policy-map PLATINUM
 class REAL-TIME
  priority percent 60
 class PREMIUM
  bandwidth percent 15
  random-detect
 class class-default
!         



!         
interface Serial0/2/0:0
 description # Uplink to NLMK IPVPN via Golden-Telcom
 bandwidth 2048
 ip address 10.192.10.98 255.255.255.252
 load-interval 30
 service-policy output PLATINUM


router bgp 65022
 bgp log-neighbor-changes
 neighbor 10.192.10.97 remote-as 3216
 !        
 address-family ipv4
  redistribute connected
  redistribute static
  redistribute ospf 110 metric 1
  neighbor 10.192.10.97 activate
  no auto-summary
  no synchronization
  network 10.98.0.0 mask 255.255.255.0
  network 10.98.1.0 mask 255.255.255.0
  network 10.98.2.0 mask 255.255.255.0
  network 10.98.3.0 mask 255.255.255.0
  network 10.98.4.0 mask 255.255.255.240
  network 10.98.16.0 mask 255.255.255.0
  network 10.98.254.0 mask 255.255.255.0
  network 10.192.10.96 mask 255.255.255.252
 exit-address-family

router ospf 110
 log-adjacency-changes
 redistribute connected metric 1 metric-type 1 subnets
 redistribute static metric 1 metric-type 1 subnets
 redistribute bgp 65022 metric 1 metric-type 1 subnets
 passive-interface default
 no passive-interface FastEthernet0/0.11
 no passive-interface FastEthernet0/0.16
 network 10.98.254.4 0.0.0.3 area 0
 network 10.98.254.16 0.0.0.3 area 0

























Viz
interface Serial0/1/0
 description # Uplink to Golden-Telecom IPVPN
 bandwidth 2048
 ip address 10.192.10.90 255.255.255.252
 load-interval 30
 service-policy output PLATINUM
!
interface Serial0/1/1
 no ip address
 shutdown
 clock rate 2000000
!
interface Vlan1
 no ip address
!
router ospf 110
 log-adjacency-changes
 redistribute connected metric 1 metric-type 1 subnets
 redistribute static metric 1 metric-type 1 subnets
 redistribute bgp 65021 metric 1 metric-type 1 subnets
 passive-interface default
 no passive-interface FastEthernet0/0.19
 network 10.90.19.0 0.0.0.255 area 0
!         
router bgp 65021
 bgp log-neighbor-changes
 neighbor 10.192.10.89 remote-as 3216
 !        
 address-family ipv4
  neighbor 10.192.10.89 activate
  no auto-summary
  no synchronization
  network 10.90.0.0 mask 255.255.255.0
  network 10.90.1.0 mask 255.255.255.252
  network 10.90.4.0 mask 255.255.255.0
  network 10.90.18.1 mask 255.255.255.255
  network 10.90.18.8 mask 255.255.255.248
  network 10.90.18.16 mask 255.255.255.252
  network 10.90.19.0 mask 255.255.255.0
  network 10.192.3.8 mask 255.255.255.248
  network 10.192.10.88 mask 255.255.255.252
 exit-address-family
!         



     10.0.0.0/8 is variably subnetted, 183 subnets, 10 masks
O       10.90.18.8/29 [110/2] via 10.90.19.3, 7w0d, FastEthernet0/0.19
O E1    10.192.10.142/32 [110/2] via 10.90.19.4, 3d12h, FastEthernet0/0.19
O       10.90.0.0/24 [110/12] via 10.90.19.3, 7w0d, FastEthernet0/0.19
O E1    10.90.4.0/24 [110/3] via 10.90.19.3, 7w0d, FastEthernet0/0.19
O E1    10.192.10.69/32 [110/2] via 10.90.19.4, 3d12h, FastEthernet0/0.19
O E1    10.90.253.2/32 [110/13] via 10.90.19.3, 7w0d, FastEthernet0/0.19
S*   0.0.0.0/0 [1/0] via 10.192.10.89
     10.0.0.0/8 is variably subnetted, 183 subnets, 10 masks                                                                                                 
C       10.90.19.0/24 is directly connected, FastEthernet0/0.19                                                                                              
C       10.192.10.88/30 is directly connected, Serial0/1/0







Viz ttk


interface FastEthernet0/0
 description # Link to TTK
 ip address 10.192.10.114 255.255.255.252
 load-interval 30
 duplex full
 speed 100
!
interface FastEthernet0/0.19
 ip ospf cost 200
!
interface FastEthernet0/1
 description #Uplink to MNG NET #pheonix 20.11.2008
 no ip address
 duplex auto
 speed auto
!
interface FastEthernet0/1.18
 ip ospf cost 200
!
interface FastEthernet0/1.19
 encapsulation dot1Q 19
 ip address 10.90.19.4 255.255.255.0
!
router ospf 110
 log-adjacency-changes
 redistribute connected metric 1 metric-type 1 subnets
 redistribute static metric 1 metric-type 1 subnets
 redistribute bgp 65021 metric 1 metric-type 1 subnets
 passive-interface default
 no passive-interface FastEthernet0/1
 no passive-interface FastEthernet0/1.19
 network 10.90.19.0 0.0.0.255 area 0
!
router bgp 65021
 bgp log-neighbor-changes
 neighbor 10.192.10.90 remote-as 65021
 neighbor 10.192.10.113 remote-as 20485
 !
 address-family ipv4
  neighbor 10.192.10.90 activate
  neighbor 10.192.10.113 activate
  neighbor 10.192.10.113 route-map viz-backup out
  no auto-summary
  no synchronization
  network 10.90.0.0 mask 255.255.0.0
  network 10.90.0.0 mask 255.255.255.0
  network 10.90.4.0 mask 255.255.255.0
  network 10.90.18.1 mask 255.255.255.255
  network 10.90.18.8 mask 255.255.255.248
  network 10.90.18.16 mask 255.255.255.252
  network 10.90.19.0 mask 255.255.255.0
  network 10.90.254.0 mask 255.255.255.0
  network 10.192.10.112 mask 255.255.255.252
 exit-address-family


route-map viz-backup permit 10
 match ip address prefix-list viz-net

ip prefix-list viz-net seq 10 permit 10.90.0.0/16 le 32
ip prefix-list viz-net seq 20 deny 0.0.0.0/0 le 32



