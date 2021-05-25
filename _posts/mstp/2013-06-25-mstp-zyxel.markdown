---
layout: post
title:  "mstp-zyxel"
date:   2013-06-25 19:12:47 +0400
categories: mstp
tags: mstp
---

# mstp-zyxel
MSTP
    

Выключить все порты, настроить, включить порт


spanning-tree mode <RSTP|MRSTP|MSTP> 
mstp configuration-name <name> 
mstp revision <0-65535> 


show mstp instance <number> 

mstp instance <number> priority <0-61440>
mstp instance <number> vlan <vlan-list>

mstp instance <number> interface port-channel <port-list>

mstp instance <number> interface port-channel <port-list> path-cost <1-65535>

mstp instance <number> interface port-channel <port-list> priority <1-255>


1.Создать вланы

2.MSTP
3500-1(config)# spanning-tree mode MSTP
3500-1(config)# mstp

3500-1(config)# mstp configuration-name MSTP_TEST
3500-1(config)# mstp revision 1

3. Добавляем в инстансы вланы
3500-1(config)# mstp instance 1 vlan 10-13
3500-1(config)# mstp instance 2 vlan 20-23
3500-1(config)# mstp instance 3 vlan 30-33
3500-1(config)# mstp instance 4 vlan 40-43

4. Конфигурируем порты для MSTP
For 3500-1

3500-1(config)# mstp instance 0 interface port-channel 21-24
3500-1(config)# mstp instance 1 interface port-channel 21-24
3500-1(config)# mstp instance 2 interface port-channel 21-24
3500-1(config)# mstp instance 3 interface port-channel 21-24
3500-1(config)# mstp instance 4 interface port-channel 21-24

5.Устанавливаем приоритеты для инстансов
3500-1(config)# mstp instance 0 priority 4096
3500-1(config)# mstp instance 1 priority 4096

6. Для корректировки дерева можно
CLI reference for instance port cost.
3500-1(config)# mstp instance interface port-channel path-cost

CLI reference for instance port priority.
3500-1(config)# mstp instance interface port-channel priority



Example of MSTP configurations.

For 3500-1
3500-1(config)# spanning-tree mode MSTP
3500-1(config)# mstp
3500-1(config)# mstp configuration-name MSTP_TEST
3500-1(config)# mstp revision 1
3500-1(config)# mstp instance 1 vlan 10-13
3500-1(config)# mstp instance 2 vlan 20-23
3500-1(config)# mstp instance 3 vlan 30-33
3500-1(config)# mstp instance 4 vlan 40-43
3500-1(config)# mstp instance 0 priority 4096
3500-1(config)# mstp instance 1 priority 4096
3500-1(config)# mstp instance 2 priority 28672
3500-1(config)# mstp instance 3 priority 28672
3500-1(config)# mstp instance 4 priority 28672
3500-1(config)# mstp instance 0 interface port-channel 21-24
3500-1(config)# mstp instance 1 interface port-channel 21-24
3500-1(config)# mstp instance 2 interface port-channel 21-24
3500-1(config)# mstp instance 3 interface port-channel 21-24
3500-1(config)# mstp instance 4 interface port-channel 21-24







На нашей версии не работает
[https://kb.zyxel.ru/hc/ru/articles/115002572733-%D0%A4%D1%83%D0%BD%D0%BA%D1%86%D0%B8%D0%B8-%D0%B7%D0%B0%D1%89%D0%B8%D1%82%D1%8B-%D0%BE%D1%82-%D0%BF%D0%BE%D0%B4%D0%BC%D0%B5%D0%BD%D1%8B-%D0%BA%D0%BE%D1%80%D0%BD%D0%B5%D0%B2%D0%BE%D0%B3%D0%BE-%D0%BA%D0%BE%D0%BC%D0%BC%D1%83%D1%82%D0%B0%D1%82%D0%BE%D1%80%D0%B0-RSTP-MSTP-Root-Guard-%D0%B8-%D0%B7%D0%B0%D1%89%D0%B8%D1%82%D1%8B-%D0%BE%D1%82-%D0%BA%D0%B0%D0%B4%D1%80%D0%BE%D0%B2-BPDU-BPDU-Guard-%D0%B2-Ethernet-%D0%BA%D0%BE%D0%BC%D0%BC%D1%83%D1%82%D0%B0%D1%82%D0%BE%D1%80%D0%B0%D1%85-ZyXEL](https://kb.zyxel.ru/hc/ru/articles/115002572733-%D0%A4%D1%83%D0%BD%D0%BA%D1%86%D0%B8%D0%B8-%D0%B7%D0%B0%D1%89%D0%B8%D1%82%D1%8B-%D0%BE%D1%82-%D0%BF%D0%BE%D0%B4%D0%BC%D0%B5%D0%BD%D1%8B-%D0%BA%D0%BE%D1%80%D0%BD%D0%B5%D0%B2%D0%BE%D0%B3%D0%BE-%D0%BA%D0%BE%D0%BC%D0%BC%D1%83%D1%82%D0%B0%D1%82%D0%BE%D1%80%D0%B0-RSTP-MSTP-Root-Guard-%D0%B8-%D0%B7%D0%B0%D1%89%D0%B8%D1%82%D1%8B-%D0%BE%D1%82-%D0%BA%D0%B0%D0%B4%D1%80%D0%BE%D0%B2-BPDU-BPDU-Guard-%D0%B2-Ethernet-%D0%BA%D0%BE%D0%BC%D0%BC%D1%83%D1%82%D0%B0%D1%82%D0%BE%D1%80%D0%B0%D1%85-ZyXEL)

























Пример

Сatalyst						Zyxel XGS-4728F
_______________________				  _____________________
|		3 порт|___________________________|23 порт		|
|		4 порт|___________________________|24 порт		|
|_____________________|				  |____________________ |



Имеем два одинаковых линка и приоритет использования высчитывается согласно номеру порта


spanning-tree mode MSTP
mstp
mstp configuration-name PSI
mstp revision 777
mstp instance 1 vlan 22,2610,2620,2630
mstp instance 2 vlan 2640,2650,2660
mstp instance 0 priority 32768
mstp instance 1 priority 32768
mstp instance 2 priority 8192
mstp instance 0 interface port-channel 23-24
mstp instance 1 interface port-channel 23-24
mstp instance 2 interface port-channel 23-24







DGS
 config stp version mstp
 config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 3 fbpdu enable lbd enable lbd_recover_timer 60
 config stp priority 32768 instance_id 0 
 create stp instance_id 1 
 config stp instance_id 1 add_vlan 22
 config stp instance_id 1 add_vlan 2610
 config stp instance_id 1 add_vlan 2620
 config stp instance_id 1 add_vlan 2630
 config stp priority 32768 instance_id 1 
 create stp instance_id 2 
 config stp instance_id 2 add_vlan 2640
 config stp instance_id 2 add_vlan 2650
 config stp instance_id 2 add_vlan 2660                                         
 config stp priority 8192 instance_id 2 
 config stp mst_config_id name PSI revision_level 777
 enable stp
 config stp ports 1-22 externalCost auto  edge true p2p auto state disable lbd enable
 config stp ports 1-27 hellotime 2 
 config stp mst_ports 1-27 instance_id 0 internalCost auto priority 128
config stp ports 1-22 fbpdu disable
 config stp ports 23-27 externalCost auto  edge false p2p auto state enable lbd disable
config stp ports 23-27 fbpdu enable
 config stp mst_ports 1-27 instance_id 1 internalCost auto priority 128
 config stp mst_ports 1-27 instance_id 2 internalCost auto priority 128








Настройка Port Fast на access-интерфейсе:

sw(config)#interface fa0/1
sw(config-if)# spanning-tree portfast

Настройка Port Fast на интерфейсе, который работает в режиме trunk (тегированый порт):

sw(config)#interface fa0/1
sw(config-if)# spanning-tree portfast trunk




Прописать на всех портах, где не надо включать spanning tree
 spanning-tree portfast trunk
 spanning-tree bpdufilter enable
 spanning-tree bpduguard enable




Catalyst

spanning-tree mode mst
spanning-tree logging
spanning-tree extend system-id
!
spanning-tree mst configuration
 name PSI
 revision 777
 instance 1 vlan 22, 2610, 2620, 2630
 instance 2 vlan 2640, 2650, 2660
!
spanning-tree mst 0-1 priority 8192



 description #Uplink
 switchport trunk encapsulation dot1q
 switchport trunk allowed vlan 2610,2620,2630,2640,2650,2660
 switchport mode trunk


 
 
 
 
 
 #############################################
 1. Прописать конфигурацию mstp
 2.Без портов
 no mstp instance 0 interface port-channel 23-24
no mstp instance 1 interface port-channel 23-24
no mstp instance 2 interface port-channel 23-24
