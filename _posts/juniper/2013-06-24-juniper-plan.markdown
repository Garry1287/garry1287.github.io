---
layout: post
title:  "План по введению в эксплуатацию juniper"
date:   2013-06-24 09:19:06 +0400
categories: juniper Networking
tags: juniper
---

# План по введению в эксплуатацию juniper

1. Te2/8 перенести в Te1/8, настроить порт под STP на Catalyst
```
interface TenGigabitEthernet1/8
 description #to Juniper
 switchport mode trunk
 mtu 9198
 load-interval 30
 storm-control broadcast level 10.00
 storm-control action shutdown
 storm-control action trap
 no cdp enable
```

2. Настроить порт на Juniper xe-0/0/0
3. Скроссировать
4. Проверить mstp 
```
    run show spanning-tree interface
    show spanning-tree bridge 
    show spanning-tree interface 
```
5. Проверить ospf
```
    show ospf interface 
    show ospf neighbor
    show log debug-ospf
```
6.Пробуем перекинуть несколько портов
    CTD-S8
    Matyra
    Проверить линки, посмотреть mac адреса
```
run show interfaces 
root@juniper> show interface description
root@juniper> show interface terse {кратко о состоянии интерфейсов}
root@juniper> show interface detail {полная информация о интерфейсах}
monitor traffic interface ge-0/0/1

run show ethernet-switching table
```

7.Перекидываем линки на CTD-S1 и k9-s9
    Проверяем STP, меняем приоритет в 0 истансе
     
     проверяем ae1
```
root> show interfaces ae1 extensive
root> show ethernet-switching table
show lacp interfaces
```         
            
8. Переносим BGW
        Te1/6  -Ctd-c5
        Переносим CTD-C6
        Gi2/10 и Gi2/16 переносим в ge-0/0/11, ge-0/0/17  (ae2)
        Проверяем BGW, маки и ae2
        + переносим резерный порт в  ae3

9. Переносим RETN-3kanal CTD-C6
    Gi2/18
    Сейчас там клиентcкие вланы пингом
    
10.REDBACK
```
show log
```
Как посмотреть порты на REDBACK
```
    [local]LPK-C01-BRAS01#show port 5/1 detail 

    link-group po4 dot1q
    dot1q pvc 13
    bind interface uplink internet
    lacp passive
    
    
    port ethernet 5/2 
    no shutdown
    encapsulation dot1q
      link-group po4
    
    port ethernet 6/2 
        no shutdown
        encapsulation dot1q
        link-group po4
    
    
    show subscribers summary 
    show subscribers all
```
            Смотрим время появления сессий
    
    ----------------------------------------------------------------------
Убить 
    
```
port ethernet 6/2 
 no shutdown
 encapsulation dot1q
 dot1q pvc 13 
  bind interface uplink internet
```

Мониторинг на cisco lacp
-------------------------------------------
```
sw1#sh etherchannel summary
sh etherchannel port-channel
sh lacp 1 internal
```

 [http://xgu.ru/wiki/%D0%90%D0%B3%D1%80%D0%B5%D0%B3%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5_%D0%BA%D0%B0%D0%BD%D0%B0%D0%BB%D0%BE%D0%B2](http://xgu.ru/wiki/%D0%90%D0%B3%D1%80%D0%B5%D0%B3%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5_%D0%BA%D0%B0%D0%BD%D0%B0%D0%BB%D0%BE%D0%B2)
    
11. Переносим оставшиеся порты
     Смотрим маки пинги.
     
     Отдельно RETN новый на 22 порт проконтролировать

12. Переносим маршруты по умолчанию
2. Статик маршруты с худшей метрикой сделать, нафиг надо - по одному перекину и всё
```
ip route 81.20.192.0 255.255.240.0 Null0
ip route 81.20.192.0 255.255.254.0 Null0
ip route 81.20.192.6 255.255.255.255 81.20.192.55
ip route 81.20.192.17 255.255.255.255 81.20.192.55
ip route 81.20.195.0 255.255.255.0 Null0
ip route 81.20.195.33 255.255.255.255 81.20.192.55
ip route 81.20.196.0 255.255.252.0 Null0
ip route 81.20.200.0 255.255.248.0 Null0
ip route 81.20.200.0 255.255.252.0 Null0
ip route 81.20.204.0 255.255.252.0 Null0
```

Убрать 38 vlan?

13. Посмотреть, сфотографировать то, что можно перенести с ctd-s1, ctd-s8


PS
Сохранение резервной конфигурации
root@juniper> request system configuration rescue save



Жёстко прописать дуплекс и скорость с двух сторон



Проверка LACP
To confirm that the interface is up run the following command (при добавлениие действующего физического интерфейса мы должны видет такую ситуацию)
```
root@srx# run show interfaces terse | match ae1
fe-0/0/3.0              up    up   aenet    --> ae1.0
fe-0/0/4.0              up    up   aenet    --> ae1.0
ae1                     up    up
ae1.0                   up    up   eth-switch
```

`run show interfaces ae1 extensive`

Проверка LAG в Juniper осуществляется с помощью команды show interfaces ae№ или, при использовании LACP — show lacp interfaces и show lacp statistics

А ещё можно включить трассировку LACP:
```
[edit]
user@Switch-1# set protocols lacp traceoptions flag ?
Possible completions:
all                                       All events and packets
configuration                   Configuration events
mc-ae                                Multi-chassis AE messages
packet                               LACP packets
ppm                                  LACP PPM messages
process                            Process events
protocol                           Protocol events
routing-socket                Routing socket events
startup                             Process startup events
```

[http://blog.sbolshakov.ru/13-2-ha-lag/](http://blog.sbolshakov.ru/13-2-ha-lag/)
