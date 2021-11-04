---
layout: post
title:  "Переделака cisco ASA в eburg'e"
date:   2008-12-06 15:27:56 +0300
categories: cisco
tags: cisco asa
---

# Переделака cisco ASA в eburg'e

MAC address 2c54.2d0c.98b7 -не active

    Соединить везде прямыми линками asa-шки?  Перекроссировки
    
    Statefull Failover Link сделать? есть
    
    virtual mac?
    Решение failover mac address phy_if active_mac standby_mac
    
```
failover mac address new-link 2c54.2d0c.98b7 2c54.2d0c.98c1

failover mac address Ethernet0/3 2c54.2d0c.98b7 2c54.2d0c.98c1
```

Или наоборот


    1.Тест как есть, рубануть по питанию стойку
    2.Тест с вирутальным маком
    3.Тест со отдельным failover link'ом


Обесточить одну АСУ
4 порты соединить между собой


Активна ASA совинтеловская 
```
Sov
 2c54.2d0c.98b7    DYNAMIC     Gi1/0/4
```



Мак адрес активной Асы, которая 8
2c54.2d0c.98c1


Это секондари
2c54.2d0c.98b7


```
Maxi-ASA#  sh failover
Failover On 
Failover unit Primary
Failover LAN Interface: new-link Ethernet0/3 (up)
Unit Poll frequency 1 seconds, holdtime 15 seconds
Interface Poll frequency 5 seconds, holdtime 25 seconds
Interface Policy 1
Monitored Interfaces 4 of 250 maximum
Version: Ours 8.0(4), Mate 8.0(4)
Last Failover at: 10:46:43 MSK Dec 4 2015
        This host: Primary - Active 
                Active time: 10140556 (sec)
                slot 0: ASA5510 hw/sw rev (2.0/8.0(4)) status (Up Sys)
                  Interface outside (10.98.99.9): Normal 
                  Interface vlan12 (10.98.0.1): Normal 
                  Interface vlan18 (10.98.16.1): Normal 
                  Interface vlan65 (10.98.254.66): Normal (Not-Monitored)
                  Interface vlan72 (0.0.0.0): Link Down (Not-Monitored)
                  Interface vlan100 (0.0.0.0): Normal (Not-Monitored)
                  Interface management (10.98.98.7): Normal 
                  Interface vlan15 (10.98.8.1): Normal (Not-Monitored)
                slot 1: empty
        Other host: Secondary - Standby Ready 
                Active time: 0 (sec)
                slot 0: ASA5510 hw/sw rev (2.0/8.0(4)) status (Up Sys)
                  Interface outside (10.98.99.10): Normal 
                  Interface vlan12 (10.98.0.254): Normal 
                  Interface vlan18 (10.98.16.254): Normal 
                  Interface vlan65 (10.98.254.67): Normal (Not-Monitored)
                  Interface vlan72 (0.0.0.0): Normal (Not-Monitored)
                  Interface vlan100 (0.0.0.0): Normal (Not-Monitored)
                  Interface management (10.98.98.8): Normal 
                  Interface vlan15 (10.98.8.2): Normal (Not-Monitored)
                slot 1: empty

Stateful Failover Logical Update Statistics
        Link : new-link Ethernet0/3 (up)
        Stateful Obj    xmit       xerr       rcv        rerr      
        General         350737135  12         4896358    0     

   4    2c54.2d0c.98b3    DYNAMIC     Gi1/0/23

   5    2c54.2d0c.98b4    DYNAMIC     Gi1/0/3
```



Понять какая Активна
Sov switch
```
  4    2c54.2d0c.98b3    DYNAMIC     Gi1/0/23
2c54.2d0c.98b3
```
10.98.98.7





Mega
2c54.2d0c.98bd
10.98.98.8

```
Maxi-ASA#   sh failover
Failover On 
Failover unit Secondary
Failover LAN Interface: new-link Ethernet0/3 (up)
Unit Poll frequency 1 seconds, holdtime 15 seconds
Interface Poll frequency 5 seconds, holdtime 25 seconds
Interface Policy 1
Monitored Interfaces 4 of 250 maximum
Version: Ours 8.0(4), Mate 8.0(4)
Last Failover at: 10:52:46 MSK Dec 4 2015
        This host: Secondary - Standby Ready 
                Active time: 0 (sec)
                slot 0: ASA5510 hw/sw rev (2.0/8.0(4)) status (Up Sys)
                  Interface outside (10.98.99.10): Normal 
                  Interface vlan12 (10.98.0.254): Normal 
                  Interface vlan15 (10.98.8.2): Normal (Not-Monitored)
                  Interface vlan18 (10.98.16.254): Normal 
                  Interface vlan65 (10.98.254.67): Normal (Not-Monitored)
                  Interface vlan72 (0.0.0.0): Link Down (Not-Monitored)
                  Interface vlan100 (0.0.0.0): Normal (Not-Monitored)
                  Interface management (10.98.98.8): Normal 
                slot 1: empty
        Other host: Primary - Active 
                Active time: 10140693 (sec)
                slot 0: ASA5510 hw/sw rev (2.0/8.0(4)) status (Up Sys)
                  Interface outside (10.98.99.9): Normal 
                  Interface vlan12 (10.98.0.1): Normal 
                  Interface vlan15 (10.98.8.1): Normal (Not-Monitored)
                  Interface vlan18 (10.98.16.1): Normal 
                  Interface vlan65 (10.98.254.66): Normal (Not-Monitored)
                  Interface vlan72 (0.0.0.0): Normal (Not-Monitored)
                  Interface vlan100 (0.0.0.0): Normal (Not-Monitored)
                  Interface management (10.98.98.7): Normal 
```