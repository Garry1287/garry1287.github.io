---
layout: post
title:  "balancer-cxema"
date:   2011-11-11 14:42:55 +0400
categories: zavod
tags: zavod
---

# balancer-cxema

Asa распределяет внутренние маршруты (статик и коннектед)
CE-шки перераспределяют BGP маршруты в ospf и по bgp объявляет маршруты пораждаемые внутри сети
Все маршруты приходят и объявляются через outside

ASA
router ospf 110
 network 10.90.0.0 255.255.255.0 area 0
 network 10.90.18.8 255.255.255.248 area 0
 area 0       
 log-adj-changes
 redistribute connected metric 1 metric-type 1 subnets
 redistribute static metric 1 metric-type 1 subnets


Схема вообщем такая. Аса по ospf взаимодействует с тем балансером, у которого cost лучше (0 лучше, чем 200).
А этот балансер отправляет пакеты на обе CE, так как они объявляют одинаковые маршруты

Если половина узла падает, начинает работать вторая ASA, начинает работать второй балансер и отправляет 
на единственный CE, либо на оба если упал только основной балансер.



18 local-ospf   (10.98.18.8/29) - Используется что-бы связать между собой asa и Балансеры
19 local-managment (10.98.19.0/24) - Используется для управления и для того, чтобы связать CE-ки с Балансером
На самой Асе в OSPF используется только одна сеть (10.98.18.8/29)

Получается 18 сеть для связи Асы и балансеров
19 сеть для связи Балансеров и CE

10 Video-Viz (Видео) 
11 Lan-DATa (Данные)
20 Failover-Link (Failover)



LB0

interface FastEthernet0/0.18
 description #NLMK LAN
 encapsulation dot1Q 18
 ip address 10.90.18.11 255.255.255.248
 no cdp enable
!
interface FastEthernet0/0.19
 description Managment Lan
 encapsulation dot1Q 19
 ip address 10.90.19.3 255.255.255.0
 no cdp enable


router ospf 110
 log-adjacency-changes
 redistribute connected metric 1 metric-type 1 subnets
 redistribute static metric 1 metric-type 1 subnets
 passive-interface default
 no passive-interface FastEthernet0/0.18
 no passive-interface FastEthernet0/0.19
 network 10.90.18.8 0.0.0.7 area 0
 network 10.90.19.0 0.0.0.255 area 0






















Viz-TTK-LB1#sh run int FastEthernet0/0.18
Building configuration...

Current configuration : 156 bytes
!
interface FastEthernet0/0.18
 description #NLMK LAN
 encapsulation dot1Q 18
 ip address 10.90.18.12 255.255.255.248
 ip ospf cost 200
 no cdp enable
end

Viz-TTK-LB1#sh run int FastEthernet0/0.19
Building configuration...

Current configuration : 153 bytes
!
interface FastEthernet0/0.19
 description #MNG LAN 
 encapsulation dot1Q 19
 ip address 10.90.19.6 255.255.255.0
 ip ospf cost 200
 no cdp enable
end


router ospf 110
 log-adjacency-changes
 redistribute connected metric 1 metric-type 1 subnets
 redistribute static metric 1 metric-type 1 subnets
 passive-interface default
 no passive-interface FastEthernet0/0.18
 no passive-interface FastEthernet0/0.19
 network 10.90.18.8 0.0.0.7 area 0
 network 10.90.19.0 0.0.0.255 area 0















CE


interface FastEthernet0/1.19
 encapsulation dot1Q 19
 ip address 10.90.19.4 255.255.255.0

Viz-TTK-CE1#sh ip route ospf 
     10.0.0.0/8 is variably subnetted, 189 subnets, 11 masks
O E1    10.192.10.204/30 [110/2] via 10.90.19.1, 1w0d, FastEthernet0/1.19
O E1    10.192.10.206/32 [110/2] via 10.90.19.1, 1w0d, FastEthernet0/1.19
O       10.90.18.8/29 [110/2] via 10.90.19.3, 7w0d, FastEthernet0/1.19
O E1    10.192.10.141/32 [110/2] via 10.90.19.1, 1w0d, FastEthernet0/1.19
O       10.90.0.0/24 [110/12] via 10.90.19.3, 7w0d, FastEthernet0/1.19
O E1    10.90.4.0/24 [110/3] via 10.90.19.3, 7w0d, FastEthernet0/1.19
O E1    10.122.0.0/25 [110/2] via 10.90.19.1, 5w4d, FastEthernet0/1.19
O E1    10.192.10.70/32 [110/2] via 10.90.19.1, 1w0d, FastEthernet0/1.19
O E1    10.90.253.2/32 [110/13] via 10.90.19.3, 7w0d, FastEthernet0/1.19
O E1    10.192.10.116/30 [110/2] via 10.90.19.1, 5w4d, FastEthernet0/1.19
O E1    10.192.10.120/30 [110/2] via 10.90.19.1, 5w4d, FastEthernet0/1.19
O E1    10.192.11.4/30 [110/2] via 10.90.19.1, 5w4d, FastEthernet0/1.19
O E1    10.90.128.0/17 [110/3] via 10.90.19.3, 4w6d, FastEthernet0/1.19




Трейсы с ASA

Type escape sequence to abort.
Tracing the route to 10.192.10.190

 1  10.90.18.11 0 msec 0 msec 0 msec
 2  10.90.19.4 0 msec 10 msec 0 msec
 3  10.192.10.113 0 msec 0 msec 0 msec
 4  10.192.10.141 40 msec 30 msec 30 msec
 5  10.192.10.142 40 msec 40 msec 70 msec
 6  10.192.10.190 50 msec 40 msec 30 msec
Viz-ASA0#     traceroute 10.192.10.189

Type escape sequence to abort.
Tracing the route to 10.192.10.189

 1  10.90.18.11 0 msec 0 msec 0 msec
 2  10.90.19.1 0 msec 0 msec 0 msec
 3  10.192.10.89 0 msec 10 msec 0 msec
 4  10.192.10.78 60 msec 40 msec 50 msec
 5  10.192.10.77 50 msec 40 msec 40 msec
 6  10.192.10.189 50 msec *  40 msec
























Количество вланов


4-6,11,16,18

10,11,18-20

5 вланов


4    MNG-MG
5    MG-LB		Link to ASA-Sov port 0
6    MG-Failover 		Link to ASA port 3 failover
11   Link_to_Maxi_Group-C0
16   Link_to_Maxi_Group-C0_Video-conf
18   MG-Lan-2









  18    18ef.63d8.b868    DYNAMIC     Gi0/1
  18    c84c.7599.66da    DYNAMIC     Gi0/1
  19    00c0.b750.9061    DYNAMIC     Gi0/1
  19    00c0.b753.04ca    DYNAMIC     Gi0/1
  19    18ef.63d8.b868    DYNAMIC     Gi0/1
  19    58bc.2738.7ef1    DYNAMIC     Gi0/1
  19    c84c.7599.66de    DYNAMIC     Gi0/1
  10    c84c.7599.66dc    DYNAMIC     Gi0/1
  11    58bc.27ac.f919    DYNAMIC     Gi0/1
  11    c84c.7599.66db    DYNAMIC     Gi0/1
  20    c84c.7599.66dd    DYNAMIC     Gi0/1







18 local-ospf   (10.98.18.8/29)
19 local-managment (10.98.19.0/24)

10 Video-Viz (Видео) 
11 Lan-DATa (Данные)
20 Failover-Link (Failover)


19 - mngt


Current configuration : 138 bytes
!
interface FastEthernet0/0.18
 description #NLMK LAN
 encapsulation dot1Q 18
 ip address 10.90.18.11 255.255.255.248
 no cdp enable
end

Viz-Sov-LB0#sh run int Fa0/0.19
Building configuration...

Current configuration : 139 bytes
!
interface FastEthernet0/0.19
 description Managment Lan
 encapsulation dot1Q 19
 ip address 10.90.19.3 255.255.255.0
 no cdp enable
end















c84c.7578.0140

interface Ethernet0/0
 description Link to Load Balancer
 nameif outside
 security-level 100
 ip address 10.90.18.9 255.255.255.248 standby 10.90.18.10 
 ospf cost 10
!
interface Ethernet0/1
 description Link to LAN
 nameif inside
 security-level 100
 ip address 10.90.4.1 255.255.255.0 standby 10.90.4.254 
 ospf cost 10
!
interface Ethernet0/2
 description # Video and VoIP ethernet-segment
 nameif conference
 security-level 100
 ip address 10.90.0.1 255.255.255.0 standby 10.90.0.2 
!             
interface Ethernet0/3
 description LAN/STATE Failover Interface
!             
interface Management0/0
 nameif management
 security-level 100
 ip address 10.90.19.8 255.255.255.0 standby 10.90.19.7 
 ospf cost 10 
 management-only
















Viz-Sov-Switch#sh mac address-table address c84c.7578.0140
          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----
  18    c84c.7578.0140    DYNAMIC     Fa0/5


ASA-ETH0/0-OSPF






Total Mac Addresses for this criterion: 1
Viz-Sov-Switch#sh mac address-table address c84c.7578.0141
          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----
  11    c84c.7578.0141    DYNAMIC     Fa0/6
Total Mac Addresses for this criterion: 1

DATA Port




Viz-Sov-Switch#sh mac address-table address c84c.7578.0142
          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----
  10    c84c.7578.0142    DYNAMIC     Fa0/11
Total Mac Addresses for this criterion: 1


 LInk ASA-TTK





Viz-Sov-Switch#sh mac address-table address c84c.7578.0143
          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----
  20    c84c.7578.0143    DYNAMIC     Fa0/16
Total Mac Addresses for this criterion: 1

ASA-Failover-Link





Viz-Sov-Switch#sh mac address-table address c84c.7578.013f
          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----
  19    c84c.7578.013f    DYNAMIC     Fa0/19

#ASA managment port






Interface Ethernet0/0 "outside", is up, line protocol is up
  Hardware is i82546GB rev03, BW 1000 Mbps, DLY 10 usec
        Auto-Duplex(Full-duplex), Auto-Speed(100 Mbps)
        Input flow control is unsupported, output flow control is unsupported
        Description: Link to Load Balancer
        MAC address c84c.7578.0140, MTU 1500
        IP address 10.90.18.10, subnet mask 255.255.255.248
        414837487 packets input, 267006064527 bytes, 0 no buffer
        Received 10034 broadcasts, 0 runts, 0 giants
        0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
        0 L2 decode drops
        364040592 packets output, 75966461339 bytes, 0 underruns
        0 pause output, 0 resume output
        0 output errors, 0 collisions, 10 interface resets
        0 late collisions, 0 deferred
        13 input reset drops, 0 output reset drops, 0 tx hangs
        input queue (blocks free curr/low): hardware (255/252)
        output queue (blocks free curr/low): hardware (255/252)
  Traffic Statistics for "outside":
        10832538 packets input, 1396236294 bytes
        3957127 packets output, 427157620 bytes
        12 packets dropped
      1 minute input rate 0 pkts/sec,  45 bytes/sec
      1 minute output rate 0 pkts/sec,  21 bytes/sec
      1 minute drop rate, 0 pkts/sec
      5 minute input rate 0 pkts/sec,  70 bytes/sec
      5 minute output rate 0 pkts/sec,  21 bytes/sec
      5 minute drop rate, 0 pkts/sec
Interface Ethernet0/1 "inside", is up, line protocol is up
  Hardware is i82546GB rev03, BW 1000 Mbps, DLY 10 usec
        Auto-Duplex(Full-duplex), Auto-Speed(100 Mbps)
        Input flow control is unsupported, output flow control is unsupported
        Description: Link to LAN
        MAC address c84c.7578.0141, MTU 1500
        IP address 10.90.4.254, subnet mask 255.255.255.0
        291300704 packets input, 68736951246 bytes, 0 no buffer
        Received 276945 broadcasts, 0 runts, 0 giants
        0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
        0 L2 decode drops
        339977187 packets output, 257653900318 bytes, 0 underruns
        0 pause output, 0 resume output
        0 output errors, 0 collisions, 10 interface resets
        0 late collisions, 0 deferred
        1 input reset drops, 0 output reset drops, 0 tx hangs
        input queue (blocks free curr/low): hardware (255/252)
        output queue (blocks free curr/low): hardware (255/252)
  Traffic Statistics for "inside":
        3992026 packets input, 428824060 bytes
        3958131 packets output, 427193224 bytes
        811 packets dropped
      1 minute input rate 0 pkts/sec,  21 bytes/sec
      1 minute output rate 0 pkts/sec,  21 bytes/sec
      1 minute drop rate, 0 pkts/sec
      5 minute input rate 0 pkts/sec,  21 bytes/sec
      5 minute output rate 0 pkts/sec,  21 bytes/sec
      5 minute drop rate, 0 pkts/sec
Interface Ethernet0/2 "conference", is up, line protocol is up
  Hardware is i82546GB rev03, BW 100 Mbps, DLY 100 usec
        Auto-Duplex(Full-duplex), Auto-Speed(100 Mbps)
        Input flow control is unsupported, output flow control is unsupported
        Description: # Video and VoIP ethernet-segment
        MAC address c84c.7578.0142, MTU 1500
        IP address 10.90.0.2, subnet mask 255.255.255.0
        96405251 packets input, 9846322257 bytes, 0 no buffer
        Received 3268365 broadcasts, 0 runts, 0 giants
        0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
        0 L2 decode drops
        75793121 packets output, 8820328315 bytes, 0 underruns
        0 pause output, 0 resume output
        0 output errors, 0 collisions, 9 interface resets
        0 late collisions, 0 deferred
        2 input reset drops, 0 output reset drops, 0 tx hangs
        input queue (blocks free curr/low): hardware (255/253)
        output queue (blocks free curr/low): hardware (255/252)
  Traffic Statistics for "conference":
        7208493 packets input, 612365640 bytes
        3956678 packets output, 427149208 bytes
        0 packets dropped
      1 minute input rate 0 pkts/sec,  28 bytes/sec
      1 minute output rate 0 pkts/sec,  21 bytes/sec
      1 minute drop rate, 0 pkts/sec
      5 minute input rate 0 pkts/sec,  30 bytes/sec
      5 minute output rate 0 pkts/sec,  21 bytes/sec
      5 minute drop rate, 0 pkts/sec




Interface Ethernet0/3 "Viz-failover", is up, line protocol is up
  Hardware is i82546GB rev03, BW 100 Mbps, DLY 100 usec
        Auto-Duplex(Full-duplex), Auto-Speed(100 Mbps)
        Input flow control is unsupported, output flow control is unsupported
        Description: LAN/STATE Failover Interface
        MAC address c84c.7578.0143, MTU 1500
        IP address 10.90.20.2, subnet mask 255.255.255.252
        222593087 packets input, 72401012454 bytes, 0 no buffer
        Received 4241 broadcasts, 0 runts, 0 giants
        0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
        0 L2 decode drops
        170658391 packets output, 36555100056 bytes, 0 underruns
        0 pause output, 0 resume output
        0 output errors, 0 collisions, 4 interface resets
        0 late collisions, 0 deferred
        0 input reset drops, 2 output reset drops, 2 tx hangs
        input queue (blocks free curr/low): hardware (255/235)
        output queue (blocks free curr/low): hardware (255/238)
  Traffic Statistics for "Viz-failover":
        68760603 packets input, 29026946392 bytes
        31306232 packets output, 3626052192 bytes
        0 packets dropped
      1 minute input rate 4 pkts/sec,  2511 bytes/sec
      1 minute output rate 1 pkts/sec,  185 bytes/sec
      1 minute drop rate, 0 pkts/sec
      5 minute input rate 4 pkts/sec,  2195 bytes/sec
      5 minute output rate 1 pkts/sec,  183 bytes/sec
      5 minute drop rate, 0 pkts/sec
















Interface Management0/0 "management", is up, line protocol is up
  Hardware is i82557, BW 100 Mbps, DLY 100 usec
        Auto-Duplex(Full-duplex), Auto-Speed(100 Mbps)
        Input flow control is unsupported, output flow control is unsupported
        MAC address c84c.7578.013f, MTU 1500
        IP address 10.90.19.7, subnet mask 255.255.255.0
        18230019 packets input, 2181498685 bytes, 0 no buffer
        Received 666126 broadcasts, 0 runts, 0 giants
        0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
        0 L2 decode drops
        17570447 packets output, 2143020624 bytes, 0 underruns
        0 pause output, 0 resume output
        0 output errors, 0 collisions, 0 interface resets
        0 babbles, 0 late collisions, 0 deferred
        0 lost carrier, 0 no carrier
        0 input reset drops, 0 output reset drops
        input queue (curr/max packets): hardware (0/1) software (0/9)
        output queue (curr/max packets): hardware (3/18) software (0/3)
  Traffic Statistics for "management":
        4103688 packets input, 433955707 bytes
        3957618 packets output, 427198139 bytes
        23 packets dropped
      1 minute input rate 0 pkts/sec,  21 bytes/sec
      1 minute output rate 0 pkts/sec,  21 bytes/sec
      1 minute drop rate, 0 pkts/sec
      5 minute input rate 1 pkts/sec,  58 bytes/sec
      5 minute output rate 1 pkts/sec,  102 bytes/sec
      5 minute drop rate, 0 pkts/sec
        Management-only interface. Blocked 0 through-the-device packets





















Fedeor: вы абсолютно правы. причем ip интерфейсов обоих асашек должны быть в одной и той-же сети. Поэтому у прова надо брать /29 сетку.
А уж переключение между провайдерами делается тупо через IP SLA.
Failover это механизм выживамния самой железки, а не канала связи.


Добрый день!

В дополнение к сказанному небольшая идея, как помочь ASA прорезервировать каналы:

Код:
ISP1        ISP2
  |           |
SW1          SW2
  | \       / |
  |   \   /   |
  |     X     |
  |   /   \   |
  | /       \ |
ASA1        ASA1


Немного коряво нарисовал, но, я думаю, идея понятна - каждый провайдер к своему свичу, каждая ASA одним портом к одному свичу, вторым ко второму.
 При умирании одной из ASA или одного из провайдеров всё будет работать. Это не отменяет необходимость использования IP SLA. 
Два свича (могут быть тупыми) - просто чтобы не было единой точки отказа (разумеется, при умирании одного из свичей теряем одного из провайдеров).




Вы всё правильно поняли по поводу failover'а. В каждую ASA надо подключить каждого провайдера. 
То есть в интерфейсы с номером 0 первой и второй ASA должен приходить первый провайдер, в в интерфейсы с номером 1 должен приходить второй провайдер.
 В тот момент, когда первая ASA сдохнет (тьфу-тьфу-тьфу), провайдеры к резервной ASA будут подключены ровно на те же интерфейсы.
А вот для "разветвления" линков от провайдеров и нужны свичи. Маршруты дополнительные не потребуются. Маршрут по умолчанию 0.0.0.0 будет переключаться 
по IP SLA либо на первого, либо на второго провайдера.


[http://www.anticisco.ru/forum/viewtopic.php?p=30813](http://www.anticisco.ru/forum/viewtopic.php?p=30813)






		  Новая схема
OSPF между CE шками и балансерами без изменений. Для соединения балансеров с асашками выделяем 2 сети /29
/29 - один адрес на Primary Unit, второй на Secondary, 3-ий на LB0. Со второй сетью тоже самое.
На асашках получается по адресу на eth0 ( outside-lb0) и eth1 ( outside-lb1) от каждого балансера.  
Прописываем дефолты с ip sla в сторону этих балансеров и всё.

route outside-lb0 0.0.0.0 0.0.0.0 xx.xx.xx.xx1 1 track 192
route outside-lb1  0.0.0.0 0.0.0.0 yy.yy.yy.yy1 10
!
sla monitor 1
 type echo protocol ipIcmpEcho xx.xx.xx.xx1 interface outside
  num-packets 3
  threshold 2500
  timeout 5000
  frequency 60
  request-data-size 100
sla monitor schedule 1 life forever start-time now
!
track 192 rtr 1 reachability



Обратные маршруты ( на сети филиала ) прописываем статиком на LB0 и LB1 в сторону ASA-шки.
На backup балансере необходимо перераспределять в ospf статические маршруты с худшей метрикой, чтобы на CE-шки приходило 2 маршрута от каждого балансера,
но от одного (backup) с худшей метрикой




CE0          CE1
  | \       / |
  |   \   /   |
  |     X     |
  |   /   \   |
  | /       \ |
LB0         LB1
  | \       / |
  |   \   /   |
  |     X     |
  |   /   \   |
  | /       \ |
ASA0        ASA1
 

Сначала попробовать сделать Stateless failover

no failover link new-link Ethernet0/3


			Перенастройка для Maxi-Eburg
По шагам
1. Прописать default на активный балансер c лучшим cost (там где cost ниже), ip route outside 0.0.0.0 0.0.0.0 10.98.99.11 10
2. Второй адрес с балансера LB1 убрать - 10.98.99.12
3. Сделать кроссировки eht2 портов в свитчи в порт 5 (7 vlan)
3. Завести вторую подсеть /29 - 10.98.99.16/29 в отдельном влане 7
    10.98.99.17 - ASA0
    10.98.99.18 - ASA1
    10.98.99.19 - LB1

interface Ethernet0/2
  nameif outside-lb1                                                                                                                                                                                                
  security-level 100
  ip address 10.98.99.17 255.255.255.248 standby 10.98.99.18 
!             

4. Прописать статические маршруты на каждом балансере в сторону ASA
ip route 10.98.0.0 255.255.255.0
ip route 10.98.8.0 255.255.252.0 
ip route 10.98.16.0 255.255.255.0

ip route 10.98.254.64 255.255.255.248

ip route 10.98.254.0 255.255.255.252
ip route 10.98.252.12 255.255.255.252




Прописать

На основном балансере
 redistribute static metric 1 metric-type 1 subnets

На Backup балансере
 redistribute static metric 10 metric-type 1 subnets



********************************************
???? По моему отдельным портом
ip address 10.98.98.7 255.255.255.0 standby 10.98.98.8
management
10.98.98.0 255.255.255.0


O E1     10.90.252.8/30 [110/3] via 10.98.98.6, 1d21h, GigabitEthernet0/1
O E1     10.98.0.0/24 [110/3] via 10.98.98.6, 1d21h, GigabitEthernet0/1
O E1     10.98.8.0/22 [110/3] via 10.98.98.6, 1d21h, GigabitEthernet0/1
O E1     10.98.16.0/24 [110/3] via 10.98.98.6, 1d21h, GigabitEthernet0/1
O E1     10.98.252.12/30 [110/103] via 10.98.98.6, 1d21h, GigabitEthernet0/1
O E1     10.192.11.228/30 [110/2] via 10.98.98.1, 1d21h, GigabitEthernet0/1

********************************************


5. Убрать OSPF
6. Сделать SLA

sla monitor 1
 type echo protocol ipIcmpEcho 10.98.99.19 interface outside-lb1
  num-packets 3
  threshold 2500
  timeout 5000
  frequency 60
  request-data-size 100
sla monitor schedule 1 life forever start-time now
!
track 192 rtr 1 reachability


route outside-lb1 0.0.0.0 0.0.0.0 10.98.99.19 1 track 192



Надо ли?
no ip verify reverse-path interface outside0
no ip verify reverse-path interface outside1



10.98		10.162
CE0 98.1       CE1 98.4 
  | \       / |
  |   \   /   |
  |     X     |ospf
  |   /   \   |
  | /       \ |
98.3	     98.6
LB0         LB1
99.11	     99.12
  | \       / |
  |   \   /   |
  |     X     |ospf
  |   /   \   |
  | /       \ |
.99.9	    .99.10
ASA0        ASA1
 

На eth0/2 повесить






interface Ethernet0/0                                                                                                                                                                                          
 nameif outside                                                                                                                                                                                                
 security-level 100                                                                                                                                                                                            
 ip address 10.98.99.9 255.255.255.248 standby 10.98.99.10                                                                                                                                                     
 ospf cost 10                                                                                                                                                                                                  
 ospf mtu-ignore                                                                                                                                                                                               
!                                                                                                                                                                                                              
interface Ethernet0/1                                                                                                                                                                                          
 no nameif                                                                                                                                                                                                     
 no security-level                                                                                                                                                                                             
 no ip address                                                                                                                                                                                                 
!                                                                                                                                                                                                              
interface Ethernet0/1.12                                                                                                                                                                                       
 vlan 12                                                                                                                                                                                                       
 nameif vlan12                                                                                                                                                                                                 
 security-level 100                                                                                                                                                                                            
 ip address 10.98.0.1 255.255.255.0 standby 10.98.0.254                                                                                                                                                        
 ospf cost 100                                                                                                                                                                                                 
!                                                                                                                                                                                                              
interface Ethernet0/1.15
 vlan 15      
 nameif vlan15
 security-level 100
 ip address 10.98.8.1 255.255.252.0 standby 10.98.8.2 
 ospf cost 100
!             
interface Ethernet0/1.18
 vlan 18      
 nameif vlan18
 security-level 100
 ip address 10.98.16.1 255.255.255.0 standby 10.98.16.254 
 ospf cost 100
!             
interface Ethernet0/1.65
 vlan 65      
 nameif vlan65
 security-level 100
 ip address 10.98.254.66 255.255.255.248 standby 10.98.254.67 
 ospf cost 100
!             
interface Ethernet0/1.72
 shutdown     
 vlan 72      
 nameif vlan72
 security-level 100
 no ip address
 ospf cost 100
!             
interface Ethernet0/1.100
 vlan 100     
 nameif vlan100
 security-level 0
 no ip address
!             
interface Ethernet0/2
 shutdown     
 no nameif    
 no security-level
 no ip address
!             
interface Ethernet0/3
 description LAN/STATE Failover Interface
!             
interface Management0/0
 nameif management
 security-level 100
 ip address 10.98.98.7 255.255.255.0 standby 10.98.98.8 
 ospf cost 10 
 management-only
!             




















Maxi-Sov-LB0#sh run int Gi0/0.4
Building configuration...

Current configuration : 125 bytes
!
interface GigabitEthernet0/0.4
 description Managment Lan
 encapsulation dot1Q 4
 ip address 10.98.98.3 255.255.255.0
end

Maxi-Sov-LB0#sh run int Gi0/0.5
Building configuration...

Current configuration : 124 bytes
!
interface GigabitEthernet0/0.5
 description #LB0 LAN 
 encapsulation dot1Q 5
 ip address 10.98.99.11 255.255.255.248
end





interface GigabitEthernet0/0.4
 description Managment Lan
 encapsulation dot1Q 4
 ip address 10.98.98.6 255.255.255.0
!
interface GigabitEthernet0/0.5
 description #LB0 LAN
 encapsulation dot1Q 5
 ip address 10.98.99.12 255.255.255.248
!






Maxi-Sov-CE0

interface GigabitEthernet0/0
 description # Uplink to NLMK IPVPN via Golden-Telecom (new Ethernet) #smithy 24.06.2013
 bandwidth 10240
 ip address 10.192.10.98 255.255.255.252
 load-interval 30
 duplex auto
 speed auto
 no cdp enable
 service-policy output PLATINUM-ETH-10MB

interface GigabitEthernet0/1
 description #Uplink to MNG NET #pheonix 29.08.2012
 ip address 10.98.98.1 255.255.255.0
 duplex auto
 speed auto
!         



Maxi-Stk-CE1

interface GigabitEthernet0/0.2317
 description #Rezerv kanal from Starttelecom 10M #smithy 28.06.2013
 bandwidth 10240
 encapsulation dot1Q 2317
 ip address 10.192.10.162 255.255.255.252
 no cdp enable
 service-policy output PLATINUM-ETH-10MB
!
interface GigabitEthernet0/1
 description MG MNG LAN
 ip address 10.98.98.4 255.255.255.0
 duplex auto
 speed auto










Альтернатива - Stateless failover. Настроить на ASAшках




failover      
failover lan unit secondary
failover lan interface new-link Ethernet0/3
failover link new-link Ethernet0/3
failover interface ip new-link 10.90.252.9 255.255.255.252 standby 10.90.252.10
monitor-interface vlan12
monitor-interface vlan18

















Супер  Новая схема

CE0          CE1
  | \       / |
  |   \   /   |
  |     X     |
  |   /   \   |
  | /       \ |
ASA0         ASA1

Делаем также как в предыдущем описании, но добавляем оба интерфейса ASA в одну zone, чтобы работала ECMP
[http://www.cisco.com/c/en/us/td/docs/security/asa/asa93/configuration/general/asa-general-cli/route-overview.html](http://www.cisco.com/c/en/us/td/docs/security/asa/asa93/configuration/general/asa-general-cli/route-overview.html)

Получается CE-шки перераспределяют маршруты BGP к ASA-шке (собранные в failover). ASA держить 2 набора маршрутов


OSPF между CE шками и балансерами без изменений. Для соединения балансеров с асашками выделяем 2 сети /29
/29 - один адрес на Primary Unit, второй на Secondary, 3-ий на CE0. Со второй сетью тоже самое.
На асашках получается по адресу на eth0 ( outside-ce0) и eth1 ( outside-ce1) от каждого CE.  


Вопрос такой, как быстро переключиться? Требуется ли IP SLA, для скорости переключения
Прописываем дефолты с ip sla в сторону этих балансеров и всё.

fas hellos
[http://www.cisco.com/c/en/us/td/docs/ios/12_0s/feature/guide/fasthelo.html](http://www.cisco.com/c/en/us/td/docs/ios/12_0s/feature/guide/fasthelo.html)

OSPF only performs equal-cost load-balancing. So manually set the cost to the same on both links if they are different. Also, under the ospf process, you will need to enter maximum-paths 2.

