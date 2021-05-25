---
layout: post
title:  "vrf-maxi-change"
date:   2013-11-01 07:49:36 +0400
categories: zavod
tags: zavod
---

# vrf-maxi-change



Торговый Дом
	

10.33.5.0/24

12
	

«Красная Роза»
	

10.102.5.0/24

Территориальный центр: Revda
	

 

13
	

ОАО "НСММЗ"
	

10.98.30.0/24

14
	

НЛМК-УЦ(Екатеринбург)
	

10.202.5.0/24










Новинская

interface FastEthernet0/0.15
 description # Maxi_Group LAN
 encapsulation dot1Q 15
 ip vrf forwarding mg-lan
 ip address 192.168.1.8 255.255.252.0
 no cdp enable

no ip vrf mg-lan

ip vrf mg-video
no route-target import 65022:1000























Ревда

no ip vrf mg-lan                                                                                                                                                
 description # Maxi-Group LAN                                                                                                                                
 rd 65022:100
 route-target export 65022:1000
 route-target import 65022:1000
 route-target import 65022:1010
!
ip vrf mg-video
 no route-target import 65022:1000


interface FastEthernet0/1.12
 description # Maxi-Group LAN
 encapsulation dot1Q 12
 ip vrf forwarding mg-lan
 ip address 192.168.100.159 255.255.252.0


interface FastEthernet0/1.15
 description # Maxi-Group Lan # Server's Group # pheonix 28/08/09
 encapsulation dot1Q 15
 ip vrf forwarding mg-lan
 ip address 10.98.4.1 255.255.255.240

interface FastEthernet0/1.20
 description #Maxi-Group LAN new
 encapsulation dot1Q 20
 ip vrf forwarding mg-lan
 ip address 10.98.252.1 255.255.255.252


interface Serial0/1/0:0
 description #Secondary  Uplink #HD
 bandwidth 2048
 ip vrf forwarding mg-lan
 ip address 10.192.10.106 255.255.255.252
 load-interval 30
 mpls ip
 mpls accounting experimental input
 mpls accounting experimental output
 service-policy output PLATINUM


 address-family ipv4 vrf mg-lan
  redistribute connected
  redistribute static
  neighbor 10.192.10.105 remote-as 20485
  neighbor 10.192.10.105 update-source Serial0/1/0:0
  neighbor 10.192.10.105 activate
  neighbor 10.192.10.105 weight 200
  neighbor 10.192.10.105 prefix-list MG-REVDA-ADV out
  no synchronization
  network 10.98.4.0 mask 255.255.255.240
  network 10.98.24.0 mask 255.255.248.0
  network 10.98.252.0 mask 255.255.255.252
  network 10.98.254.4 mask 255.255.255.252
  network 10.98.254.16 mask 255.255.255.252
  network 192.168.100.0 mask 255.255.252.0
 exit-address-family




ip route vrf mg-lan 0.0.0.0 0.0.0.0 10.192.10.105
ip route vrf mg-lan 10.98.24.0 255.255.248.0 10.98.252.2



Weight на ТТК сделать меньше, тогда исходящий пойдёт в Ебург
Значит наоборот больше.
Оставить как есть

На ттк меньший weight
А на ibgo не менять



real-time
ip precedence 5





















   
Берёзовский

no ip vrf mg-lan                                                                                                                                                

interface FastEthernet0/1.12
 description # Maxi-Group LAN
 encapsulation dot1Q 12
 ip vrf forwarding mg-lan
 ip address 192.168.40.30 255.255.252.0


interface FastEthernet0/1.20
 description #Maxi-Group LAN new
 encapsulation dot1Q 20
 ip vrf forwarding mg-lan
 ip address 10.98.20.1 255.255.252.0







Н.Серьги
no ip vrf mg-lan 



interface FastEthernet0/1.12
 description # Maxi-Group LAN
 encapsulation dot1Q 12
 ip vrf forwarding mg-lan
 ip address 192.168.201.152 255.255.252.0





interface FastEthernet0/1.20
 description #Maxi-Group Lan new
 encapsulation dot1Q 20
 ip vrf forwarding mg-lan
 ip address 10.98.32.1 255.255.252.0















Access-list к видео терминалу
















Maxi-C0-Eburg#traceroute vrf mg-video 172.19.7.27

Type escape sequence to abort.
Tracing the route to 172.19.7.27

  1 10.98.99.12 0 msec 0 msec 4 msec
  2 10.98.98.1 0 msec 4 msec 0 msec
  3 10.192.10.97 4 msec 4 msec 0 msec
  4 10.192.10.78 [MPLS: Label 1834 Exp 1] 60 msec 60 msec 60 msec
  5 10.192.10.77 208 msec 76 msec 48 msec
  6 10.192.10.86 68 msec 64 msec 64 msec
  7 10.186.1.6 52 msec 40 msec 52 msec
  8 192.168.4.2 52 msec 64 msec 68 msec
  9 172.19.7.27 40 msec 40 msec 52 msec





Maxi-C0-Eburg#traceroute vrf mg-video 172.19.7.20

Type escape sequence to abort.
Tracing the route to 172.19.7.20

  1 10.98.99.12 0 msec 0 msec 4 msec
  2 10.98.98.4 0 msec 4 msec 0 msec
  3 10.192.10.161 4 msec 0 msec 4 msec
  4 10.192.10.21 52 msec 56 msec 52 msec
  5 10.192.10.22 48 msec 48 msec 48 msec
  6 10.192.10.86 56 msec 56 msec 60 msec
  7 10.186.1.6 44 msec 44 msec 44 msec
  8 192.168.4.4 44 msec 64 msec 44 msec
  9  * 
    172.19.7.20 56 msec 60 msec
















Maxi-C1-Revda# traceroute vrf mg-lan 172.19.7.20 numeric 

Type escape sequence to abort.
Tracing the route to 172.19.7.20

  1 10.192.10.105 4 msec 8 msec 8 msec
  2 10.192.10.141 [MPLS: Label 1399 Exp 1] 36 msec
    10.192.10.70 [MPLS: Label 1399 Exp 1] 40 msec
    10.192.10.141 [MPLS: Label 1399 Exp 1] 36 msec
  3 10.192.10.69 40 msec 56 msec 56 msec
  4 10.192.10.186 56 msec 56 msec 64 msec
  5 10.186.1.7 64 msec 60 msec 60 msec
  6 192.168.4.4 64 msec 64 msec 64 msec
  7 172.19.7.20 60 msec 56 msec 48 msec
Maxi-C1-Revda# traceroute vrf mg-lan 172.19.7.27 numeric 

Type escape sequence to abort.
Tracing the route to 172.19.7.27

  1 10.192.10.105 4 msec 4 msec 4 msec                                                                                                                       
  2 10.192.10.70 [MPLS: Label 1399 Exp 1] 36 msec                                                                                                            
    10.192.10.141 [MPLS: Label 1399 Exp 1] 36 msec                                                                                                           
    10.192.10.70 [MPLS: Label 1399 Exp 1] 36 msec                                                                                                            
  3 10.192.10.142 40 msec 40 msec 56 msec                                                                                                                    
  4 10.192.10.186 40 msec 40 msec 40 msec                                                                                                                    
  5 10.186.1.7 40 msec 40 msec 40 msec                                                                                                                       
  6 192.168.4.2 40 msec 44 msec 40 msec                                                                                                                      
  7 172.19.7.27 44 msec 44 msec 40 msec                                                                                                                      
Maxi-C1-Revda#                                                                                                                                               
                    

Maxi-C1-Revda# traceroute vrf mg-lan 172.19.7.20 numeric 

Type escape sequence to abort.
Tracing the route to 172.19.7.20

  1 10.192.10.105 4 msec 8 msec 8 msec
  2 10.192.10.141 [MPLS: Label 1399 Exp 1] 36 msec
    10.192.10.70 [MPLS: Label 1399 Exp 1] 40 msec
    10.192.10.141 [MPLS: Label 1399 Exp 1] 36 msec
  3 10.192.10.69 40 msec 56 msec 56 msec
  4 10.192.10.186 56 msec 56 msec 64 msec
  5 10.186.1.7 64 msec 60 msec 60 msec
  6 192.168.4.4 64 msec 64 msec 64 msec
  7 172.19.7.20 60 msec 56 msec 48 msec
Maxi-C1-Revda# traceroute vrf mg-lan 172.19.7.27 numeric 

Type escape sequence to abort.
Tracing the route to 172.19.7.27

  1 10.192.10.105 4 msec 4 msec 4 msec                                                                                                                       
  2 10.192.10.70 [MPLS: Label 1399 Exp 1] 36 msec                                                                                                            
    10.192.10.141 [MPLS: Label 1399 Exp 1] 36 msec                                                                                                           
    10.192.10.70 [MPLS: Label 1399 Exp 1] 36 msec                                                                                                            
  3 10.192.10.142 40 msec 40 msec 56 msec                                                                                                                    
  4 10.192.10.186 40 msec 40 msec 40 msec                                                                                                                    
  5 10.186.1.7 40 msec 40 msec 40 msec                                                                                                                       
  6 192.168.4.2 40 msec 44 msec 40 msec                                                                                                                      
  7 172.19.7.27 44 msec 44 msec 40 msec                                                                                                                      
Maxi-C1-Revda#                                                                                                                                               
                    












Maxi-C3-N.Sergi#traceroute vrf mg-video 172.19.7.20 numeric 

Type escape sequence to abort.
Tracing the route to 172.19.7.20

  1  *  *  * 
  2 10.98.254.73 [MPLS: Label 209 Exp 0] 8 msec 12 msec 8 msec
  3 10.98.99.12 12 msec 8 msec 12 msec
  4 10.98.98.4 8 msec 12 msec 8 msec
  5 10.192.10.161 12 msec 8 msec 12 msec
  6 10.192.10.21 64 msec 88 msec 60 msec
  7 10.192.10.22 68 msec 68 msec 68 msec
  8 10.192.10.86 68 msec 68 msec 68 msec
  9 10.186.1.7 60 msec 56 msec 56 msec
 10 192.168.4.2 68 msec 64 msec 64 msec
 11 172.19.7.20 60 msec 56 msec 60 msec



Maxi-C3-N.Sergi#traceroute vrf mg-video 172.19.7.27 numeric 
                                                                                                                                                             
Type escape sequence to abort.                                                                                                                               
Tracing the route to 172.19.7.27                                                                                                                             
                                                                                                                                                             
  1  *  *  *                                                                                                                                                 
  2 10.98.254.73 [MPLS: Label 209 Exp 0] 8 msec 12 msec 8 msec                                                                                               
  3 10.98.99.12 12 msec 8 msec 12 msec                                                                                                                       
  4 10.98.98.4 8 msec 12 msec 8 msec                                                                                                                         
  5 10.192.10.161 12 msec 8 msec 12 msec                                                                                                                     
  6 10.192.10.21 64 msec 60 msec 64 msec                                                                                                                     
  7 10.192.10.22 68 msec 68 msec 68 msec                                                                                                                     
  8 10.192.10.86 68 msec 72 msec 68 msec                                                                                                                     
  9 10.186.1.6 52 msec 56 msec 56 msec                                                                                                                       
 10 192.168.4.4 68 msec 68 msec 76 msec                                                                                                                      
 11 172.19.7.27 68 msec 68 msec 72 msec 











ip route 0.0.0.0 0.0.0.0 10.98.254.66
ip route vrf mg-video 0.0.0.0 0.0.0.0 10.98.254.74
ip route vrf mg-video 10.98.0.0 255.255.0.0 Null0






в Н.Сергах не работает, в Ревде работает 
 
(14:48:56)  Turapov:  
из новой сети по новому маршруту 
 
(06:57:35)  Turapov:  
Доброе утро! 
 
(07:00:19)  Turapov:  
У вас случайно вчера не было изменений на канале между Ревдой и Екб?
У Нас вчера пропала связь с новых адресов. Со старых (192,168,100,0) есть 
 
(08:51:34)  Turapov:  
В Екб звонил, сказали вчера питание пропадало. Может конфиг не сохранен был?









10.98.252.0/30   - Ревда	

10.98.252.4/30 - Серги   (5 наш 6 ваш)

10.98.252.8/30 - Берёзовский (9 наш 10 ваш)


Фильтрация внешинх маршрутов, приходящих из Ревды
Maxi-C2-Berezovskii(config)#ip as-path access-list 1 permit ^$
Maxi-C2-Berezovskii(config)#router bgp 65022
Maxi-C2-Berezovskii(config-router)# address-family vpnv4
Maxi-C2-Berezovskii(config-router-af)#
Maxi-C2-Berezovskii(config-router-af)#neighbor 10.98.253.2 filter-list 1 in 




административная дистанция
метрика








*> 81.20.202.228/30 0.0.0.0                  0         32768 ?


neighbor 2.2.2.2 ebgp-multihop 2
neighbor 2.2.2.2 update-source Loopback1
ebgp-multihop 2 - нужен для установления связи с loopback
next-hop-self необходим в ibgp, потому что без этого атрибута маршруты приходят от имени ebgp
все обновления для соседа отправлять с указанием в качестве next-hop локального маршрутизатора (то есть себя, который является только ibgp маршрутизатором)

 next-hop-unchanged 
Изменение поведения по умолчанию атрибута next-hop для eBGP-соседа — все обновления для соседа отправлять без изменения атрибута next-hop: 



Advertise the next hop via an IGP.

Have router B advertise itself as the next hop for all advertised BGP routes.

Advertise the BGP routes via an IGP








