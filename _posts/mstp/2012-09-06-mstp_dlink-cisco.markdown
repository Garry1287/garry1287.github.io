---
layout: post
title:  "mstp_dlink-cisco"
date:   2012-09-06 13:12:11 +0400
categories: mstp
tags: mstp
---

# mstp_dlink-cisco
Вот, нашёл среди Цисковых мануалов:
STP Root Guard. Во всех топологиях Ethernet уровня 2, обеспечивающих резервирование каналов связи, для предотвращения зацикливания в сети используется протокол покрывающего дерева (STP). Хакер может злонамеренно нарушить стабильность топологии STP посредством ввода в топологию нового корневого узла STP (STP Root). В процессе схождения протокола STP абоненты порта доступа не имеют доступа к своим сетевым услугам. Функция STP Root Guard не дает хакеру возможности изменить корневой узел STP. Функция защиты корневого узла протокола покрывающего дерева (STP) не позволяет сделать корневым узлом STP в сети провайдера услуг коммутаторы, установленные у клиента. Конфигурирование защиты корневого узла осуществляется посредством активирования этой функции на интерфейсе, ведущем к другому коммутатору. В случае, если подключенный к абонентскому порту коммутатор попытается стать корневым коммутатором, данный порт будет заблокирован.

То бишь если на порт с включённой настройкой STP Root Guard приходит BPDU-пакетик от якобы нового рута, то свитч тупо блокирует этот порт (можно, например на некоторое время, как это сделано в LBD), а не начинает перестраивать всю топологию.

Таким образом, если на этом порту сидит мега-хакер - он потеряет возможность обьявить себя рутом в сети и тем самым нарушить работу этой сети. А если где-то в сети есть колечко и на этот порт придёт нормальный пакетик от нормального рута, то порт так же будет заблокирован.
То бишь в обоих случаях - устойчивость сети к нелегальным действиям конечных клиентов возрастает. 


restricted_role (true) запрещает порту становиться корневым
restricted_tcn (true) отключает распространение полученных с этого порта уведомлений Topology Change Notification (TCN)
Еще надо выставить клиентский порт "крайним" - edge = true

config stp ports 1-24 restricted_role true restricted_tcn true edge true

Таким образом, клиент теперь не может перестроить дерево.






edge port
На них должно быть включено STP и LBD. Ну а от перестроения дерева спасает только отключения STP на порту. Но тогда не будут отрабатываться петли между портами.




На магистральных loopdetect необходимо выключить, в новых версиях ПО он и stp не работают совместно на портах. 
2) Restricted_role [true | false] – If true causes the Port not to be selected as Root Port for the CIST or any MSTI, even it has the best spanning tree priority vector. Such a Port will be selected as an Alternate Port after the Root Port has been selected. This parameter should be false by default. If set, it can cause lack of spanning tree connectivity. It is set by a network administrator to prevent bridges external to a core region of the network influencing the spanning tree active topology, possibly because those bridges are not under the full control of the administrator. Если в двух словах то она на входе отбрасывает root-ые BPDU, защищая тем самым от того что клиент может посылать BPDU как бы от имени корня и перестраивая тем самым дерево. Работает при включенном STP на порту.
3) Restricted_tcn [true | false] – If true causes the Port not to propagate received topology change notifications and topology changes to other Ports. This parameter should be false by default. If set it can cause temporary loss of connectivity after changes in a spanning trees active topology as a result of persistent incorrectly learned station location information.
It is set by a network administrator to prevent bridges external to a core region of the network, causing address flushing in that region, possibly because those bridges are not under the full control of the administrator or MAC_Operational for the attached LANs transitions frequently.
Очень похожа на FBPDU disabled только за тем исключением что рабоатет при включённом STP и не распространяте BPDU с порта на котором включена на другие порты. 
Также защищает от распространения fake BPDU генерируемых клиентом.



Как-то не очень все вяжется... Разнотолки какие-то... В документации одно, на форуме другое... Давайте по порядку? Беру доку от 36-го свитча:
config stp:
fbpdu [enable | disable] − Allows the forwarding of STP BPDU packets from other network devices when STP is disabled on the Switch. The default is enable.
Разрешает форвардинг BPDU пакетов через свитч, когда STP выключено. По умолчанию включено. Значит ли это, что эта настройка не действует при включенном STP? значит ли это, что включенная опция (true) разрешает форвардинг пакетов, а не фильрацию?
config stp ports:
fbpdu [enable | disable] − Allows the forwarding of STP BPDU packets from other network devices when STP is disabled on the Switch. This function can only be in use when STP is globally disabled and forwarding BPDU packets is enabled. The default is enabled and BPDU packets will not be forwarded.
Разрешает форвардинг BPDU пакетов от других сетевый устройств (т.е. подразумеваем, что действует на входящий траффик?) (и снова) когда STP ВЫКЛЮЧЕН на свитче. Это действует ТОЛЬКО когда STP выключен ГЛОБАЛЬНО и форвардинг пакетов включен. По умолчанию ВКЛЮЧЕН и BPDU пакеты НЕ будут переданы. :shock:

Иван, не моглы бы Вы научить правильно понимать эти пункты? Моя логика отказывает... У нас есть свитчи и с выключенным STP и важно понимать что мы включаем а что мы выключаем.

Берем доку 35-й серии R5
Choosing True will allow the forwarding of BPDU packets in the specified ports from other network devices. This will go into effect only if STP is globally disabled AND Forwarding BPDU is globally enabled (See STP Bridge Global Settings above). The default setting False, does not forward BPDU packets when STP is disabled.
Здесь с логикой все более хорошо, по умолчанию выключено и не форвардит. Но, опытным путем было замечено - ФОРВАРДИТ! STP было выключено, fbpdu false. Таки оно не рабочее, или таки оно на исходящие BPDU действует?

Restricted_Role и Restricted_TCN - в доке по 36-му не нашел. Видимо, этих опций там нет (Firmware Version : Build 2.40-B51). В доке по 35-му не совсем понял. Не могли бы Вы пояснить механизм действия этих опций на 35-й и как управлять форвардингом BPDU пакетов в случае включенного STP на 36-й?
Завтра исследование будет продолжено, но, было бы гораздо легче, если бы документация и фактическое поведение соответствовали друг другу...



1) FBPDU действительно работает только при выключенном STP. Оно позволяет не распространять BPDU с порта на котором эта опция стоит в disable.
2) Restricted_role [true | false] – If true causes the Port not to be selected as Root Port for the CIST or any MSTI, even it has the best spanning tree priority vector. Such a Port will be selected as an Alternate Port after the Root Port has been selected. This parameter should be false by default. If set, it can cause lack of spanning tree connectivity. It is set by a network administrator to prevent bridges external to a core region of the network influencing the spanning tree active topology, possibly because those bridges are not under the full control of the administrator. Если в двух словах то она на входе отбрасывает root-ые BPDU, защищая тем самым от того что клиент может посылать BPDU как бы от имени корня и перестраивая тем самым дерево. Работает при включенном STP на порту.
3) Restricted_tcn [true | false] – If true causes the Port not to propagate received topology change notifications and topology changes to other Ports. This parameter should be false by default. If set it can cause temporary loss of connectivity after changes in a spanning trees active topology as a result of persistent incorrectly learned station location information. It is set by a network administrator to prevent bridges external to a core region of the network, causing address flushing in that region, possibly because those bridges are not under the full control of the administrator or MAC_Operational for the attached LANs transitions frequently. Очень похожа на FBPDU disabled только за тем исключением что рабоатет при включённом STP и не распространяте BPDU с порта на котором включена на другие порты. Также защищает от распространения fake BPDU генерируемых клиентом.


D-Link мануал писал(а):Edge
Выбор значения True в данном поле определяет порт как пограничный. Пограничный порт подключен к сегменту сети, на котором невозможно образование петли. Пограничный порт не должен принимать BPDU-пакеты. Если был принят BPDU-пакет, это приведёт к автоматической потере статуса пограничного порта. Выбор значения False означает, что порт не является пограничным портом.


Restricted Role
Этот параметр может принимать два значения: True и False. При выборе значения TRUE этот порт не будет корневым портом для CIST или других MSTI, даже если он будет обладать наименьшим приоритетом. Таким образом, порт становится альтернативным портом, который будет выбираться всегда после корневого порта. По умолчанию этот параметр установлен как FALSE. Выбор True может привести к потере связности покрывающего дерева. Это позволяет избежать влияния внешних мостов на активную топологию покрывающего дерева, поскольку данные мосты не находятся под управлением сетевого администратора.


Restricted Tcn
Возможно два значения этого поля: True и False. При выборе значения TRUE полученные с этого порта уведомления (topology change notifications и topology change) не будут распространяться на другие порты. Этот параметр установлен в значение FALSE, по умолчанию. При установленной опции False может временно теряться связность из-за некорректных пакетов изменения топологии (topology change), полученных с клиентских портов






Portfast — функция, которая позволяет порту пропустить состояния listening и learning и сразу же перейти в состояние forwarding. Настраивается на портах уровня доступа, к которым подключены пользователи или сервера.

Порт с включенной функцией Port Fast проходит через обычный цикл состояний spanning-tree, когда коммутатор перезагружается.


Цель функции Port Fast минимизировать время, которое необходимо для того чтобы порт перешел в состояние forward. Поэтому она эффективна только когда применена к портам, к которым подключены хосты. Если включить Port Fast на портах, которые соединены с другими коммутаторами, то есть риск создания петли. Включение этой функции, так же препятствует возникновению сообщений о изменении состояния порта TCN BPDU (topology change notification Bridge Protocol Data Unit) 





Portfast — функция, которая позволяет порту пропустить состояния listening и learning и сразу же перейти в состояние forwarding. Настраивается на портах уровня доступа, к которым подключены пользователи или сервера.

Порт с включенной функцией Port Fast проходит через обычный цикл состояний spanning-tree, когда коммутатор перезагружается.

Note-icon.gif

Цель функции Port Fast минимизировать время, которое необходимо для того чтобы порт перешел в состояние forward. Поэтому она эффективна только когда применена к портам, к которым подключены хосты.
 Если включить Port Fast на портах, которые соединены с другими коммутаторами, то есть риск создания петли. 
Включение этой функции, так же препятствует возникновению сообщений о изменении состояния порта TCN BPDU (topology change notification Bridge Protocol Data Unit) 







Пример

Сatalyst						Dlink DGS3527G
_______________________				  _____________________
|		3 порт|___________________________|23 порт		|
|		4 порт|___________________________|24 порт		|
|_____________________|				  |____________________ |



Имеем два одинаковых линка и приоритет использования высчитывается согласно номеру порта



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




По умолчанию получаем, что траффик не балансируется
 
Сatalyst
##### MST0    vlans mapped:   1-21,23-2609,2611-2619,2621-2629,2631-2639
                               2641-2649,2651-2659,2661-4094
Bridge        address 0013.1afa.6280  priority      8192  (8192 sysid 0)
Root          this switch for the CIST
Operational   hello time 2 , forward delay 15, max age 20, txholdcount 6 
Configured    hello time 2 , forward delay 15, max age 20, max hops    20

Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/3            Desg FWD 200000    128.3    P2p 
Fa0/4            Desg FWD 200000    128.4    P2p 
Fa0/24           Desg FWD 200000    128.24   P2p Edge 

##### MST1    vlans mapped:   22,2610,2620,2630
Bridge        address 0013.1afa.6280  priority      8193  (8192 sysid 1)
Root          this switch for MST1

Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/3            Desg FWD 200000    128.3    P2p 
Fa0/4            Desg FWD 200000    128.4    P2p 
Fa0/24           Desg FWD 200000    128.24   P2p Edge 

##### MST2    vlans mapped:   2640,2650,2660
Bridge        address 0013.1afa.6280  priority      32770 (32768 sysid 2)
Root          address 5cd9.983e.9d00  priority      8194  (8192 sysid 2)
              port    Fa0/3           cost          200000    rem hops 19

Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/3            Root FWD 200000    128.3    P2p 
Fa0/4            Altn BLK 200000    128.4    P2p 



Dlink

show stp ports   24                                              Command: show stp ports 24_ports 24 instance_id 1 internalCost 100000 priority 128

 MSTP Port Information
 ----------------------
 Port Index     : 24    , Hello Time: 2 /2 , Port STP : Enabled  , LBD : No 
 External PathCost : Auto/200000   , Edge Port : No /No , P2P : Auto /Yes
 Port Forward BPDU : Enabled  
 MSTI   Designated Bridge   Internal PathCost  Prio  Status      Role
 -----  ------------------  -----------------  ----  ----------  ----------
 0      2000/00131AFA6280   200000             128   Discarding  Alternate 
 1      2001/00131AFA6280   200000             128   Discarding  Alternate 
 2      2002/5CD9983E9D00   200000             128   Forwarding  Designated


DGS-3627G:5#show stp ports   23
Command: show stp ports 23

 MSTP Port Information
 ----------------------
 Port Index     : 23    , Hello Time: 2 /2 , Port STP : Enabled  , LBD : No 
 External PathCost : Auto/200000   , Edge Port : No /No , P2P : Auto /Yes
 Port Forward BPDU : Enabled  
 MSTI   Designated Bridge   Internal PathCost  Prio  Status      Role
 -----  ------------------  -----------------  ----  ----------  ----------
 0      2000/00131AFA6280   200000             128   Forwarding  Root      
 1      2001/00131AFA6280   200000             128   Forwarding  Root      
 2      2002/5CD9983E9D00   200000             128   Forwarding  Designated



Получается для всех 3 инстансов Линк между 4 портом Catalyst и 24 портом Dlink является Alternate




Чтобы поменять
int Fa0/4                      
spanning-tree mst 2 cost 100000



Результат
##### MST2    vlans mapped:   2640,2650,2660
Bridge        address 0013.1afa.6280  priority      32770 (32768 sysid 2)
Root          address 5cd9.983e.9d00  priority      8194  (8192 sysid 2)
              port    Fa0/4           cost          100000    rem hops 19

Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/3            Altn BLK 200000    128.3    P2p 
Fa0/4            Root FWD 100000    128.4    P2p 


Получаем, что Fa0/3 и становиться альтернативным и второй инстанс будет работать по линку между 4 портом Catalyst и 24 портом Dlink






Для Длинка
Для того чтобы развернуть например теперь 1 инстанс надо выполнить команду на Dlink

Даем команду и устанавливаем для 24 порта в 1 инстансе стоимость равную 100000
 config stp mst_ports 24 instance_id 1 internalCost 100000 priority 128

В результате первый инстанс перестраивается
23 порт становиться альтернативным, 24 порт - становиться root

DGS-3627G:5#show stp ports   23
Command: show stp ports 23

 MSTP Port Information
 ----------------------
 Port Index     : 23    , Hello Time: 2 /2 , Port STP : Enabled  , LBD : No 
 External PathCost : Auto/200000   , Edge Port : No /No , P2P : Auto /Yes
 Port Forward BPDU : Enabled  
 MSTI   Designated Bridge   Internal PathCost  Prio  Status      Role
 -----  ------------------  -----------------  ----  ----------  ----------
 0      2000/00131AFA6280   200000             128   Forwarding  Root      
 1      2001/00131AFA6280   200000             128   Discarding  Alternate 
 2      2002/5CD9983E9D00   200000             128   Forwarding  Designated




                                                                               
DGS-3627G:5#show stp ports   24
Command: show stp ports 24

 MSTP Port Information
 ----------------------
 Port Index     : 24    , Hello Time: 2 /2 , Port STP : Enabled  , LBD : No 
 External PathCost : Auto/200000   , Edge Port : No /No , P2P : Auto /Yes
 Port Forward BPDU : Enabled  
 MSTI   Designated Bridge   Internal PathCost  Prio  Status      Role
 -----  ------------------  -----------------  ----  ----------  ----------
 0      2000/00131AFA6280   200000             128   Discarding  Alternate 
 1      2001/00131AFA6280   100000             128   Forwarding  Root      
 2      2002/5CD9983E9D00   200000             128   Forwarding  Designated



Для того чтобы вернуть как было.
config stp mst_ports 24 instance_id 1 internalCost auto priority 128



ДЛЯ УСТАНОВКИ ПРАВИЛЬНЫХ ПРИОРИТЕТОВ НЕОБХОДИМО НА НЕ РУТОВОМ СВИТЧЕ В НУЖНОМ ИНСТАНСЕ НА ПОРТУ КОТОРЫЙ НУЖНО ИСПОЛЬЗОВАТЬ ПРОПИСЫВАТЬ
МЕНЬШИЙ COST (на root портах и на alt портах)

config stp mst_ports 1 instance_id 2 internalCost 5000 priority 128
spanning-tree mst 2 cost 5000





Второй способ балансироки

Делаем приоритет во 2 инстансе на Dlink для 24 порта равным 64

config stp mst_ports 24 instance_id 2 internalCost auto priority 64

DGS-3627G:5#show stp ports   24
Command: show stp ports 24

 MSTP Port Information
 ----------------------
 Port Index     : 24    , Hello Time: 2 /2 , Port STP : Enabled  , LBD : No 
 External PathCost : Auto/200000   , Edge Port : No /No , P2P : Auto /Yes
 Port Forward BPDU : Enabled  
 MSTI   Designated Bridge   Internal PathCost  Prio  Status      Role
 -----  ------------------  -----------------  ----  ----------  ----------
 0      2000/00131AFA6280   200000             128   Discarding  Alternate 
 1      2001/00131AFA6280   200000             128   Discarding  Alternate 
 2      2002/5CD9983E9D00   200000             64    Forwarding  Designated



И видим что на Каталисте 3 порт стал альтернативным, а 4 root

k9-s6#sh spanning-tree mst

##### MST0    vlans mapped:   1-21,23-2609,2611-2619,2621-2629,2631-2639
                               2641-2649,2651-2659,2661-4094
Bridge        address 0013.1afa.6280  priority      8192  (8192 sysid 0)
Root          this switch for the CIST
Operational   hello time 2 , forward delay 15, max age 20, txholdcount 6 
Configured    hello time 2 , forward delay 15, max age 20, max hops    20

Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/3            Desg FWD 200000    128.3    P2p 
Fa0/4            Desg FWD 200000    128.4    P2p 
Fa0/24           Desg FWD 200000    128.24   P2p Edge 

##### MST1    vlans mapped:   22,2610,2620,2630
Bridge        address 0013.1afa.6280  priority      8193  (8192 sysid 1)
Root          this switch for MST1

Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/3            Desg FWD 200000    128.3    P2p 
Fa0/4            Desg FWD 200000    128.4    P2p 
Fa0/24           Desg FWD 200000    128.24   P2p Edge 

##### MST2    vlans mapped:   2640,2650,2660
Bridge        address 0013.1afa.6280  priority      32770 (32768 sysid 2)
Root          address 5cd9.983e.9d00  priority      8194  (8192 sysid 2)
              port    Fa0/4           cost          200000    rem hops 19

Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/3            Altn BLK 200000    128.3    P2p 
Fa0/4            Root FWD 200000    128.4    P2p 


Получается, что пустили 2 инстанс через линк 4 портом Catalyst и 24 портом Dlink

И теперь развернём 1 инстанс таким же образом

Делаем на Catalyst
(config)#int Fa0/4
(config-if)#spanning-tree mst 1 port-priority 64


Результат

DGS-3627G:5#show stp ports   24                                                 
Command: show stp ports 24

 MSTP Port Information
 ----------------------
 Port Index     : 24    , Hello Time: 2 /2 , Port STP : Enabled  , LBD : No 
 External PathCost : Auto/200000   , Edge Port : No /No , P2P : Auto /Yes
 Port Forward BPDU : Enabled  
 MSTI   Designated Bridge   Internal PathCost  Prio  Status      Role
 -----  ------------------  -----------------  ----  ----------  ----------
 0      2000/00131AFA6280   200000             128   Discarding  Alternate 
 1      2001/00131AFA6280   200000             128   Forwarding  Root      
 2      2002/5CD9983E9D00   200000             128   Forwarding  Designated




                                                                             
DGS-3627G:5#show stp ports   23
Command: show stp ports 23

 MSTP Port Information
 ----------------------
 Port Index     : 23    , Hello Time: 2 /2 , Port STP : Enabled  , LBD : No 
 External PathCost : Auto/200000   , Edge Port : No /No , P2P : Auto /Yes
 Port Forward BPDU : Enabled  
 MSTI   Designated Bridge   Internal PathCost  Prio  Status      Role
 -----  ------------------  -----------------  ----  ----------  ----------
 0      2000/00131AFA6280   200000             128   Forwarding  Root      
 1      2001/00131AFA6280   200000             128   Discarding  Alternate 
 2      2002/5CD9983E9D00   200000             128   Forwarding  Designated




Вывод - имеем 2 способа управлять потоками траффика
1. На свитче, у которого ALT и ROOT порты, в нашем случае - который не корневой, прописываем path cost меньшую чем стандартная на ALT порту
и дерево перестраивается. Естественно делаем всё это в соответствующем инстансе
2. На свитче, у которого 2 Designated порта (Dlink для второго инстанса) прописываем для одного из них port priority меньшую, чем стандартная.
  В данном случае для 24 порта прописываем больший приоритет и дерево перестраивается.































Конфигурация для Промсвязи


instance 1
1021
284
294
298
214
648
671
691
693
861
862
953
954
1023
2007
2008
2500





instance 2
10
132
154
2999
9
16
100
101
105
109
151
152
201
204
628
629
700
817
895
1026
2503
4000
4001
172
1029



instance 3
1030

54
55
57
58
60
202
213
281
577
787
894
1011
1012
1019
2002
773
778
68
203
272
833
1022
3154

instance 4
21
22
23
24
25
26
34
36
38
205
1027
1953
1952
11
106
113
122
165
206
3998
1017
1024
1025
1950
1951
1955
1956
1957


spanning-tree mst 2 priority 28672 (secondary)
spanning-tree mst 3 priority 24576 (primary)



Конфиги mstp

cde-s0
spanning-tree mst configuration
 name PSI
 revision 777
 instance 1 vlan 214,284,294,298,648,671,691,693,861,862,953,954,1021,1023,2007,2008,2500
 instance 2 vlan 9,10,13,16,100,101,105,109,132,151,152,154,172,201,204,628,629,700,817,895,1026,1029,2503,2999,4000,4001
 instance 3 vlan 54,55,57,58,60,68,202,203,213,272,281,577,773,778,787,833,894,1011,1012,1019,1022,2002,3154
 instance 4 vlan 11,21,22,23,24,25,26,34,36,38,106,113,122,165,205,206,1017,1024,1025,1027,1950,1951,1952,1953,1955,1956,1957,3998
!
spanning-tree mst 0-1 priority 24576
spanning-tree mst 2 priority 28672
spanning-tree mst 4 priority 28672

ctd-s1
spanning-tree mst configuration
 name PSI
 revision 777
 instance 1 vlan 214,284,294,298,648,671,691,693,861,862,953,954,1021,1023,2007,2008,2500
 instance 2 vlan 9,10,13,16,100,101,105,109,132,151,152,154,172,201,204,628,629,700,817,895,1026,1029,2503,2999,4000,4001
 instance 3 vlan 54,55,57,58,60,68,202,203,213,272,281,577,773,778,787,833,894,1011,1012,1019,1022,2002,3154
 instance 4 vlan 11,21,22,23,24,25,26,34,36,38,106,113,122,165,205,206,1017,1024,1025,1027,1950,1951,1952,1953,1955,1956,1957,3998
!
spanning-tree mst 2 priority 24576
spanning-tree mst 0-1 priority 28672
spanning-tree mst 4 priority 24576

ats45-s0
spanning-tree mst configuration
 name PSI
 revision 777
 instance 1 vlan 214,284,294,298,648,671,691,693,861,862,953,954,1021,1023,2007,2008,2500
 instance 2 vlan 9,10,13,16,100,101,105,109,132,151,152,154,172,201,204,628,629,700,817,895,1026,1029,2503,2999,4000,4001
 instance 3 vlan 54,55,57,58,60,68,202,203,213,272,281,577,773,778,787,833,894,1011,1012,1019,1022,2002,3154
 instance 4 vlan 11,21,22,23,24,25,26,34,36,38,106,113,122,165,205,206,1017,1024,1025,1027,1950,1951,1952,1953,1955,1956,1957,3998
!
spanning-tree mst 3 priority 24576


ctd-s6
spanning-tree mst configuration
 name PSI
 revision 777
 instance 1 vlan 214,284,294,298,648,671,691,693,861,862,953,954,1021,1023,2007,2008,2500
 instance 2 vlan 9,10,13,16,100,101,105,109,132,151,152,154,172,201,204,628,629,700,817,895,1026,1029,2503,2999,4000,4001
 instance 3 vlan 54,55,57,58,60,68,202,203,213,272,281,577,773,778,787,833,894,1011,1012,1019,1022,2002,3154
 instance 4 vlan 11,21,22,23,24,25,26,34,36,38,106,113,122,165,205,206,1017,1024,1025,1027,1950,1951,1952,1953,1955,1956,1957,3998
!


k9-s9
 config stp version mstp
 config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 3 fbpdu enable lbd enable lbd_recover_timer 60
 config stp priority 32768 instance_id 0 
 create stp instance_id 1 
config stp instance_id 1 add_vlan 214
config stp instance_id 1 add_vlan 284
config stp instance_id 1 add_vlan 294
config stp instance_id 1 add_vlan 298
config stp instance_id 1 add_vlan 648
config stp instance_id 1 add_vlan 671
config stp instance_id 1 add_vlan 691
config stp instance_id 1 add_vlan 693
config stp instance_id 1 add_vlan 861
config stp instance_id 1 add_vlan 862
config stp instance_id 1 add_vlan 953
config stp instance_id 1 add_vlan 954
config stp instance_id 1 add_vlan 1021
config stp instance_id 1 add_vlan 1023
config stp instance_id 1 add_vlan 2007
config stp instance_id 1 add_vlan 2008
config stp instance_id 1 add_vlan 2500
   config stp priority 32768 instance_id 1 
   create stp instance_id 2 
config stp instance_id 2 add_vlan 9
config stp instance_id 2 add_vlan 10
config stp instance_id 2 add_vlan 13
config stp instance_id 2 add_vlan 16
config stp instance_id 2 add_vlan 100
config stp instance_id 2 add_vlan 101
config stp instance_id 2 add_vlan 105
config stp instance_id 2 add_vlan 109
config stp instance_id 2 add_vlan 132
config stp instance_id 2 add_vlan 151
config stp instance_id 2 add_vlan 152
config stp instance_id 2 add_vlan 154
config stp instance_id 2 add_vlan 172
config stp instance_id 2 add_vlan 201
config stp instance_id 2 add_vlan 204
config stp instance_id 2 add_vlan 628
config stp instance_id 2 add_vlan 629
config stp instance_id 2 add_vlan 700
config stp instance_id 2 add_vlan 817
config stp instance_id 2 add_vlan 895
config stp instance_id 2 add_vlan 1026
config stp instance_id 2 add_vlan 1029
config stp instance_id 2 add_vlan 2503
config stp instance_id 2 add_vlan 2999
config stp instance_id 2 add_vlan 4000
config stp instance_id 2 add_vlan 4001
   config stp priority 32768 instance_id 2 
   create stp instance_id 3 
config stp instance_id 3 add_vlan 54
config stp instance_id 3 add_vlan 55
config stp instance_id 3 add_vlan 57
config stp instance_id 3 add_vlan 58
config stp instance_id 3 add_vlan 60
config stp instance_id 3 add_vlan 68
config stp instance_id 3 add_vlan 202
config stp instance_id 3 add_vlan 203
config stp instance_id 3 add_vlan 213
config stp instance_id 3 add_vlan 272
config stp instance_id 3 add_vlan 281
config stp instance_id 3 add_vlan 577
config stp instance_id 3 add_vlan 773
config stp instance_id 3 add_vlan 778
config stp instance_id 3 add_vlan 787
config stp instance_id 3 add_vlan 833
config stp instance_id 3 add_vlan 894
config stp instance_id 3 add_vlan 1011
config stp instance_id 3 add_vlan 1012
config stp instance_id 3 add_vlan 1019
config stp instance_id 3 add_vlan 1022
config stp instance_id 3 add_vlan 2002
config stp instance_id 3 add_vlan 3154
   config stp priority 32768 instance_id 3
   create stp instance_id 4
config stp instance_id 4 add_vlan 11
config stp instance_id 4 add_vlan 21
config stp instance_id 4 add_vlan 22
config stp instance_id 4 add_vlan 23
config stp instance_id 4 add_vlan 24
config stp instance_id 4 add_vlan 25
config stp instance_id 4 add_vlan 26
config stp instance_id 4 add_vlan 34
config stp instance_id 4 add_vlan 36
config stp instance_id 4 add_vlan 38
config stp instance_id 4 add_vlan 106
config stp instance_id 4 add_vlan 113
config stp instance_id 4 add_vlan 122
config stp instance_id 4 add_vlan 165
config stp instance_id 4 add_vlan 205
config stp instance_id 4 add_vlan 206
config stp instance_id 4 add_vlan 1017
config stp instance_id 4 add_vlan 1024
config stp instance_id 4 add_vlan 1025
config stp instance_id 4 add_vlan 1027
config stp instance_id 4 add_vlan 1950
config stp instance_id 4 add_vlan 1951
config stp instance_id 4 add_vlan 1952
config stp instance_id 4 add_vlan 1953
config stp instance_id 4 add_vlan 1955
config stp instance_id 4 add_vlan 1956
config stp instance_id 4 add_vlan 1957
config stp instance_id 4 add_vlan 3998
   config stp priority 32768 instance_id 4     
config stp mst_config_id name PSI revision_level 777
enable stp
config stp ports 1-23 externalCost auto  edge true p2p auto state disable lbd enable
config stp ports 25 externalCost auto  edge true p2p auto state disable lbd enable
config stp ports 27 externalCost auto  edge true p2p auto state disable lbd enable 
config stp ports 1-27 hellotime 2 
config stp mst_ports 1-27 instance_id 0 internalCost auto priority 128
config stp ports 1-23 fbpdu disable
config stp ports 25 fbpdu disable
config stp ports 27 fbpdu disable
config stp ports 24 externalCost auto  edge false p2p auto state enable lbd disable
config stp ports 26 externalCost auto  edge false p2p auto state enable lbd disable
config stp ports 24 fbpdu enable
config stp ports 26 fbpdu enable
config stp mst_ports 1-27 instance_id 1 internalCost auto priority 128
config stp mst_ports 1-27 instance_id 2 internalCost auto priority 128


k9-s4




 config stp version mstp
 config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 3 fbpdu enable lbd enable lbd_recover_timer 60
 config stp priority 32768 instance_id 0 
  create stp instance_id 1 
config stp instance_id 1 add_vlan 214
config stp instance_id 1 add_vlan 284
config stp instance_id 1 add_vlan 294
config stp instance_id 1 add_vlan 298
config stp instance_id 1 add_vlan 648
config stp instance_id 1 add_vlan 671
config stp instance_id 1 add_vlan 691
config stp instance_id 1 add_vlan 693
config stp instance_id 1 add_vlan 861
config stp instance_id 1 add_vlan 862
config stp instance_id 1 add_vlan 953
config stp instance_id 1 add_vlan 954
config stp instance_id 1 add_vlan 1021
config stp instance_id 1 add_vlan 1023
config stp instance_id 1 add_vlan 2007
config stp instance_id 1 add_vlan 2008
config stp instance_id 1 add_vlan 2500
   config stp priority 32768 instance_id 1 
   create stp instance_id 2 
config stp instance_id 2 add_vlan 9
config stp instance_id 2 add_vlan 10
config stp instance_id 2 add_vlan 13
config stp instance_id 2 add_vlan 16
config stp instance_id 2 add_vlan 100
config stp instance_id 2 add_vlan 101
config stp instance_id 2 add_vlan 105
config stp instance_id 2 add_vlan 109
config stp instance_id 2 add_vlan 132
config stp instance_id 2 add_vlan 151
config stp instance_id 2 add_vlan 152
config stp instance_id 2 add_vlan 154
config stp instance_id 2 add_vlan 172
config stp instance_id 2 add_vlan 201
config stp instance_id 2 add_vlan 204
config stp instance_id 2 add_vlan 628
config stp instance_id 2 add_vlan 629
config stp instance_id 2 add_vlan 700
config stp instance_id 2 add_vlan 817
config stp instance_id 2 add_vlan 895
config stp instance_id 2 add_vlan 1026
config stp instance_id 2 add_vlan 1029
config stp instance_id 2 add_vlan 2503
config stp instance_id 2 add_vlan 2999
config stp instance_id 2 add_vlan 4000
config stp instance_id 2 add_vlan 4001
   config stp priority 32768 instance_id 2 
   create stp instance_id 3 
config stp instance_id 3 add_vlan 54
config stp instance_id 3 add_vlan 55
config stp instance_id 3 add_vlan 57
config stp instance_id 3 add_vlan 58
config stp instance_id 3 add_vlan 60
config stp instance_id 3 add_vlan 68
config stp instance_id 3 add_vlan 202
config stp instance_id 3 add_vlan 203
config stp instance_id 3 add_vlan 213
config stp instance_id 3 add_vlan 272
config stp instance_id 3 add_vlan 281
config stp instance_id 3 add_vlan 577
config stp instance_id 3 add_vlan 773
config stp instance_id 3 add_vlan 778
config stp instance_id 3 add_vlan 787
config stp instance_id 3 add_vlan 833
config stp instance_id 3 add_vlan 894
config stp instance_id 3 add_vlan 1011
config stp instance_id 3 add_vlan 1012
config stp instance_id 3 add_vlan 1019
config stp instance_id 3 add_vlan 1022
config stp instance_id 3 add_vlan 2002
config stp instance_id 3 add_vlan 3154
   config stp priority 28672 instance_id 3
   create stp instance_id 4
config stp instance_id 4 add_vlan 11
config stp instance_id 4 add_vlan 21
config stp instance_id 4 add_vlan 22
config stp instance_id 4 add_vlan 23
config stp instance_id 4 add_vlan 24
config stp instance_id 4 add_vlan 25
config stp instance_id 4 add_vlan 26
config stp instance_id 4 add_vlan 34
config stp instance_id 4 add_vlan 36
config stp instance_id 4 add_vlan 38
config stp instance_id 4 add_vlan 106
config stp instance_id 4 add_vlan 113
config stp instance_id 4 add_vlan 122
config stp instance_id 4 add_vlan 165
config stp instance_id 4 add_vlan 205
config stp instance_id 4 add_vlan 206
config stp instance_id 4 add_vlan 1017
config stp instance_id 4 add_vlan 1024
config stp instance_id 4 add_vlan 1025
config stp instance_id 4 add_vlan 1027
config stp instance_id 4 add_vlan 1950
config stp instance_id 4 add_vlan 1951
config stp instance_id 4 add_vlan 1952
config stp instance_id 4 add_vlan 1953
config stp instance_id 4 add_vlan 1955
config stp instance_id 4 add_vlan 1956
config stp instance_id 4 add_vlan 1957
config stp instance_id 4 add_vlan 3998
   config stp priority 32768 instance_id 4   
config stp mst_config_id name PSI revision_level 777
enable stp
config stp ports 1-18 externalCost auto  edge true p2p auto state disable lbd enable
config stp ports 21-23 externalCost auto  edge true p2p auto state disable lbd enable
config stp ports 25-27 externalCost auto  edge true p2p auto state disable lbd enable 
config stp ports 1-27 hellotime 2 
config stp mst_ports 1-27 instance_id 0 internalCost auto priority 128
config stp ports 1-18 fbpdu disable
config stp ports 21-23 fbpdu disable
config stp ports 25-27 fbpdu disable
config stp ports 19 externalCost auto  edge false p2p auto state enable lbd disable
config stp ports 20 externalCost auto  edge false p2p auto state enable lbd disable
config stp ports 24 externalCost auto  edge false p2p auto state enable lbd disable
config stp ports 19 fbpdu enable
config stp ports 20 fbpdu enable
config stp ports 24 fbpdu enable
config stp mst_ports 1-27 instance_id 1 internalCost auto priority 128
config stp mst_ports 1-27 instance_id 2 internalCost auto priority 128



Там, где не надо включать STP
На access порту
spanning-tree portfast
spanning-tree bpduguard enable

На транк порту
spanning-tree portfast trunk
spanning-tree bpdufilter enable

Приоритеты
 storm-control broadcast level 50.00
 storm-control action shutdown
 spanning-tree portfast trunk
 spanning-tree bpdufilter enable
 spanning-tree bpduguard enable


Сначала, потому что bpduguard кладёт порт в даун, а фильтр только фильтрует. Как только отключил bpdufilter, так порт и заблокировался
  no spanning-tree bpduguard enable
  no spanning-tree portfast trunk
  no spanning-tree bpdufilter enable


spanning-tree mst configuration
  no instance 3 vlan 2
  no instance 3 vlan 102
  no instance 3 vlan 103
  no instance 3 vlan 104
  no instance 3 vlan 107
  no instance 3 vlan 108
  no instance 3 vlan 120
  no instance 3 vlan 153
  no instance 3 vlan 156
  no instance 3 vlan 684
  no instance 3 vlan 899
  no instance 2 vlan 520
  no instance 2 vlan 846
  no instance 1 vlan 110
  no instance 1 vlan 200
  no instance 1 vlan 207
  no instance 1 vlan 260
  no instance 1 vlan 276
  no instance 1 vlan 303
  no instance 1 vlan 651
  no instance 1 vlan 655
  no instance 1 vlan 694
  no instance 1 vlan 816
  no instance 1 vlan 822
  no instance 1 vlan 837
  no instance 1 vlan 855
  no instance 1 vlan 875
  no instance 1 vlan 1014
  no instance 1 vlan 1018
  no instance 1 vlan 1020
  no instance 1 vlan 4007




Позволяют задать диапазон портов.

External Cost

Этот параметр определяет относительную стоимость продвижения паетов
пакетов к списку определённых портов. Стоимость порта может
вычисляться автоматически или задана определённым значением. Значение
по умолчанию 0 (авто).
0 (авто) - автоматически устанавливает оптимальную скорость пересылки
пакетов на порт(ы). Значения стоимости порта по умолчанию: для
100Мбит/с порта=200000; для Gigabit порта=20000
Значение от 1 до 200000000 - определяет внешнюю стоимость. Чем меньше
значение, тем выше приоритет порта и больше вероятность того, что именно
он будет выбран для продвижения пакетов.


Hello Time

Интервал между передачами конфигурационных сообщений корневым
портом на другие устройства в LAN. Пользователь может выблать значение
от 1 до 2 секунд. Значение по умолчанию 2 секунды. Это поле доступно
только, когда на Коммутаторе выбран протокол MSTP.

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

Restricted Role

Этот параметр может принимать два значения: True и False. При выборе
значения TRUE этот порт не будет корневым портом для CIST или других
MSTI, даже если он будет обладать наименьшим приоритетом. Таким
образом, порт становится альтернативным портом, который будет
выбираться всегда после корневого порта. По умолчанию этот параметр
установлен как FALSE. Выбор True может привести к потере связности
покрывающего дерева. Это позволяет избежать влияния внешних мостов на активную топология покрывающего дерева, поскольку данные мосты не
находятся под управлением сетевого администратора.

Restricted Tcn

Возможно два значения этого поля: True и False. При выборе значения
TRUE полученные с этого порта уведомления (topology change notifications и
topology change) не будут распространяться на другие порты. Этот параметр
установлен в значение FALSE, по умолчанию. При установленной опции
False может временно теряться связность из-за некорректных пакетов
изменения топологии (topology change), полученных с клиентских портов.

P2P 
Значение True в данном поле означает, что данный порт является портом
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

Forward BPDU
Значение True позволит пересылку BPDU-пакетов с сетевых устройств на
заданные порты. Для этого опция STP должна быть глобально отключена, а
продвижение BPDU-пакетов глобально разрешено (более подробная
информация приведена в главе STP Bridge Global Settings).
Значение по умолчанию False: в этом случае BPDU-пакеты не будут
пересылаться, даже если опция STP отключена.
State Позволяет включить/отключить STP для выбранной группы портов.
Значение по умолчанию Enabled (включено).







Как-то не очень все вяжется... Разнотолки какие-то... В документации одно, на форуме другое... Давайте по порядку? Беру доку от 36-го свитча:
config stp:
fbpdu [enable | disable] − Allows the forwarding of STP BPDU packets from other network devices when STP is disabled on the Switch. 
The default is enable.
Разрешает форвардинг BPDU пакетов через свитч, когда STP выключено.
 По умолчанию включено. Значит ли это, что эта настройка не действует при включенном STP?
 значит ли это, что включенная опция (true) разрешает форвардинг пакетов, а не фильрацию?

config stp ports:
fbpdu [enable | disable] − Allows the forwarding of STP BPDU packets from other network devices when STP is disabled on the Switch. 
This function can only be in use when STP is globally disabled and forwarding BPDU packets is enabled. 
The default is enabled and BPDU packets will not be forwarded.
Разрешает форвардинг BPDU пакетов от других сетевый устройств (т.е. подразумеваем, что действует на входящий траффик?) 
(и снова) когда STP ВЫКЛЮЧЕН на свитче. Это действует ТОЛЬКО когда STP выключен ГЛОБАЛЬНО и форвардинг пакетов включен.
 По умолчанию ВКЛЮЧЕН и BPDU пакеты НЕ будут переданы. :shock:

Иван, не моглы бы Вы научить правильно понимать эти пункты? Моя логика отказывает... 
У нас есть свитчи и с выключенным STP и важно понимать что мы включаем а что мы выключаем.

Берем доку 35-й серии R5
Choosing True will allow the forwarding of BPDU packets in the specified ports from other network devices.
 This will go into effect only if STP is globally disabled AND Forwarding BPDU is globally enabled (See STP Bridge Global Settings above). 
The default setting False, does not forward BPDU packets when STP is disabled.
Здесь с логикой все более хорошо, по умолчанию выключено и не форвардит. Но, опытным путем было замечено - ФОРВАРДИТ!
 STP было выключено, fbpdu false. Таки оно не рабочее, или таки оно на исходящие BPDU действует?

Restricted_Role и Restricted_TCN - в доке по 36-му не нашел. Видимо, этих опций там нет (Firmware Version : Build 2.40-B51). 
В доке по 35-му не совсем понял. 
Не могли бы Вы пояснить механизм действия этих опций на 35-й и как управлять форвардингом BPDU пакетов в случае включенного STP на 36-й?
Завтра исследование будет продолжено, но, было бы гораздо легче, если бы документация и фактическое поведение соответствовали друг другу...








1) FBPDU действительно работает только при выключенном STP. 
Оно позволяет не распространять BPDU с порта на котором эта опция стоит в disable.

2) Restricted_role [true | false] – If true causes the Port not to be selected as Root Port for the CIST or any MSTI, even it has the best spanning tree priority vector.
 Such a Port will be selected as an Alternate Port after the Root Port has been selected. This parameter should be false by default. If set, it can cause lack of spanning tree connectivity. 
It is set by a network administrator to prevent bridges external to a core region of the network influencing the spanning tree active topology, possibly because those bridges are not under the full control of the administrator. 
Если в двух словах то она на входе отбрасывает root-ые BPDU, защищая тем самым от того что клиент может посылать BPDU как бы от имени корня и перестраивая тем самым дерево. Работает при включенном STP на порту.

3) Restricted_tcn [true | false] – If true causes the Port not to propagate received topology change notifications and topology changes to other Ports.
 This parameter should be false by default. If set it can cause temporary loss of connectivity after changes in a spanning trees active topology as a result of persistent incorrectly learned station location information. 
It is set by a network administrator to prevent bridges external to a core region of the network, causing address flushing in that region, possibly because those bridges are not under the full control of the administrator or MAC_Operational for the attached LANs transitions frequently. 
Очень похожа на FBPDU disabled только за тем исключением что рабоатет при включённом STP и не распространяте BPDU с порта на котором включена на другие порты. Также защищает от распространения fake BPDU генерируемых клиентом.




Вкратце:

Port VLAN ID (PVID) inconsistency -- A per-VLAN spanning tree (PVST+) Bridge
Protocol Data Unit (BPDU) is received on a different VLAN than it was
originated.

А уж там надо смотреть, кто BPDU из 15-го влана засовывает в 17-й.. (Может,
кстати, и не только BPDU, а все подряд, не разбираясь).

49 - сtd-s1
13, 10, 1951, 1950, 11, 101, 132, 1956, 22

11w0d: %LINK-3-UPDOWN: Interface GigabitEthernet0/52, changed state to up
11w0d: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/52, changed state to up
11w0d: %SW_MATM-4-MACFLAP_NOTIF: Host 001c.b14e.3cc3 in vlan 13 is flapping between port Gi0/52 and port Gi0/49
11w0d: %SW_MATM-4-MACFLAP_NOTIF: Host 0023.ab64.dec1 in vlan 10 is flapping between port Gi0/52 and port Gi0/49
11w0d: %SW_MATM-4-MACFLAP_NOTIF: Host 000b.46c4.e260 in vlan 10 is flapping between port Gi0/52 and port Gi0/49
11w0d: %SW_MATM-4-MACFLAP_NOTIF: Host 14da.e9e8.3082 in vlan 1951 is flapping between port Gi0/52 and port Gi0/49
11w0d: %SW_MATM-4-MACFLAP_NOTIF: Host 0006.d7d3.52c1 in vlan 10 is flapping between port Gi0/52 and port Gi0/49
11w0d: %SW_MATM-4-MACFLAP_NOTIF: Host 001e.bee1.8a40 in vlan 10 is flapping between port Gi0/49 and port Gi0/17
11w0d: %SW_MATM-4-MACFLAP_NOTIF: Host 0024.1478.731b in vlan 10 is flapping between port Gi0/49 and port Gi0/3
11w0d: %SW_MATM-4-MACFLAP_NOTIF: Host dc0e.a107.cef9 in vlan 1950 is flapping between port Gi0/52 and port Gi0/49
11w0d: %SW_MATM-4-MACFLAP_NOTIF: Host 000d.280c.fe1c in vlan 10 is flapping between port Gi0/52 and port Gi0/49
11w0d: %SW_MATM-4-MACFLAP_NOTIF: Host 001d.6036.8058 in vlan 11 is flapping between port Gi0/52 and port Gi0/49
11w0d: %SW_MATM-4-MACFLAP_NOTIF: Host 0018.f38f.6d73 in vlan 101 is flapping between port Gi0/52 and port Gi0/49
11w0d: %SW_MATM-4-MACFLAP_NOTIF: Host 503d.e534.6800 in vlan 13 is flapping between port Gi0/52 and port Gi0/49
11w0d: %SW_MATM-4-MACFLAP_NOTIF: Host 0030.48ca.c314 in vlan 132 is flapping between port Gi0/52 and port Gi0/49
11w0d: %SW_MATM-4-MACFLAP_NOTIF: Host c84c.7554.f21b in vlan 13 is flapping between port Gi0/52 and port Gi0/49
11w0d: %SW_MATM-4-MACFLAP_NOTIF: Host 0015.6702.980e in vlan 1956 is flapping between port Gi0/52 and port Gi0/49
11w0d: %SW_MATM-4-MACFLAP_NOTIF: Host 0201.0000.0000 in vlan 132 is flapping between port Gi0/49 and port Gi0/52
11w0d: %SW_MATM-4-MACFLAP_NOTIF: Host 0015.6712.0446 in vlan 22 is flapping between port Gi0/52 and port Gi0/49

11w0d: %SPANTREE-2-RECV_PVID_ERR: Received BPDU with inconsistent peer vlan id 1 on GigabitEthernet0/52 VLAN1956.
11w0d: %SPANTREE-2-BLOCK_PVID_LOCAL: Blocking GigabitEthernet0/52 on MST0. Inconsistent local vlan.
11w0d: %SW_MATM-4-MACFLAP_NOTIF: Host f46d.0452.c553 in vlan 1951 is flapping between port Gi0/52 and port Gi0/49
11w0d: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/52, changed state to down
11w0d: %LINK-3-UPDOWN: Interface GigabitEthernet0/52, changed state to down

11w0d: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.3 on Vlan10 from 2WAY to DOWN, Neighbor Down: Dead timer expired
11w0d: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.9 on Vlan10 from 2WAY to DOWN, Neighbor Down: Dead timer expired
11w0d: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.3 on Vlan10 from 2WAY to DOWN, Neighbor Down: Dead timer expired
11w0d: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.2 on Vlan10 from 2WAY to DOWN, Neighbor Down: Dead timer expired
11w0d: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.10 on Vlan10 from 2WAY to DOWN, Neighbor Down: Dead timer expired
11w0d: %CLEAR-5-COUNTERS: Clear counter on interface GigabitEthernet0/1 by garry on vty0 (192.168.113.1)




3     2011-06-01 12:59:28 INFO(6) Port 20 link up, 1000Mbps FULL duplex         
2     2011-06-01 12:59:28 INFO(6) Spanning Tree MST configuration ID name and re
                                  vision level change (name:00:1C:F0:20:62:40 re
                                  vision level:0)   




2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host 000d.280c.fe1c in vlan 10 is flapping between port Gi0/13 and port Gi0/12
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host 000b.46c4.e260 in vlan 10 is flapping between port Gi0/3 and port Gi0/12
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host 503d.e534.6800 in vlan 13 is flapping between port Gi0/12 and port Gi0/10
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host e05f.b952.4b7f in vlan 13 is flapping between port Gi0/12 and port Gi0/10
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host 0006.d7d3.52c1 in vlan 10 is flapping between port Gi0/12 and port Gi0/25
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host ecc8.8205.89a0 in vlan 38 is flapping between port Gi0/12 and port Gi0/25
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host 0023.ab64.dec1 in vlan 10 is flapping between port Gi0/12 and port Gi0/25
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host dc0e.a107.cef9 in vlan 1950 is flapping between port Gi0/25 and port Gi0/12
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host 14da.e9e8.3082 in vlan 1951 is flapping between port Gi0/25 and port Gi0/12
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host 001e.bee1.8a40 in vlan 10 is flapping between port Gi0/12 and port Gi0/25
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host 001c.5718.1641 in vlan 10 is flapping between port Gi0/12 and port Gi0/25
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host 0024.1478.731b in vlan 10 is flapping between port Gi0/12 and port Gi0/25
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host c84c.75c4.f11b in vlan 10 is flapping between port Gi0/12 and port Gi0/27
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host f46d.0452.c553 in vlan 1951 is flapping between port Gi0/25 and port Gi0/12
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host 0015.176a.0e64 in vlan 10 is flapping between port Gi0/12 and port Gi0/6
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host 001d.6036.8058 in vlan 11 is flapping between port Gi0/25 and port Gi0/12
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host 0018.f38f.6d73 in vlan 101 is flapping between port Gi0/12 and port Gi0/25
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host 0030.48ca.c314 in vlan 132 is flapping between port Gi0/12 and port Gi0/25
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host c84c.7554.f21b in vlan 13 is flapping between port Gi0/25 and port Gi0/12
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host 0015.6702.980e in vlan 1956 is flapping between port Gi0/25 and port Gi0/12
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host 0015.6712.0446 in vlan 22 is flapping between port Gi0/12 and port Gi0/25
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host 0023.546b.882b in vlan 10 is flapping between port Gi0/12 and port Gi0/16
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host 0201.0000.0000 in vlan 132 is flapping between port Gi0/12 and port Gi0/25
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host 0015.1710.4351 in vlan 132 is flapping between port Gi0/12 and port Gi0/25
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host e05f.b952.4b7f in vlan 38 is flapping between port Gi0/12 and port Gi0/10
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host 0004.23b0.4500 in vlan 132 is flapping between port Gi0/12 and port Gi0/24
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host 0002.5553.103f in vlan 10 is flapping between port Gi0/12 and port Gi0/1
2d23h: %SW_MATM-4-MACFLAP_NOTIF: Host 6c62.6d74.fba8 in vlan 11 is flapping between port Gi0/25 and port Gi0/12
2d23h: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.55 on Vlan13 from 2WAY to DOWN, Neighbor Down: Dead timer expired
2d23h: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.3 on Vlan10 from 2WAY to DOWN, Neighbor Down: Dead timer expired
2d23h: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.53 on Vlan13 from LOADING to FULL, Loading Done
2d23h: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.55 on Vlan13 from 2WAY to DOWN, Neighbor Down: Dead timer expired
2d23h: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.9 on Vlan10 from 2WAY to DOWN, Neighbor Down: Dead timer expired
2d23h: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.3 on Vlan10 from 2WAY to DOWN, Neighbor Down: Dead timer expired
2d23h: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.2 on Vlan10 from 2WAY to DOWN, Neighbor Down: Dead timer expired
2d23h: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.10 on Vlan10 from 2WAY to DOWN, Neighbor Down: Dead timer expired
2d23h: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.62 on Vlan13 from FULL to DOWN, Neighbor Down: Dead timer expired
2d23h: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.53 on Vlan13 from FULL to DOWN, Neighbor Down: Dead timer expired
2d23h: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.52 on Vlan13 from LOADING to FULL, Loading Done
2d23h: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.51 on Vlan13 from LOADING to FULL, Loading Done
2d23h: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.53 on Vlan13 from LOADING to FULL, Loading Done







RSTP+MSTP


Это означает, что надо использовать обычный формат (STP -dot1d) mac адреса bpdu сообщений - 0180C2000000
А так у нас стоит nni_bpdu_addr dot1ad и это значит что используется другой

При включенном mstp & qinq dgs3620-28sc (firmware 2.00b023) посылает bpdu:
в uni порт - на адрес 01:80:c2:00:00:00
в nni порт - на адрес 01:80:c2:00:00:08

Такой вопрос: можно ли сделать так, чтобы для nni порта использовался mac адрес 01:80:c2:00:00:00?

Нельзя.
В nni порт коммутаторы отсылают bpdu на мак 01:80:c2:00:00:08


Как выяснилось - если очень хочется, то можно:
config stp nni_bpdu_addr dot1d



L2 Tunneling нужно включить для BPDU пакетиков


102 влан нужен ли?

Жёстко транки переписать


interface GigabitEthernet0/52
 description #Link to K9-AGG(cabinet 608)
 switchport trunk encapsulation dot1q
 switchport trunk allowed vlan 9-11,13,16,21-26,34,36,38,54,55,57,58,60,68,100
 switchport trunk allowed vlan add 101,105,106,109,113,122,132,151,152,154,165
 switchport trunk allowed vlan add 172,201-206,213,214,272,281,284,294,298,577
 switchport trunk allowed vlan add 628,629,648,671,691,693,700,773,778,787,817
 switchport trunk allowed vlan add 833,861,862,894,895,953,954,1011,1012,1017
 switchport trunk allowed vlan add 1019,1021-1027,1029,1030,1950-1953,1955-1957
 switchport trunk allowed vlan add 2002,2007,2008,2500,2503,2999,3154,3998,4000
 switchport trunk allowed vlan add 4001
 switchport mode trunk
 load-interval 30



interface GigabitEthernet0/25
 description # CDE-S0.sc.int via FO converter
 switchport trunk encapsulation dot1q
 switchport trunk allowed vlan 9-11,13,16,21-26,34,36,38,54,55,57,58,60,68
 switchport trunk allowed vlan add 100-102,105,106,109,113,122,132,151,152,154
 switchport trunk allowed vlan add 165,172,201-206,208,213,214,272,281,284,294
 switchport trunk allowed vlan add 298,303,316,317,548,577,628,629,648,655,671
 switchport trunk allowed vlan add 691,693,700,773,778,787,817,833,861,862,894
 switchport trunk allowed vlan add 895,953,954,973,975,1011,1012,1015-1017,1019
 switchport trunk allowed vlan add 1021-1027,1029,1030,1950-1953,1955-1957,2002
 switchport trunk allowed vlan add 2007,2008,2500,2503,2999,3049,3130,3151,3154
 switchport trunk allowed vlan add 3998,4000,4001
 switchport mode trunk
 switchport nonegotiate
 load-interval 30
end

Возможно дело в MST0
[http://forum.dlink.ru/viewtopic.php?f=2&t=142236&hilit=STP+%D0%B8+Qinq](http://forum.dlink.ru/viewtopic.php?f=2&t=142236&hilit=STP+%D0%B8+Qinq)

Gi0/12           Desg FWD 20000     128.12   P2p Edge *PVID_Inc 



Удалить влан 3151 из cde-49 ctd-25
Новый влан создать
и добавть в STP
И эти тоже
switchport trunk allowed vlan add 303
switchport trunk allowed vlan add 316
switchport trunk allowed vlan add 317
switchport trunk allowed vlan add 973
switchport trunk allowed vlan add 975
switchport trunk allowed vlan add 3130
switchport trunk allowed vlan add 3154
не нужен нах
switchport trunk allowed vlan remove 1020





switchport trunk allowed vlan remove 102
switchport trunk allowed vlan remove 548
switchport trunk allowed vlan remove 655
switchport trunk allowed vlan remove 1015
switchport trunk allowed vlan remove 1016
switchport trunk allowed vlan remove 3049

switchport trunk allowed vlan remove 3151 

303 - WIPL-GKRCH-RTC (cde-ctd) lipetsk-car1-fa0-0 # RTComm C7202VXR, Lipetsk - BC @ Gipromez
316 - PSI-CTK-Kasnacheistvo (cde-) Trunk to LES IP MPLS - а куда - хз
317 - CTK-RTcomm-School (ats-cde)	Universitetsy - Trunk to LES IP MPLS
548 - Indezit-Impex-Bankomat ( Только на ctd) - CTD-C3 VPN PORT - Trunk to POP at Stinol
655 - LiftService-INET ( только cde) CDE-C3- Link to ALTAI-S0 - TGK-4 @ Poperechniy pr. (u12 transit)
973 - INdesit-VPN-L2 (cde-ctd) Sovintel (BeeLine Bussines) ethernet link (Cisco 3745) # - Trunk to POP at Stinol
975 - SoGaz-L2-RTK (ats-ctd) BC @ Gipromez - Trunk to RosTelecom VPN -2
1015 - разные вланы на разных цисках (удалить)
1016 - только на сde
3049 - разные вланы на разных цисках (удалить)
3130 - UC-INET-NLMK (cde-ctd-k9)
3151 - (malina на сde и сtd) hkf_p2k на ats 
3154 - sintel  Косяк Женька
 


switchport trunk allowed vlan add 303
switchport trunk allowed vlan add 316
switchport trunk allowed vlan add 317
switchport trunk allowed vlan add 973
switchport trunk allowed vlan add 975
switchport trunk allowed vlan add 3130
switchport trunk allowed vlan add 3154



Не совпадают списки вланов -ок
Попробовать убрать на время, отфильтровать qinq вланы
Сниффить Смотреть типы bpdu, одинаковые ли они

Несогласованные порты
show spanning-tree inconsistentports





Проблема в том что CIST Regional Root может быть только пограничный свитч и им стал единственный ctd-s1, а у него приоритет оказался меньше, чем
у k9-s4. Получилось что CIST Root находится вне MSTP сisco свитчей, а так не работает
Смотреть последний абзац - сценарий 3
[http://blog.internetworkexpert.com/2008/09/24/mstp-tutorial-part-ii-outside-a-region/](http://blog.internetworkexpert.com/2008/09/24/mstp-tutorial-part-ii-outside-a-region/)

CIST Root Bridges Election Process

    When a switch boots up, it declares itself as CIST Root and CIST Regional Root and announces this fact in outgoing BPDUs. The switch will adjust its decision upon reception of better information and continue advertising the best known CIST Root and CIST Regional Root on all internal ports. On the boundary ports, the switch advertises only the CIST Root Bridge ID and CIST External Root Path Cost thus hiding the details of the region’s internal topology.
    CIST External Root Path Cost is the cost to reach the CIST Root across the links connecting the boundary ports – i.e. the inter-region links. When a BPDU is received on an internal port, this cost is not changed. When a BPDU is received on a boundary port, this cost is adjusted based on the receiving boundary port cost. In result, the CIST External Root Path Cost is propagated unmodified inside any region.
    Only a boundary switch could be elected as the CIST Regional Root, and this is the switch with the lowest cost to reach the CIST Root. If a boundary switch hears better CIST External Root Path cost received on its internal link, it will relinquish its role of CIST Regional Root and start announcing the new metric out of its boundary ports.
    Every boundary switch needs to properly block its boundary ports. If the switch is a CIST Regional Root, it elects one of the boundary ports as the “CIST Root port” and blocks all other boundary ports. If a boundary switch is not the CIST Regional Root, it will mark the boundary ports as CIST Designated or Alternate. The boundary port on a non regional-root bridge becomes designated only if it has superior information for the CIST Root: better External Root Path cost or if the costs are equal better CIST Regional Root Bridge ID. This follows the normal rules of STP process.
    As a result of CIST construction, every region will have one switch having single port unblocked in the direction of the CIST Root. This switch is the CIST Regional Root. All boundary switches will advertise the region’s CIST Regional Root Bridge ID out of their non-blocking boundary ports. From the outside perspective, the whole region will look like a single virtual bridge with the Bridge ID = CIST Regional Root ID and single root port elected on the CIST Regional Root switch.
    The region that contains the CIST Root will have all boundary ports unblocked and marked as CIST designated ports. Effectively the region would look like a virtual root bridge with the Bridge ID equal to CIST Root and all ports being designated. Notice that the region with CIST Root has CIST Regional Root equal to CIST Root as they share the same lowest bridge priority value across all regions.




1d20h: %SYS-5-CONFIG_I: Configured from console by garry on vty0 (192.168.113.1)
1d20h: %SPANTREE-2-RECV_PVID_ERR: Received BPDU with inconsistent peer vlan id 1 on GigabitEthernet0/12 VLAN1956.
1d20h: %SPANTREE-2-BLOCK_PVID_LOCAL: Blocking GigabitEthernet0/12 on MST0. Inconsistent local vlan.
1d20h: %SYS-5-CONFIG_I: Configured from console by garry on vty0 (192.168.113.1)
1d20h: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.3 on Vlan10 from 2WAY to DOWN, Neighbor Down: Dead timer expired
1d20h: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.2 on Vlan10 from 2WAY to DOWN, Neighbor Down: Dead timer expired
1d20h: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.62 on Vlan13 from FULL to DOWN, Neighbor Down: Dead timer expired
1d20h: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.10 on Vlan10 from 2WAY to DOWN, Neighbor Down: Dead timer expired
1d20h: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.9 on Vlan10 from 2WAY to DOWN, Neighbor Down: Dead timer expired
1d20h: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.55 on Vlan13 from 2WAY to DOWN, Neighbor Down: Dead timer expired
1d20h: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.51 on Vlan13 from LOADING to FULL, Loading Done
1d20h: %SYS-5-CONFIG_I: Configured from console by garry on vty0 (192.168.113.1)
1d20h: %SYS-5-CONFIG_I: Configured from console by garry on vty0 (192.168.113.1)
1d20h: %SPANTREE-2-UNBLOCK_CONSIST_PORT: Unblocking GigabitEthernet0/12 on MST0. Port consistency restored.
1d20h: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.62 on Vlan13 from LOADING to FULL, Loading Done
1d22h: %LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan1440, changed state to up
1d22h: %SYS-5-CONFIG_I: Configured from console by smithy on vty0 (81.20.192.32)





 Configuration Name : PSI                               Revision Level :777
 MSTI ID     Vid list
 -------     -------------------------------------------------------------
    CIST     1-8,12,14-15,17-20,27-33,35,37,39-53,56,59,61-67,69-99,102-104,1
             07-108,110-112,114-121,123-131,133-150,153,155-164,166-171,173-2
             00,207,209-212,215-271,273-280,282-283,285-293,295-297,299-576,5
             78-627,630-647,649-670,672-690,692,694-699,701-772,774-777,779-7
             86,788-816,818-832,834-860,863-893,896-952,955-1010,1013-1016,10
             18,1020,1028,1031-1949,1954,1958-2001,2003-2006,2009-2499,2501-2
             502,2504-2998,3000-3153,3155-3997,3999,4002-4094
       1     214,284,294,298,648,671,691,693,861-862,953-954,1021,1023,2007-2
             008,2500
       2     9-10,13,16,100-101,105,109,132,151-152,154,172,201,204,208,628-6
             29,700,817,895,1026,1029-1030,2503,2999,4000-4001
       3     54-55,57-58,60,68,202-203,213,272,281,577,773,778,787,833,894,10
             11-1012,1019,1022,2002,3154
       4     11,21-26,34,36,38,106,113,122,165,205-206,1017,1024-1025,1027,19
             50-1953,1955-1957,3998





Name      [PSI]
Revision  777   Instances configured 5

Instance  Vlans mapped
--------  ---------------------------------------------------------------------
0         1-8,12,14-15,17-20,27-33,35,37,39-53,56,59,61-67,69-99,102-104
          107-108,110-112,114-121,123-131,133-150,153,155-164,166-171,173-200
          207,209-212,215-271,273-280,282-283,285-293,295-297,299-576,578-627
          630-647,649-670,672-690,692,694-699,701-772,774-777,779-786,788-816
          818-832,834-860,863-893,896-952,955-1010,1013-1016,1018,1020
          1028,1031-1949,1954,1958-2001,2003-2006,2009-2499,2501-2502,2504-2998
          3000-3153,3155-3997,3999,4002-4094
1         214,284,294,298,648,671,691,693,861-862,953-954,1021,1023,2007-2008
          2500
2         9-10,13,16,100-101,105,109,132,151-152,154,172,201,204,208,628-629
          700,817,895,1026,1029-1030,2503,2999,4000-4001
3         54-55,57-58,60,68,202-203,213,272,281,577,773,778,787,833,894
          1011-1012,1019,1022,2002,3154
4         11,21-26,34,36,38,106,113,122,165,205-206,1017,1024-1025,1027
          1950-1953,1955-1957,3998
-------------------------------------------------------------------------------

Root Guard  - это для защиты корневого коммутатора и защиты от клиентов. если функция включена на интерфейсе, то при получении на нём BPDU лучшего, чем текущий корневой коммутатор, порт переходит в состояние root-inconsistent (эквивалентно состоянию listening). После того как порт перестает получать BPDU, он переходит в нормальное состояние.

Включение Root Guard на интерфейсе (переводит порт в роль designated): 


Loop Guard 





1. Поменять
 Port RestrictedRole : False,  Port RestrictedTCN : False
2. Дебаг на отправленные и полученные
3. Поднять и поискать master порт
4. Сделать default влан untagged на 20 порту
5. debug spanning-tree events
6. debug spanning-tree all
7. sh spanning-tree interface Gi0/12 detail


IEEE 802.2 LLC SAP

Помогло или нет
no cdp enable


Possible spoofing attack from 5C-D9-98-3E-9A-00 port 8

*ROOT_Inc, *LOOP_Inc, *PVID_Inc and *TYPE_Inc—The port is in a broken state (BKN*) for an inconsistency. The port would be (respectively) Root inconsistent, Loopguard inconsistent, PVID inconsistent, or Type inconsistent. 












create access_profile profile_id 10 ethernet destination_mac FF-FF-FF-FF-FF-FF
config access_profile profile_id 10 add access_id 10 ethernet destination_mac 01-80-C2-00-00-00  port 2-7,9-27 deny
config access_profile profile_id 10 add access_id 11 ethernet destination_mac 01-00-0C-CC-CC-CD  port 2-7,9-27 deny



 config stp version mstp
 config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 3 fbpdu disable lbd enable lbd_recover_timer 60 nni_bpdu_addr dot1ad
 config stp priority 32768 instance_id 0
 create stp instance_id 1
 config stp instance_id 1 add_vlan 214
 config stp instance_id 1 add_vlan 284
 config stp instance_id 1 add_vlan 294
 config stp instance_id 1 add_vlan 298
 config stp instance_id 1 add_vlan 648
 config stp instance_id 1 add_vlan 671
 config stp instance_id 1 add_vlan 691
 config stp instance_id 1 add_vlan 693
 config stp instance_id 1 add_vlan 861
 config stp instance_id 1 add_vlan 862
 config stp instance_id 1 add_vlan 953
 config stp instance_id 1 add_vlan 954
 config stp instance_id 1 add_vlan 1021
 config stp instance_id 1 add_vlan 1023
 config stp instance_id 1 add_vlan 2007
 config stp instance_id 1 add_vlan 2008
 config stp instance_id 1 add_vlan 2500
 config stp priority 32768 instance_id 1
 create stp instance_id 2
 config stp instance_id 2 add_vlan 9
 config stp instance_id 2 add_vlan 10
 config stp instance_id 2 add_vlan 13
 config stp instance_id 2 add_vlan 16
 config stp instance_id 2 add_vlan 100
 config stp instance_id 2 add_vlan 101
 config stp instance_id 2 add_vlan 105
 config stp instance_id 2 add_vlan 109
 config stp instance_id 2 add_vlan 132
 config stp instance_id 2 add_vlan 151
 config stp instance_id 2 add_vlan 152
 config stp instance_id 2 add_vlan 154
 config stp instance_id 2 add_vlan 172
 config stp instance_id 2 add_vlan 201
 config stp instance_id 2 add_vlan 204
 config stp instance_id 2 add_vlan 208
 config stp instance_id 2 add_vlan 628
 config stp instance_id 2 add_vlan 629
 config stp instance_id 2 add_vlan 700
 config stp instance_id 2 add_vlan 817
 config stp instance_id 2 add_vlan 895
 config stp instance_id 2 add_vlan 1026
 config stp instance_id 2 add_vlan 1029
 config stp instance_id 2 add_vlan 1030
 config stp instance_id 2 add_vlan 2503
 config stp instance_id 2 add_vlan 2999
 config stp instance_id 2 add_vlan 4000
 config stp instance_id 2 add_vlan 4001
 config stp priority 32768 instance_id 2
 create stp instance_id 3
 config stp instance_id 3 add_vlan 54
 config stp instance_id 3 add_vlan 55
 config stp instance_id 3 add_vlan 57
 config stp instance_id 3 add_vlan 58
 config stp instance_id 3 add_vlan 60
 config stp instance_id 3 add_vlan 68
 config stp instance_id 3 add_vlan 202
 config stp instance_id 3 add_vlan 203
 config stp instance_id 3 add_vlan 213
 config stp instance_id 3 add_vlan 272
 config stp instance_id 3 add_vlan 281
 config stp instance_id 3 add_vlan 577
 config stp instance_id 3 add_vlan 773
 config stp instance_id 3 add_vlan 778
 config stp instance_id 3 add_vlan 787
 config stp instance_id 3 add_vlan 833
 config stp instance_id 3 add_vlan 894
 config stp instance_id 3 add_vlan 1011
 config stp instance_id 3 add_vlan 1012
 config stp instance_id 3 add_vlan 1019
 config stp instance_id 3 add_vlan 1022
 config stp instance_id 3 add_vlan 2002
 config stp instance_id 3 add_vlan 3154
 config stp priority 28672 instance_id 3
 create stp instance_id 4
 create stp instance_id 4
 config stp instance_id 4 add_vlan 11
 config stp instance_id 4 add_vlan 21
 config stp instance_id 4 add_vlan 22
 config stp instance_id 4 add_vlan 23
 config stp instance_id 4 add_vlan 24
 config stp instance_id 4 add_vlan 25
 config stp instance_id 4 add_vlan 26
 config stp instance_id 4 add_vlan 34
 config stp instance_id 4 add_vlan 36
 config stp instance_id 4 add_vlan 38
 config stp instance_id 4 add_vlan 106
 config stp instance_id 4 add_vlan 113
 config stp instance_id 4 add_vlan 122
 config stp instance_id 4 add_vlan 165
 config stp instance_id 4 add_vlan 205
 config stp instance_id 4 add_vlan 206
 config stp instance_id 4 add_vlan 1017
 config stp instance_id 4 add_vlan 1024
 config stp instance_id 4 add_vlan 1025
 config stp instance_id 4 add_vlan 1027
 config stp instance_id 4 add_vlan 1950
 config stp instance_id 4 add_vlan 1951
 config stp instance_id 4 add_vlan 1952
 config stp instance_id 4 add_vlan 1953
 config stp instance_id 4 add_vlan 1955
 config stp instance_id 4 add_vlan 1956
 config stp instance_id 4 add_vlan 1957
 config stp instance_id 4 add_vlan 3998
 config stp priority 32768 instance_id 4
 config stp mst_config_id name PSI revision_level 777


 config stp ports 2-7,9-27 externalCost auto  edge true p2p auto state disable restricted_role true restricted_tcn true lbd enable
 config stp ports 1-27 hellotime 2
 config stp mst_ports 1-27 instance_id 0 internalCost auto priority 128
 config stp ports 2-7,9-27 fbpdu disable
 config stp ports 1,8 externalCost auto  edge false p2p auto state enable restricted_role false restricted_tcn false lbd disable
 config stp ports 1-8 fbpdu enable
 config stp mst_ports 1-27 instance_id 1 internalCost auto priority 128
 config stp mst_ports 1-27 instance_id 2 internalCost auto priority 128
 config stp mst_ports 1-27 instance_id 3 internalCost auto priority 128
 config stp mst_ports 1-27 instance_id 4 internalCost auto priority 128

 enable stp


config stp ports 1,8 externalCost auto  edge false p2p auto state enable lbd disable



1035				FSB-BILL
123 		2		net-bill


655 		1		lift_vpn
813				EUROSET-WIPLL


config stp instance_id 2 add_vlan 1035
config stp instance_id 2 add_vlan 123
config stp instance_id 1 add_vlan 655
config stp instance_id 1 add_vlan 813

        
    
                                                                                                                              
                                                                              
          



spanning-tree mode mst
spanning-tree extend system-id
!
spanning-tree mst configuration
 name PSI
 revision 777
 instance 1 vlan 214, 284, 294, 298, 648, 655, 671, 691, 693, 813, 861-862
 instance 1 vlan 953-954, 1021, 1023, 2007-2008, 2500
 instance 2 vlan 9-10, 13, 16, 100-101, 105, 109, 123, 132, 151-152, 154
 instance 2 vlan 172, 201, 204, 208, 628-629, 700, 817, 895, 1026, 1029-1030
 instance 2 vlan 1035, 2503, 2999, 4000-4001
 instance 3 vlan 54-55, 57-58, 60, 68, 202-203, 213, 272, 281, 577, 773
 instance 3 vlan 778, 787, 833, 894, 1011-1012, 1019, 1022, 2002, 3154
 instance 4 vlan 11, 21-26, 34, 36, 38, 106, 113, 122, 165, 205-206, 1017
 instance 4 vlan 1024-1025, 1027, 1950-1953, 1955-1957, 3998








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



Поключен клиент portfast, bpduguard,
Подключен trunk - сервер  portfast trunk, bpdufilter
подключен коммутатор access уровня (downlink)  rootguard, portfast trunk
подключен коммутатор равный с stp, loopguard
Порт домового коммутатора к которому подключен коммутатор района(uplink), loopguard




-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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
 
 bpdu-block {
interface (interface-name disable | all);
disable-timeout seconds;
}
  [http://www.juniper.net/techpubs/en_US/junos15.1/topics/task/configuration/spanning-trees-bpdu-block-cli.html](http://www.juniper.net/techpubs/en_US/junos15.1/topics/task/configuration/spanning-trees-bpdu-block-cli.html)

  ROOTGUARD
  
no-root-port;

[edit protocols mstp interface interface-name],
[edit protocols rstp interface interface-name],
[edit protocols stp interface interface-name]
[http://www.juniper.net/techpubs/en_US/junos16.1/topics/reference/configuration-statement/no-root-port-edit-protocols-stp.html](http://www.juniper.net/techpubs/en_US/junos16.1/topics/reference/configuration-statement/no-root-port-edit-protocols-stp.html)

  
  
  
  Настройка порта edge
  [edit protocols (mstp | rstp | vstp) interface interface-name],
[edit protocols mstp msti msti-id interface interface-name],
  
  
  
    Shared — порт, работающий в режиме Half Duplex
    Point-to-Point — порт, работающий в режиме Full Duplex.

  
logging event trunk-status
 logging event bundle-status
 logging event spanning-tree
 spanning-tree portfast trunk
 spanning-tree bpdufilter enable
 
 
 
 
 
 [http://prosto-seti.blogspot.com/2016/07/bpduguard-bpdufilter.html](http://prosto-seti.blogspot.com/2016/07/bpduguard-bpdufilter.html)
