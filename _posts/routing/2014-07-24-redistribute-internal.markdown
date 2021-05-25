---
layout: post
title:  "redistribute-internal"
date:   2014-07-24 22:34:31 +0400
categories: routing
tags: routing
---

# redistribute-internal
eBGP передаёт префиксы внешним соседям, если эти префиксы известны внутри iBGP и OSPF(IGP). В cisco по умолчанию.
eBGP передаёт только тогда, когда OSPF согласует маршруты внутри.

Если из вне приходят маршруты по eBGP на один граничный маршрутизатор и по iBGP проходят на другой граничный
то чтобы трафик проходил через внутрненние маршрутизаторы (OSPF) нужен маршрут внутри OSPF, то есть должно быть перераспределение
eBGP в iBGP и OSPF


bgp redistribute-internal
По умолчанию редистрибуция из IBGP в IGP отключена.
Чтобы ее включить выполните команду “bgp redistribute-internal” в режиме конфигурации BGP на маршрутизаторе. 

If a metric is not specified, OSPF puts a default value of 20 when redistributing routes from all protocols except Border Gateway Protocol (BGP) routes, which get a metric of 1.
20 - метрика по умолчанияю используемая при перераспределении всех протоколов в ospf, кроме bgp

When there is a major net that is subnetted, you need to use the keyword subnet to redistribute protocols into OSPF. Without this keyword, OSPF only redistributes major nets that are not subnetted.
Без использования слова subnets будет происходить перераспределение только супер-сети (главной) без подсетей.
Помните, что если ключевое слово subnet не используется, будут перераспределены только домены без подсетей

 subnets. Если эта команда не используется при перераспределении, в средOSPF может перераспределяться информация о сетях, созданных на основе
класса. В сети OSPF ключевое слово subnets обычно применяется при пере-
распределении в среду OSPF маршрутов больше чем к одной сети. А если не
указано ключевое слово subnets, то в среду OSPF перераспределяются только
те маршруты, которые не были созданы в результате формирования подсетей.



 forward metric - это метрика внути ospf (не складывается с случае E2)



redistribute bgp 65047 metric 1 metric-type 1 subnets

Означает перераспределить bgp маршруты в среду ospf, отбросив свою метрику, заменив её  ospf метрикой 1 и типом 1


[20/0]  AD/metrica

AD - более важное значение имеет, чем metrica


Непосредственное подключение  0
Статический маршрут  1
EBGP  20
EIGRP (внутренний)  90
IGRP  100
OSPF  110
ISIS  115
RIP  120
EGP  140
EIGRP (внешний)  170
IBGP  200
Локальный BGP  200
Неизвестный  255




 Е1 маршрута используется общая метрика для всего пути
 Е2 маршрута только стоимость редистрибуции
 
 E1 имеет приоритет перед E2
    Intra-Area (O)
    Inter-Area (O IA)
    External Type 1 (E1)
    External Type 2 (E2)
    NSSA Type 1 (N1)
    NSSA Type 2 (N2)

 
 По умолчанию приходит на E2,
 redistribute eigrp 100 subnets
 
 Чтобы приходило как E1 надо прописывать
 redistribute eigrp 100 subnets metric-type 1 metric 100
 Это означает, что маршруты протокола eigrp перераспределяются в ospf с типом 1 и метрикой 100
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 Enter the commands in the configuration mode as described here:

 
 
 match {internal
| external 1 |
external 2}

(Необязательная.) Критерии, согласно которым маршруты OSPF пере-
распределяются в другие домены маршрутизации. Эта опция может
иметь одно из приведенных ниже значений.
• internal. Маршруты, внутренние по отношению к указанной ав-
тономной системе. (intra и inter маршруты)
•
 external 1. Маршруты, которые являются внешними по отноше-
нию к автономной системе, но импортируются в среду OSPF как
внешние маршруты типа 1.
•
 external 2. Маршруты, которые являются внешними по отноше-
нию к автономной системе, но импортируются в среду OSPF как
внешние маршруты типа 2


  redistribute ospf 110 match internal external 1 external 2
  Это означает что мы перераспределяем все маршруты ospf
  
 По умолчанию перераспределяются только internal маршруты
 redistribute ospf 110 
 
 
 Так перераспределить только внешние (Е1 и E2)
 
    RTB(config-router)# router bgp 100
    RTB(config-router)# redistribute ospf 1 match external

In this configuration of Router B, we redistribute only OSPF External routes, but both type-1 and type-2:

Это аналогично команде, которая выше
redistribute ospf 1 match external 1 external 2


Это позволяет перераспределять только один тип
redistribute ospf 1 match external 1

или

router bgp 100
 redistribute ospf 1 match external 2







Проблема в том, что когда падает BGP - внешние маршруты, то на CE роутер приходят по OSPF эти внешние маршруты с другого CE через внутренний интерфейс
и наша CE перераспределяет эти маршруты в BGP,  согласно правилам перераспределения. Теперь, когда канал поднимается получается, что на CE есть 2 маршрута по BGP - пришедший из вне и перераспределённые из OSPF
Соответственно те маршруты, которые перераспределены из OSPF более приоритетны, так как пораждены на нашем CE и внешние BGP маршруты не попадают в таблицу маршрутизации.

Я так это понимаю. Выхода 2.
1. Не получать по OSPF маршруты с другого СЕ, что может быть не совсем кошерно
2. Не перераспределять никаких сетей в BGP из OSPF, кроме сетей калуги (10.60.0.0)

Второй вариант считаю приемлимый.
 
 Либо
 Исправить
 redistribute ospf 110 match internal external 1 external 2
 
  redistribute ospf 110 match external 2
  
  Либо
   redistribute ospf 110 route-map OSPF2BGP subnets
   
   
   access-list 30 permit 10.60.0.0 0.0.255.255 
   access-list 30 deny  any

   
   route-map OSPF2BGP permit 20
        match ip address 30
        set metric-type type-1
        set metric 1
        

Либо 
router bgp 65047
    redistribute ospf 110
    distribute-list 30 out ospf 110
    
    
    
    Вопрос следующий - как у нас работает на других узлах - тоже посмотреть ночью
    Я нигде не распределяю в bgp маршруты из ospf
    
    Надо проверить приходят ли внешние маршруты с другого CE по ospf при падении канала на нашем СЕ
    Приходят при правильной настройке, BGP бысто перестраиватеся. Проблем со стороны PSI не должно быть
    
    Попробовать переделать и посмотреть что будет при падении канала (Виз сталь)
        Да приходят, все маршруты приходят как E1, так уж там настроено
