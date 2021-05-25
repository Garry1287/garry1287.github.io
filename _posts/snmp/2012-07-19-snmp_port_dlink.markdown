---
layout: post
title:  "snmp_port_dlink"
date:   2012-07-19 15:53:47 +0400
categories: snmp
tags: snmp
---

# snmp_port_dlink
 /usr/bin/snmpset -c private -v 2c 192.168.124.238 1.3.6.1.2.1.17.7.1.4.3.1.1.1235 s MATIR-vl1235 
1.3.6.1.2.1.17.7.1.4.3.1.2.1235 x 000000F000000000 1.3.6.1.2.1.17.7.1.4.3.1.4.1235 x 0000010000000000 IF-MIB::ifAlias.24 s kv.77,L.V.Fedjanina 
1.3.6.1.2.1.17.7.1.4.3.1.5.1235 i 4 1.3.6.1.4.1.171.12.42.4.2.1.2.1235 i 1 1.3.6.1.4.1.171.12.1.2.18.4.0 i 2


/usr/bin/snmpset -c private -v 2c 192.168.124.197 1.3.6.1.2.1.17.7.1.4.3.1.1.598 s Univer-vl598
1.3.6.1.2.1.17.7.1.4.3.1.2.598 x 000000F000000000 1.3.6.1.2.1.17.7.1.4.3.1.4.598 x 0000010000000000 IF-MIB::ifAlias.24 s kv.22,A.N.Derevjankin
1.3.6.1.2.1.17.7.1.4.3.1.5.598 i 4 1.3.6.1.4.1.171.12.42.4.2.1.2.598 i 1 1.3.6.1.4.1.171.12.1.2.18.4.0 i 2



Error in packet.
Reason: inconsistentValue (The set value is illegal or unsupported in some way)
Failed object: SNMPv2-SMI::mib-2.17.7.1.4.3.1.5.1235 






 /usr/bin/snmpset -c private -v 2c 192.168.124.238 1.3.6.1.2.1.17.7.1.4.3.1.1.1235 s MATIR-vl1235 1.3.6.1.2.1.17.7.1.4.3.1.2.1235 x 000000F000000000 1.3.6.1.2.1.17.7.1.4.3.1.4.1235 x 0000010000000000 IF-MIB::ifAlias.24 s kv.77,L.V.Fedjanina 1.3.6.1.2.1.17.7.1.4.3.1.5.1235 i 4 1.3.6.1.4.1.171.12.42.4.2.1.2.1235 i 1 1.3.6.1.4.1.171.12.1.2.18.4.0 i 2 
/usr/bin/snmpset -c private -v 2c 192.168.124.238 1.3.6.1.2.1.17.7.1.4.3.1.1.1236 s MATIR-vl1236 1.3.6.1.2.1.17.7.1.4.3.1.2.1236 x 000000F000000000 1.3.6.1.2.1.17.7.1.4.3.1.4.1236 x 4000000000000000 IF-MIB::ifAlias.2 s kv.62,E.S.SHilova 1.3.6.1.2.1.17.7.1.4.3.1.5.1236 i 4 1.3.6.1.4.1.171.12.42.4.2.1.2.1236 i 1 1.3.6.1.4.1.171.12.1.2.18.4.0 i 2




















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








































telnet 192.168.121.31
conf t
interface Gi0/0/2.1950100
 description kv.41,N.G.Konopkina
 encapsulation dot1Q 1950 second-dot1q 100
 ip unnumbered Loopback2
 ip accesss-group BLOCK in
 service-policy type control ISG-CUSTOMERS-POLICY
  ip subscriber l2-connected
  initiator dhcp class-aware
end
exit

Для включенных
ip unnumbered Loopback1
ip accesss-group PRIVATE in


Для белых адресов
 ip unnumbered Loopback3
 ip accesss-group PUBLIC in

/usr/bin/snmpset -c private -v 2c 192.168.120.45
1.3.6.1.2.1.17.7.1.4.3.1.1.100 s kv.41,N.G.Konopkina
1.3.6.1.2.1.17.7.1.4.3.1.2.100 x 000000F000000000
1.3.6.1.2.1.17.7.1.4.3.1.5.100 i 4 1.3.6.1.4.1.171.12.1.2.6.0 i 2

/usr/bin/snmpset -c private -v 2c 192.168.120.46
1.3.6.1.2.1.17.7.1.4.3.1.1.100 s kv.41,N.G.Konopkina
1.3.6.1.2.1.17.7.1.4.3.1.2.100 x 000000F000000000
1.3.6.1.2.1.17.7.1.4.3.1.4.100 x 8000000000000000 IF-MIB::ifAlias.1 s
kv.41,N.G.Konopkina 1.3.6.1.2.1.17.7.1.4.3.1.5.100 i 4
1.3.6.1.4.1.171.12.1.2.6.0 i 2

telnet 192.168.120.46
config dhcp_local_relay vlan vlanid 100 state enable
save
logout

/usr/bin/snmpset -c private -v 2c 192.168.120.47
1.3.6.1.2.1.17.7.1.4.3.1.1.100 s kv.41,N.G.Konopkina
1.3.6.1.2.1.17.7.1.4.3.1.2.100 x 000000F000000000
1.3.6.1.2.1.17.7.1.4.3.1.5.100 i 4 1.3.6.1.4.1.171.12.1.2.6.0 i 2

/usr/bin/snmpset -c private -v 2c 192.168.120.48
1.3.6.1.2.1.17.7.1.4.3.1.1.100 s kv.41,N.G.Konopkina
1.3.6.1.2.1.17.7.1.4.3.1.2.100 x 000000F000000000
1.3.6.1.2.1.17.7.1.4.3.1.5.100 i 4 1.3.6.1.4.1.171.12.1.2.6.0 i 2

telnet 192.168.120.32
create vlan_translation ports 5 cvid 100 add 1950
create vlan_translation ports 6 cvid 100 add 1950
save
logout


/usr/bin/snmpset -c private -v 2c 192.168.120.32
1.3.6.1.2.1.17.7.1.4.3.1.1.100 s kv.41,N.G.Konopkina
1.3.6.1.2.1.17.7.1.4.3.1.2.100 x 0C00000000000000
1.3.6.1.2.1.17.7.1.4.3.1.5.100 i 4 1.3.6.1.4.1.171.12.1.2.18.4.0 i 2

INSERT INTO radcheck (USERNAME,ATTRIBUTE,OP,VALUE) VALUES
('000400640001:0006f07d682c9300','Cleartext-Password',':=','ISG');
INSERT INTO radreply (USERNAME,ATTRIBUTE,OP,VALUE) VALUES
('000400640001:0006f07d682c9300','Cisco-AVPair','=','subscriber:accounting-list=ISG-AUTH-1');
INSERT INTO radreply (USERNAME,ATTRIBUTE,OP,VALUE) VALUES
('000400640001:0006f07d682c9300','Cisco-Account-Info','+=','A10240');
INSERT INTO radreply (USERNAME,ATTRIBUTE,OP,VALUE) VALUES
('000400640001:0006f07d682c9300','Service-Type','=','Framed-User');
INSERT INTO radusergroup (USERNAME,GROUPNAME) VALUES
('000400640001:0006f07d682c9300','phys2');
COMMIT;





































VID             : 1          VLAN Name     : default
VLAN Type       : Static     Advertisement : Enabled
Member Ports    :                    
Static Ports    :                    
Current Tagged Ports  :                    
Current Untagged Ports:                    
Static Tagged Ports   :                    
Static Untagged Ports :                    
Forbidden Ports       :                    

VID             : 26         VLAN Name     : mngt
VLAN Type       : Static     Advertisement : Disabled
Member Ports    : 1:1-1:16,1:20-1:22,2:1-2:16,2:23
Static Ports    : 1:1-1:16,1:20-1:22,2:1-2:16,2:23
Current Tagged Ports  : 1:1-1:16,1:20-1:22,2:1-2:16
Current Untagged Ports: 2:23               
Static Tagged Ports   : 1:1-1:16,1:20-1:22,2:1-2:16
Static Untagged Ports : 2:23               
Forbidden Ports       :                    
                                                                               

VID             : 52         VLAN Name     : testSyrsky
VLAN Type       : Static     Advertisement : Disabled
Member Ports    : 1:11,2:11          
Static Ports    : 1:11,2:11          
Current Tagged Ports  : 1:11,2:11          
Current Untagged Ports:                    
Static Tagged Ports   : 1:11,2:11          
Static Untagged Ports :                    
Forbidden Ports       :                    

VID             : 1953       VLAN Name     : TRSirsky
VLAN Type       : Static     Advertisement : Disabled
Member Ports    : 1:1-1:16,1:20-1:22,2:1-2:16
Static Ports    : 1:1-1:16,1:20-1:22,2:1-2:16
Current Tagged Ports  : 1:20,1:22          
Current Untagged Ports: 1:1-1:16,1:21,2:1-2:16
Static Tagged Ports   : 1:20,1:22          
Static Untagged Ports : 1:1-1:16,1:21,2:1-2:16
Forbidden Ports     






tagged (суммируется с untagged)
snmpwalk -v 2c -c private 192.168.120.104 1.3.6.1.2.1.17.7.1.4.3.1.2
SNMPv2-SMI::mib-2.17.7.1.4.3.1.2.1 = Hex-STRING:
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
SNMPv2-SMI::mib-2.17.7.1.4.3.1.2.26 = Hex-STRING:
FF FF 1C 00 00 00 00 00 FF FF 02 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
SNMPv2-SMI::mib-2.17.7.1.4.3.1.2.52 = Hex-STRING:
00 20 00 00 00 00 00 00 00 20 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
SNMPv2-SMI::mib-2.17.7.1.4.3.1.2.1953 = Hex-STRING:
FF FF 1C 00 00 00 00 00 FF FF 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00







untagged

garry@garry:/var/home/garry> snmpwalk -v 2c -c private 192.168.120.104
1.3.6.1.2.1.17.7.1.4.3.1.4
SNMPv2-SMI::mib-2.17.7.1.4.3.1.4.1 = Hex-STRING:
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
SNMPv2-SMI::mib-2.17.7.1.4.3.1.4.26 = Hex-STRING: 00 00 00 00 00 00 00
00 00 00 02 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
SNMPv2-SMI::mib-2.17.7.1.4.3.1.4.52 = Hex-STRING: 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
SNMPv2-SMI::mib-2.17.7.1.4.3.1.4.1953 = Hex-STRING: FF FF 08 00 00 00 00
00 FF FF 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00



Boot PROM Version          : Build 4.00.002
Firmware Version           : Build 4.00.024
Hardware Version           : C1






