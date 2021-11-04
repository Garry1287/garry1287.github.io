---
layout: post
title:  "Asa failover"
date:   2009-02-09 00:16:22 +0300
categories: cisco
tags: cisco asa
---

# Failover на cisco ASA
Настройка по шагам в Вене

1. Прописать ip адреса на интерфейсах

```
interface GigabitEthernet0/0
 description TO_BALANCERS_SWITCH0_FA0/7(access_vlan_1967)
 nameif inside
 security-level 100
 ip address 10.170.253.1 255.255.255.248  standby 10.170.253.2
 
 interface GigabitEthernet0/1
 description TO_JuniperFirewall(access_vlan_1966)
 nameif outside
 security-level 100
 ip address 10.170.25.4 255.255.255.0 standby 10.170.25.5
 
interface Management0/0
 management-only
 nameif management
 security-level 100
 ip address 10.170.250.31 255.255.255.0 standby 10.170.250.32
```
 
2.
```
failover lan unit primary
failover lan interface new-link GigabitEthernet0/5
```
Предварительно выделить адреса на failover link
```
failover interface ip new-link 10.170.255.1 255.255.255.252 standby 10.170.255.2

int GigabitEthernet0/5
no shut
description LAN/STATE Failover Interface

failover link new-link GigabitEthernet0/5
failover
wr
```

3. Настройка резервной asa
```
failover lan interface new-link GigabitEthernet0/5
failover interface ip new-link 10.170.255.1 255.255.255.252 standby 10.170.255.2

int GigabitEthernet0/5
no shut
description LAN/STATE Failover Interface

failover lan unit secondary
failover
```
[http://www.cisco.com/c/en/us/td/docs/security/asa/asa80/configuration/guide/conf_gd/failover.html#wp1041883](http://www.cisco.com/c/en/us/td/docs/security/asa/asa80/configuration/guide/conf_gd/failover.html#wp1041883)
 

## 2 типа аварийного переключения
1. Active/active - это 2 контекста
2. Active/stanby 


## Режимы работы

1. Stateful failover - с сохранением текущего состояния: обе ASA обмениваются информацией о состоянии сеансов по выделенному линку
(Statefull Failover Link), и если какая-либо из ASA выйдет из строя, то другая подхватит существующие сеансы и продолжит работу.

2. Stateless failover - когда при отказе основной все сеансы связи сбрасываются; 
активируется резервная ASA, соединения для всех сеансов устанавливаются заново (использует Failover Link). (Hardware)



## Failover link

Любой Ethernet-интерфейс может использоваться в качестве failover-интерфейса, однако нельзя указывать интерфейс, на котором уже задано имя интерфейса.
Failover-интерфейс не настраивается как обычный интерфейс для передачи данных,
 он существует только для коммуникаций связанных с failover (он может использоваться в качестве stateful failover link). 


## Stateful failover link

Для того чтобы использовать возможности Stateful Failover, надо настроить stateful failover link (state link) для передачи информации о состоянии соединений.
Возможны такие варианты выбора stateful failover link:

   * Выделенный интерфейс
   * Общий интерфейс с failover link
   * Общий интерфейс с обычным интерфейсом для передачи данных. Однако, эту опцию не рекомендуется использовать. Кроме того, она поддерживается только в single context, routed mode. 



Health Monitoring - мониторинг link up/down  линка выделенного для failover (failover link) Мониторит падения, сетевую активность, arp и броадкаст пинг
С помощью него определяется подняты ли оба unit

Failover link используется для обмена информацией между unit-ами
Есть 2 типа failover link

1. LAN-based failover (на основе ethernet порта
2. Serial Cable Failover Link (HW) serial Failover cable, RS-232


```
failover      
failover lan unit primary
failover lan interface new-link Ethernet0/3
failover link new-link Ethernet0/3
failover interface ip new-link 10.90.252.9 255.255.255.252 standby 10.90.252.10
```


`no failover link new-link Ethernet0/3`

---
Это настройка (Stateless failover), только с Failover link 
```
failover lan unit secondary
failover lan interface new-link Ethernet0/3
failover interface ip new-link 10.90.252.9 255.255.255.252 standby 10.90.252.10
```
Это настройка   Stateful failover c Stateful failover link 
```
failover link new-link Ethernet0/3
```
---

Interface Monitoring

Указываем интерфейсы, которые хотим мониторить и указываем условие, (процент или количество) интерфейсов, при падении которых должен произойти файловер.
```
monitor-interface vlan12
monitor-interface vlan18
```
При падение интерфейсов в сторону клиента происходит переключение.

Проверка failover

Ввести на пассивном
`failover active`


Ввести на активном
`no failover active`



Чтобы отключить переход на другой ресурс при сбое
`no failover`


Чтобы верноуть неисправному модулю статус исправного необходимо ввести
`failover reset`







Правильная настройка портов свитча
WS3560-24TS-E configuration
```
interface FastEthernet0/1
switchport mode access
spanning-tree portfast
spanning-tree bpduguard enable
end

interface FastEthernet0/2
switchport mode access
spanning-tree portfast
spanning-tree bpduguard enable
end
```



--------------------------------------------------------------------------------

Step 8
	

For Active/Standby mode:

failover mac address phy_if active_mac standby_mac

 

For Active/Active mode:

mac address phy_if active_mac standby_mac
 

ciscoasa(config)# failover mac address gigabitethernet0/2 00a0.c969.87c8 00a0.c918.95d8

 

Or

ciscoasa(config-fover-group)# mac address gigabitethernet0/2 00a0.c969.87c8 00a0.c918.95d8
	

Configures the virtual MAC address for an interface.

The phy_if argument is the physical name of the interface, such as gigabitethernet0/1.

The active_mac and standby_mac arguments are MAC addresses in H.H.H format, where H is a 16-bit hexadecimal digit. For example, the MAC address 00-0C-F1-42-4C-DE would be entered as 000C.F142.4CDE.

The active_mac address is associated with the active IP address for the interface, and the standby_mac is associated with the standby IP address for the interface.

You can also set the MAC address using other commands or methods, but we recommend using only one method. If you set the MAC address using multiple methods, the MAC address used depends on many variables, and might not be predictable.

Use the show interface command to display the MAC address used by an interface.





Соединить везде прямыми линками asa-шки?  Перекроссировки
Statefull Failover Link сделать? есть
virtual mac?
Решение failover mac address phy_if active_mac standby_mac
spanning-tree portfast на коммутаторе прописать


1.Тест как есть, рубануть по питанию стойку
2.Тест с вирутальным маком
3.Тест со отдельным failover link'ом

[http://www.cisco.com/c/en/us/td/docs/security/asa/asa91/configuration/general/asa_91_general_config/ha_failover.html](http://www.cisco.com/c/en/us/td/docs/security/asa/asa91/configuration/general/asa_91_general_config/ha_failover.html)



Маршруты
[http://www.cisco.com/c/en/us/support/docs/security/adaptive-security-appliance-asa-software/115986-asa-eqm-products-configuration-example.html](http://www.cisco.com/c/en/us/support/docs/security/adaptive-security-appliance-asa-software/115986-asa-eqm-products-configuration-example.html)
