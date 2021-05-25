---
layout: post
title:  "traffic-control"
date:   2014-09-12 09:10:08 +0400
categories: dlink
tags: dlink
---

# traffic-control
config traffic control_trap both
config traffic control 1-8 broadcast enable multicast enable unicast disable action drop threshold 64 countdown 5 time_interval 5



config safeguard_engine state enable utilization rising 80 falling 50 trap_log enable mode fuzzy

config filter dhcp_server ports 1-8 state enable                              
config filter dhcp_server ports 9-10 state disable                            
config filter dhcp_server illegal_server_log_suppress_duration 5min            
config filter dhcp_server trap enable                                          
config filter dhcp_server log enable 

enable sntp                                                                    
config time_zone operator + hour 4 min 0
config sntp primary 192.168.115.1 secondary 81.20.192.19 poll-interval 720


create vlan Chursin.A.N.Chelyuskina.1.42 tag 2683
config vlan Chursin.A.N.Chelyuskina.1.42 add tagged 25-28
config vlan Chursin.A.N.Chelyuskina.1.42 add untagged 17 

config ports 17 speed auto flow_control disable state enable description "Chursin.A.N.Chelyuskina.1.42"

config bandwidth_control 17 rx_rate 10240 tx_rate 10240


config traffic control_trap both
config traffic control 1-3 broadcast enable multicast enable unicast disable action drop threshold 10
config traffic control 25-26 broadcast disable action shutdown threshold 128000 time_interval 5 countdown 0
config traffic control 25-26 multicast disable action shutdown threshold 128000
config traffic control 4-5 unicast disable threshold 128000

На коммутаторах серии DES-3200 на прошивке 1.52.b007 threshold возможно указывать лишь от 64 pps. Возможно ли в будущих прошивках сделать возможным указывать этот параметр от 0, как например в 3526.
А в 3526 нехватает возможности мониторить шторм с конкретного порта, а не с группы портов как в текущих прошивках.

Настройки одинаковые в любом случае, 10 пакетов в секунду вполне хватит и для broadcast-а и для multicast-а.
Есть параметр Threshold, он задаётся либо в пакетах, тогда ставите 10 на клиентском порту, либо в kbps, тогда выставляете минимальное значение.

На DES-3200 параметр threshold выставляется не в pps, а в килобитах в секунду. 
64 Kbit/s - минимально возможное значение, поддерживаемое чипсетом, меньше сделать невозможно.


Action
shutdown – Для обнаружения пакетного шторма будет использоваться
программный механизм управления трафиком. При обнаружении шторма
порт будет закрыт для всех пакетов, кроме STP BPDU-пакетов,
используемых для функционирования покрывающего дерева коммутатора.
Если по истечении времени countdown пакетный шторм продолжается, порт
переходит в режим Shutdown Forever и не будет работать, пока пользователь
не введет вручную команду config ports enable или по истечении 5 мин
режим Shutdown Forever сменится режимом Auto- Recovery. При выборе
данной опции необходимо особенное внимание уделить настройке
временного интервала.
.............
Count Down Таймер Count Down позволяет определить время в минутах, в течение
которого Коммутатор не будет закрывать порт, на котором обнаружен
пакетный шторм. Этот параметр имеет значение только для портов,
настроенных со значением Shutdown в поле Action, т.е. при использовании
программной функции управления трафика. Допустимые значения в данном
поле 0, 5-30 с. По умолчанию задано 0, что означет, что порт никогда не
будет переходить в состояние shutdown.


Итак, я правильно понял, что как только появляется шторм (ну т.е. как свич поделит количество пакетов на 5 секунд (или сколько установишь)) и решит, 
что штормит, он сразу же начинает отбрасывать пакеты и делает это столько времени в минутах сколько укажешь в Count Down-е. 
После этого, если дела не улучшились - он выключает порт на 5 минут, после чего порт опять включается и история повторяется. Может повториться и раньше, если включить порт руками до истечения пяти минут. 
Если в Count Down-е поставить "0", то свич сразу выключит порт на 5 минут. Всё так?

На самом деле он не выключает, 
видать у Вас устаревшая версия английского manual, 
в последних версиях как раз пишется, что не отключит вообще, если выставить ноль.

config traffic control 1-24 broadcast enable action shutdown threshold 1 time_interval 5 countdown 5

он должен будет тушить порт, если шторм продержится более 5 минут, а штормом будет являться шквал пакетов, 
общим количеством более 999 штук в секунду. 
Но генерирую всего 480 пакетов, поток считается штормом. Разъясните пожалуйста, где что пропустил? 

Я Вам прошивку выслал. Лучше тестировать с ней. Теперь по параметрам. В R5 уже threshold измеряется в пакетах в секунду. 
Т.е. Вы задали порог срабатывания в один пакет в секунду. 
Time_interval означает период в секундах с которым свитч будет проверять наличие шторма и пытаться включить порт обратно при его отсутствии. 
После же того как закончится Countdown в минутах свитч отключит порт при наличии шторма вообще.


Т.е. после настроек Time Interval = 5 и Count Down = 5, коммутатор регистрирует, что входящий broadcast трафик за 5 сек превысел пороговое значение и в течении последущих 5 мин продолжал превышать,
 коммутатор положил порт, и через какое-то время сам его поднял?

Нормальные настройки

config traffic control 1-5 broadcast enable multicast enable
config traffic control 1-5 action drop
config traffic control 1-5 threshold 64 countdown 10 time_interval 10
config traffic trap both

По поводу threshold = 0 трафик просто отбрасывается.

На клиентских портах лучше использовать drop режим и ставить макс 10 пакетов в секунду, этого будет достаточно для нормальной работы и для безопасности сети.




Количество пакетов в секунду (PPS)
10% бродкаст трафика это нормально, больше уже не надо
советуют на домовых портах 64 pps 


Если речь идет о коммутаторах уровня агрегации, то значения threshold подбираются эмпирически исходя из примерного количества клиентов и по результатам мониторинга количества трафика на портах. В плане работы механизма у Вас все верно написано, но учтите, что под юникастом тут понимается DFL (Destination Lookup Failure), то есть трафик для которого МАС-адрес назначения не может быть найден в FDB.
Что касается того, какой трафик попадает на CPU: сюда входит весь трафик предназначенный непосредственно IP-интерфейсам коммутатора, броадкаст и мультикаст во вланах, где есть IP-интерфейсы, также ресурсы CPU задействуются в случае логирования и использования определенного функционала, такого как например DHCP Relay, DHCP Snooping, сбор статистики по SNMP, отсылка трапов и т.д.



На DGS
64x24x6=9216
64 pps на одного, в линейке 6-8 коммутаторов
ну наверно 12288


config traffic control  1-27 broadcast enable multicast enable unicast disable action drop threshold 12288 countdown 5 time_interval 5

