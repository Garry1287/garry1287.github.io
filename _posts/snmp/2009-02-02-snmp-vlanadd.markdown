---
layout: post
title:  "snmp-vlanadd"
date:   2009-02-02 21:09:03 +0300
categories: snmp
tags: snmp
---

# snmp-vlanadd
tagged (cуммируются с untagged)

garry@garry:/var/home/garry> snmpwalk -v 2c -c public 192.168.118.71
1.3.6.1.2.1.17.7.1.4.3.1.2
SNMPv2-SMI::mib-2.17.7.1.4.3.1.2.1 = Hex-STRING: 00 00 00 00 00 00 00 00
SNMPv2-SMI::mib-2.17.7.1.4.3.1.2.25 = Hex-STRING: 00 00 00 F0 00 00 00 00
SNMPv2-SMI::mib-2.17.7.1.4.3.1.2.490 = Hex-STRING: FF FF FF F0 00 00 00 00
SNMPv2-SMI::mib-2.17.7.1.4.3.1.2.491 = Hex-STRING: 00 00 00 C0 00 00 00 00



untagged
garry@garry:/var/home/garry> snmpwalk -v 2c -c public 192.168.118.71
1.3.6.1.2.1.17.7.1.4.3.1.4
SNMPv2-SMI::mib-2.17.7.1.4.3.1.4.1 = Hex-STRING: 00 00 00 00 00 00 00 00
SNMPv2-SMI::mib-2.17.7.1.4.3.1.4.25 = Hex-STRING: 00 00 00 00 00 00 00 00
SNMPv2-SMI::mib-2.17.7.1.4.3.1.4.490 = Hex-STRING: FF FF FF 00 00 00 00 00
SNMPv2-SMI::mib-2.17.7.1.4.3.1.4.491 = Hex-STRING: 00 00 00 00 00 00 00 00



8 портов    8 портов    8 портов    4 порта
FF                 FF                   FF          F0                
                    00 00 00 00
11111111    11111111    11111111    11110000

Получается на этой моделе используется 3,5 октета

VID             : 1           VLAN Name       : default
VLAN Type       : Static      Advertisement   : Enabled
Member Ports    :                    
Static Ports    :                    
Current Tagged Ports   :                    
Current Untagged Ports :                    
Static Tagged Ports    :                    
Static Untagged Ports  :                    
Forbidden Ports        :                    

VID             : 25          VLAN Name       : mngt
VLAN Type       : Static      Advertisement   : Disabled
Member Ports    : 25-28              
Static Ports    : 25-28              
Current Tagged Ports   : 25-28              
Current Untagged Ports :                    
Static Tagged Ports    : 25-28              
Static Untagged Ports  :                    
Forbidden Ports        :                    
                                                                              

VID             : 490         VLAN Name       : borodinskaya45
VLAN Type       : Static      Advertisement   : Disabled
Member Ports    : 1-28               
Static Ports    : 1-28               
Current Tagged Ports   : 25-28              
Current Untagged Ports : 1-24               
Static Tagged Ports    : 25-28              
Static Untagged Ports  : 1-24               
Forbidden Ports        :                    
                                                                              

VID             : 491         VLAN Name       : borodinskaya49
VLAN Type       : Static      Advertisement   : Disabled
Member Ports    : 25-26              
Static Ports    : 25-26              
Current Tagged Ports   : 25-26              
Current Untagged Ports :                    
Static Tagged Ports    : 25-26              
Static Untagged Ports  :  

         

Сохранить конфиг
snmpset -v2c -c private 192.168.118.71 1.3.6.1.4.1.171.12.1.2.6.0 i 2
Прописать описание на порт - 32 символа
snmpset -v2c -c private 192.168.118.71 IF-MIB::ifAlias.28 s "28port"