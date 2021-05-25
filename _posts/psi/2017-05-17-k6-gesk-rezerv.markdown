---
layout: post
title:  "k6-gesk-rezerv"
date:   2017-05-17 17:36:40 +0300
categories: PSI
tags: PSI
---

# k6-gesk-rezerv
interface GigabitEthernet0/2
 description #uplink to P8-S2
 switchport trunk allowed vlan 10,11,22,1015,1016,1038,1040,1041,1898,1899,1999
 switchport mode trunk
 switchport nonegotiate
end



10 для backbone (asa)
11 (lan)
22 для k9-s6
1015 k6-Local
1016 k6-INET
1038 sap-k6-c0-mn-sw
1040 GESK
1041 Sumtel_lesk
1898 TRtestZyxel1
1899 TRtestZyxel2 
1999 isgtest



config ipif System ipaddress 192.168.70.200/24




config traffic control 1-8 broadcast enable multicast enable unicast disable action drop threshold 64 countdown 5 time_interval 5
config loopdetect ports 1-8 state enabled

enable syslog
create syslog host 1 ipaddress 192.168.70.1 severity all facility local7 udp_port 514  state enable 
config log_save_timing log_trigger






config snmp system_name k6-dlink.sc.int
config snmp system_location k6-dlink 
config snmp system_contact iptech@sc.ru



Добавить в mstp
Добавить в фильтры

Последний этап
Добавлял сам влан



1015 k6-Local
1016 k6-INET

mstp


spanning-tree mst configuration
    instance 1 vlan 1015
    instance 1 vlan 1016




 config stp instance_id 1 add_vlan 1015
 config stp instance_id 1 add_vlan 1016


















Резерв через k6-dlink (192.168.70.200)
Управление на Dlink сделано через крайнюю, чтобы можно было отсюда рулить всем.
9 порт - это кроссировка с Крайней, через него подан только влан для менеджмента
10 порт - линк с Комунальной 9, с которого приходят следующие вланы
11 - backbone (резерв)
22 - резевр менеджмента (вообще то не нужен)
1038 - sap-k6-c0-mn-sw (резерв управления для k6-c0) через саппфир менеджмент, для управления местной сетью
1041 - Sumtel_lesk ( основной)
  
1 порт - Лэск

Ручное переключение резерва
Чтобы переключить Лэск на резерв, нужно убрать его из 10 порта
потом добавить на k6-s0 на Gi0/1, в который скроссирован этот dlink


