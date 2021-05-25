---
layout: post
title:  "victoria-cxema"
date:   2015-04-08 01:02:02 +0300
categories: PSI
tags: PSI
---

# victoria-cxema
router ospf 111 vrf inet
 router-id 81.20.196.174
 log-adjacency-changes
 redistribute connected metric 1 subnets
 redistribute static metric 1 subnets
 redistribute bgp 20866 metric 1 subnets
 passive-interface default
 no passive-interface GigabitEthernet0/0.823
 no passive-interface GigabitEthernet0/0.825
 network 81.20.196.172 0.0.0.3 area 0
 network 81.20.196.184 0.0.0.3 area 0
!
router ospf 110
 router-id 81.20.192.76
 log-adjacency-changes
 summary-address 81.20.198.168 255.255.255.248
 summary-address 81.20.198.24 255.255.255.248
 summary-address 81.20.203.128 255.255.255.224
 summary-address 81.20.204.192 255.255.255.224
 redistribute connected metric 1 subnets
 redistribute static metric 1 subnets
 passive-interface default
 no passive-interface GigabitEthernet0/0.822
 no passive-interface GigabitEthernet0/0.824
 network 81.20.196.168 0.0.0.3 area 0
 network 81.20.196.176 0.0.0.3 area 0
 distribute-list prefix no-sc-local-distribution out
!
router bgp 20866
 no bgp default ipv4-unicast
 bgp log-neighbor-changes
 neighbor 81.20.192.66 remote-as 20866
 neighbor 81.20.192.66 update-source Loopback0
 neighbor 81.20.192.67 remote-as 20866
 neighbor 81.20.192.67 update-source Loopback0
 neighbor 81.20.192.68 remote-as 20866
 neighbor 81.20.192.68 update-source Loopback0
 neighbor 81.20.192.70 remote-as 20866
 neighbor 81.20.192.70 update-source Loopback0
 neighbor 81.20.192.71 remote-as 20866
 neighbor 81.20.192.71 update-source Loopback0
 neighbor 81.20.192.72 remote-as 20866
 neighbor 81.20.192.72 update-source Loopback0
 neighbor 81.20.192.74 remote-as 20866
 neighbor 81.20.192.74 update-source Loopback0
 neighbor 81.20.192.77 remote-as 20866
 neighbor 81.20.192.77 update-source Loopback0
 neighbor 81.20.192.78 remote-as 20866
 neighbor 81.20.192.78 update-source Loopback0
 neighbor 81.20.192.79 remote-as 20866
 neighbor 81.20.192.79 update-source Loopback0
 neighbor 81.20.201.246 remote-as 20866
 neighbor 81.20.201.246 update-source Loopback0
 neighbor 172.16.255.253 remote-as 20866
 neighbor 172.16.255.253 update-source Loopback0

address-family vpnv4
  neighbor 81.20.192.66 activate
  neighbor 81.20.192.66 send-community extended
  neighbor 81.20.192.67 activate
  neighbor 81.20.192.67 send-community extended
  neighbor 81.20.192.68 activate
  neighbor 81.20.192.68 send-community extended
  neighbor 81.20.192.70 activate
  neighbor 81.20.192.70 send-community extended
  neighbor 81.20.192.71 activate
  neighbor 81.20.192.71 send-community extended
  neighbor 81.20.192.72 activate
  neighbor 81.20.192.72 send-community extended
  neighbor 81.20.192.74 activate
  neighbor 81.20.192.74 send-community extended
  neighbor 81.20.192.77 activate
  neighbor 81.20.192.77 send-community extended
  neighbor 81.20.192.78 activate
  neighbor 81.20.192.78 send-community extended
  neighbor 81.20.192.79 activate
  neighbor 81.20.192.79 send-community extended
  neighbor 81.20.201.246 activate
  neighbor 81.20.201.246 send-community extended
  neighbor 172.16.255.253 activate
  neighbor 172.16.255.253 send-community extended
 exit-address-family

 address-family ipv4 vrf inet
  redistribute connected
  redistribute static
  default-information originate
  no synchronization
 exit-address-family






!
Импортируем наши маршруты в vrf inet

ip vrf inet
rd 20866:1
 route-target export 20866:10
 route-target import 20866:10
 route-target import 20866:20
 route-target import 20866:30
 route-target import 20866:40
 route-target import 20866:50
 route-target import 20866:60
 route-target import 20866:70
 route-target import 20866:80
 route-target import 20866:90
 route-target import 20866:100
 route-target import 20866:110
 route-target import 20866:120
 route-target import 20866:130
 route-target import 20866:140
 route-target import 20866:150
 route-target import 20866:160
 route-target import 20866:170
 route-target import 20866:180
 route-target import 20866:190
 route-target import 20866:200
 route-target import 20866:210
 route-target import 20866:220
 route-target import 20866:230
 route-target import 20866:240
 route-target import 20866:250
 route-target import 20866:260
 route-target import 20866:270
 route-target import 20866:280
 route-target import 20866:290
 route-target import 20866:300
 route-target import 20866:310
 route-target import 20866:320
 route-target import 20866:330
 route-target import 20866:340
 route-target import 20866:350
 route-target import 20866:360
 route-target import 20866:370
 route-target import 20866:380
 route-target import 20866:390
 route-target import 20866:400
 route-target import 20866:410
 route-target import 20866:420
 route-target import 20866:430
 route-target import 20866:440
 route-target import 20866:450


ip vrf cust1
 rd 20866:2
 route-target export 20866:20
 route-target import 20866:20
 route-target import 20866:10



ip vrf mgmt-victoria
 rd 20866:117
 route-target export 20866:1170
 route-target import 20866:1170
!
ip vrf mngt-ats-victoria
 description # MNGT for ATS on Victoria
 rd 20866:420
 route-target export 20866:4200
 route-target import 20866:4200
 maximum routes 500 100
!
ip vrf rtk-psi-homekredit
 description # HOME-KREDIT RTK IPVPN
 rd 20866:152
 route-target export 20866:1520
 route-target import 20866:1520
 maximum routes 500 100
!
ip name-server 81.20.192.16
ip auth-proxy max-nodata-conns 3
ip admission max-nodata-conns 3
vpdn enable

!
mpls label protocol ldp
!
voice-card 0
 no dspfarm






192.168.253.56/29, version 138, epoch 0, cached adjacency 81.20.196.169
0 packets, 0 bytes
  Flow: AS 0, mask 29
  tag information set
    local tag: 31
  via 81.20.196.169, GigabitEthernet0/0.824, 0 dependencies
    next hop 81.20.196.169, GigabitEthernet0/0.824
    valid cached adjacency
    tag rewrite with Gi0/0.824, 81.20.196.169, tags imposed: {}



sh mpls
sh mpls forwarding
sh mpls forwarding label 
show ip cef exact-route src dst











ip dhcp pool vrfcust12
   vrf cust12
   network 192.168.0.0 255.255.255.0
   dns-server 81.20.192.16 81.20.192.17 
   default-router 192.168.0.1 

Создаем vrf cust4

ip vrf cust4
 rd 20866:5
 route-target export 20866:50
 route-target import 20866:50
 route-target import 20866:10


 address-family ipv4 vrf cust4
  redistribute connected route-map rm-Lo104
  no synchronization
 exit-address-family


Создаем route-map для попадания в таблицу маршрутизации lo адреса
route-map rm-Lo104 permit 10
 match interface Loopback104


interface Loopback104
 description #Lk-profile NAT
 ip vrf forwarding cust4
 ip address 81.20.196.62 255.255.255.255
 mpls netflow egress
end


interface GigabitEthernet0/1.104
 description V-gsk 2 #pheonix
 encapsulation dot1Q 104
 ip vrf forwarding cust4
 ip address 192.168.0.1 255.255.255.0
 ip nat inside
 ip virtual-reassembly
 rate-limit input 2048000 384000 768000 conform-action transmit exceed-action drop
 rate-limit output 2048000 384000 768000 conform-action transmit exceed-action drop
 mpls netflow egress
end

ip nat inside source list 1 interface Loopback104 vrf cust4 overload




1.Поднимаем 2 ospf процесса между роутерами   824 - нормальный, 825 для хитрой схемы. Оба интерфейса добавляем в один ospf процесс, маршруты будут приходить через оба интерфейса.
2. Пример маршрутов на ats45.

O E2    81.20.201.188/30 
           [110/1] via 81.20.196.170, 1d06h, GigabitEthernet0/0.824  (Тойота)


O E2    81.20.201.252/32 
           [110/1] via 81.20.196.174, 1d06h, GigabitEthernet0/0.825(обычный клиент через хитрую схему - его лупбэк)

3. На victoria создаем 2 ospf процесса 110 и 111.
111 ospf создаем внутри vrf inet

4. Получаем все внешние маршруты на викторийской циске в обычной таблице маршрутизации и внутри vrf inet

5. Такие клиенты как Тойота (обычные) работают через 824 интерфейс
6. Для эмуляции локалки делаем следующее

ip vrf inet
rd 20866:1
 route-target export 20866:10
 route-target import 20866:10
 route-target import 20866:20
 route-target import 20866:30
 route-target import 20866:40
 route-target import 20866:50
 route-target import 20866:60
 route-target import 20866:70
 route-target import 20866:80
 route-target import 20866:90
 route-target import 20866:100
 route-target import 20866:110
 route-target import 20866:120
 route-target import 20866:130
 route-target import 20866:140
 route-target import 20866:150
 route-target import 20866:160
 route-target import 20866:170
 route-target import 20866:180
 route-target import 20866:190
 route-target import 20866:200
 route-target import 20866:210
 route-target import 20866:220
 route-target import 20866:230
 route-target import 20866:240
 route-target import 20866:250
 route-target import 20866:260
 route-target import 20866:270
 route-target import 20866:280
 route-target import 20866:290
 route-target import 20866:300
 route-target import 20866:310
 route-target import 20866:320
 route-target import 20866:330
 route-target import 20866:340
 route-target import 20866:350
 route-target import 20866:360
 route-target import 20866:370
 route-target import 20866:380
 route-target import 20866:390
 route-target import 20866:400
 route-target import 20866:410
 route-target import 20866:420
 route-target import 20866:430
 route-target import 20866:440
 route-target import 20866:450


ip vrf cust4
 rd 20866:5
 route-target export 20866:50
 route-target import 20866:50
 route-target import 20866:10

vrf cust для клиента, vrf inet для получения и отправки маршрутов на ats45

Вешаем на лупбэк белый адрес 

interface Loopback104
 description #Lk-profile NAT
 ip vrf forwarding cust4
 ip address 81.20.196.62 255.255.255.255
 mpls netflow egress
end


Маршрут к этому адресу на лупбэке в vrf inet импортируем с помощью  route-target import 20866:50, а от сюда он полетит дальше на ats45


Создаем route-map для попадания в таблицу маршрутизации vrf cust4 lo адреса
route-map rm-Lo104 permit 10
 match interface Loopback104

и применяем
 address-family ipv4 vrf cust4
  redistribute connected route-map rm-Lo104
  no synchronization
 exit-address-family



Дефолтный маршут попадает в vrf cust4 через
route-target import 20866:10


B       81.20.196.172/30 is directly connected, 1d06h, GigabitEthernet0/0.825
B       81.20.196.184/30 is directly connected, 1d06h, GigabitEthernet0/0.823
C       81.20.196.62/32 is directly connected, Loopback104
C    192.168.0.0/24 is directly connected, GigabitEthernet0/1.104
B*   0.0.0.0/0 [20/0] via 81.20.196.173 (inet), 1d06h


Интерфейс в сторону клиента, можно адреса по dhcp раздавать

interface GigabitEthernet0/1.104
 description V-gsk 2 #pheonix
 encapsulation dot1Q 104
 ip vrf forwarding cust4
 ip address 192.168.0.1 255.255.255.0
 ip nat inside
 ip virtual-reassembly
 rate-limit input 2048000 384000 768000 conform-action transmit exceed-action drop
 rate-limit output 2048000 384000 768000 conform-action transmit exceed-action drop
 mpls netflow egress
end

Это для натирования "локалки" клиента
ip nat inside source list 1 interface Loopback104 vrf cust4 overload


6. Володя добавил ещё 2 интерфеса с другого роутера с другими costs ospf для резервирования

Разница между rd и rt [https://mxssl.wordpress.com/category/mpls/](https://mxssl.wordpress.com/category/mpls/)
20866:1 81.20.192.62/32 20866:10
rd              маршрут                 rt (коммьюнити)
