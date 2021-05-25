---
layout: post
title:  "revda+maxi-rezerv"
date:   2018-02-18 15:48:03 +0300
categories: zavod
tags: zavod
---

# revda+maxi-rezerv
Цель такова, чтобы не пропадал сервис при падении ревдинского канала
Надо из Ебурга объявлять специфики для своих сетей (Ебург, Берёзовский) 
и общую сеть для Ревды и Н.Серег

Из Ревды необходимо объявлять специфики Ревды и Н.Серег
и общую сеть для Ебурга и Берёзовского

Сети Ревды
10.98.24.0/21
10.98.19.0/24
10.98.254.254/32
10.98.1.0/24
10.98.4.0/28
10.98.254.20/30
10.98.254.24/30
10.98.252.0/30
10.98.253.2/32
10.98.254.8/30
10.192.10.104/30



*> 10.98.1.0/24     0.0.0.0                  0         32768 i                                                                                               
*> 10.98.3.0/24     10.98.254.26             2         32768 i                                                                                               
*> 10.98.4.0/28     0.0.0.0                  0         32768 i                                                                                               
*> 10.98.19.0/24    10.98.252.2              0         32768 i                                                                                               
*> 10.98.24.0/21    10.98.252.2              0         32768 i                                                                                               
*> 10.98.32.0/22    10.98.254.26             2         32768 i                                                                                               
*> 10.98.252.0/30   0.0.0.0                  0         32768 i                                                                                               
*> 10.98.252.4/30   10.98.254.26             2         32768 i                                                                                               
*> 10.98.254.8/30   0.0.0.0                  0         32768 i                                                                                               
*> 10.98.254.24/30  0.0.0.0                  0         32768 i                                                                                               
*> 10.98.254.32/30  10.98.254.26             2         32768 i                                                                                               
*> 10.98.254.254/32 0.0.0.0                  0         32768 i 



  network 10.98.1.0 mask 255.255.255.0
  network 10.98.3.0 mask 255.255.255.0
  network 10.98.4.0 mask 255.255.255.240
  network 10.98.19.0 mask 255.255.255.0
  network 10.98.24.0 mask 255.255.248.0
  network 10.98.32.0 mask 255.255.252.0
  network 10.98.252.0 mask 255.255.255.252
  network 10.98.252.4 mask 255.255.255.252
  network 10.98.254.4 mask 255.255.255.252
  network 10.98.254.8 mask 255.255.255.252
  network 10.98.254.16 mask 255.255.255.252
  network 10.98.254.24 mask 255.255.255.252
  network 10.98.254.32 mask 255.255.255.252
  network 10.98.254.254 mask 255.255.255.255






Серьги
10.98.32.0/22
10.98.3.0/24
10.98.254.24/30
10.98.252.4/30
10.98.253.4/32
10.98.254.32/30

Maxi-C3-N.Sergi#sh ip route static
     10.0.0.0/8 is variably subnetted, 261 subnets, 12 masks
S       10.98.32.0/22 [1/0] via 10.98.252.6
Maxi-C3-N.Sergi#sh ip route connected 
     10.0.0.0/8 is variably subnetted, 261 subnets, 12 masks
C       10.98.3.0/24 is directly connected, FastEthernet0/1.11
C       10.98.254.24/30 is directly connected, FastEthernet0/0
C       10.98.252.4/30 is directly connected, FastEthernet0/1.20
C       10.98.253.4/32 is directly connected, Loopback0
C       10.98.254.32/30 is directly connected, FastEthernet0/1.10
C    192.168.200.0/22 is directly connected, FastEthernet0/1.12







Берёзовский
10.98.20.0/22
10.98.2.0/24 
10.98.254.28/30
10.98.253.3/32
10.98.254.12/30
10.98.252.8/30

sh ip route static 
     10.0.0.0/8 is variably subnetted, 261 subnets, 12 masks
S       10.98.20.0/22 [1/0] via 10.98.252.10




sh ip route connected 
     10.0.0.0/8 is variably subnetted, 261 subnets, 12 masks
C       10.98.2.0/24 is directly connected, FastEthernet0/1.11
C       10.98.254.28/30 is directly connected, FastEthernet0/1.10
C       10.98.253.3/32 is directly connected, Loopback0
C       10.98.254.12/30 is directly connected, FastEthernet0/0
C       10.98.252.8/30 is directly connected, FastEthernet0/1.20
C    192.168.40.0/22 is directly connected, FastEthernet0/1.12







Ебург
10.98.0.0/24
10.98.16.0/24
10.98.254.72/29
10.98.0.0/16 is directly connected, Null0 --- Нужно ли Вообще, только чтобы объявить можно было с обоих CE? На не нужно
10.98.254.64/29
10.98.253.1/32
10.98.254.0/30
10.98.254.12/30
10.98.254.8/30
10.98.254.64/29



C    10.98.0.0 255.255.255.0 is directly connected, vlan12
C    10.98.16.0 255.255.255.0 is directly connected, vlan18
C    10.98.254.72 255.255.255.248 is directly connected, vlan72








O E1 10.98.20.0 255.255.252.0 [110/102] via 10.98.254.65, 199:59:29, vlan65
O    10.98.254.20 255.255.255.252 
           [110/125] via 10.98.254.65, 199:59:29, vlan65
O    10.98.254.28 255.255.255.252 
           [110/102] via 10.98.254.65, 199:59:29, vlan65
O    10.98.254.24 255.255.255.252 
           [110/125] via 10.98.254.65, 199:59:30, vlan65
O    10.98.252.4 255.255.255.252 [110/126] via 10.98.254.65, 199:59:30, vlan65
O E1 10.98.253.4 255.255.255.255 [110/126] via 10.98.254.65, 199:59:30, vlan65
O E1 10.98.252.0 255.255.255.252 [110/125] via 10.98.254.65, 199:59:30, vlan65
O E1 10.98.253.1 255.255.255.255 [110/101] via 10.98.254.65, 199:59:30, vlan65
O E1 10.98.253.3 255.255.255.255 [110/102] via 10.98.254.65, 199:59:30, vlan65
O    10.98.254.0 255.255.255.252 [110/101] via 10.98.254.65, 199:59:30, vlan65
O E1 10.98.253.2 255.255.255.255 [110/125] via 10.98.254.65, 199:59:30, vlan65
O    10.98.254.12 255.255.255.252 
           [110/101] via 10.98.254.65, 199:59:30, vlan65
O E1 10.98.252.8 255.255.255.252 [110/102] via 10.98.254.65, 199:59:30, vlan65
O    10.98.254.32 255.255.255.252 
           [110/126] via 10.98.254.65, 199:59:30, vlan65

O E1 192.168.40.0 255.255.252.0 [110/102] via 10.98.254.65, 199:59:30, vlan65
O E1 192.168.200.0 255.255.252.0 [110/126] via 10.98.254.65, 199:59:30, vlan65
O E1 192.168.0.0 255.255.252.0 [110/101] via 10.98.254.65, 199:59:30, vlan65






     10.0.0.0/8 is variably subnetted, 261 subnets, 12 masks
S       10.98.0.0/16 is directly connected, Null0

     10.0.0.0/8 is variably subnetted, 261 subnets, 12 masks
C       10.98.253.1/32 is directly connected, Loopback0
C       10.98.254.0/30 is directly connected, FastEthernet0/0.10
C       10.98.254.12/30 is directly connected, FastEthernet0/0.14
C       10.98.254.8/30 is directly connected, FastEthernet0/0.13
C       10.98.254.64/29 is directly connected, FastEthernet0/0.65
C    192.168.0.0/22 is directly connected, FastEthernet0/0.15












Sovintel

router ospf 110
 redistribute connected metric 1 metric-type 1 subnets
 redistribute static metric 1 metric-type 1 subnets
 redistribute bgp 65022 metric 1 metric-type 1 subnets
 passive-interface default
 no passive-interface GigabitEthernet0/1
 network 10.98.98.0 0.0.0.255 area 0
!
router bgp 65022
 bgp log-neighbor-changes
 neighbor 10.192.10.97 remote-as 3216
 !
 address-family ipv4
  network 10.98.0.0 mask 255.255.0.0
  network 10.98.0.0 mask 255.255.255.0
  network 10.98.2.0 mask 255.255.255.0
  network 10.98.3.0 mask 255.255.255.0
  network 10.98.16.0 mask 255.255.255.0
  network 10.98.98.0 mask 255.255.255.0
  network 10.98.99.0 mask 255.255.255.0
  network 10.98.254.0 mask 255.255.255.0
  redistribute connected
  redistribute static
  redistribute ospf 110
  neighbor 10.192.10.97 activate
  neighbor 10.192.10.97 prefix-list filer_nsergi_phone out
 exit-address-family
!
ip forward-protocol nd
!
ip http server
ip http access-class 23
ip http authentication local
ip http secure-server
ip http timeout-policy idle 60 life 86400 requests 10000
!
!
!
ip prefix-list filer_nsergi_ph seq 20 permit 10.98.0.0/16 le 30
ip prefix-list filer_nsergi_ph seq 30 deny 0.0.0.0/0 le 32
!
ip prefix-list filer_nsergi_phone seq 5 deny 10.98.254.24/30
ip prefix-list filer_nsergi_phone seq 20 permit 10.98.0.0/16 le 30
ip prefix-list filer_nsergi_phone seq 30 deny 0.0.0.0/0 le 32


Только маршруты O

*> 10.98.252.4/30   10.98.98.6             128         32768 ?
*> 10.98.254.0/30   10.98.98.6             103         32768 ?
*> 10.98.254.8/30   10.98.98.6             126         32768 ?
*> 10.98.254.12/30  10.98.98.6             103         32768 ?
*> 10.98.254.20/30  10.98.98.6             127         32768 ?
*> 10.98.254.28/30  10.98.98.6             104         32768 ?
*> 10.98.254.32/30  10.98.98.6             128         32768 ?
*> 10.98.254.64/29  10.98.98.6             102         32768 ?
*> 10.98.254.72/29  10.98.98.6             102         32768 ?

O E1 отсутсвуют в перераспределении BGP

/16 мы же объявляем? Поэтому должно быть доступно

aggregate-address без sumary-only объявляет и общий и остальные


















Megafon
router ospf 110
 redistribute connected metric 1 metric-type 1 subnets
 redistribute static metric 1 metric-type 1 subnets
 redistribute bgp 65022 metric 1 metric-type 1 subnets
 passive-interface default
 no passive-interface GigabitEthernet0/1
 network 10.98.98.0 0.0.0.255 area 0
!
router bgp 65022
 bgp log-neighbor-changes
 neighbor 10.192.10.93 remote-as 29648
 neighbor 10.192.10.161 remote-as 29648
 !
 address-family ipv4
  network 10.98.0.0 mask 255.255.0.0
  network 10.98.0.0 mask 255.255.255.0
  network 10.98.2.0 mask 255.255.255.0
  network 10.98.3.0 mask 255.255.255.0
  network 10.98.16.0 mask 255.255.255.0
  network 10.98.98.0 mask 255.255.255.0
  network 10.98.99.0 mask 255.255.255.248
  network 10.98.254.0 mask 255.255.255.0
  network 10.192.10.92 mask 255.255.255.252
  redistribute connected
  redistribute static
  redistribute ospf 110 metric 1
  neighbor 10.192.10.93 activate
  neighbor 10.192.10.161 activate                                                                                                                            
  neighbor 10.192.10.161 prefix-list filer_nsergi_phone out                                                                                                  
 exit-address-family                                                                                                                                         
!                                                                                                                                                            
ip forward-protocol nd                                                                                                                                       
!                                                                                                                                                            
ip http server                                                                                                                                               
ip http access-class 23                                                                                                                                      
ip http authentication local                                                                                                                                 
ip http secure-server                                                                                                                                        
ip http timeout-policy idle 60 life 86400 requests 10000                                                                                                     
!                                                                                                                                                            
ip route 0.0.0.0 0.0.0.0 10.192.10.93                                                                                                                        
!                                                                                                                                                            
!                                                                                                                                                            
ip prefix-list filer_nsergi_ph seq 20 permit 10.98.0.0/16 le 30                                                                                              
ip prefix-list filer_nsergi_ph seq 30 deny 0.0.0.0/0 le 32                                                                                                   
!                                                                                                                                                            
ip prefix-list filer_nsergi_phone seq 5 deny 10.98.254.24/30                                                                                                 
ip prefix-list filer_nsergi_phone seq 20 permit 10.98.0.0/16 le 30                                                                                           
ip prefix-list filer_nsergi_phone seq 30 deny 0.0.0.0/0 le 32         



















Чинил я получается объявляя сети по BGP в Ебурге
ip route 10.98.19.0 255.255.255.0 10.98.252.2
ip route 10.98.24.0 255.255.248.0 10.98.252.2

А потом убирал обратно







На СE сделать
router bgp 65022
address-family ipv4
aggregate-address 10.98.0.0 255.255.0.0
no network 10.98.0.0 mask 255.255.0.0
network 10.98.254.72 mask 255.255.255.248
network 10.98.254.64 mask 255.255.255.248
network 10.98.253.1 mask 255.255.255.255
network 10.98.254.0 mask 255.255.255.252
network 10.98.254.12 mask 255.255.255.252
network 10.98.254.8 mask 255.255.255.252
network 10.98.20.0 mask 255.255.252.0
network 10.98.254.28 mask 255.255.255.252
network 10.98.253.3 mask 255.255.255.255
network 10.98.252.8 mask 255.255.255.252
no redistribute ospf 110
no network 10.98.3.0 mask 255.255.255.0
no network 10.98.254.0 mask 255.255.255.0




10.98.20.0/22
10.98.2.0/24 
10.98.254.28/30
10.98.253.3/32
10.98.254.12/30
10.98.252.8/30

10.98.0.0/24
10.98.16.0/24
10.98.254.72/29
10.98.0.0/16 is directly connected, Null0 --- Нужно ли Вообще, только чтобы объявить можно было с обоих CE? На не нужно
10.98.254.64/29
10.98.253.1/32
10.98.254.0/30
10.98.254.12/30
10.98.254.8/30
10.98.254.64/29








  




В Ревде сделать
router bgp 65022
address-family ipv4
aggregate-address 10.98.0.0 255.255.0.0
network 10.98.253.4 mask 255.255.255.255
network 10.98.254.20 mask 255.255.255.252
network 10.98.253.2 mask 255.255.255.255
no network 10.98.254.16 mask 255.255.255.252
no network 10.98.254.4 mask 255.255.255.252




network 10.98.3.0 mask 255.255.255.0
network 10.98.32.0 mask 255.255.252.0
network 10.98.254.24 mask 255.255.255.252
network 10.98.252.4 mask 255.255.255.252
network 10.98.253.4 mask 255.255.255.255
network 10.98.254.32 mask 255.255.255.252
network 10.98.24.0 mask 255.255.248.0
network 10.98.19.0 mask 255.255.255.0
network 10.98.254.254 mask 255.255.255.255
network 10.98.1.0 mask 255.255.255.0
network 10.98.4.0 mask 255.255.255.240
network 10.98.254.24 mask 255.255.255.252
network 10.98.252.0 mask 255.255.255.252
network 10.98.254.8 mask 255.255.255.252


network 10.98.254.4 mask 255.255.255.252
no network 10.98.254.16 mask 255.255.255.252
  
  
  



10.98.24.0/21
10.98.19.0/24
10.98.254.254/32
10.98.1.0/24
10.98.4.0/28
10.98.254.20/30
10.98.254.24/30
10.98.252.0/30
10.98.253.2/32
10.98.254.8/30
10.192.10.104/30



10.98.32.0/22
10.98.3.0/24
10.98.254.24/30
10.98.252.4/30
10.98.253.4/32
10.98.254.32/30


В Ебурге убрать
no ip route 10.98.0.0 255.255.0.0 Null0
