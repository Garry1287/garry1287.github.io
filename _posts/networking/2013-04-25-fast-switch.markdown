---
layout: post
title:  "fast-switch"
date:   2013-04-25 02:23:35 +0400
categories: Networking
tags: Networking
---

# fast-switch
[http://www.sakhttk.ru/ru/support/faq_vpn/30.html](http://www.sakhttk.ru/ru/support/faq_vpn/30.html)


Частые вопросы по IP VPN
Как осуществляется балансировка нагрузки при использовании load balancing?

Load balancing – стандартный функционал Cisco IOS и присутствует на всех моделях маршрутизаторов. Load balancing активируется автоматически если в таблице маршрутизации одновременно присутствует несколько маршрутов с одинаковыми метриками на одну подсеть. Механизм работает для статических маршрутов и всех стандартных протоколов маршрутизации за исключением BGP, в котором по-умолчанию используется только один маршрут. Возможны два механизма распределения пакетов по альтернативным маршрутам: per-packet и per-destination. Per-packet load balancing подразумевает использование альтернативных путей для каждого пакета, т.е. последовательно приходящие пакеты будут направляться поочередно по разным путям. Per-destination load balancing использует один путь для одного destination, не допуская, таким образом, возможности переупорядочивания пакетов, вызванных неравноценностью путей на которых осуществляется балансировка. Механизм per-destination удобно использовать для передачи трафика приложений, чувствительных к переупорядочиванию пакетов в процессе передачи через IP-сеть. В основном – это мультимедийные приложения работающие в реальном времени, такие как приложения передачи голоса или видео. Используемый тип балансировки пакетов зависит от типа коммутации IP-пакетов, используемого на маршрутизаторе. В большинстве маршрутизаторов Cisco по-умолчанию используется fast-switching и балансировка per-destination. Для того чтобы включить per-packet балансировку нужно использовать process-switching:

Router# config t
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)# interface Ethernet 0
Router(config-if)# no ip route-cache
Router(config-if)# ^Z

Команда no ip route-cache выключает fast-switching и включает process-switching, что приводит к тому, что маршрутизатор начинает производить балансировку для каждого пакета.

ПРИМЕЧАНИЕ: Process-switching занимает значительный ресурс CPU и его включение может привести к падению маршрутизатора. Кроме того при включенном на интерфейсе process-switching-е происходит некорректный подсчет статистики на NetFlow. В силу сказанного, КТТК не рекомендует использовать process-switching и не принимает претензий от клиента по расхождению в статистике NetFlow если у клиента process-switching включен.

Для того чтобы вновь включить fast-switching необходимо дать следующие конфигурационные команды:

Router# config t

Enter configuration commands, one per line. End with CNTL/Z.
Router(config)# interface Ethernet 0
Router(config-if)# ip route-cache
Router(config-if)# ^Z

Команда sh run не показывает ip route-cache поскольку использование fast-switching является поведением по-умолчанию.

Использование Cisco Express Forwarding (CEF) позволяет осуществлять балансировку нагрузки с большей скоростью, при этом балансировка per-destination работает для каждой пары source-destination. При включении CEF по-умолчанию будет использоваться per-destination load balancing. Для включения per-packet load balancing в CEF необходимо дать команды:

Router #conf t
Enter configuration commands, one per line. End with CNTL/Z.
Router (config)#ip cef
Router (config)#interface FastEthernet0
Router (config-subif)#ip load-sharing per-packet
Router (config-subif)#^Z
Router #

Как уже говорилось, по-умолчанию BGP использует только один маршрут, для того, чтобы включить BGP load sharing необходимо дать команду maximum-paths для определения максимального количества параллельно используемых путей маршрутизации с одинаковыми стоимостями. Пример:

!

router bgp 11
neighbor 160.20.20.2 remote-as 10
neighbor 150.10.10.2 remote-as 10
network 1.0.0.0
maximum-paths 2
...