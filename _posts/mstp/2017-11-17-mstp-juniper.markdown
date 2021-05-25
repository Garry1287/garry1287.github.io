---
layout: post
title:  "mstp-juniper"
date:   2017-11-17 10:13:05 +0300
categories: mstp
tags: mstp
---

# mstp-juniper
Step-by-Step Procedure

To configure interfaces and MSTP on Switch 1:


Создание вланов
    Configure the VLANs voice-vlan, employee-vlan, guest-vlan, and camera-vlan:
    [edit vlans]
    user@switch1# set voice-vlan description “Voice VLAN”
    user@switch1# set voice-vlan vlan-id 10
    user@switch1# set employee-vlan description “Employee VLAN”
    user@switch1# set employee-vlan vlan-id 20
    user@switch1# set guest-vlan description “Guest VLAN”
    user@switch1# set guest-vlan vlan-id 30
    user@switch1# set camera-vlan description “Camera VLAN”
    user@switch1# set guest-vlan vlan-id 40
    Configure the VLANs on the interfaces, including support for the Ethernet Switching protocol:
    [edit interfaces]


Прописывание на портах
    user@switch1# set ge–0/0/13 unit 0 family ethernet-switching vlan members [10 20 30 40]
    user@switch1# set ge-0/0/9 unit 0 family ethernet-switching vlan members [10 20 30 40]
    user@switch1# set ge-0/0/11 unit 0 family ethernet-switching vlan members [10 20 30 40]
    Configure the port mode for the interfaces:
    [edit interfaces]

    user@switch1# set ge–0/0/13 unit 0 family ethernet-switching port-mode trunk
    user@switch1# set ge-0/0/9 unit 0 family ethernet-switching port-mode trunk
    user@switch1# set ge-0/0/11 unit 0 family ethernet-switching port-mode trunk


    Configure MSTP on the switch, including the two MSTIs:
    [edit protocols]

    user@switch1# mstp configuration-name region1
    user@switch1# mstp bridge-priority 16k  (0 инстанс

Прописываем
    user@switch1# mstp interface ge-0/0/13.0 cost 1000
    user@switch1# mstp interface ge-0/0/13.0 mode point-to-point
    user@switch1# mstp interface ge-0/0/9.0 cost 1000
    user@switch1# mstp interface ge-0/0/9.0 mode point-to-point
    user@switch1# mstp interface ge-0/0/11.0 cost 4000
    user@switch1# mstp interface ge-0/0/11.0 mode point-to-point


    user@switch1# mstp msti 1 bridge-priority 16k
    user@switch1# mstp msti 1 vlan [10 20]
    user@switch1# mstp msti 1 interface ge-0/0/11.0 cost 4000
    user@switch1# mstp msti 2 bridge-priority 8k
    user@switch1# mstp msti 2 vlan [30 40]




me0 {
        unit 0 {
            family inet {
                address 192.168.113.119/24;
            }
        }
    }



    vlan {
        unit 22 {
            family inet {
                address 192.168.0.1/24;
            }
        }
    }
}









Наша конфигурация

Cost не надо, пусть сам



set mstp bridge-priority 24k
set mstp msti 1 bridge-priority 24k
set mstp msti 2 bridge-priority 24k
set mstp msti 3 bridge-priority 24k
set mstp msti 4 bridge-priority 24k
set mstp interface xe-0/0/38.0 mode point-to-point
set mstp interface xe-0/0/39.0 mode point-to-point






show interfaces brief    
Physical interface: xe-0/0/38, Enabled, Physical link is Down
  Description: CTD-S6-Te1/2
  Link-level type: Ethernet, MTU: 1514, Speed: 10Gbps, Duplex: Full-Duplex, Loopback: Disabled, Source filtering: Disabled, Flow control: Enabled
  Device flags   : Present Running Down
  Interface flags: Hardware-Down SNMP-Traps Internal: 0x0
  Link flags     : None

  Logical interface xe-0/0/38.0 
    Flags: Device-Down SNMP-Traps 0x0 Encapsulation: ENET2
    eth-switch

Physical interface: xe-0/0/39, Enabled, Physical link is Down
  Link-level type: Ethernet, MTU: 1514, Speed: 10Gbps, Duplex: Full-Duplex, Loopback: Disabled, Source filtering: Disabled, Flow control: Enabled
  Device flags   : Present Running
  Interface flags: Hardware-Down SNMP-Traps Internal: 0x0
  Link flags     : None

  Logical interface xe-0/0/39.0 
    Flags: Device-Down SNMP-Traps 0x0 Encapsulation: ENET2
    eth-switch

Physical interface: bme0, Enabled, Physical link is Up
  Type: Ethernet, Link-level type: Ethernet, MTU: 1576, Clocking: Unspecified, Speed: Unspecified
  Device flags   : Present Running



    }
    ge-0/0/38 {
        unit 0 {
            family ethernet-switching;
        }
    }
    xe-0/0/38 {
        description CTD-S6-Te1/2;
        unit 0 {
            family ethernet-switching;
        }
    }
    ge-0/0/39 {
        unit 0 {
            family ethernet-switching;
        }
    }
    xe-0/0/39 {
        unit 0 {
            family ethernet-switching;
        }







garry> start shell user root 
root@:RE:0% tftp 192.168.113.1
tftp> put /config/juniper.conf.gz juniper.conf.gz
Sent 1184 bytes in 0.0 seconds
tftp> quit
root@:RE:0% exit
exit

{master:0}

[http://www.juniper.net/techpubs/en_US/junos11.4/topics/concept/spanning-trees-ex-series-mstp-understanding.html](http://www.juniper.net/techpubs/en_US/junos11.4/topics/concept/spanning-trees-ex-series-mstp-understanding.html)
[http://www.juniper.net/techpubs/en_US/junos12.2/topics/example/spanning-trees-ex-series-mstp-configuring.html](http://www.juniper.net/techpubs/en_US/junos12.2/topics/example/spanning-trees-ex-series-mstp-configuring.html)


[http://kb.juniper.net/InfoCenter/index?page=content&id=KB11194](http://kb.juniper.net/InfoCenter/index?page=content&id=KB11194)

[http://juniper.ucoz.ru/index/reserv_copy/0-45](http://juniper.ucoz.ru/index/reserv_copy/0-45)


DEBUG
[http://kb.juniper.net/InfoCenter/index?page=content&id=KB11362&actp=LIST](http://kb.juniper.net/InfoCenter/index?page=content&id=KB11362&actp=LIST)



















Вроде всё чётко

{master:0}[edit]
garry# run show spanning-tree bridge           

STP bridge parameters 
Context ID                          : 0
Enabled protocol                    : MSTP

STP bridge parameters for CIST
  Root ID                           : 8192.e0:5f:b9:52:4b:40
  Root cost                         : 0
  Root port                         : xe-0/0/38.0
  CIST regional root                : 8192.e0:5f:b9:52:4b:40
  CIST internal root cost           : 2000
  Hello time                        : 2 seconds
  Maximum age                       : 20 seconds
  Forward delay                     : 15 seconds
  Hop count                         : 19 
  Message age                       : 0 
  Number of topology changes        : 1
  Time since last topology change   : 115 seconds
  Topology change initiator         : xe-0/0/38.0
  Topology change last recvd. from  : e0:5f:b9:52:4b:41
  Local parameters 
    Bridge ID                       : 24576.64:87:88:b4:60:41
    Extended system ID              : 0
    Internal instance ID            : 0

STP bridge parameters for MSTI 1
  MSTI regional root                : 8193.5c:d9:98:3e:9a:00
  Root cost                         : 32000
  Root port                         : xe-0/0/38.0
  Hello time                        : 2 seconds
  Maximum age                       : 20 seconds
  Forward delay                     : 15 seconds
  Hop count                         : 17 
  Number of topology changes        : 1
  Topology change initiator         : xe-0/0/38.0
  Topology change last recvd. from  : e0:5f:b9:52:4b:41
  Local parameters 
    Bridge ID                       : 24577.64:87:88:b4:60:41
    Extended system ID              : 0
    Internal instance ID            : 1

STP bridge parameters for MSTI 2
  MSTI regional root                : 8194.00:1c:b1:4e:3c:80
  Root cost                         : 12000
  Root port                         : xe-0/0/38.0
  Hello time                        : 2 seconds
  Maximum age                       : 20 seconds
  Forward delay                     : 15 seconds
  Hop count                         : 18 
  Number of topology changes        : 1
  Topology change initiator         : xe-0/0/38.0
  Topology change last recvd. from  : e0:5f:b9:52:4b:41
  Local parameters 
    Bridge ID                       : 24578.64:87:88:b4:60:41
    Extended system ID              : 0
    Internal instance ID            : 2

STP bridge parameters for MSTI 3
  MSTI regional root                : 8195.00:23:ab:64:de:80
  Root cost                         : 17000
  Root port                         : xe-0/0/38.0
  Hello time                        : 2 seconds
  Maximum age                       : 20 seconds
  Forward delay                     : 15 seconds
  Hop count                         : 17 
  Number of topology changes        : 1 
  Topology change initiator         : xe-0/0/38.0
  Topology change last recvd. from  : e0:5f:b9:52:4b:41
  Local parameters                      
    Bridge ID                       : 24579.64:87:88:b4:60:41
    Extended system ID              : 0 
    Internal instance ID            : 3 
                                        
STP bridge parameters for MSTI 4
  MSTI regional root                : 8196.00:1c:b1:4e:3c:80
  Root cost                         : 12000
  Root port                         : xe-0/0/38.0
  Hello time                        : 2 seconds
  Maximum age                       : 20 seconds
  Forward delay                     : 15 seconds
  Hop count                         : 18 
  Number of topology changes        : 1 
  Topology change initiator         : xe-0/0/38.0
  Topology change last recvd. from  : e0:5f:b9:52:4b:41
  Local parameters                      
    Bridge ID                       : 24580.64:87:88:b4:60:41
    Extended system ID              : 0 
    Internal instance ID            : 4 
















Juniper

set vlans v2610 vlan-id 2610
set vlans v2620 vlan-id 2620
set vlans v2630 vlan-id 2630


set interfaces ge-0/0/36.0 family ethernet-switching port-mode trunk
set interfaces ge-0/0/37.0 family ethernet-switching port-mode trunk 
set interfaces ge-0/0/36.0 family ethernet-switching vlan members 22
set interfaces ge-0/0/37.0 family ethernet-switching vlan members 22





mstp {
    configuration-name TEST;
    revision-level 1;
    interface ge-0/0/36.0 {
        mode point-to-point;
    }
    interface ge-0/0/37.0 {
        mode point-to-point;
    }
    msti 1 {
        bridge-priority 8k;
        vlan 2610;
    }
    msti 2 {
        vlan 2620;
    }
    msti 3 {
        vlan 2630;
    }
}



    ge-0/0/36 {
        unit 0 {
            family ethernet-switching {
                port-mode trunk;
                vlan {
                    members [ 22 2610 2620 2630 ];
                }
            }
        }
    }
 
    }
    ge-0/0/37 {
        unit 0 {
            family ethernet-switching {
                port-mode trunk;        
                vlan {
                    members [ 22 2610 2620 2630 ];
                }
            }
        }
    }








Catalyst

spanning-tree mode mst
spanning-tree logging
spanning-tree extend system-id
!
spanning-tree mst configuration
 name TEST
 revision 1
 instance 1 vlan 2610
 instance 2 vlan 2620
 instance 3 vlan 2630
!
spanning-tree mst 0,3 priority 8192


interface FastEthernet0/3
 description #Link 1 MSTP
 switchport trunk encapsulation dot1q
 switchport trunk allowed vlan 22,2610,2620,2630
 switchport mode trunk
 power inline never
 load-interval 30
 storm-control broadcast level 50.00
end

k9-s6#sh run int Fa0/4
Building configuration...

Current configuration : 259 bytes
!
interface FastEthernet0/4
 description #Link 2 MSTP
 switchport trunk encapsulation dot1q
 switchport trunk allowed vlan 22,2610,2620,2630
 switchport mode trunk
 power inline never
 load-interval 30
 storm-control broadcast level 50.00
 no cdp en




DGS

 create vlan mngt22 tag 22
 config vlan mngt22 add tagged 23,24

 create vlan v2610 tag 2610
 config vlan v2610 add tagged 23,24
 config vlan v2610 add untagged 21

 create vlan v2620 tag 2620
 config vlan v2620 add tagged 23,24

 create vlan v2630 tag 2630
 config vlan v2630 add tagged 23,24

 config stp version mstp
 config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 3 fbpdu enable lbd enable lbd_recover_timer 60 nni_bpdu_addr dot1ad

 create stp instance_id 1 
 config stp instance_id 1 add_vlan 2610
 
 create stp instance_id 2 
 config stp instance_id 2 add_vlan 2620
 config stp priority 8192 instance_id 2 

 create stp instance_id 3 
config stp instance_id 3 add_vlan 2630                                                                               
                                        
                          
 config stp mst_config_id name TEST revision_level 1                          
 enable stp                                                                     
 config stp ports 23,24 externalCost auto  edge false p2p auto state enable restricted_role false restricted_tcn false lbd disable
 config stp ports 1-27 hellotime 2                                              
 config stp mst_ports 1-27 instance_id 0 internalCost auto priority 128         
config stp ports 23,24 fbpdu enable                                      
 config stp ports 1-22,25-27 externalCost auto  edge true p2p auto state disable restricted_role false restricted_tcn false lbd enable
config stp ports 1-22,25-27 fbpdu disable                                







point-to-point - это stp порт
edge - это не stp порт





Portfast -  настраивается на портах к которому подключены hosts, portfast trunk подключкается на транковом порту. (edge)
BPDUguard  - при получении bpdu порт падает в err-disable - настраивается на access портах. На клиентских портах надо настраивать например
                        BPDUguard is configured on access switch host ports were BPDU's should never be seen
BPDUfilter не пропускает bpdu - настраивается на access портах
Note: if BPDUguard and BPDUfilter are enabled on a switchport, BPDUguard will have no affect as BPDUfilter takes higher precedence over BPDUguard.
ROOTguard - защищает от получения superior BPDU от нового коммутатора, который может себя посчитать root, настраивается на портах, к которым могут быть подключены коммутаторы аксесс уровня
                            его не надо настроивать на портах, от которых ожидаешь этого BPDU, то есть от коммутаторов которые могут стать ROOT. Порт будет заблокирован.
ROOTguard is configured on distribution switch downlinks to the access layer
[https://zyxel.ru/kb/4835/](https://zyxel.ru/kb/4835/)

Loop Guard - обеспечивает дополнительную защиту на 2 уровне от возникновения петель. STP петля возникает когда блокированный порт в избыточной топологии перестаёт получать bpdu, то он думает, что может перейти в forwarding - ошибочно естественно. В случае использования Loop Guard порт после прекращения получения пакетов BPDU переводится в состояние loop-inconsistent и остаются по прежнему блокированным.
Если на блокированный порт перестаёт получать bpdu, то он думает, что может перейти в forwarding
LOOPguard is configured on links between distribution switches and uplink ports on access switches
Функция защиты от образования петель не может быть включена на портах, для которых включен протокол покрывающего дерева (RSTP или MSTP) на ZYXEL


UDLD — использует сообщения канального уровня для того чтобы обнаружить ситуацию когда коммутатор более не получает кадры от соседа. Коммутатор передающий интерфейс которого не вышел из строя, переводится в состояние err-disable. Используется на оптических портах. Причина в оптике перепутано rx tx. C точки зрения STP - возникновение петли. Механизм к STP не имеет отношение, но предотвращает петли

лупгарды на аплинке доступа
лупгарды между распределением
рутгарды на даунлинке распределения
рутгарды / бпдугарды / портфаст на даунлинке доступа

[http://www.cyberforum.ru/cisco/thread875880.html](http://www.cyberforum.ru/cisco/thread875880.html)
[https://learningnetwork.cisco.com/thread/36203](https://learningnetwork.cisco.com/thread/36203)



Поключен клиент portfast, bpduguard                                                                                                                     access port клиента в stp коммутаторе (edge порт)
Подключен trunk - сервер  portfast trunk, bpdufilter                                                                                             trunk port клиента в stp коммутаторе (edge порт)
подключен коммутатор access уровня (downlink)  rootguard, portfast trunk                                              trunk port для домового коммутатора, клиентского коммутатора в stp коммутаторе (если на нём нет stp, то edge)
подключен коммутатор равный с stp, loopguard                                                                                                trunk port для коммутатор кольца в stp коммутаторе
Порт домового коммутатора к которому подключен коммутатор района(uplink), loopguard               trunk port downlink для коммутатора (тоже самое, что пункт выше)

В случае MSTP (все коммутаторы одинаковы)
access port клиента                                                                 portfast, bpduguard    
trunk port клиента                                                                     portfast trunk, bpdufilter
trunk port коммуатора доступа, который не в STP         portfast trunk, bpdufilter


В случае RSTP агрегаторов и коммутаторов доступа ( 2 вида коммутаторов)
Аггрегатор
Порт в сторону ядра Uplink                                                 portfast trunk, bpdufilter
Порт в сторону коммутатора доступа Downlink            rootguard (restricted_role true) , portfast trunk
Порт в сторону коммутатора юриков                               portfast trunk, bpdufilter
Порт в сторону клиента access                                          portfast, bpduguard

У длинка
В сторону доступа
 config stp ports 1-20,22,25-27 externalCost auto  edge false p2p auto state enable lbd disable
 config stp ports 1-20,22-24 fbpdu enable
 
 21 UPLINK
 config stp ports 21 externalCost auto  edge true p2p auto state disable lbd disable
 config stp ports 21 fbpdu disable   
 
 Автоматом переходит в p2p, если получает fbdu
 config stp ports 23-24 externalCost auto  edge false p2p auto state disable lbd disable




Доступа
UPLINK в сторону аггрегатора                                             loopguard (point-to-point (restricted_tcn true, not edge)  
UPLINK в сторону такого же коммутатора доступа       loopguard (point-to-point (not edge) restricted_role false restricted_tcn false    config stp ports 25-28 externalCost auto edge false p2p auto state enable
DOWNLINK клиенткий access порт                                     portfast, bpduguard (restricted_role true restricted_tcn true edge true fbpdu disable)
DOWNLINK в сторону коммутатора юриков, без STP    portfast trunk, bpdufilter (edge true, restricted_role true, restricted_tcn true)
DOWNLINK в сторону оборудования радио например (trunk) portfast trunk, bpdufilter (edge true, restricted_role true, restricted_tcn true)

У длинка
config stp ports 1-24 externalCost auto edge true p2p auto state disable
config stp ports 1-24 fbpdu disable
config stp ports 1-24 restricted_role true
config stp ports 1-24 restricted_tcn true
config stp loop_guard ports 25-28 state enable     (loopguard)
config stp ports 25-28 externalCost auto edge false p2p auto state enable
config stp ports 25-28 fbpdu enable                                            
config stp ports 25-28 restricted_role false
config stp ports 26-28 restricted_tcn false
config stp ports 25 restricted_tcn true  (В сторону агреггатора)


STP Loopguard не ловит петли - функционал предназначен для защиты топологии от образования петли в случае образования односторонней связи на линке, когда по какой-то причине коммутатор не принимает приходящие на заблокированный порт BPDU, и разблокирует его, образовывая петлю.
То, что вы тестировали, совсем не похоже на тест Loopguard.

config stp version rstp
config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 6 fbpdu enable hellotime 2
config stp nni_bpdu_addr dot1d
config stp priority 32768 instance_id 0 
config stp mst_config_id name 1C:BD:B9:64:94:60 revision_level 0
config stp ports 1-24 externalCost auto edge true p2p auto state disable
config stp mst_ports 1-28 instance_id 0 internalCost auto priority 128
config stp ports 1-24 fbpdu disable
config stp ports 1-24 restricted_role true
config stp ports 1-24 restricted_tcn true
config stp loop_guard ports 1-28 state disable
config stp ports 25-28 externalCost auto edge false p2p auto state enable
config stp ports 25-28 fbpdu enable                                            
config stp ports 25-28 restricted_role false
config stp ports 25-28 restricted_tcn false
disable stp


# BPDU_PROTECTION  (Это bpdufilter или drop)   fbpdu enable   -  это функция для пересылки fbpdu через свитч, на котором stp выключена.   Если stp включена, то включает или выключает stp на порту
                                                                                
disable bpdu_protection
config bpdu_protection recovery_timer 60
config bpdu_protection trap none
config bpdu_protection log both
config bpdu_protection ports 1-28 mode shutdown




-----------------JUNIPER------------------------------
clear ethernet-switching bpdu-error почистит ошибки
show ethernet-switching interfaces


BPDUGUARD juniper
set rstp bpdu-block-on-edge interface ge-0/0/0.0 edge   - аналог bpduguard, (для подключения клиетов)
тоже самое, но порт не edge
user@switch# set ethernet-switching-options bpdu-block interface ge-0/0/5.0 shutdown
user@switch# set ethernet-switching-options bpdu-block interface ge-0/0/6.0 shutdown

 
 BPDUFilter juniper
user@switch# set protocols rstp interface ge-0/0/5.0 disable
user@switch# set protocols rstp interface ge-0/0/6.0 disable
user@switch# set ethernet-switching-options bpdu-block interface ge-0/0/5.0 drop
user@switch# set ethernet-switching-options bpdu-block interface ge-0/0/6.0 drop
 
 garry@ctd-s2# set protocols mstp interface ge-0/0/0 disable 
garry@ctd-s2# set ethernet-switching-options bpdu-block interface ge-0/0/0 drop 

 
 
 bpdu-block {
interface (interface-name disable | all);
disable-timeout seconds;
}
  [http://www.juniper.net/techpubs/en_US/junos15.1/topics/task/configuration/spanning-trees-bpdu-block-cli.html](http://www.juniper.net/techpubs/en_US/junos15.1/topics/task/configuration/spanning-trees-bpdu-block-cli.html)

  ROOTGUARD
  
set protocols mstp interface xe-0/0/2.0 mode point-to-point   no-root-port;

[edit protocols mstp interface interface-name],
[edit protocols rstp interface interface-name],
[edit protocols stp interface interface-name]
[http://www.juniper.net/techpubs/en_US/junos16.1/topics/reference/configuration-statement/no-root-port-edit-protocols-stp.html](http://www.juniper.net/techpubs/en_US/junos16.1/topics/reference/configuration-statement/no-root-port-edit-protocols-stp.html)

  
  
  
  Настройка порта edge
  [edit protocols (mstp | rstp | vstp) interface interface-name],
[edit protocols mstp msti msti-id interface interface-name],
  
  
  
  
  
Forward BPDU
Аналог bpdufilter
  config stp ports 25-28 fbpdu enable
  config stp ports 1-24 fbpdu disable
  
  
  
  
  
    Shared — порт, работающий в режиме Half Duplex
    Point-to-Point — порт, работающий в режиме Full Duplex.

  
  
logging event trunk-status
 logging event bundle-status
 logging event spanning-tree
 spanning-tree portfast trunk
 spanning-tree bpdufilter enable
 
 ___________________________________ DLINK______________________________________
 Restricted Role - это аналого Rootguard
 restricted_role true необходимо прописывать на downlink в сторону ассess уровней
 
  При настройке протоколов RSTP или MSTP на управляемых коммутаторах, расположенных на границе сети, с помощью параметра restricted_role можно ограничить роли, выполняемые портом в активной топологии. При включении этого параметра порт не будет выбран в качестве корневого порта даже в том случае, если получит BPDU с наименьшим значением приоритета. После выбора корневого порта этот порт будет выбран в качестве альтернативного. По умолчанию функция restricted_role отключена.

Этот параметр может принимать два значения: True и False. При выборе
значения TRUE этот порт не будет корневым портом для CIST или других
MSTI, даже если он будет обладать наименьшим приоритетом. Таким
образом, порт становится альтернативным портом, который будет
выбираться всегда после корневого порта. По умолчанию этот параметр
установлен как FALSE. Выбор True может привести к потере связности
покрывающего дерева. Это позволяет избежать влияния внешних мостов на активную топология покрывающего дерева, поскольку данные мосты не
находятся под управлением сетевого администратора.
 
 
   restricted_tcn (true) не фильтрует как BPDUfilter на самом же порту,  а просто не передаёт дальше. Порт на котором restricted_tcn (true) может быть в STP 
   TCN - уведомление о изменении топологии и соответсвенно порт смотрящий в сторону агрегатора не должен их получать. Ему от аггреготора может прийдти TCN только в одном случае - от других колец.
   
 Restricted TCN - The Restricted TCN parameter does not allow Topology Change Notification (TCN) BPDUs to be processed on the port.
True - The port cannot process receive/transmit TCN BPDUs.
False - The port can process receive/transmit TCN BPDU packets.
 
 Запрещает на порту коммутатора прием BPDU TCN, т.о. на данном порту не будет фиксироваться изменение топологии. По умолчанию функция выключена (значение false). Рекомендуется включать на портах, смотрящих в сторону агрегатора, чтобы изменение топологии в одном кольце не сказывалось на других
 
  Restricted Tcn - не совсем аналог BPDUfilter. Необходимо включать на портах аксеес уровня, смотрящих в сторону агреггатора, чтобы другие кольца не влияли  на наше 

  restricted_tcn (true) отключает распространение полученных с этого порта уведомлений Topology Change Notification (TCN)
Еще надо выставить клиентский порт "крайним" - edge = true

config stp ports 1-24 restricted_role true restricted_tcn true edge true
 
 
 Очень похожа на FBPDU disabled только за тем исключением что рабоатет при включённом STP и не распространяте BPDU с порта на котором включена на другие порты. 
Также защищает от распространения fake BPDU генерируемых клиентом.
 
 Restricted Tcn
Возможно два значения этого поля: True и False. При выборе значения TRUE полученные с этого порта уведомления (topology change notifications и topology change) не будут распространяться на другие порты. Этот параметр установлен в значение FALSE, по умолчанию. При установленной опции False может временно теряться связность из-за некорректных пакетов изменения топологии (topology change), полученных с клиентских портов
 
   restricted_tcn (true) не фильтрует как BPDUfilter на самом же порту,  а просто не передаёт дальше. Порт на котором restricted_tcn (true) может быть в STP 
 
 
 
 Restricted Tcn
true на edge портах
false на uplink

Возможно два значения этого поля: True и False. При выборе значения
TRUE полученные с этого порта уведомления (topology change notifications и
topology change) не будут распространяться на другие порты. Этот параметр
установлен в значение FALSE, по умолчанию. При установленной опции
False может временно теряться связность из-за некорректных пакетов
изменения топологии (topology change), полученных с клиентских портов.
P2P Значение True в данном поле означает, что данный порт является портом
point-to-point (P2P)-портом. Р2Р-порты похожи на пограничные порты,
однако Р2Р-порты обязательно должны работать в режиме полного
дуплекса. Так же как и пограничные порты, P2P-порты переходят в
состояние продвижения пакетов быстрее, обеспечивая преимущество
протокола RSTP. Значение False означает, что порт не является Р2Р-портом.
Значение Auto позволяет порту быть со статусом Р2Р всегда, когда
возможно и оперировать так, как если бы значение Р2Р-статуса было True.
Если порт по каким-либо причинам не может поддерживать этот статус
(например, если порт был принудительно поставлен в режим полу-
дуплекса), порт будет оперировать так, как если бы значение P2P-статуса
было False. Значение по умолчанию для данного параметра Auto.


Возможно два значения этого поля: True и False. При выборе значения
TRUE полученные с этого порта уведомления (topology change notifications и
topology change) не будут распространяться на другие порты. Этот параметр
установлен в значение FALSE, по умолчанию. При установленной опции
False может временно теряться связность из-за некорректных пакетов
изменения топологии (topology change), полученных с клиентских портов.

 
 
 
 
 Migration

При установке значения "yes" порты будут посылать BPDU-пакеты на
другие мосты, запрашивая информацию об их настройках STP. Если
коммутатор сконфигурирован под RSTP, порт может мигрировать от 802.1d
STP до 802.1w RSTP. Если Коммутатор настроен на использование
протокола MSTP, порт может автоматически выбирать сове состояние
между 802.1d STP и 802.1s MSTP. RSTP и MSTP поддерживают
совместимость со стандартом STP, однако, преимущества RSTP и MSTP не
реализуются на порту при соединении 802.1d с 802.1w или 802.1s.

Edge

Выбор значения True в данном поле определяет порт как пограничный.
Пограничный порт подключен к сегменту сети, на котором невозможно
образование петли. Пограничный порт не должен принимать BPDU-пакеты.
Если был принят BPDU-пакет, это приведёт к автоматической потере
статуса пограничного порта. Выбор значения False означает, что порт не
является пограничным портом.
 
 
 
 
 
 
 
 
 
 
 
 Попробовать включить restricted_role true на порта DGS3627G k9-s9
 
 
 
 
 
 
 
 
 
 ERPS
