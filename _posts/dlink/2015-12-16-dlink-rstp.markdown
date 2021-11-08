---
layout: post
title:  "Rstp на dlink"
date:   2015-12-16 00:39:36 +0300
categories: dlink
tags: dlink
---

# Rstp на dlink

## Пример Манежа

DSG3627
```
 config stp version rstp
 config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 3 fbpdu disable hellotime 2 lbd enable lbd_recover_timer 60
 config stp priority 4096 instance_id 0 
 config stp mst_config_id name 00:22:B0:30:E9:00 revision_level 0
 
 config stp ports 1-8 externalCost auto  edge false p2p auto state enable lbd disable
 config stp mst_ports 1-27 instance_id 0 internalCost auto priority 128
config stp ports 1-8 fbpdu enable
 config stp ports 9-27 externalCost auto  edge true p2p auto state disable lbd disable
config stp ports 9-27 fbpdu disable
enable stp
```

3200
```
# STP
                                                                               
config stp version rstp
config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 6 fbpdu enable hellotime 2
config stp priority 32768 instance_id 0 
config stp mst_config_id name 1C:BD:B9:64:94:60 revision_level 0
config stp ports 1-24 externalCost auto edge true p2p auto state disable
config stp mst_ports 1-28 instance_id 0 internalCost auto priority 128
config stp ports 1-24 fbpdu disable
config stp ports 1-24 restricted_role true
config stp ports 1-24 restricted_tcn true
config stp ports 25-28 externalCost auto edge false p2p auto state enable
config stp ports 25-28 fbpdu enable
config stp ports 25-28 restricted_role false
config stp ports 25-28 restricted_tcn false
enable stp
```

## Конфиг 13 район

```
config stp version rstp
config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 6 fbpdu enable hellotime 2
config stp priority 32768 instance_id 0 
config stp mst_config_id name 1C:BD:B9:64:94:60 revision_level 0
config stp ports 1-24 externalCost auto edge true p2p auto state disable
config stp mst_ports 1-28 instance_id 0 internalCost auto priority 128
config stp ports 1-24 fbpdu disable
config stp ports 1-24 restricted_role true
config stp ports 1-24 restricted_tcn true
config stp ports 25-28 externalCost auto edge false p2p auto state enable
config stp ports 25-28 fbpdu enable
config stp ports 25-28 restricted_role false
config stp ports 25-28 restricted_tcn false
enable stp
```




192.168.124.39

5 кольцо ОК

6 кольцо 2 последних не видно
ул.Ильича 18		6.4.1	192.168.124.37	1c-7e-e5-6d-49-20	PVZ82B7000490	6	1:6,2:6
ул.Волгоградская 5		6.5.1	192.168.124.38	1c-7e-e5-6d-4b-60	PVZ82B7000430	6	1:6,2:6

7 OK, obratny poradok


Не видно в 8
Жуковского 5		8.5.1	192.168.124.48	1c-7e-e5-6d-58-40	PVZ82B7000004	8	1:8,2:8


9 ок. но обратный порядок


```
vlan 21
 name CDE-RADIO-MGMT
!
vlan 22
 name CDE-MGMT
!
vlan 23
 name WIMAX-MGMT

vlan 155
 name OEZ-CHSZ-INET

vlan 129
 name Novikova-INET-VoIp

vlan 168
 name VNC_TEC2

vlan 176
 name Bist_INET-VoIP

!
vlan 178
 name Borino(JKH)-INET
                                                                                                                                                
vlan 579
 name Kondi-BSR-nlmk-INET                                                                                                                                                         

vlan 610
 name OEZ-TP-INET-VOIP
!
vlan 611
 name CHKINGDOM-ROSSIA-IPVPN

vlan 625
 name Liter(OEZ)-INET
                                                                                                                                                    
vlan 626
 name INET_BEKARD

vlan 803
 name LGEK-VPN
                                                                                                                                 
                                                                                                                                                             
vlan 817
 name STINOL

vlan 2024
 name city-bank-psi

vlan 3012
 name UVSK-2

vlan 3021
 name RemEnMet-L-INET


vlan 3032
 name Grazhd_pripasy_VOIP

vlan 3065
 name Lapina-Kamennoe-INET


vlan 3071
 name Anisimov
!
vlan 3073
 name PPT-Lipetsk

vlan 3082
 name Bekard-2-OEZ
                                                                                                                               
vlan 3997
 name pppoe_nlmk
                                                                                                                                                           
vlan 4007
 name KMN-VPN

 switchport trunk allowed vlan add 21-23,129,154,155,158,159,161,168,176,178,579
 switchport trunk allowed vlan add 608-612,625,626,803,817,953,954,2024,3012
 switchport trunk allowed vlan add 3021,3032,3064,3065,3071,3073,3082,3997,4007
```

```
config stp version rstp
config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 3 fbpdu disable hellotime 2 lbd enable lbd_recover_timer 60 nni_bpdu_addr dot1ad
config stp priority 4096 instance_id 0 
config stp mst_config_id name 00:22:B0:2B:64:00 revision_level 0
enable stp
config stp ports 1:1-1:20 externalCost auto  edge false p2p auto state enable restricted_role false restricted_tcn false lbd disable
config stp mst_ports 1:1-1:25 instance_id 0 internalCost auto priority 128
config stp ports 1:1-1:20 fbpdu enable
config stp ports 1:12-1:25 externalCost auto  edge true p2p auto state disable restricted_role false restricted_tcn false lbd disable
config stp ports 1:12-1:25 fbpdu disable

config stp ports 2:1-2:20 externalCost auto  edge false p2p auto state enable restricted_role false restricted_tcn false lbd disable
config stp mst_ports 2:1-2:25 instance_id 0 internalCost auto priority 128
config stp ports 2:1-2:20 fbpdu enable

config stp ports 2:12-2:25 externalCost auto  edge true p2p auto state disable restricted_role false restricted_tcn false lbd disable
config stp ports 2:12-2:25 fbpdu disable
```






```                                                       
config stp version rstp
enable stp                                                      
config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 6 fbpdu enable hellotime 2
config stp priority 32768 instance_id 0                                                   
config stp ports 1-24 externalCost auto edge true p2p auto state disable       
config stp mst_ports 1-28 instance_id 0 internalCost auto priority 128
config stp ports 1-24 fbpdu disable                                            
config stp ports 1-24 restricted_role true                                     
config stp ports 1-24 restricted_tcn true                                      
config stp ports 25-28 externalCost auto edge false p2p auto state enable      
config stp ports 25-28 fbpdu enable                                            
config stp ports 25-28 restricted_role false   
```


```
 config stp version rstp                                                        
 config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 3 fbpdu disable hellotime 2 lbd enable lbd_recover_timer 60
 config stp priority 16384 instance_id 0 
enable stp
```

```                                                                     
 config stp version rstp                                                        
 config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 3 fbpdu disable hellotime 2 lbd enable lbd_recover_timer 60
 config stp priority 4096 instance_id 0                                        
 config stp mst_config_id name 00:22:B0:1B:EC:00 revision_level 0               
 enable stp                                                                     
 config stp ports 9-27 externalCost auto  edge false p2p auto state enable lbd disable
 config stp mst_ports 1-27 instance_id 0 internalCost auto priority 128         
config stp ports 1-20,22-24 fbpdu enable                                        
 config stp ports 21 externalCost auto  edge true p2p auto state disable lbd disable
config stp ports 21,25-27 fbpdu disable                                         
                                           
config stp priority 4096 instance_id 0
config stp ports 1-4 externalCost auto  edge true p2p auto state disable lbd disable 
config stp ports 9-27 externalCost auto edge true p2p auto state disable lbd disable
 config stp ports 5-8 externalCost auto  edge false p2p auto state enable lbd disable
config stp ports 5-8 fbpdu enable 


config stp ports 21 externalCost auto edge true p2p auto state disable lbd disable
config stp ports 1-20 externalCost auto edge false p2p auto state enable lbd disable
config stp ports 22-23 fbpdu enable

config stp ports 1-20 externalCost auto edge false p2p auto state enable lbd disable
config stp ports 22-24 externalCost auto edge false p2p auto state enable lbd disable

config stp ports 1-20 fbpdu enable
config stp ports 22-24 fbpdu enable
```



