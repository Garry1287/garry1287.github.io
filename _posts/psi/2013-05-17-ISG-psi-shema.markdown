---
layout: post
title:  "ISG-psi-shema"
date:   2013-05-17 15:24:14 +0400
categories: PSI
tags: PSI
---

# ISG-psi-shema
{% raw %}

34-08-04-37-E7-10

000634080437e710

INSERT INTO radcheck (USERNAME,ATTRIBUTE,OP,VALUE) VALUES ('000400340001:000634080437e710','Cleartext-Password',':=','ISG');
INSERT INTO radreply (USERNAME,ATTRIBUTE,OP,VALUE) VALUES ('000400340001:000634080437e710','Cisco-AVPair','=','subscriber:accounting-list=ISG-AUTH-1');
INSERT INTO radreply (USERNAME,ATTRIBUTE,OP,VALUE) VALUES ('000400340001:000634080437e710','Cisco-Account-Info','+=','A30720');
INSERT INTO radreply (USERNAME,ATTRIBUTE,OP,VALUE) VALUES ('000400340001:000634080437e710','Service-Type','=','Framed-User');
INSERT INTO radreply (USERNAME,ATTRIBUTE,OP,VALUE) VALUES ('000400340001:000634080437e710','Cisco-AVPair','=','lcp:interface-config=description TEST-iptv');
INSERT INTO radusergroup (USERNAME,GROUPNAME) VALUES ('000400340001:000634080437e710','phys2');






VID             : 2222       VLAN Name     : RB-TEST
VLAN Type       : Static     Advertisement : Disabled
Member Ports    : 21-24               
Static Ports    : 21-24               
Current Tagged Ports  : 21-24               
Current Untagged Ports:                     
Static Tagged Ports   : 21-24               
Static Untagged Ports :                     
Forbidden Ports       : 



VID             : 29         VLAN Name     : tv-kisa
VLAN Type       : Static     Advertisement : Disabled
Member Ports    : 3,23-24             
Static Ports    : 3,23-24             
Current Tagged Ports  : 3,23-24             
Current Untagged Ports:                     
Static Tagged Ports   : 3,23-24             
Static Untagged Ports :                     
Forbidden Ports       : 

VID             : 13         VLAN Name     : new-backbone
VLAN Type       : Static     Advertisement : Disabled
Member Ports    : 21-24               
Static Ports    : 21-24               
Current Tagged Ports  : 21-24               
Current Untagged Ports:                     
Static Tagged Ports   : 21-24               
Static Untagged Ports :                     
Forbidden Ports       :     

VID             : 11         VLAN Name     : LAN
VLAN Type       : Static     Advertisement : Disabled
Member Ports    : 23-24               
Static Ports    : 23-24               
Current Tagged Ports  : 23-24               
Current Untagged Ports:                     
Static Tagged Ports   : 23-24               
Static Untagged Ports :                     
Forbidden Ports       :                        

















config ports 1  speed auto flow_control disable state enable  description "Arbuzov A.S.kv 74"
 config ports 1  learning enable
 config ports 1  mdix auto
 config ports 2  speed auto flow_control disable state enable  description "Litti D.M. kv 19"
 config ports 2  learning enable
 config ports 2  mdix auto
 config ports 3  speed auto flow_control disable state enable  description "Vasilev A.V. kv 5"
 config ports 3  learning enable
 config ports 3  mdix auto
 config ports 4  speed auto flow_control disable state enable  description "Dvorjankin kv 86"
 config ports 4  learning enable
 config ports 4  mdix auto
 config ports 5  speed auto flow_control enable state enable  description "Rak R. kv 28"
 config ports 5  learning enable
 config ports 5  mdix auto
 config ports 6  speed auto flow_control disable state enable  description "Pashkovskyi kv 114"
 config ports 6  learning enable
 config ports 6  mdix auto
 config ports 7  speed auto flow_control disable state enable  description "Sonina kv 56"
 config ports 7  learning enable
 config ports 7  mdix auto
 config ports 8  speed auto flow_control disable state enable  description "Abramova kv 95"
 config ports 8  learning enable
 config ports 8  mdix auto
 config ports 9  speed auto flow_control disable state enable  description "Gutchenko.kv.7"
 config ports 9  learning enable
 config ports 9  mdix auto
 config ports 10  speed auto flow_control disable state enable  description "kv.36"
 config ports 10  learning enable
 config ports 10  mdix auto
 config ports 11  speed auto flow_control disable state enable  description "kv.39"
 config ports 11  learning enable
 config ports 11  mdix auto
 config ports 12  speed auto flow_control disable state enable  description "zanyatkemto"
 config ports 12  learning enable
 config ports 12  mdix auto
 config ports 13  speed auto flow_control disable state enable  description "kv.41"
 config ports 13  learning enable
 config ports 13  mdix auto
 config ports 14  speed auto flow_control disable state enable  description "kv.33"
 config ports 14  learning enable
 config ports 14  mdix auto
 config ports 15  speed auto flow_control disable state enable  description "kv.6"
 config ports 15  learning enable
 config ports 15  mdix auto
 config ports 1  speed auto flow_control disable state disable  clear_description
 config ports 1  learning enable
 config ports 1  mdix auto
 config ports 2  speed auto flow_control disable state disable  clear_description
config ports 2  learning enable
 config ports 2  mdix auto
 config ports 18  speed auto flow_control disable state disable  clear_description
 config ports 18  learning enable
 config ports 18  mdix auto
 config ports 19  speed auto flow_control disable state disable  clear_description
 config ports 19  learning enable
 config ports 19  mdix auto
 config ports 20  speed auto flow_control disable state disable  clear_description
 config ports 20  learning enable
 config ports 20  mdix auto
 config ports 21  speed auto flow_control disable state disable  clear_description
 config ports 21  learning enable
 config ports 21  mdix auto
 config ports 22  speed auto flow_control disable state disable  clear_description
 config ports 22  learning enable
 config ports 22  mdix auto
 config ports 23  speed auto flow_control disable state disable  clear_description
 config ports 23  learning enable
 config ports 23  mdix auto
 config ports 24  speed auto flow_control disable state disable  clear_description
 config ports 24  learning enable
 config ports 24  mdix auto
 config ports 25 medium_type fiber speed auto flow_control disable state enable  clear_description
 config ports 25 medium_type fiber learning enable
 config ports 25  speed auto flow_control disable state enable  clear_description
 config ports 25  learning enable
 config ports 25  mdix auto
 config ports 26 medium_type fiber speed auto flow_control disable state enable  clear_description
 config ports 26 medium_type fiber learning enable
 config ports 26  speed auto flow_control disable state enable  clear_description
 config ports 26  learning enable
 config ports 26  mdix auto
 config ports 27  speed auto flow_control disable state enable  clear_description
 config ports 27  learning enable
 config ports 27  mdix auto
 config ports 28  speed auto flow_control disable state enable  clear_description
 config ports 28  learning enable
 config ports 28  mdix auto


config snmp system_name agr10-s0.sc.int
config snmp system_location agronomicheskaya10
config snmp system_contact ibd@sc.ru


create vlan mngt tag 25
config vlan mngt add tagged 25-26
create vlan agr10 tag 466
config vlan agr10 add tagged 25-26
config vlan agr10 add untagged 1-24
disable gvrp
config gvrp 1 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 2 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 3 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 4 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 5 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 6 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 7 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 8 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 9 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 10 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 11 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 12 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 13 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 14 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 15 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 1 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 2 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 18 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 19 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 20 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 21 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 22 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 23 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 24 state disable ingress_checking enable acceptable_frame admit_all pvid 466
config gvrp 25 state disable ingress_checking enable acceptable_frame admit_all pvid 1
config gvrp 26 state disable ingress_checking enable acceptable_frame admit_all pvid 1
config gvrp 27 state disable ingress_checking enable acceptable_frame admit_all pvid 1
config gvrp 28 state disable ingress_checking enable acceptable_frame admit_all pvid 1
  

enable sntp
config time_zone operator + hour 3 min 0
config sntp primary 192.18.118.1 secondary 0.0.0.0 poll-interval 720
config dst repeating s_week last s_day sun s_mth 4 s_time 2:0 e_week last e_day sun e_mth 10 e_time 3:0 offset 60

config ipif System vlan mngt ipaddress 192.18.118.59/24 state enable
enable telnet 23
enable web 80
disable autoconfig

create iproute default 192.18.118.1 1










config snmp system_name k9-s9.sc.int
config snmp system_location K9 office
config snmp system_contact ibd@sc.ru

config safeguard_engine state enable utilization rising 90 falling 50 trap_log disable mode strict

enable sntp
config time_zone operator + hour 3 min 0
config sntp primary 192.168.113.1 secondary 0.0.0.0 poll-interval 720
config dst repeating s_week last s_day sun s_mth 4 s_time 2:0 e_week last e_day sun e_mth 10 e_time 3:0 offset 60

config ipif System ipaddress 192.168.113.234/24 vlan mgnt
create iproute default 192.168.113.1 1 primary


        ОБА             
create vlan mngt tag 22
config vlan mngt add tagged 1-2, 24 advertisement disable
create vlan mngt-24 tag 24
config vlan mngt-24 add tagged 1-2,24
create vlan phys_mngt tag 25
config vlan phys_mngt add tagged 1-2,24 advertisement disable

  


ЛИПКА
create vlan MicroMax tag 23
config vlan MicroMax add tagged 1, 24 advertisement disable
create vlan mngt-sokol tag 26
config vlan mngt-sokol add tagged 1,24 advertisement disable
create vlan parus_wippl tag 113
config vlan parus_wippl add tagged 1, 24 advertisement disable
create vlan Parus_inet tag 122
config vlan Parus_inet add tagged 1, 24 advertisement disable
create vlan parus_voip tag 15
config vlan parus_voip add tagged 1, 24 advertisement disable
create vlan Lesnoy-dom-nlmk tag 214
config vlan Lesnoy-dom-nlmk add tagged 1, 24 advertisement disable
create vlan lipka tag 298
config vlan lipka add tagged 1, 24 advertisement disable
create vlan chapaeva4 tag 486                                                   
config vlan chapaeva4 add tagged 1, 24 advertisement disable                     
create vlan borodinskaya47ap3 tag 487                                           
config vlan borodinskaya47ap3 add tagged 1, 24 advertisement disable             
create vlan borodinskaya47ap2 tag 488                                           
config vlan borodinskaya47ap2 add tagged 1, 24 advertisement disable             
create vlan borodinskaya47p10 tag 489                                           
config vlan borodinskaya47p10 add tagged 1, 24 advertisement disable             
create vlan borodinskaya45 tag 490                                              
config vlan borodinskaya45 add tagged 1, 24 advertisement disable                
create vlan borodinskaya49 tag 491                                              
config vlan borodinskaya49 add tagged 1, 24 advertisement disable                
create vlan borodinskaya47p3 tag 492                                            
config vlan borodinskaya47p3 add tagged 1, 24 advertisement disable              
create vlan borodinskaya47p5 tag 493                                            
config vlan borodinskaya47p5 add tagged 1, 24 advertisement disable              
create vlan borodinskaya47p8 tag 494                                            
config vlan borodinskaya47p8 add tagged 1, 24 advertisement disable              
create vlan borodinskaya47p1 tag 495                                            
config vlan borodinskaya47p1 add tagged 1, 24 advertisement disable              
create vlan borodinskaya51p3 tag 496                                            
config vlan borodinskaya51p3 add tagged 1, 24-21 advertisement disable           
create vlan borodinskaya51p2 tag 497                                            
config vlan borodinskaya51p2 add tagged 1, 24 advertisement disable
create vlan BOST-MPLS tag 861                                                   
config vlan BOST-MPLS add tagged 1, 24 advertisement disable                     
create vlan BOST-INET tag 862                                                   
config vlan BOST-INET add tagged 1, 24 advertisement disable                     
create vlan TEMP-BOST-LG-MGMT tag 899                                           
config vlan TEMP-BOST-LG-MGMT add tagged 1, 24 advertisement disable                         
create vlan Lipka_new tag 1023                                                  
config vlan Lipka_new add tagged 1, 24 advertisement disable                     
create vlan studen20_p7 tag 1406                                                
config vlan studen20_p7 add tagged 1, 24 advertisement disable                   
create vlan studen20_p2 tag 1407                                                
config vlan studen20_p2 add tagged 1, 24 advertisement disable                   
create vlan studen18 tag 1408                                                   
config vlan studen18 add tagged 1, 24 advertisement disable                      
create vlan chap4 tag 1409                                                      
config vlan chap4 add tagged 1, 24 advertisement disable                         
create vlan chapaeva2 tag 1410                                                  
config vlan chapaeva2 add tagged 1, 24 advertisement disable                     
create vlan borodinskaya47p8_2 tag 1411                                         
config vlan borodinskaya47p8_2 add tagged 1, 24 advertisement disable            
create vlan borodinskaya47p5_2 tag 1413                                         
config vlan borodinskaya47p5_2 add tagged 1, 24 advertisement disable            
create vlan borodinskaya45_2 tag 1414                                           
config vlan borodinskaya45_2 add tagged 1, 24 advertisement disable            
create vlan borodinskaya47ap2_2 tag 1420                                        
config vlan borodinskaya47ap2_2 add tagged 1, 24 advertisement disable           
create vlan TRSokol tag 1950                                         
config vlan TRSokol add tagged 1, 24 advertisement disable             
create vlan lipka-wippl tag 2001                                                
config vlan lipka-wippl add tagged 1, 24-23 advertisement disable                
create vlan GK-Metallurg-VPN tag 2003                                           
config vlan GK-Metallurg-VPN add tagged 1, 24-23 advertisement disable
create vlan Metallurg-VPN tag 3057                                              
config vlan Metallurg-VPN add tagged 1, 24-24 advertisement disable             
create vlan uprav_comp_borod tag 3060                                           
config vlan uprav_comp_borod add tagged 1, 24 advertisement disable              
create vlan GZK-Sokol-Voip tag 3061                                             
config vlan GZK-Sokol-Voip add tagged 1, 24 advertisement disable
create vlan Anisimov tag 3071                                                   
config vlan Anisimov add tagged 1, 24-21 advertisement disable
create vlan Krasilnikova tag 3051                                               
config vlan Krasilnikova add tagged 1, 24 advertisement disable               
create vlan gk-metallurg tag 3054                                               
config vlan gk-metallurg add tagged 1, 24 advertisement disable  
create vlan Rivera-Lipka tag 3035                                               
config vlan Rivera-Lipka add tagged 1, 24 advertisement disable 
create vlan electroapparat tag 3019                                             
config vlan electroapparat add tagged 1, 24 advertisement disable 
create vlan rivera2 tag 3055                                                    
config vlan rivera2 add tagged 1, 24 advertisement disable


                                                  

                                  


Кузнечная

create vlan Dom-Inozemzev tag 206
config vlan Dom-Inozemzev add tagged 2, 24 advertisement disable
create vlan 1RB-equvant tag 260
config vlan 1RB-equvant add tagged 2, 24 advertisement disable
create vlan Kuz10-INET tag 422                                                  
config vlan Kuz10-INET add tagged 2, 24 advertisement disable
create vlan Kuz10-Eurokomerts tag 3076                                          
config vlan Kuz10-Eurokomerts add tagged 2, 24 advertisement disable
create vlan Kompaniya_BKS tag 3080                                              
config vlan Kompaniya_BKS add tagged 2, 24 advertisement disable
create vlan Vtb24-client tag 691                                                
config vlan Vtb24-client add tagged 2, 24 advertisement disable
create vlan Kuz10_3 tag 1418                                                    
config vlan Kuz10_3 add tagged 2, 24 advertisement disable
create vlan evrazia-ipvpn tag 2008                                              
config vlan evrazia-ipvpn add tagged 2, 24 advertisement disable
create vlan vpn-rtcomm-bks tag 2501                                             
config vlan vpn-rtcomm-bks add tagged 2, 24 advertisement disable
create vlan H-Lipetsk-Inet tag 3009                                             
config vlan H-Lipetsk-Inet add tagged 2, 24 advertisement disable
create vlan IP_Chernisheva tag 3011                                             
config vlan IP_Chernisheva add tagged 2, 24 advertisement disable
create vlan TSUM tag 3028                                                       
config vlan TSUM add tagged 2, 24 advertisement disable                
create vlan VSK-RTcomm tag 3030                                                 
config vlan VSK-RTcomm add tagged 2, 24 advertisement disable
create vlan singenta tag 3034                                                   
config vlan singenta add tagged 2, 24 advertisement disable
create vlan Chuchilkin-KUZ10 tag 3041                                           
config vlan Chuchilkin-KUZ10 add tagged 2, 24 advertisement disable            
                
                   
1. Какой формат опции 82 понимает redback
Мы работаем с форматом dlink и cicso роутер настраивали под него
 Не совсем понятно

        Agent-Remote-Id = "\000\006\000\"\260\004\014\036"
        ADSL-Agent-Remote-Id = "\000\006\000\"\260\004\014\036"
        Agent-Circuit-Id = "\000\004\000\017\000\002"
        ADSL-Agent-Circuit-Id = "\000\004\000\017\000\002"
        DHCP-Option = "==\007\001\000\035`\327hy"


2
NAS-Port-Id = "2/1 vlan-id 2222:15 clips 131177"


          
radtest 000400640001:0006f07d682c9300 ISG localhost 1812 testing123
Sending Access-Request of id 127 to 127.0.0.1 port 1812
        User-Name = "000400330001:00061cbdb965fb60"
        User-Password = "ISG"
        NAS-IP-Address = 81.20.192.30
        NAS-Port = 1812
rad_recv: Access-Accept packet from host 127.0.0.1 port 1812, id=127, length=85
        Cisco-AVPair = "subscriber:accounting-list=ISG-AUTH-1"
        Cisco-Account-Info = "A30720"
        Service-Type = Framed-User

radtest 00:1d:60:d7:68:79 Redback localhost 1812 testing123

00-22-B0-04-0C-1E
\000\006\000\"\260\004\014\036

000400170002:000600 
rad_recv: Access-Request packet from host 81.20.192.54 port 1812, id=55, length=303
        User-Name = "00:1d:60:d7:68:79"
        User-Password = "Redback"
        Service-Type = Outbound-User
        NAS-Identifier = "Redback"
        NAS-Port = 33619968
        NAS-Real-Port = 562749455
        NAS-Port-Type = Virtual
        NAS-Port-Id = "2/1 vlan-id 2222:15 clips 131177"
        Medium-Type = DSL
        Mac-Addr = "00-1d-60-d7-68-79"
        Platform-Type = SE-100
        OS-Version = "6.1.3.3"
        Agent-Remote-Id = "\000\006\000\"\260\004\014\036"
        ADSL-Agent-Remote-Id = "\000\006\000\"\260\004\014\036"
        Agent-Circuit-Id = "\000\004\000\017\000\002"
        ADSL-Agent-Circuit-Id = "\000\004\000\017\000\002"
        DHCP-Option = "==\007\001\000\035`\327hy"
        DHCP-Option = "\014\014\004Se06"
        DHCP-Vendor-Class-ID = "MSFT 5.0"
# Executing section authorize from file /etc/raddb/sites-enabled/default
+- entering group authorize {...}
++[preprocess] returns ok
++[chap] returns noop
++[mschap] returns noop
++[digest] returns noop
[suffix] No '@' in User-Name = "00:1d:60:d7:68:79", looking up realm NULL
[suffix] No such realm "NULL"
++[suffix] returns noop
[files] users: Matched entry 00:1d:60:d7:68:79 at line 217
++[files] returns ok
++[expiration] returns noop
++[logintime] returns noop
++[pap] returns updated
Found Auth-Type = PAP
# Executing group from file /etc/raddb/sites-enabled/default
+- entering group PAP {...}
[pap] login attempt with password "Redback"
[pap] Using clear text password "Redback"
[pap] User authenticated successfully
++[pap] returns ok
Login OK: [00:1d:60:d7:68:79/Redback] (from client 81.20.192.54 port 33619968)
# Executing section post-auth from file /etc/raddb/sites-enabled/default
+- entering group post-auth {...}
++[exec] returns noop
Sending Access-Accept of id 55 to 81.20.192.54 port 1812
        IP-Interface-Name = "dhcp"
        Context-Name = "internet"
        DHCP-Max-Leases = 60
        Service-Name = "service-1"
        Service-Parameter = "Rate=1024 Burst=192000 Rate-local=100000 Burst-local=18750000 filter=filter-clear"
Finished request 12.
Going to the next request
Waking up in 4.9 seconds.
rad_recv: Access-Request packet from host 81.20.192.54 port 1812, id=56, length=303
        User-Name = "00:1d:60:d7:68:79"
        User-Password = "Redback"
        Service-Type = Outbound-User
        NAS-Identifier = "Redback"
        NAS-Port = 33619968
        NAS-Real-Port = 562749455
        NAS-Port-Type = Virtual
        NAS-Port-Id = "2/1 vlan-id 2222:15 clips 131178"
        Medium-Type = DSL
        Mac-Addr = "00-1d-60-d7-68-79"
        Platform-Type = SE-100
        OS-Version = "6.1.3.3"
        Agent-Remote-Id = "\000\006\000\"\260\004\014\036"
        ADSL-Agent-Remote-Id = "\000\006\000\"\260\004\014\036"
        Agent-Circuit-Id = "\000\004\000\017\000\002"
        ADSL-Agent-Circuit-Id = "\000\004\000\017\000\002"
        DHCP-Option = "==\007\001\000\035`\327hy"
        DHCP-Option = "\014\014\004Se06"
        DHCP-Vendor-Class-ID = "MSFT 5.0"
# Executing section authorize from file /etc/raddb/sites-enabled/default
+- entering group authorize {...}
++[preprocess] returns ok
++[chap] returns noop
++[mschap] returns noop
++[digest] returns noop
[suffix] No '@' in User-Name = "00:1d:60:d7:68:79", looking up realm NULL
[suffix] No such realm "NULL"
++[suffix] returns noop
[files] users: Matched entry 00:1d:60:d7:68:79 at line 217
++[files] returns ok
++[expiration] returns noop
++[logintime] returns noop
++[pap] returns updated
Found Auth-Type = PAP
# Executing group from file /etc/raddb/sites-enabled/default
+- entering group PAP {...}
[pap] login attempt with password "Redback"
[pap] Using clear text password "Redback"
[pap] User authenticated successfully
++[pap] returns ok
Login OK: [00:1d:60:d7:68:79/Redback] (from client 81.20.192.54 port 33619968)
# Executing section post-auth from file /etc/raddb/sites-enabled/default
+- entering group post-auth {...}
++[exec] returns noop
Sending Access-Accept of id 56 to 81.20.192.54 port 1812
        IP-Interface-Name = "dhcp"
        Context-Name = "internet"
        DHCP-Max-Leases = 60
        Service-Name = "service-1"
        Service-Parameter = "Rate=1024 Burst=192000 Rate-local=100000 Burst-local=18750000 filter=filter-clear"
Finished request 13.
Going to the next request
Waking up in 1.8 seconds.
Cleaning up request 12 ID 55 with timestamp +73301
Waking up in 3.1 seconds.
Cleaning up request 13 ID 56 with timestamp +73304
Ready to process requests.
rad_recv: Access-Request packet from host 81.20.192.54 port 1812, id=57, length=303
        User-Name = "00:1d:60:d7:68:79"
        User-Password = "Redback"
        Service-Type = Outbound-User
        NAS-Identifier = "Redback"
        NAS-Port = 33619968
        NAS-Real-Port = 562749455
        NAS-Port-Type = Virtual
        NAS-Port-Id = "2/1 vlan-id 2222:15 clips 131179"
        Medium-Type = DSL
        Mac-Addr = "00-1d-60-d7-68-79"
        Platform-Type = SE-100
        OS-Version = "6.1.3.3"
        Agent-Remote-Id = "\000\006\000\"\260\004\014\036"
        ADSL-Agent-Remote-Id = "\000\006\000\"\260\004\014\036"
        Agent-Circuit-Id = "\000\004\000\017\000\002"
        ADSL-Agent-Circuit-Id = "\000\004\000\017\000\002"
        DHCP-Option = "==\007\001\000\035`\327hy"
        DHCP-Option = "\014\014\004Se06"
        DHCP-Vendor-Class-ID = "MSFT 5.0"
# Executing section authorize from file /etc/raddb/sites-enabled/default
+- entering group authorize {...}
++[preprocess] returns ok
++[chap] returns noop
++[mschap] returns noop
++[digest] returns noop
[suffix] No '@' in User-Name = "00:1d:60:d7:68:79", looking up realm NULL
[suffix] No such realm "NULL"
++[suffix] returns noop
[files] users: Matched entry 00:1d:60:d7:68:79 at line 217
++[files] returns ok
++[expiration] returns noop
++[logintime] returns noop
++[pap] returns updated
Found Auth-Type = PAP
# Executing group from file /etc/raddb/sites-enabled/default
+- entering group PAP {...}
[pap] login attempt with password "Redback"
[pap] Using clear text password "Redback"
[pap] User authenticated successfully
++[pap] returns ok
Login OK: [00:1d:60:d7:68:79/Redback] (from client 81.20.192.54 port 33619968)
# Executing section post-auth from file /etc/raddb/sites-enabled/default
+- entering group post-auth {...}
++[exec] returns noop
Sending Access-Accept of id 57 to 81.20.192.54 port 1812
        IP-Interface-Name = "dhcp"
        Context-Name = "internet"
        DHCP-Max-Leases = 60
        Service-Name = "service-1"
        Service-Parameter = "Rate=1024 Burst=192000 Rate-local=100000 Burst-local=18750000 filter=filter-clear"
Finished request 14.
Going to the next request
Waking up in 4.9 seconds.
Cleaning up request 14 ID 57 with timestamp +73312
Ready to process requests.


Boot PROM Version : Build 5.00.009
Firmware Version  : Build 6.00.B56
Hardware Version  : A4


sh dhcp_local_relay
DHCP/BOOTP Local Relay Status    : Enabled
DHCP/BOOTP Local Relay VLAN List : 50-51


# DHCP_RELAY

disable dhcp_relay
config dhcp_relay hops 4 time 0
config dhcp_relay option_82 state disable
config dhcp_relay option_82 check disable
config dhcp_relay option_82 policy replace
config dhcp_relay option_82 remote_id default
config dhcp_relay option_60 state disable
config dhcp_relay option_60 default mode drop
config dhcp_relay option_61 state disable
config dhcp_relay option_61 default drop

# DHCP_LOCAL_RELAY

config dhcp_local_relay vlan vlanid 50-51 state enable
config dhcp_local_relay option_82 ports 1-26 policy keep 







































[local]Redback#Aug 22 11:46:14: [2/1:1023:63/7/2/117]: %AAA-7-AUTHEN: Received AUTHEN_REQUEST msg from CLIPSd for username 00:1d:60:d7:68:79 with external handle = 131189
Aug 22 11:46:14: [2/1:1023:63/7/2/117]: %AAA-7-GEN: aaa_sess_wrap_lookup_with_ccthandle: AAA cct node lookup fail: cct 2/1:1023:63/7/2/117 (0x100ffff78000075)
Aug 22 11:46:14: %AAA-7-GEN: aaa_idx 50000076: aaa_sess_wrap_lookup_with_index: AAA idx node lookup fail: idx 0x50000076
Aug 22 11:46:14: [0000]: [2/1:1023:63/7/2/117]: %AAA-7-AUTHEN: aaa_idx 50000076: aaa_create_session_with_cct_handle: creating session for cct 2/1:1023:63/7/2/117 index 1342177398
Aug 22 11:46:14: [2/1:1023:63/7/2/117]: %AAA-7-AUTHEN: Assigned aaa_idx 1342177398 to username 00:1d:60:d7:68:79
Aug 22 11:46:14: %AAA-7-GEN: aaa_convert_context_name_to_id: Context ID 0x40080002
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-AUTHEN: aaa_idx 50000076: Binding subscriber 00:1d:60:d7:68:79 to context internet via bind context (aaa_idx = 1342177398).
Aug 22 11:46:14: %AAA-7-ANCP: [aaa_DslAddOrFindSessionCircuit] searching in CCT tree for cct "Cct invalid" madeNew 1
Aug 22 11:46:14: %AAA-7-ANCP: [aaa_dslAddToOpaqueTree] putting ACI  in opaque tree
Aug 22 11:46:14: %AAA-7-ANCP:  addorfindcircuit add new count of flexible tree 0, count of opaque tree 1
Aug 22 11:46:14: %AAA-7-ANCP: aaa_DSL_add_session chaining under DSL_LINE  aciLen 7
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-AUTHEN: aaa_idx 50000076: Received session slot mask 0x0 
Aug 22 11:46:14: %AAA-7-GEN: aaa_idx 50000076: Processing AUTHEN_REQUEST msg.
Aug 22 11:46:14: [0002]: %AAA-7-GEN: AAA sub name node lookup fail: cntxt 0x40080002 subscriber 00:1d:60:d7:68:79
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-AUTHEN: aaa_idx 50000076: Adding aaa_idx 1342177398 to context internet
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-AUTHEN: aaa_idx 50000076: Sending Authentication request to global
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-AUTHEN: aaa_idx 50000076: aaa_send_db_req: Created tlv list (more_data) for session 00:1d:60:d7:68:79
Aug 22 11:46:14: %AAA-7-GEN: aaa_idx 50000076: Sending DB_REQUEST to global.
Aug 22 11:46:14: %AAA-7-RADIUS: rad_mgr, Process radius requests in db request queue
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-RADIUS: aaa_idx 50000076: rad_process_aaad_req: Receive request (Authentication)
Aug 22 11:46:14: [0001]: [2/1:1023:63/7/2/117]: %AAA-7-RAD_ATTR: aaa_idx 50000076: rad_add_attr_to_tlv_list, Add attr NAS_Port_ID (2/1 vlan-id 2222:15 clips 131189) with len 33 to tlv list
Aug 22 11:46:14: [0001]: [2/1:1023:63/7/2/117]: %AAA-7-RADIUS: aaa_idx 50000076: aaaidx_tree_insert: insert aaa_idx to idx tree for global db_request_type Authentication. (00:1d:60:d7:68:79) 
Aug 22 11:46:14: %AAA-7-RADIUS: rad_send, Process radius requests in authen low priority queue
Aug 22 11:46:14: [0001]: [2/1:1023:63/7/2/117]: %AAA-7-RADIUS: aaa_idx 50000076: do_auth_send: Find free authen server 81.20.192.55 (ctx local, src port 1812, dst port 1812). (00:1d:60:d7:68:79)
Aug 22 11:46:14: [0001]: [2/1:1023:63/7/2/117]: %AAA-7-RAD_PKT: aaa_idx 50000076: Send packet (303 bytes) to 81.20.192.55/1812 (00:1d:60:d7:68:79):

   0    01 43 01 2f ba 61 d8 9e 3f 8a 6f f7 16 6a d1 bb
  16    98 ee ec a2 01 13 30 30 3a 31 64 3a 36 30 3a 64
  32    37 3a 36 38 3a 37 39 02 12 bf df c0 d0 ae cd 65
  48    e5 fd 97 31 a9 e5 ab 1d 3e 06 06 00 00 00 05 20
  64    09 52 65 64 62 61 63 6b 05 06 02 01 00 00 1a 0c
  80    00 00 09 30 3e 06 21 8a e0 0f 3d 06 00 00 00 05
  96    57 22 32 2f 31 20 76 6c 61 6e 2d 69 64 20 32 32
 112    32 32 3a 31 35 20 63 6c 69 70 73 20 31 33 31 31
 128    38 39 1a 0c 00 00 09 30 26 06 00 00 00 0b 1a 19
 144    00 00 09 30 91 13 30 30 2d 31 64 2d 36 30 2d 64
 160    37 2d 36 38 2d 37 39 1a 0c 00 00 09 30 62 06 00
 176    00 00 04 1a 0f 00 00 09 30 70 09 36 2e 31 2e 33
 192    2e 33 1a 10 00 00 09 30 60 0a 00 06 00 22 b0 04
 208    0c 1e 1a 10 00 00 0d e9 02 0a 00 06 00 22 b0 04
 224    0c 1e 1a 0e 00 00 09 30 61 08 00 04 00 0f 00 02
 240    1a 0e 00 00 0d e9 01 08 00 04 00 0f 00 02 1a 12
 256    00 00 09 30 ca 0c 3d 3d 07 01 00 1d 60 d7 68 79
 272    1a 0f 00 00 09 30 ca 09 0c 0c 04 53 65 30 36 1a
 288    10 00 00 09 30 7d 0a 4d 53 46 54 20 35 2e 30

Aug 22 11:46:14: [0001]: %AAA-7-RADIUS: Using local address 81.20.192.54
Aug 22 11:46:14: [0001]: %AAA-7-RADIUS: do_send: 303 bytes send to radius server  81.20.192.55 (1812).
Aug 22 11:46:14: %AAA-7-RADIUS: rad_process_send_queue, 1 requests processed (0 retransmit) 
Aug 22 11:46:14: %AAA-7-RADIUS: rad_process_received_pkt: Receive 166 bytes from radius server 81.20.192.55 (1812)
Aug 22 11:46:14: [0001]: %AAA-7-RADIUS: rad_find_match_srv: Find matching server 81.20.192.55/1812
Aug 22 11:46:14: %AAA-7-RADIUS: rad_response_sanity_check: Message-Authenticator is not present
Aug 22 11:46:14: [0001]: [2/1:1023:63/7/2/117]: %AAA-7-RAD_PKT: aaa_idx 50000076: Received packet (166 bytes) from 81.20.192.55/1812 (00:1d:60:d7:68:79):

   0    02 43 00 a6 f1 23 1b f4 a0 c1 26 5d 8f 28 16 6c
  16    19 e1 e9 f1 1a 0c 00 00 09 30 68 06 64 68 63 70
  32    1a 10 00 00 09 30 04 0a 69 6e 74 65 72 6e 65 74
  48    1a 0c 00 00 09 30 03 06 00 00 00 3c 1a 11 00 00
  64    09 30 be 0b 73 65 72 76 69 63 65 2d 31 1a 59 00
  80    00 09 30 c0 53 52 61 74 65 3d 31 30 32 34 20 42
  96    75 72 73 74 3d 31 39 32 30 30 30 20 52 61 74 65
 112    2d 6c 6f 63 61 6c 3d 31 30 30 30 30 30 20 42 75
 128    72 73 74 2d 6c 6f 63 61 6c 3d 31 38 37 35 30 30
 144    30 30 20 66 69 6c 74 65 72 3d 66 69 6c 74 65 72
 160    2d 63 6c 65 61 72

Aug 22 11:46:14: %AAA-7-RADIUS: rad_mgr, Process radius requests in db response queue
Aug 22 11:46:14: %AAA-7-RAD_ATTR: Receive Redback attr 104 (IP_Interface), tag = 32, status = success
Aug 22 11:46:14: %AAA-7-RAD_ATTR: Receive Redback attr 4 (Context_Name), tag = 32, status = success
Aug 22 11:46:14: %AAA-7-RAD_ATTR: Receive Redback attr 3 (DHCP_Max_Leases), tag = 32, status = success
Aug 22 11:46:14: %AAA-7-RAD_ATTR: rad_attr_parse_svc_attr: Service name service-1
Aug 22 11:46:14: %AAA-7-RAD_ATTR: rad_attr_add_svc_attrs_tlv: Service attribute 190 add to list with tag 32 status success ec 1
Aug 22 11:46:14: %AAA-7-RAD_ATTR: rad_attr_parse_svc_attr: Service attribute 190 with tag 32 parser status success
Aug 22 11:46:14: %AAA-7-RAD_ATTR: Receive Redback attr 190 (Service_Name), tag = 32, status = success
Aug 22 11:46:14: %AAA-7-RAD_ATTR: rad_attr_parse_svc_attr: Service parameter Rate=1024 Burst=192000 Rate-local=100000 Burst-local=18750000 filter=filter-clear
Aug 22 11:46:14: %AAA-7-RAD_ATTR: rad_attr_add_svc_attrs_tlv: Service attribute 192 add to list with tag 32 status success ec 1
Aug 22 11:46:14: %AAA-7-RAD_ATTR: rad_attr_parse_svc_attr: Service attribute 192 with tag 32 parser status success
Aug 22 11:46:14: %AAA-7-RAD_ATTR: Receive Redback attr 192 (Service_Parameter), tag = 32, status = success
Aug 22 11:46:14: [0001]: [2/1:1023:63/7/2/117]: %AAA-7-RADIUS: aaa_idx 50000076: rad_create_auth_db_reply: Radius authentication success. (00:1d:60:d7:68:79)
Aug 22 11:46:14: %AAA-7-AUTHEN: aaa_idx 50000076: aaa_process_ipc_authen_response, Received Authentication response msg for aaa_idx 1342177398.
Aug 22 11:46:14: [2/1:1023:63/7/2/117]: %AAA-7-AUTHEN: aaa_idx 50000076: aaa_process_ipc_authen_response: copying attributes of length 268
Aug 22 11:46:14: [0001]: [2/1:1023:63/7/2/117]: %AAA-7-RADIUS: aaa_idx 50000076: rad_process_response: process response to req Authentication. (00:1d:60:d7:68:79)
Aug 22 11:46:14: [0001]: [2/1:1023:63/7/2/117]: %AAA-7-RADIUS: aaa_idx 50000076: rad_free_resource:, Free radius message, rad_idx 209
Aug 22 11:46:14: %AAA-7-RADIUS: aaa_idx 50000076: rad_clean_aaa_idx_tree: Clean aaa_idx tree for global db_request_type Authentication
Aug 22 11:46:14: %AAA-7-GEN: aaa_idx 50000076: Processing DB_RESPONSE msg.
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-AUTHOR: aaa_idx 50000076: aaa_is_sess_on_tm_card: slot 2 is a TM card
Aug 22 11:46:14: %AAA-7-GEN: aaa_convert_context_name_to_id: Context ID 0x40080002
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-GEN: aaa_idx 50000076: aaa_process_db_response: Received successful DB response.
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-AUTHOR: aaa_idx 50000076: aaa_bind_subscriber:  Binding subscriber via DHCP
Aug 22 11:46:14: %AAA-7-ACCT: dhcp vendor class id applied, length 9
Aug 22 11:46:14: %AAA-7-ACCT: dhcp option client id applied, length 9
Aug 22 11:46:14: %AAA-7-ACCT: dhcp option hostname applied, length 6
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-AUTHOR: aaa_idx 50000076: aaa_bind_subscriber: No QOS queue attribute for session 00:1d:60:d7:68:79, check parent cct
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-AUTHOR: aaa_idx 50000076: aaa_bind_subscriber: No QOS metering attribute for session 00:1d:60:d7:68:79, check parent cct
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-AUTHOR: aaa_idx 50000076: aaa_bind_subscriber: No QOS policing attribute for session 00:1d:60:d7:68:79, check parent cct
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-AUTHOR: aaa_idx 50000076: aaa_bind_subscriber: No QOS overhead attribute for session 00:1d:60:d7:68:79, check parent cct
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-AUTHEN: aaa_idx 50000076: aaa_fill_client_data: to copy attributes length 160
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-AUTHEN: aaa_idx 50000076: aaa_fill_client_data: to copy attributes length 200
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-AUTHEN: aaa_idx 50000076: aaa_fill_client_struct: return SUCCESS
Aug 22 11:46:14: [2/1:1023:63/7/2/117]: %AAA-7-AUTHEN: aaa_idx 50000076: Received SESSION_UP msg from client CLIPSd
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-AUTHEN: aaa_idx 50000076: aaa_process_ipc_session_up: session 00:1d:60:d7:68:79 iphost 169.254.218.209 context_id 0x40080002  bounce flag 0 sess_class 0x20
Aug 22 11:46:14: %AAA-7-GEN: aaa_idx 50000076: Processing SESSION_UP msg.
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-SVC: aaa_idx 50000076: aaa_svc_validate: svc validation for subscriber = 00:1d:60:d7:68:79,status = missing mandatory attr (svc-options) 
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-EXCEPT: aaa_idx 50000076: aaa_svc_proc_activate: service validation error
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-EXCEPT: aaa_idx 50000076: aaa_svc_proc: Process service activate error 51
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-SVC: aaa_idx 50000076: aaa_svc_cleanup_class_used_mask: Reset session used class mask upon activate error 0x0 0x0 0x0 0x0 0x0 0x0
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-EXCEPT: aaa_idx 50000076: aaa_process_session_up: service attribute processing failed for subscriber 00:1d:60:d7:68:79
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-INTF: aaa_idx 50000076: send state change of sub to ISM,new state is clear, cause 26
Aug 22 11:46:14: [2/1:1023:63/7/2/117]: %AAA-7-AUTHEN: aaa_idx 50000076: Received SESSION_DOWN msg extern_handle 131189
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-DHCP: aaa_idx 50000076: aaa_is_dhcp_clips_bounce_down: bounce flag 0 class 0x20 tc 26
Aug 22 11:46:14: %AAA-7-GEN: aaa_idx 50000076: aaa_sess_dn_mgr, Processing SESSION_DOWN msg.
Aug 22 11:46:14: [2/1:1023:63/7/2/117]: %AAA-7-ANCP: aaa_DSL_undoQosRates for DSL ACI=""
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-AUTHOR: aaa_idx 50000076: aaa_attr_inheritance: check for inherited queuing policy, root 2/1:1023:63/1/2/13
Aug 22 11:46:14: [0002]: [2/1:1023:63/1/2/13]: %AAA-7-AUTHOR: aaa_idx 50000076: aaa_get_qos_inherited_policy: No qos policy applied to parent circuit for session 00:1d:60:d7:68:79
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-AUTHOR: aaa_idx 50000076: aaa_attr_inheritance: check for inherited metering policy, root 2/1:1023:63/1/2/13
Aug 22 11:46:14: [0002]: [2/1:1023:63/1/2/13]: %AAA-7-AUTHOR: aaa_idx 50000076: aaa_get_qos_inherited_policy: No qos policy applied to parent circuit for session 00:1d:60:d7:68:79
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-AUTHOR: aaa_idx 50000076: aaa_attr_inheritance: check for inherited policing policy, root 2/1:1023:63/1/2/13
Aug 22 11:46:14: [0002]: [2/1:1023:63/1/2/13]: %AAA-7-AUTHOR: aaa_idx 50000076: aaa_get_qos_inherited_policy: No qos policy applied to parent circuit for session 00:1d:60:d7:68:79
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-AUTHOR: aaa_idx 50000076: aaa_attr_inheritance: check for inherited overhead policy, root 2/1:1023:63/1/2/13
Aug 22 11:46:14: [0002]: [2/1:1023:63/1/2/13]: %AAA-7-AUTHOR: aaa_idx 50000076: aaa_get_qos_inherited_policy: No qos policy applied to parent circuit for session 00:1d:60:d7:68:79
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-INTF: aaa_idx 50000076: send state change of sub to ISM,new state is down-complete, cause 26
Aug 22 11:46:14: [0002]: [2/1:1023:63/7/2/117]: %AAA-7-AUTHEN: aaa_idx 50000076: Deleting session term cause 26
Aug 22 11:46:14: [2/1:1023:63/7/2/117]: %AAA-7-ANCP: Remove DSL ACI=""
Aug 22 11:46:14: [2/1:1023:63/7/2/117]: %AAA-7-ANCP:  no more subs
Aug 22 11:46:14: %AAA-7-ANCP: Delete DSL ACI="" count of flexible tree 0, count of opaque tree 1
Aug 22 11:46:30: [2/1:1023:63/7/2/118]: %AAA-7-AUTHEN: Received AUTHEN_REQUEST msg from CLIPSd for username 00:1d:60:d7:68:79 with external handle = 131190
Aug 22 11:46:30: [2/1:1023:63/7/2/118]: %AAA-7-GEN: aaa_sess_wrap_lookup_with_ccthandle: AAA cct node lookup fail: cct 2/1:1023:63/7/2/118 (0x100ffff78000076)
Aug 22 11:46:30: %AAA-7-GEN: aaa_idx 50000077: aaa_sess_wrap_lookup_with_index: AAA idx node lookup fail: idx 0x50000077
Aug 22 11:46:30: [0000]: [2/1:1023:63/7/2/118]: %AAA-7-AUTHEN: aaa_idx 50000077: aaa_create_session_with_cct_handle: creating session for cct 2/1:1023:63/7/2/118 index 1342177399
Aug 22 11:46:30: [2/1:1023:63/7/2/118]: %AAA-7-AUTHEN: Assigned aaa_idx 1342177399 to username 00:1d:60:d7:68:79
Aug 22 11:46:30: %AAA-7-GEN: aaa_convert_context_name_to_id: Context ID 0x40080002
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-AUTHEN: aaa_idx 50000077: Binding subscriber 00:1d:60:d7:68:79 to context internet via bind context (aaa_idx = 1342177399).
Aug 22 11:46:30: %AAA-7-ANCP: [aaa_DslAddOrFindSessionCircuit] searching in CCT tree for cct "Cct invalid" madeNew 1
Aug 22 11:46:30: %AAA-7-ANCP: [aaa_dslAddToOpaqueTree] putting ACI  in opaque tree
Aug 22 11:46:30: %AAA-7-ANCP:  addorfindcircuit add new count of flexible tree 0, count of opaque tree 1
Aug 22 11:46:30: %AAA-7-ANCP: aaa_DSL_add_session chaining under DSL_LINE  aciLen 7
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-AUTHEN: aaa_idx 50000077: Received session slot mask 0x0 
Aug 22 11:46:30: %AAA-7-GEN: aaa_idx 50000077: Processing AUTHEN_REQUEST msg.
Aug 22 11:46:30: [0002]: %AAA-7-GEN: AAA sub name node lookup fail: cntxt 0x40080002 subscriber 00:1d:60:d7:68:79
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-AUTHEN: aaa_idx 50000077: Adding aaa_idx 1342177399 to context internet
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-AUTHEN: aaa_idx 50000077: Sending Authentication request to global
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-AUTHEN: aaa_idx 50000077: aaa_send_db_req: Created tlv list (more_data) for session 00:1d:60:d7:68:79
Aug 22 11:46:30: %AAA-7-GEN: aaa_idx 50000077: Sending DB_REQUEST to global.
Aug 22 11:46:30: %AAA-7-RADIUS: rad_mgr, Process radius requests in db request queue
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-RADIUS: aaa_idx 50000077: rad_process_aaad_req: Receive request (Authentication)
Aug 22 11:46:30: [0001]: [2/1:1023:63/7/2/118]: %AAA-7-RAD_ATTR: aaa_idx 50000077: rad_add_attr_to_tlv_list, Add attr NAS_Port_ID (2/1 vlan-id 2222:15 clips 131190) with len 33 to tlv list
Aug 22 11:46:30: [0001]: [2/1:1023:63/7/2/118]: %AAA-7-RADIUS: aaa_idx 50000077: aaaidx_tree_insert: insert aaa_idx to idx tree for global db_request_type Authentication. (00:1d:60:d7:68:79) 
Aug 22 11:46:30: %AAA-7-RADIUS: rad_send, Process radius requests in authen low priority queue
Aug 22 11:46:30: [0001]: [2/1:1023:63/7/2/118]: %AAA-7-RADIUS: aaa_idx 50000077: do_auth_send: Find free authen server 81.20.192.55 (ctx local, src port 1812, dst port 1812). (00:1d:60:d7:68:79)
Aug 22 11:46:30: [0001]: [2/1:1023:63/7/2/118]: %AAA-7-RAD_PKT: aaa_idx 50000077: Send packet (303 bytes) to 81.20.192.55/1812 (00:1d:60:d7:68:79):

   0    01 44 01 2f 9f 76 7a 5e 31 95 9e 8e c8 f8 92 90
  16    ce 0b 51 3b 01 13 30 30 3a 31 64 3a 36 30 3a 64
  32    37 3a 36 38 3a 37 39 02 12 d7 d9 01 8f 8e bb 4a
  48    1f 0c e5 19 fe 52 65 2d 1b 06 06 00 00 00 05 20
  64    09 52 65 64 62 61 63 6b 05 06 02 01 00 00 1a 0c
  80    00 00 09 30 3e 06 21 8a e0 0f 3d 06 00 00 00 05
  96    57 22 32 2f 31 20 76 6c 61 6e 2d 69 64 20 32 32
 112    32 32 3a 31 35 20 63 6c 69 70 73 20 31 33 31 31
 128    39 30 1a 0c 00 00 09 30 26 06 00 00 00 0b 1a 19
 144    00 00 09 30 91 13 30 30 2d 31 64 2d 36 30 2d 64
 160    37 2d 36 38 2d 37 39 1a 0c 00 00 09 30 62 06 00
 176    00 00 04 1a 0f 00 00 09 30 70 09 36 2e 31 2e 33
 192    2e 33 1a 10 00 00 09 30 60 0a 00 06 00 22 b0 04
 208    0c 1e 1a 10 00 00 0d e9 02 0a 00 06 00 22 b0 04
 224    0c 1e 1a 0e 00 00 09 30 61 08 00 04 00 0f 00 02
 240    1a 0e 00 00 0d e9 01 08 00 04 00 0f 00 02 1a 12
 256    00 00 09 30 ca 0c 3d 3d 07 01 00 1d 60 d7 68 79
 272    1a 0f 00 00 09 30 ca 09 0c 0c 04 53 65 30 36 1a
 288    10 00 00 09 30 7d 0a 4d 53 46 54 20 35 2e 30

Aug 22 11:46:30: [0001]: %AAA-7-RADIUS: Using local address 81.20.192.54
Aug 22 11:46:30: [0001]: %AAA-7-RADIUS: do_send: 303 bytes send to radius server  81.20.192.55 (1812).
Aug 22 11:46:30: %AAA-7-RADIUS: rad_process_send_queue, 1 requests processed (0 retransmit) 
Aug 22 11:46:30: %AAA-7-RADIUS: rad_process_received_pkt: Receive 166 bytes from radius server 81.20.192.55 (1812)
Aug 22 11:46:30: [0001]: %AAA-7-RADIUS: rad_find_match_srv: Find matching server 81.20.192.55/1812
Aug 22 11:46:30: %AAA-7-RADIUS: rad_response_sanity_check: Message-Authenticator is not present
Aug 22 11:46:30: [0001]: [2/1:1023:63/7/2/118]: %AAA-7-RAD_PKT: aaa_idx 50000077: Received packet (166 bytes) from 81.20.192.55/1812 (00:1d:60:d7:68:79):

   0    02 44 00 a6 b7 c8 cc a2 d5 7e 6e 8e 9e 5c 4b 0e
  16    5d 64 26 1e 1a 0c 00 00 09 30 68 06 64 68 63 70
  32    1a 10 00 00 09 30 04 0a 69 6e 74 65 72 6e 65 74
  48    1a 0c 00 00 09 30 03 06 00 00 00 3c 1a 11 00 00
  64    09 30 be 0b 73 65 72 76 69 63 65 2d 31 1a 59 00
  80    00 09 30 c0 53 52 61 74 65 3d 31 30 32 34 20 42
  96    75 72 73 74 3d 31 39 32 30 30 30 20 52 61 74 65
 112    2d 6c 6f 63 61 6c 3d 31 30 30 30 30 30 20 42 75
 128    72 73 74 2d 6c 6f 63 61 6c 3d 31 38 37 35 30 30
 144    30 30 20 66 69 6c 74 65 72 3d 66 69 6c 74 65 72
 160    2d 63 6c 65 61 72

Aug 22 11:46:30: %AAA-7-RADIUS: rad_mgr, Process radius requests in db response queue
Aug 22 11:46:30: %AAA-7-RAD_ATTR: Receive Redback attr 104 (IP_Interface), tag = 32, status = success
Aug 22 11:46:30: %AAA-7-RAD_ATTR: Receive Redback attr 4 (Context_Name), tag = 32, status = success
Aug 22 11:46:30: %AAA-7-RAD_ATTR: Receive Redback attr 3 (DHCP_Max_Leases), tag = 32, status = success
Aug 22 11:46:30: %AAA-7-RAD_ATTR: rad_attr_parse_svc_attr: Service name service-1
Aug 22 11:46:30: %AAA-7-RAD_ATTR: rad_attr_add_svc_attrs_tlv: Service attribute 190 add to list with tag 32 status success ec 1
Aug 22 11:46:30: %AAA-7-RAD_ATTR: rad_attr_parse_svc_attr: Service attribute 190 with tag 32 parser status success
Aug 22 11:46:30: %AAA-7-RAD_ATTR: Receive Redback attr 190 (Service_Name), tag = 32, status = success
Aug 22 11:46:30: %AAA-7-RAD_ATTR: rad_attr_parse_svc_attr: Service parameter Rate=1024 Burst=192000 Rate-local=100000 Burst-local=18750000 filter=filter-clear
Aug 22 11:46:30: %AAA-7-RAD_ATTR: rad_attr_add_svc_attrs_tlv: Service attribute 192 add to list with tag 32 status success ec 1
Aug 22 11:46:30: %AAA-7-RAD_ATTR: rad_attr_parse_svc_attr: Service attribute 192 with tag 32 parser status success
Aug 22 11:46:30: %AAA-7-RAD_ATTR: Receive Redback attr 192 (Service_Parameter), tag = 32, status = success
Aug 22 11:46:30: [0001]: [2/1:1023:63/7/2/118]: %AAA-7-RADIUS: aaa_idx 50000077: rad_create_auth_db_reply: Radius authentication success. (00:1d:60:d7:68:79)
Aug 22 11:46:30: %AAA-7-AUTHEN: aaa_idx 50000077: aaa_process_ipc_authen_response, Received Authentication response msg for aaa_idx 1342177399.
Aug 22 11:46:30: [2/1:1023:63/7/2/118]: %AAA-7-AUTHEN: aaa_idx 50000077: aaa_process_ipc_authen_response: copying attributes of length 268
Aug 22 11:46:30: [0001]: [2/1:1023:63/7/2/118]: %AAA-7-RADIUS: aaa_idx 50000077: rad_process_response: process response to req Authentication. (00:1d:60:d7:68:79)
Aug 22 11:46:30: [0001]: [2/1:1023:63/7/2/118]: %AAA-7-RADIUS: aaa_idx 50000077: rad_free_resource:, Free radius message, rad_idx 210
Aug 22 11:46:30: %AAA-7-RADIUS: aaa_idx 50000077: rad_clean_aaa_idx_tree: Clean aaa_idx tree for global db_request_type Authentication
Aug 22 11:46:30: %AAA-7-GEN: aaa_idx 50000077: Processing DB_RESPONSE msg.
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-AUTHOR: aaa_idx 50000077: aaa_is_sess_on_tm_card: slot 2 is a TM card
Aug 22 11:46:30: %AAA-7-GEN: aaa_convert_context_name_to_id: Context ID 0x40080002
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-GEN: aaa_idx 50000077: aaa_process_db_response: Received successful DB response.
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-AUTHOR: aaa_idx 50000077: aaa_bind_subscriber:  Binding subscriber via DHCP
Aug 22 11:46:30: %AAA-7-ACCT: dhcp vendor class id applied, length 9
Aug 22 11:46:30: %AAA-7-ACCT: dhcp option client id applied, length 9
Aug 22 11:46:30: %AAA-7-ACCT: dhcp option hostname applied, length 6
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-AUTHOR: aaa_idx 50000077: aaa_bind_subscriber: No QOS queue attribute for session 00:1d:60:d7:68:79, check parent cct
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-AUTHOR: aaa_idx 50000077: aaa_bind_subscriber: No QOS metering attribute for session 00:1d:60:d7:68:79, check parent cct
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-AUTHOR: aaa_idx 50000077: aaa_bind_subscriber: No QOS policing attribute for session 00:1d:60:d7:68:79, check parent cct
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-AUTHOR: aaa_idx 50000077: aaa_bind_subscriber: No QOS overhead attribute for session 00:1d:60:d7:68:79, check parent cct
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-AUTHEN: aaa_idx 50000077: aaa_fill_client_data: to copy attributes length 160
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-AUTHEN: aaa_idx 50000077: aaa_fill_client_data: to copy attributes length 200
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-AUTHEN: aaa_idx 50000077: aaa_fill_client_struct: return SUCCESS
Aug 22 11:46:30: [2/1:1023:63/7/2/118]: %AAA-7-AUTHEN: aaa_idx 50000077: Received SESSION_UP msg from client CLIPSd
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-AUTHEN: aaa_idx 50000077: aaa_process_ipc_session_up: session 00:1d:60:d7:68:79 iphost 169.254.218.209 context_id 0x40080002  bounce flag 0 sess_class 0x20
Aug 22 11:46:30: %AAA-7-GEN: aaa_idx 50000077: Processing SESSION_UP msg.
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-SVC: aaa_idx 50000077: aaa_svc_validate: svc validation for subscriber = 00:1d:60:d7:68:79,status = missing mandatory attr (svc-options) 
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-EXCEPT: aaa_idx 50000077: aaa_svc_proc_activate: service validation error
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-EXCEPT: aaa_idx 50000077: aaa_svc_proc: Process service activate error 51
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-SVC: aaa_idx 50000077: aaa_svc_cleanup_class_used_mask: Reset session used class mask upon activate error 0x0 0x0 0x0 0x0 0x0 0x0
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-EXCEPT: aaa_idx 50000077: aaa_process_session_up: service attribute processing failed for subscriber 00:1d:60:d7:68:79
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-INTF: aaa_idx 50000077: send state change of sub to ISM,new state is clear, cause 26
Aug 22 11:46:30: [2/1:1023:63/7/2/118]: %AAA-7-AUTHEN: aaa_idx 50000077: Received SESSION_DOWN msg extern_handle 131190
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-DHCP: aaa_idx 50000077: aaa_is_dhcp_clips_bounce_down: bounce flag 0 class 0x20 tc 26
Aug 22 11:46:30: %AAA-7-GEN: aaa_idx 50000077: aaa_sess_dn_mgr, Processing SESSION_DOWN msg.
Aug 22 11:46:30: [2/1:1023:63/7/2/118]: %AAA-7-ANCP: aaa_DSL_undoQosRates for DSL ACI=""
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-AUTHOR: aaa_idx 50000077: aaa_attr_inheritance: check for inherited queuing policy, root 2/1:1023:63/1/2/13
Aug 22 11:46:30: [0002]: [2/1:1023:63/1/2/13]: %AAA-7-AUTHOR: aaa_idx 50000077: aaa_get_qos_inherited_policy: No qos policy applied to parent circuit for session 00:1d:60:d7:68:79
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-AUTHOR: aaa_idx 50000077: aaa_attr_inheritance: check for inherited metering policy, root 2/1:1023:63/1/2/13
Aug 22 11:46:30: [0002]: [2/1:1023:63/1/2/13]: %AAA-7-AUTHOR: aaa_idx 50000077: aaa_get_qos_inherited_policy: No qos policy applied to parent circuit for session 00:1d:60:d7:68:79
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-AUTHOR: aaa_idx 50000077: aaa_attr_inheritance: check for inherited policing policy, root 2/1:1023:63/1/2/13
Aug 22 11:46:30: [0002]: [2/1:1023:63/1/2/13]: %AAA-7-AUTHOR: aaa_idx 50000077: aaa_get_qos_inherited_policy: No qos policy applied to parent circuit for session 00:1d:60:d7:68:79
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-AUTHOR: aaa_idx 50000077: aaa_attr_inheritance: check for inherited overhead policy, root 2/1:1023:63/1/2/13
Aug 22 11:46:30: [0002]: [2/1:1023:63/1/2/13]: %AAA-7-AUTHOR: aaa_idx 50000077: aaa_get_qos_inherited_policy: No qos policy applied to parent circuit for session 00:1d:60:d7:68:79
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-INTF: aaa_idx 50000077: send state change of sub to ISM,new state is down-complete, cause 26
Aug 22 11:46:30: [0002]: [2/1:1023:63/7/2/118]: %AAA-7-AUTHEN: aaa_idx 50000077: Deleting session term cause 26
Aug 22 11:46:30: [2/1:1023:63/7/2/118]: %AAA-7-ANCP: Remove DSL ACI=""
Aug 22 11:46:30: [2/1:1023:63/7/2/118]: %AAA-7-ANCP:  no more subs
Aug 22 11:46:30: %AAA-7-ANCP: Delete DSL ACI="" count of flexible tree 0, count of opaque tree 1












rad_recv: Access-Request packet from host 81.20.192.54 port 1812, id=67, length=303
        User-Name = "00:1d:60:d7:68:79"
        User-Password = "Redback"
        Service-Type = Outbound-User
        NAS-Identifier = "Redback"
        NAS-Port = 33619968
        NAS-Real-Port = 562749455
        NAS-Port-Type = Virtual
        NAS-Port-Id = "2/1 vlan-id 2222:15 clips 131189"
        Medium-Type = DSL
        Mac-Addr = "00-1d-60-d7-68-79"
        Platform-Type = SE-100
        OS-Version = "6.1.3.3"
        Agent-Remote-Id = "\000\006\000\"\260\004\014\036"
        ADSL-Agent-Remote-Id = "\000\006\000\"\260\004\014\036"
        Agent-Circuit-Id = "\000\004\000\017\000\002"
        ADSL-Agent-Circuit-Id = "\000\004\000\017\000\002"
        DHCP-Option = "==\007\001\000\035`\327hy"
        DHCP-Option = "\014\014\004Se06"
        DHCP-Vendor-Class-ID = "MSFT 5.0"
# Executing section authorize from file /etc/raddb/sites-enabled/default
+- entering group authorize {...}
++[preprocess] returns ok
++[chap] returns noop
++[mschap] returns noop
++[digest] returns noop
[suffix] No '@' in User-Name = "00:1d:60:d7:68:79", looking up realm NULL
[suffix] No such realm "NULL"
++[suffix] returns noop
[files] users: Matched entry 00:1d:60:d7:68:79 at line 217
++[files] returns ok
++[expiration] returns noop
++[logintime] returns noop
++[pap] returns updated
Found Auth-Type = PAP
# Executing group from file /etc/raddb/sites-enabled/default
+- entering group PAP {...}
[pap] login attempt with password "Redback"
[pap] Using clear text password "Redback"
[pap] User authenticated successfully
++[pap] returns ok
Login OK: [00:1d:60:d7:68:79/Redback] (from client 81.20.192.54 port 33619968)
# Executing section post-auth from file /etc/raddb/sites-enabled/default
+- entering group post-auth {...}
++[exec] returns noop
Sending Access-Accept of id 67 to 81.20.192.54 port 1812
        IP-Interface-Name = "dhcp"
        Context-Name = "internet"
        DHCP-Max-Leases = 60
        Service-Name = "service-1"
        Service-Parameter = "Rate=1024 Burst=192000 Rate-local=100000 Burst-local=18750000 filter=filter-clear"
Finished request 0.
Going to the next request
Waking up in 4.9 seconds.
Cleaning up request 0 ID 67 with timestamp +321
Ready to process requests.
rad_recv: Access-Request packet from host 81.20.192.54 port 1812, id=68, length=303
        User-Name = "00:1d:60:d7:68:79"
        User-Password = "Redback"
        Service-Type = Outbound-User
        NAS-Identifier = "Redback"
        NAS-Port = 33619968
        NAS-Real-Port = 562749455
        NAS-Port-Type = Virtual
        NAS-Port-Id = "2/1 vlan-id 2222:15 clips 131190"
        Medium-Type = DSL
        Mac-Addr = "00-1d-60-d7-68-79"
        Platform-Type = SE-100
        OS-Version = "6.1.3.3"
        Agent-Remote-Id = "\000\006\000\"\260\004\014\036"
        ADSL-Agent-Remote-Id = "\000\006\000\"\260\004\014\036"
        Agent-Circuit-Id = "\000\004\000\017\000\002"
        ADSL-Agent-Circuit-Id = "\000\004\000\017\000\002"
        DHCP-Option = "==\007\001\000\035`\327hy"
        DHCP-Option = "\014\014\004Se06"
        DHCP-Vendor-Class-ID = "MSFT 5.0"
# Executing section authorize from file /etc/raddb/sites-enabled/default
+- entering group authorize {...}
++[preprocess] returns ok
++[chap] returns noop
++[mschap] returns noop
++[digest] returns noop
[suffix] No '@' in User-Name = "00:1d:60:d7:68:79", looking up realm NULL
[suffix] No such realm "NULL"
++[suffix] returns noop
[files] users: Matched entry 00:1d:60:d7:68:79 at line 217
++[files] returns ok
++[expiration] returns noop
++[logintime] returns noop
++[pap] returns updated
Found Auth-Type = PAP
# Executing group from file /etc/raddb/sites-enabled/default
+- entering group PAP {...}
[pap] login attempt with password "Redback"
[pap] Using clear text password "Redback"
[pap] User authenticated successfully
++[pap] returns ok
Login OK: [00:1d:60:d7:68:79/Redback] (from client 81.20.192.54 port 33619968)
# Executing section post-auth from file /etc/raddb/sites-enabled/default
+- entering group post-auth {...}
++[exec] returns noop
Sending Access-Accept of id 68 to 81.20.192.54 port 1812
        IP-Interface-Name = "dhcp"
        Context-Name = "internet"
        DHCP-Max-Leases = 60
        Service-Name = "service-1"
        Service-Parameter = "Rate=1024 Burst=192000 Rate-local=100000 Burst-local=18750000 filter=filter-clear"
Finished request 1.
Going to the next request
Waking up in 4.9 seconds.
Cleaning up request 1 ID 68 with timestamp +337
Ready to process requests.
























Oct  5 10:34:00.994: DHCPD: Sending notification of DISCOVER:
Oct  5 10:34:00.994:   DHCPD: htype 1 chaddr 001d.60d7.6879
Oct  5 10:34:00.994:   DHCPD: remote id 0106001cf09d7167
Oct  5 10:34:00.994:   DHCPD: circuit id 000400320001
Oct  5 10:34:00.994:   DHCPD: interface = GigabitEthernet0/0/2.195750
Oct  5 10:34:00.994:   DHCPD: class id 4d53465420352e30
Oct  5 10:34:00.994: DHCPD: Sending notification of DISCOVER:
Oct  5 10:34:00.994:   DHCPD: htype 1 chaddr 001d.60d7.6879
Oct  5 10:34:00.994:   DHCPD: remote id 0106001cf09d7167
Oct  5 10:34:00.994:   DHCPD: circuit id 000400320001
Oct  5 10:34:00.994:   DHCPD: interface = GigabitEthernet0/0/2.195750
Oct  5 10:34:00.994:   DHCPD: class id 4d53465420352e30
Oct  5 10:34:00.995: AAA/BIND(00006BBE): Bind i/f  
Oct  5 10:34:00.995: AAA/BIND(00006BBE): Bind i/f GigabitEthernet0/0/2.195750 
Oct  5 10:34:00.996: AAA/AUTHOR (0x6BBE): Pick method list 'ISG-AUTH-1'
Oct  5 10:34:00.996: RADIUS/ENCODE(00006BBE):Orig. component type = Iedge IP SIP
Oct  5 10:34:00.997: RADIUS: Format E value 0xF4F4 for character U with bitmask 0xFFFFFFFF
Oct  5 10:34:00.997: RADIUS: Format E port 0xF4F4 with bit 32 processed
Oct  5 10:34:00.997: RADIUS(00006BBE): Config NAS IP: 0.0.0.0
Oct  5 10:34:00.997: RADIUS(00006BBE): Config NAS IPv6: ::
Oct  5 10:34:00.997: RADIUS/ENCODE(00006BBE): acct_session_id: 62708
Oct  5 10:34:00.997: RADIUS/ENCODE(00006BBE): Acct-session-id pre-pended with Nas Port = 0/0/2/50.1957
Oct  5 10:34:00.997: RADIUS(00006BBE): Config NAS IP: 0.0.0.0
Oct  5 10:34:00.997: RADIUS(00006BBE): sending
Oct  5 10:34:00.997: RADIUS/ENCODE: Best Local IP-Address 81.20.192.51 for Radius-Server 81.20.192.57
Oct  5 10:34:00.997: RADIUS(00006BBE): Send Access-Request to 81.20.192.57:1812 id 1645/213, len 301
Oct  5 10:34:00.997: RADIUS:  authenticator 05 D2 A4 07 0D D5 CD 9E - 04 CD 14 F4 3B B0 3E 55
Oct  5 10:34:00.997: RADIUS:  User-Name           [1]   31  "000400320001:0106001cf09d7167"
Oct  5 10:34:00.997: RADIUS:  User-Password       [2]   18  *
Oct  5 10:34:00.997: RADIUS:  NAS-Port-Type       [61]  6   PPPoEoQinQ                [34]
Oct  5 10:34:00.997: RADIUS:  Vendor, Cisco       [26]  21  
Oct  5 10:34:00.997: RADIUS:   cisco-nas-port     [2]   15  "0/0/2/50.1957"
Oct  5 10:34:00.997: RADIUS:  NAS-Port            [5]   6   62708                     
Oct  5 10:34:00.997: RADIUS:  NAS-Port-Id         [87]  15  "0/0/2/50.1957"
Oct  5 10:34:00.997: RADIUS:  Vendor, Cisco       [26]  35  
Oct  5 10:34:00.997: RADIUS:   Cisco AVpair       [1]   29  "circuit-id-tag=000400320001"
Oct  5 10:34:00.997: RADIUS:  Vendor, Cisco       [26]  38  
Oct  5 10:34:00.997: RADIUS:   Cisco AVpair       [1]   32  "remote-id-tag=0106001cf09d7167"
Oct  5 10:34:00.997: RADIUS:  Vendor, Cisco       [26]  36  
Oct  5 10:34:00.997: RADIUS:   Cisco AVpair       [1]   30  "vendor-class-id-tag=MSFT 5.0"
Oct  5 10:34:00.997: RADIUS:  Service-Type        [6]   6   Outbound                  [5]
Oct  5 10:34:00.997: RADIUS:  NAS-IP-Address      [4]   6   81.20.192.51              
Oct  5 10:34:00.997: RADIUS:  Acct-Session-Id     [44]  32  "0/0/2/50.1957_780000000000F4F4"
Oct  5 10:34:00.997: RADIUS:  Nas-Identifier      [32]  25  "ctd-c5-ISG.ctd-c5.sc.ru"
Oct  5 10:34:00.997: RADIUS:  Event-Timestamp     [55]  6   1317810840                
Oct  5 10:34:00.997: RADIUS(00006BBE): Sending a IPv4 Radius
                                        Packet
Oct  5 10:34:00.998: RADIUS(00006BBE): Started 5 sec timeout
Oct  5 10:34:01.036: RADIUS: Received from id 1645/213 81.20.192.57:1812, Access-Accept, len 95
Oct  5 10:34:01.036: RADIUS:  authenticator 32 F5 D6 B4 E3 84 FA F6 - 48 4E FB 45 BB E7 23 47
Oct  5 10:34:01.036: RADIUS:  Vendor, Cisco       [26]  14  
Oct  5 10:34:01.036: RADIUS:   ssg-account-info   [250] 8   "A30720"
Oct  5 10:34:01.036: RADIUS:  Service-Type        [6]   6   Framed                    [2]
Oct  5 10:34:01.036: RADIUS:  Vendor, Cisco       [26]  55  
Oct  5 10:34:01.036: RADIUS:   Cisco AVpair       [1]   49  "lcp:interface-config=description Test oldswitch"
Oct  5 10:34:01.036: RADIUS(00006BBE): Received from id 1645/213
Oct  5 10:34:01.037: SVM [30720]: needs downloading
Oct  5 10:34:01.037: SVM [120005AB/30720]: allocated version 1
Oct  5 10:34:01.037: SVM [120005AB/30720]: [6900028D]: client queued
Oct  5 10:34:01.037: SVM [120005AB/30720]: [PM-Download:6900028D] locked 0->1
Oct  5 10:34:01.037: SVM [120005AB/30720]: [AAA-Download:4429415C] locked 0->1
Oct  5 10:34:01.037: AAA/AUTHOR (0x6BBE): Pick method list 'default'
Oct  5 10:34:01.040: SVM [FA0005AC/30720]: added child
Oct  5 10:34:01.040: SVM [120005AB/30720]: TC created
Oct  5 10:34:01.040: SVM [120005AB/30720]: [TC-Child:44C8B0F8] locked 0->1
Oct  5 10:34:01.040: SVM [FA0005AC/CHILD/30720]: [TC-Parent:44C8B17C] locked 0->1
Oct  5 10:34:01.040: SVM [120005AB/30720]: TC svc_info found
Oct  5 10:34:01.040: SVM [FA0005AC/CHILD/30720]: set accounting handle
Oct  5 10:34:01.040: SVM [120005AB/30720]: downloaded first version
Oct  5 10:34:01.040: SVM [120005AB/30720]: [6900028D]: client download ok
Oct  5 10:34:01.040: SVM [120005AB/30720]: [SVM-to-client-msg:6900028D] locked 0->1
Oct  5 10:34:01.040: SVM [120005AB/30720]: [AAA-Download:4429415C] unlocked 1->0
Oct  5 10:34:01.040: SVM [120005AB/30720]: alloc feature info
Oct  5 10:34:01.040: SVM [120005AB/30720]: [SVM-Feature-Info:44B18364] locked 0->1
Oct  5 10:34:01.040: SVM [120005AB/30720]: has Policy info
Oct  5 10:34:01.040: SVM [120005AB/30720]: [PM-Info:44C3FE80] locked 0->1
Oct  5 10:34:01.040: SVM [120005AB/30720]: populated client
Oct  5 10:34:01.040: SVM [120005AB/30720]: [PM-Download:6900028D] unlocked 1->0
Oct  5 10:34:01.041: SVM [120005AB/30720]: [SVM-to-client-msg:6900028D] unlocked 1->0
Oct  5 10:34:01.041: SVM [120005AB/30720]: [PM-Service:44CBC770] locked 0->1
Oct  5 10:34:01.041: SVM [120005AB/30720]: [SVM-Feature-Info:44B18364] unlocked 1->0
Oct  5 10:34:01.041: DHCPD: Callback for workspace (ID=0x8200003B)
Oct  5 10:34:01.041: DHCPD: No authentication required. Continue
Oct  5 10:34:01.041: DHCPD: Callback: class '' now specified for client 0100.1d60.d768.79
Oct  5 10:34:01.041: DHCPD: Callback: class error returns for client












000400320001:0106001cf09d7167



INSERT INTO radcheck (USERNAME,ATTRIBUTE,OP,VALUE) VALUES ('000400320001:0106001cf09d7167','Cleartext-Password',':=','ISG');
INSERT INTO radreply (USERNAME,ATTRIBUTE,OP,VALUE) VALUES ('000400320001:0106001cf09d7167','Cisco-AVPair','=','subscriber:accounting-list=ISG-AUTH-1');
INSERT INTO radreply (USERNAME,ATTRIBUTE,OP,VALUE) VALUES ('000400320001:0106001cf09d7167','Cisco-Account-Info','+=','A30720');
INSERT INTO radreply (USERNAME,ATTRIBUTE,OP,VALUE) VALUES ('000400320001:0106001cf09d7167','Service-Type','=','Framed-User');
INSERT INTO radreply (USERNAME,ATTRIBUTE,OP,VALUE) VALUES ('000400320001:0106001cf09d7167','Cisco-AVPair','=','lcp:interface-config=description Test DEs3526');
INSERT INTO radusergroup (USERNAME,GROUPNAME) VALUES ('000400320001:0106001cf09d7167','phys2');




OOct  5 10:55:21.198: DHCPD: Sending notification of DISCOVER:
Oct  5 10:55:21.198:   DHCPD: htype 1 chaddr 001d.60d7.6879
Oct  5 10:55:21.198:   DHCPD: remote id 0106001cf09d7167
Oct  5 10:55:21.198:   DHCPD: circuit id 000400320001
Oct  5 10:55:21.198:   DHCPD: interface = GigabitEthernet0/0/2.195750
Oct  5 10:55:21.198:   DHCPD: class id 4d53465420352e30
Oct  5 10:55:21.199: DHCPD: Sending notification of DISCOVER:
Oct  5 10:55:21.199:   DHCPD: htype 1 chaddr 001d.60d7.6879
Oct  5 10:55:21.199:   DHCPD: remote id 0106001cf09d7167
Oct  5 10:55:21.199:   DHCPD: circuit id 000400320001
Oct  5 10:55:21.199:   DHCPD: interface = GigabitEthernet0/0/2.195750
Oct  5 10:55:21.199:   DHCPD: class id 4d53465420352e30
Oct  5 10:55:21.199: AAA/BIND(00006BD1): Bind i/f  
Oct  5 10:55:21.199: AAA/BIND(00006BD1): Bind i/f GigabitEthernet0/0/2.195750 
Oct  5 10:55:21.200: AAA/AUTHOR (0x6BD1): Pick method list 'ISG-AUTH-1'
Oct  5 10:55:21.201: RADIUS/ENCODE(00006BD1):Orig. component type = Iedge IP SIP
Oct  5 10:55:21.201: RADIUS: Format E value 0xF50B for character U with bitmask 0xFFFFFFFF
Oct  5 10:55:21.201: RADIUS: Format E port 0xF50B with bit 32 processed
Oct  5 10:55:21.201: RADIUS(00006BD1): Config NAS IP: 0.0.0.0
Oct  5 10:55:21.201: RADIUS(00006BD1): Config NAS IPv6: ::
Oct  5 10:55:21.201: RADIUS/ENCODE(00006BD1): acct_session_id: 62731
Oct  5 10:55:21.201: RADIUS/ENCODE(00006BD1): Acct-session-id pre-pended with Nas Port = 0/0/2/50.1957
Oct  5 10:55:21.201: RADIUS(00006BD1): Config NAS IP: 0.0.0.0
Oct  5 10:55:21.201: RADIUS(00006BD1): sending
Oct  5 10:55:21.201: RADIUS/ENCODE: Best Local IP-Address 81.20.192.51 for Radius-Server 81.20.192.57
Oct  5 10:55:21.201: RADIUS(00006BD1): Send Access-Request to 81.20.192.57:1812 id 1645/231, len 301
Oct  5 10:55:21.201: RADIUS:  authenticator DF 66 4D F9 EE 42 3A 6D - C8 4E 78 AC 27 4A D8 7A
Oct  5 10:55:21.201: RADIUS:  User-Name           [1]   31  "000400320001:0106001cf09d7167"
Oct  5 10:55:21.201: RADIUS:  User-Password       [2]   18  *
Oct  5 10:55:21.201: RADIUS:  NAS-Port-Type       [61]  6   PPPoEoQinQ                [34]
Oct  5 10:55:21.201: RADIUS:  Vendor, Cisco       [26]  21  
Oct  5 10:55:21.202: RADIUS:   cisco-nas-port     [2]   15  "0/0/2/50.1957"
Oct  5 10:55:21.202: RADIUS:  NAS-Port            [5]   6   62731                     
Oct  5 10:55:21.202: RADIUS:  NAS-Port-Id         [87]  15  "0/0/2/50.1957"
Oct  5 10:55:21.202: RADIUS:  Vendor, Cisco       [26]  35  
Oct  5 10:55:21.202: RADIUS:   Cisco AVpair       [1]   29  "circuit-id-tag=000400320001"
Oct  5 10:55:21.202: RADIUS:  Vendor, Cisco       [26]  38  
Oct  5 10:55:21.202: RADIUS:   Cisco AVpair       [1]   32  "remote-id-tag=0106001cf09d7167"
Oct  5 10:55:21.202: RADIUS:  Vendor, Cisco       [26]  36  
Oct  5 10:55:21.202: RADIUS:   Cisco AVpair       [1]   30  "vendor-class-id-tag=MSFT 5.0"
Oct  5 10:55:21.202: RADIUS:  Service-Type        [6]   6   Outbound                  [5]
Oct  5 10:55:21.202: RADIUS:  NAS-IP-Address      [4]   6   81.20.192.51              
Oct  5 10:55:21.202: RADIUS:  Acct-Session-Id     [44]  32  "0/0/2/50.1957_780000000000F50B"
Oct  5 10:55:21.202: RADIUS:  Nas-Identifier      [32]  25  "ctd-c5-ISG.ctd-c5.sc.ru"
Oct  5 10:55:21.202: RADIUS:  Event-Timestamp     [55]  6   1317812121                
Oct  5 10:55:21.202: RADIUS(00006BD1): Sending a IPv4 Radius
                                        Packet
Oct  5 10:55:21.202: RADIUS(00006BD1): Started 5 sec timeout
Oct  5 10:55:21.239: RADIUS: Received from id 1645/231 81.20.192.57:1812, Access-Accept, len 95
Oct  5 10:55:21.239: RADIUS:  authenticator 82 F2 71 B4 C3 81 EB 3B - 8F 34 80 D6 4C A8 F1 EB
Oct  5 10:55:21.239: RADIUS:  Vendor, Cisco       [26]  14  
Oct  5 10:55:21.239: RADIUS:   ssg-account-info   [250] 8   "A30720"
Oct  5 10:55:21.239: RADIUS:  Service-Type        [6]   6   Framed                    [2]
Oct  5 10:55:21.239: RADIUS:  Vendor, Cisco       [26]  55  
Oct  5 10:55:21.239: RADIUS:   Cisco AVpair       [1]   49  "lcp:interface-config=description Test oldswitch"
Oct  5 10:55:21.239: RADIUS(00006BD1): Received from id 1645/231
Oct  5 10:55:21.240: SVM [30720]: needs downloading
Oct  5 10:55:21.240: SVM [530005CF/30720]: allocated version 1
Oct  5 10:55:21.240: SVM [530005CF/30720]: [8B0002A9]: client queued
Oct  5 10:55:21.240: SVM [530005CF/30720]: [PM-Download:8B0002A9] locked 0->1
Oct  5 10:55:21.240: SVM [530005CF/30720]: [AAA-Download:44E4F970] locked 0->1
Oct  5 10:55:21.241: AAA/AUTHOR (0x6BD1): Pick method list 'default'
Oct  5 10:55:21.243: SVM [A40005D0/30720]: added child
Oct  5 10:55:21.243: SVM [530005CF/30720]: TC created
Oct  5 10:55:21.243: SVM [530005CF/30720]: [TC-Child:44C8B0F8] locked 0->1
Oct  5 10:55:21.243: SVM [A40005D0/CHILD/30720]: [TC-Parent:44C8B17C] locked 0->1
Oct  5 10:55:21.243: SVM [530005CF/30720]: TC svc_info found
Oct  5 10:55:21.243: SVM [A40005D0/CHILD/30720]: set accounting handle
Oct  5 10:55:21.243: SVM [530005CF/30720]: downloaded first version
Oct  5 10:55:21.243: SVM [530005CF/30720]: [8B0002A9]: client download ok
Oct  5 10:55:21.243: SVM [530005CF/30720]: [SVM-to-client-msg:8B0002A9] locked 0->1
Oct  5 10:55:21.243: SVM [530005CF/30720]: [AAA-Download:44E4F970] unlocked 1->0
Oct  5 10:55:21.243: SVM [530005CF/30720]: alloc feature info
Oct  5 10:55:21.244: SVM [530005CF/30720]: [SVM-Feature-Info:44B18364] locked 0->1
Oct  5 10:55:21.244: SVM [530005CF/30720]: has Policy info
Oct  5 10:55:21.244: SVM [530005CF/30720]: [PM-Info:44C41470] locked 0->1
Oct  5 10:55:21.244: SVM [530005CF/30720]: populated client
Oct  5 10:55:21.244: SVM [530005CF/30720]: [PM-Download:8B0002A9] unlocked 1->0
Oct  5 10:55:21.244: SVM [530005CF/30720]: [SVM-to-client-msg:8B0002A9] unlocked 1->0
Oct  5 10:55:21.244: SVM [530005CF/30720]: [PM-Service:44CBD2B0] locked 0->1
Oct  5 10:55:21.244: SVM [530005CF/30720]: [SVM-Feature-Info:44B18364] unlocked 1->0
Oct  5 10:55:21.244: DHCPD: Callback for workspace (ID=0x2E00004D)
Oct  5 10:55:21.244: DHCPD: No authentication required. Continue
Oct  5 10:55:21.244: DHCPD: Callback: class '' now specified for client 0100.1d60.d768.79
Oct  5 10:55:21.244: DHCPD: Callback: class error returns for client
Oct  5 10:55:21.244: SVM [530005CF/30720]: already downloaded; sharing
Oct  5 10:55:21.244: SVM [530005CF/30720]: [PM-Service:44CBD2B0] unlocked 1->0
Oct  5 10:55:21.244: SVM [530005CF/30720]: [PM-Info:44C41470] unlocked 1->0
Oct  5 10:55:21.244: SVM [530005CF/30720]: breaking parent-child lock
Oct  5 10:55:21.244: SVM [A40005D0/CHILD/30720]: breaking parent-child lock
Oct  5 10:55:21.244: SVM [A40005D0/CHILD/30720]: destroy
Oct  5 10:55:21.244: SVM ERROR: unknown handle A40005D0
Oct  5 10:55:21.245: SVM [530005CF/30720]: destroy
Oct  5 10:55:21.245: SVM ERROR: unknown handle 530005CF












Oct  5 11:25:43.727: DHCPD: Sending notification of DISCOVER:
Oct  5 11:25:43.727:   DHCPD: htype 1 chaddr 6c62.6db5.cfc7
Oct  5 11:25:43.727:   DHCPD: remote id 00063408045f3a70
Oct  5 11:25:43.727:   DHCPD: circuit id 0004006e0005
Oct  5 11:25:43.727:   DHCPD: interface = GigabitEthernet0/0/2.1954110
Oct  5 11:25:43.727:   DHCPD: class id 4d53465420352e30
Oct  5 11:25:43.728: DHCPD: Sending notification of DISCOVER:
Oct  5 11:25:43.728:   DHCPD: htype 1 chaddr 6c62.6db5.cfc7
Oct  5 11:25:43.728:   DHCPD: remote id 00063408045f3a70
Oct  5 11:25:43.728:   DHCPD: circuit id 0004006e0005
Oct  5 11:25:43.728:   DHCPD: interface = GigabitEthernet0/0/2.1954110
Oct  5 11:25:43.728:   DHCPD: class id 4d53465420352e30
Oct  5 11:25:43.728: AAA/BIND(00006BEE): Bind i/f  
Oct  5 11:25:43.728: AAA/BIND(00006BEE): Bind i/f GigabitEthernet0/0/2.1954110 
Oct  5 11:25:43.729: AAA/AUTHOR (0x6BEE): Pick method list 'ISG-AUTH-1'
Oct  5 11:25:43.730: RADIUS/ENCODE(00006BEE):Orig. component type = Iedge IP SIP
Oct  5 11:25:43.730: RADIUS: Format E value 0xF5A4 for character U with bitmask 0xFFFFFFFF
Oct  5 11:25:43.730: RADIUS: Format E port 0xF5A4 with bit 32 processed
Oct  5 11:25:43.730: RADIUS(00006BEE): Config NAS IP: 0.0.0.0
Oct  5 11:25:43.730: RADIUS(00006BEE): Config NAS IPv6: ::
Oct  5 11:25:43.730: RADIUS/ENCODE(00006BEE): acct_session_id: 62884
Oct  5 11:25:43.730: RADIUS/ENCODE(00006BEE): Acct-session-id pre-pended with Nas Port = 0/0/2/110.1954
Oct  5 11:25:43.730: RADIUS(00006BEE): Config NAS IP: 0.0.0.0
Oct  5 11:25:43.730: RADIUS(00006BEE): sending
Oct  5 11:25:43.730: RADIUS/ENCODE: Best Local IP-Address 81.20.192.51 for Radius-Server 81.20.192.57
Oct  5 11:25:43.730: RADIUS(00006BEE): Send Access-Request to 81.20.192.57:1812 id 1645/3, len 304
Oct  5 11:25:43.730: RADIUS:  authenticator 03 E3 6B 64 27 79 D9 DE - 4E 58 25 F9 0D C0 F7 E2
Oct  5 11:25:43.730: RADIUS:  User-Name           [1]   31  "0004006e0005:00063408045f3a70"
Oct  5 11:25:43.730: RADIUS:  User-Password       [2]   18  *
Oct  5 11:25:43.730: RADIUS:  NAS-Port-Type       [61]  6   PPPoEoQinQ                [34]
Oct  5 11:25:43.730: RADIUS:  Vendor, Cisco       [26]  22  
Oct  5 11:25:43.730: RADIUS:   cisco-nas-port     [2]   16  "0/0/2/110.1954"
Oct  5 11:25:43.730: RADIUS:  NAS-Port            [5]   6   62884                     
Oct  5 11:25:43.730: RADIUS:  NAS-Port-Id         [87]  16  "0/0/2/110.1954"
Oct  5 11:25:43.730: RADIUS:  Vendor, Cisco       [26]  35  
Oct  5 11:25:43.730: RADIUS:   Cisco AVpair       [1]   29  "circuit-id-tag=0004006e0005"
Oct  5 11:25:43.730: RADIUS:  Vendor, Cisco       [26]  38  
Oct  5 11:25:43.730: RADIUS:   Cisco AVpair       [1]   32  "remote-id-tag=00063408045f3a70"
Oct  5 11:25:43.730: RADIUS:  Vendor, Cisco       [26]  36  
Oct  5 11:25:43.730: RADIUS:   Cisco AVpair       [1]   30  "vendor-class-id-tag=MSFT 5.0"
Oct  5 11:25:43.731: RADIUS:  Service-Type        [6]   6   Outbound                  [5]
Oct  5 11:25:43.731: RADIUS:  NAS-IP-Address      [4]   6   81.20.192.51              
Oct  5 11:25:43.731: RADIUS:  Acct-Session-Id     [44]  33  "0/0/2/110.1954_780000000000F5A4"
Oct  5 11:25:43.731: RADIUS:  Nas-Identifier      [32]  25  "ctd-c5-ISG.ctd-c5.sc.ru"
Oct  5 11:25:43.731: RADIUS:  Event-Timestamp     [55]  6   1317813943                
Oct  5 11:25:43.731: RADIUS(00006BEE): Sending a IPv4 Radius
                                        Packet
Oct  5 11:25:43.731: RADIUS(00006BEE): Started 5 sec timeout
Oct  5 11:25:43.773: RADIUS: Received from id 1645/3 81.20.192.57:1812, Access-Accept, len 85
Oct  5 11:25:43.773: RADIUS:  authenticator BC 46 46 A9 35 F4 C6 72 - 95 B0 33 B6 BE 9E 15 4E
Oct  5 11:25:43.773: RADIUS:  Vendor, Cisco       [26]  45  
Oct  5 11:25:43.773: RADIUS:   Cisco AVpair       [1]   39  "subscriber:accounting-list=ISG-AUTH-1"
Oct  5 11:25:43.773: RADIUS:  Vendor, Cisco       [26]  14  
Oct  5 11:25:43.773: RADIUS:   ssg-account-info   [250] 8   "A10240"
Oct  5 11:25:43.773: RADIUS:  Service-Type        [6]   6   Framed                    [2]
Oct  5 11:25:43.773: RADIUS(00006BEE): Received from id 1645/3
Oct  5 11:25:43.774: SVM [E60005FB/10240]: already downloaded; sharing
Oct  5 11:25:43.774: SVM [E60005FB/10240]: [D5000F32]: client download ok
Oct  5 11:25:43.774: SVM [E60005FB/10240]: [SVM-to-client-msg:D5000F32] locked 0->1
Oct  5 11:25:43.774: SVM [E60005FB/10240]: [PM-Download:D5000F32] locked 0->1
Oct  5 11:25:43.775: SVM [E60005FB/10240]: alloc feature info
Oct  5 11:25:43.775: SVM [E60005FB/10240]: [SVM-Feature-Info:44B18364] locked 0->1
Oct  5 11:25:43.775: SVM [E60005FB/10240]: has Policy info
Oct  5 11:25:43.775: SVM [E60005FB/10240]: [PM-Info:44C4B070] locked 1->2
Oct  5 11:25:43.775: SVM [E60005FB/10240]: populated client
Oct  5 11:25:43.775: SVM [E60005FB/10240]: [PM-Download:D5000F32] unlocked 1->0
Oct  5 11:25:43.775: SVM [E60005FB/10240]: [SVM-to-client-msg:D5000F32] unlocked 1->0
Oct  5 11:25:43.775: SVM [E60005FB/10240]: [PM-Service:44CBCBF8] locked 1->2
Oct  5 11:25:43.776: RADIUS/ENCODE(00006BEE):Orig. component type = Iedge IP SIP
Oct  5 11:25:43.776: RADIUS/ENCODE(00006BEE): Acct-session-id pre-pended with Nas Port = 0/0/2/110.1954
Oct  5 11:25:43.776: RADIUS: Format E value 0xF5A4 for character U with bitmask 0xFFFFFFFF
Oct  5 11:25:43.776: RADIUS: Format E port 0xF5A4 with bit 32 processed
Oct  5 11:25:43.776: RADIUS(00006BEE): Config NAS IP: 0.0.0.0
Oct  5 11:25:43.776: RADIUS(00006BEE): Config NAS IPv6: ::
Oct  5 11:25:43.776: RADIUS(00006BEE): Config NAS IP: 0.0.0.0
Oct  5 11:25:43.776: RADIUS(00006BEE): sending
Oct  5 11:25:43.777: RADIUS/ENCODE: Best Local IP-Address 81.20.192.51 for Radius-Server 81.20.192.57
Oct  5 11:25:43.777: RADIUS(00006BEE): Send Accounting-Request to 81.20.192.57:1813 id 1646/12, len 366
Oct  5 11:25:43.777: RADIUS:  authenticator 1E 54 07 25 29 C3 EA 12 - F9 C2 11 8E 1C E9 1A FD
Oct  5 11:25:43.777: RADIUS:  Acct-Session-Id     [44]  33  "0/0/2/110.1954_780000000000F5A4"
Oct  5 11:25:43.777: RADIUS:  Framed-Protocol     [7]   6   PPP                       [1]
Oct  5 11:25:43.777: RADIUS:  User-Name           [1]   31  "0004006e0005:00063408045f3a70"
Oct  5 11:25:43.777: RADIUS:  Vendor, Cisco       [26]  32  
Oct  5 11:25:43.777: RADIUS:   Cisco AVpair       [1]   26  "connect-progress=Call Up"
Oct  5 11:25:43.777: RADIUS:  Vendor, Cisco       [26]  12  
Oct  5 11:25:43.777: RADIUS:   ssg-control-info   [253] 6   "I0;0"
Oct  5 11:25:43.777: RADIUS:  Vendor, Cisco       [26]  12  
Oct  5 11:25:43.777: RADIUS:   ssg-control-info   [253] 6   "O0;0"
Oct  5 11:25:43.777: RADIUS:  Acct-Authentic      [45]  6   Local                     [2]
Oct  5 11:25:43.777: RADIUS:  Acct-Status-Type    [40]  6   Start                     [1]
Oct  5 11:25:43.777: RADIUS:  NAS-Port-Type       [61]  6   PPPoEoQinQ                [34]
Oct  5 11:25:43.777: RADIUS:  Vendor, Cisco       [26]  22  
Oct  5 11:25:43.777: RADIUS:   cisco-nas-port     [2]   16  "0/0/2/110.1954"
Oct  5 11:25:43.777: RADIUS:  NAS-Port            [5]   6   62884                     
Oct  5 11:25:43.777: RADIUS:  NAS-Port-Id         [87]  16  "0/0/2/110.1954"
Oct  5 11:25:43.777: RADIUS:  Vendor, Cisco       [26]  35  
Oct  5 11:25:43.777: RADIUS:   Cisco AVpair       [1]   29  "circuit-id-tag=0004006e0005"
Oct  5 11:25:43.777: RADIUS:  Vendor, Cisco       [26]  38  
Oct  5 11:25:43.777: RADIUS:   Cisco AVpair       [1]   32  "remote-id-tag=00063408045f3a70"
Oct  5 11:25:43.777: RADIUS:  Vendor, Cisco       [26]  36  
Oct  5 11:25:43.777: RADIUS:   Cisco AVpair       [1]   30  "vendor-class-id-tag=MSFT 5.0"
Oct  5 11:25:43.777: RADIUS:  Service-Type        [6]   6   Framed                    [2]
Oct  5 11:25:43.777: RADIUS:  NAS-IP-Address      [4]   6   81.20.192.51              
Oct  5 11:25:43.777: RADIUS:  Event-Timestamp     [55]  6   1317813943                
Oct  5 11:25:43.777: RADIUS:  Nas-Identifier      [32]  25  "ctd-c5-ISG.ctd-c5.sc.ru"
Oct  5 11:25:43.777: RADIUS:  Acct-Delay-Time     [41]  6   0                         
Oct  5 11:25:43.777: RADIUS(00006BEE): Sending a IPv4 Radius
                                        Packet
Oct  5 11:25:43.778: RADIUS(00006BEE): Started 5 sec timeout
Oct  5 11:25:43.778: SVM [640005FC/CHILD/10240]: [SM-SIP-Apply:640005FC] locked 1->2
Oct  5 11:25:43.778: SVM [E60005FB/10240]: [FM-Bind:88000D7D] locked 1->2
Oct  5 11:25:43.778: SVM [E60005FB/10240]: [SVM-Feature-Info:44B18364] unlocked 1->0
Oct  5 11:25:43.778: SVM [640005FC/CHILD/10240]: alloc feature info
Oct  5 11:25:43.779: SVM [640005FC/CHILD/10240]: [SVM-Feature-Info:44B18364] locked 0->1
Oct  5 11:25:43.779: SVM [E60005FB/10240]: already downloaded; sharing
Oct  5 11:25:43.779: SVM [E60005FB/10240]: already downloaded; sharing
Oct  5 11:25:43.779: SVM [E60005FB/10240]: already downloaded; sharing
Oct  5 11:25:43.779: DHCPD: Callback for workspace (ID=0x42000065)
Oct  5 11:25:43.779: DHCPD: No authentication required. Continue
Oct  5 11:25:43.779: DHCPD: Callback: class '' now specified for client 016c.626d.b5cf.c7
Oct  5 11:25:43.779: DHCPD: Sending notification of DISCOVER:
Oct  5 11:25:43.779:   DHCPD: htype 1 chaddr 6c62.6db5.cfc7
Oct  5 11:25:43.779:   DHCPD: remote id 00063408045f3a70
Oct  5 11:25:43.780:   DHCPD: circuit id 0004006e0005
Oct  5 11:25:43.780:   DHCPD: interface = GigabitEthernet0/0/2.1954110
Oct  5 11:25:43.780:   DHCPD: class id 4d53465420352e30
Oct  5 11:25:43.780: DHCPD: client requests 172.20.125.183.
Oct  5 11:25:43.780: DHCPD: Adding binding to radix tree (172.20.125.183)
Oct  5 11:25:43.780: DHCPD: Adding binding to hash tree
Oct  5 11:25:43.780: DHCPD: assigned IP address 172.20.125.183 to client 016c.626d.b5cf.c7.
Oct  5 11:25:43.782: SVM [E60005FB/10240]: [Accounting-Feature:44CA9574] locked 1->2
Oct  5 11:25:43.783: SVM [640005FC/CHILD/10240]: [FM-Bind:47000C09] locked 1->2
Oct  5 11:25:43.783: SVM [640005FC/CHILD/10240]: [SVM-Feature-Info:44B18364] unlocked 1->0
Oct  5 11:25:43.783: RADIUS/ENCODE(00006BEE):Orig. component type = Iedge IP SIP
Oct  5 11:25:43.783: RADIUS/ENCODE(00006BEE): Acct-session-id pre-pended with Nas Port = 0/0/2/110.1954
Oct  5 11:25:43.783: RADIUS/ENCODE(00006BEE): Acct-session-id pre-pended with Nas Port = 0/0/2/110.1954
Oct  5 11:25:43.783: RADIUS: Format E value 0xF5A4 for character U with bitmask 0xFFFFFFFF
Oct  5 11:25:43.783: RADIUS: Format E port 0xF5A4 with bit 32 processed
Oct  5 11:25:43.783: RADIUS(00006BEE): Config NAS IP: 0.0.0.0
Oct  5 11:25:43.783: RADIUS(00006BEE): Config NAS IPv6: ::
Oct  5 11:25:43.783: RADIUS(00006BEE): Config NAS IP: 0.0.0.0
Oct  5 11:25:43.783: RADIUS(00006BEE): sending
Oct  5 11:25:43.784: RADIUS/ENCODE: Best Local IP-Address 81.20.192.51 for Radius-Server 81.20.192.57
Oct  5 11:25:43.784: RADIUS(00006BEE): Send Accounting-Request to 81.20.192.57:1813 id 1646/13, len 375
Oct  5 11:25:43.784: RADIUS:  authenticator 5C 3B 4C 6F DD 87 1F 7D - 9B EF 8A 4D 63 27 E7 88
Oct  5 11:25:43.784: RADIUS:  Acct-Session-Id     [44]  33  "0/0/2/110.1954_780000000000F5A5"
Oct  5 11:25:43.784: RADIUS:  Framed-Protocol     [7]   6   PPP                       [1]
Oct  5 11:25:43.784: RADIUS:  Vendor, Cisco       [26]  14  
Oct  5 11:25:43.784: RADIUS:   ssg-service-info   [251] 8   "N10240"
Oct  5 11:25:43.784: RADIUS:  Vendor, Cisco       [26]  57  
Oct  5 11:25:43.784: RADIUS:   Cisco AVpair       [1]   51  "parent-session-id=0/0/2/110.1954_780000000000F5A4"
Oct  5 11:25:43.784: RADIUS:  User-Name           [1]   31  "0004006e0005:00063408045f3a70"
Oct  5 11:25:43.784: RADIUS:  Acct-Status-Type    [40]  6   Start                     [1]
Oct  5 11:25:43.784: RADIUS:  NAS-Port-Type       [61]  6   PPPoEoQinQ                [34]
Oct  5 11:25:43.784: RADIUS:  Vendor, Cisco       [26]  22  
Oct  5 11:25:43.784: RADIUS:   cisco-nas-port     [2]   16  "0/0/2/110.1954"
Oct  5 11:25:43.784: RADIUS:  NAS-Port            [5]   6   62884                     
Oct  5 11:25:43.784: RADIUS:  NAS-Port-Id         [87]  16  "0/0/2/110.1954"
Oct  5 11:25:43.784: RADIUS:  Vendor, Cisco       [26]  35  
Oct  5 11:25:43.784: RADIUS:   Cisco AVpair       [1]   29  "circuit-id-tag=0004006e0005"
Oct  5 11:25:43.784: RADIUS:  Vendor, Cisco       [26]  38  
Oct  5 11:25:43.784: RADIUS:   Cisco AVpair       [1]   32  "remote-id-tag=00063408045f3a70"
Oct  5 11:25:43.784: RADIUS:  Vendor, Cisco       [26]  36  
Oct  5 11:25:43.784: RADIUS:   Cisco AVpair       [1]   30  "vendor-class-id-tag=MSFT 5.0"
Oct  5 11:25:43.784: RADIUS:  Service-Type        [6]   6   Framed                    [2]
Oct  5 11:25:43.784: RADIUS:  NAS-IP-Address      [4]   6   81.20.192.51              
Oct  5 11:25:43.784: RADIUS:  Event-Timestamp     [55]  6   1317813943                
Oct  5 11:25:43.784: RADIUS:  Nas-Identifier      [32]  25  "ctd-c5-ISG.ctd-c5.sc.ru"
Oct  5 11:25:43.784: RADIUS:  Acct-Delay-Time     [41]  6   0                         
Oct  5 11:25:43.784: RADIUS(00006BEE): Sending a IPv4 Radius
                                        Packet
Oct  5 11:25:43.785: RADIUS(00006BEE): Started 5 sec timeout
Oct  5 11:25:43.887: RADIUS: Received from id 1646/12 81.20.192.57:1813, Accounting-response, len 20
Oct  5 11:25:43.888: RADIUS:  authenticator D9 18 9E CE 4A 49 04 3A - EB 9D 53 40 E0 77 B9 91
Oct  5 11:25:43.963: RADIUS: Received from id 1646/13 81.20.192.57:1813, Accounting-response, len 20
Oct  5 11:25:43.963: RADIUS:  authenticator F1 CF 02 F9 70 3C 02 BC - 80 64 E8 69 EA D7 8E 80
Oct  5 11:25:45.779: DHCPD: Sending notification of DISCOVER:
Oct  5 11:25:45.779:   DHCPD: htype 1 chaddr 6c62.6db5.cfc7
Oct  5 11:25:45.779:   DHCPD: remote id 00063408045f3a70
Oct  5 11:25:45.779:   DHCPD: circuit id 0004006e0005
Oct  5 11:25:45.779:   DHCPD: interface = GigabitEthernet0/0/2.1954110
Oct  5 11:25:45.779:   DHCPD: class id 4d53465420352e30
Oct  5 11:25:45.780: DHCPD: Found previous server binding
Oct  5 11:25:45.780: DHCPD: requested address 172.20.125.183 has already been assigned.
Oct  5 11:25:45.780: DHCPD: DHCPOFFER notify setup address 172.20.125.183 mask 255.255.224.0
Oct  5 11:25:45.784: DHCPD: Callback for workspace (ID=0x42000065)
Oct  5 11:25:45.784: DHCPD: Callback: switching path now setup for client 016c.626d.b5cf.c7
Oct  5 11:25:45.784: DHCPD: Sending notification of DISCOVER:
Oct  5 11:25:45.784:   DHCPD: htype 1 chaddr 6c62.6db5.cfc7
Oct  5 11:25:45.784:   DHCPD: remote id 00063408045f3a70
Oct  5 11:25:45.784:   DHCPD: circuit id 0004006e0005
Oct  5 11:25:45.784:   DHCPD: interface = GigabitEthernet0/0/2.1954110
Oct  5 11:25:45.784:   DHCPD: class id 4d53465420352e30
Oct  5 11:25:45.784: DHCPD: Found previous server binding
Oct  5 11:25:45.784: DHCPD: requested address 172.20.125.183 has already been assigned.
Oct  5 11:25:45.784: DHCPD: unicast BOOTREPLY output i/f override GigabitEthernet0/0/2.1954110
Oct  5 11:25:45.804: DHCPD: input i/f override GigabitEthernet0/0/2.1954110 for client
Oct  5 11:25:45.804: DHCPD: Sending notification of ASSIGNMENT:
Oct  5 11:25:45.804:  DHCPD: address 172.20.125.183 mask 255.255.224.0
Oct  5 11:25:45.804:   DHCPD: htype 1 chaddr 6c62.6db5.cfc7
Oct  5 11:25:45.804:   DHCPD: remote id 00063408045f3a70
Oct  5 11:25:45.804:   DHCPD: circuit id 0004006e0005
Oct  5 11:25:45.804:   DHCPD: lease time remaining (secs) = 300
Oct  5 11:25:45.804:   DHCPD: interface = GigabitEthernet0/0/2.1954110
Oct  5 11:25:45.804: DHCPD: Updating DPM hdl in DHCP binding for 172.20.125.183 
Oct  5 11:25:45.804:  DHCPD: lease time = 300
Oct  5 11:25:45.804: DHCPD: dhcpd_lookup_route: host = 172.20.125.183
Oct  5 11:25:45.804: DHCPD: dhcpd_lookup_route: index = 114
Oct  5 11:25:45.804: DHCPD: dhcpd_create_and_hash_route: host = 172.20.125.183
Oct  5 11:25:45.804: DHCPD: dhcpd_create_and_hash_route index = 114
Oct  5 11:25:45.804: DHCPD: dhcpd_add_route: lease = 300 
Oct  5 11:25:45.804: DHCPD: unicast BOOTREPLY output i/f override GigabitEthernet0/0/2.1954110
Oct  5 11:25:54.272: DHCPD: checking for expired leases.

















rad_recv: Access-Request packet from host 81.20.192.51 port 1645, id=236, length=301
        User-Name = "000400320001:0106001cf09d7167"
        User-Password = "ISG"
        NAS-Port-Type = PPPoEoQinQ
        Cisco-NAS-Port = "0/0/2/50.1957"
        NAS-Port = 62736
        NAS-Port-Id = "0/0/2/50.1957"
        Cisco-AVPair = "circuit-id-tag=000400320001"
        Cisco-AVPair = "remote-id-tag=0106001cf09d7167"
        Cisco-AVPair = "vendor-class-id-tag=MSFT 5.0"
        Service-Type = Outbound-User
        NAS-IP-Address = 81.20.192.51
        Acct-Session-Id = "0/0/2/50.1957_780000000000F510"
        NAS-Identifier = "ctd-c5-ISG.ctd-c5.sc.ru"
        Event-Timestamp = "Oct  5 2011 14:57:47 MSD"
# Executing section authorize from file /usr/local/etc/raddb/sites-enabled/default
+- entering group authorize {...}
++[preprocess] returns ok
[auth_log]      expand: /usr/local/var/log/radius/radacct/%{Client-IP-Address}/auth-detail-%Y%m%d -> /usr/local/var/log/radius/radacct/81.20.192.51/auth-detail-20111005
[auth_log] /usr/local/var/log/radius/radacct/%{Client-IP-Address}/auth-detail-%Y%m%d expands to /usr/local/var/log/radius/radacct/81.20.192.51/auth-detail-20111005
[auth_log]      expand: %t -> Wed Oct  5 14:57:47 2011
++[auth_log] returns ok
++[chap] returns noop
++[mschap] returns noop
++[files] returns noop
[sql]   expand: %{User-Name} -> 000400320001:0106001cf09d7167
[sql] sql_set_user escaped user --> '000400320001:0106001cf09d7167'
Closing socket 4 as its lifetime has been exceeded
rlm_sql (sql): Trying to (re)connect unconnected handle 4..
rlm_sql (sql): Attempting to connect rlm_sql_oracle #4
rlm_sql (sql): Connected new DB handle, #4
rlm_sql (sql): Reserving sql socket id: 4
rlm_sql (sql): got socket 4 after skipping 0 unconnected handles, tried to reconnect 1 though
[sql]   expand: SELECT id,UserName,Attribute,Value,op FROM radcheck WHERE Username = '%{SQL-User-Name}' ORDER BY id -> SELECT id,UserName,Attribute,Value,op FROM radcheck WHERE Username = '000400320001:0106001cf09d7167' ORDER BY id
[sql] User found in radcheck table
[sql]   expand: SELECT id,UserName,Attribute,Value,op FROM radreply WHERE Username = '%{SQL-User-Name}' ORDER BY id -> SELECT id,UserName,Attribute,Value,op FROM radreply WHERE Username = '000400320001:0106001cf09d7167' ORDER BY id
[sql]   expand: SELECT GroupName FROM radusergroup WHERE UserName='%{SQL-User-Name}' -> SELECT GroupName FROM radusergroup WHERE UserName='000400320001:0106001cf09d7167'
[sql]   expand: SELECT radgroupcheck.id,radgroupcheck.GroupName,radgroupcheck.Attribute,radgroupcheck.Value,radgroupcheck.op  FROM radgroupcheck,radusergroup WHERE radusergroup.Username = '%{SQL-User-Name}' AND radusergroup.GroupName = radgroupcheck.GroupName ORDER BY radgroupcheck.id -> SELECT radgroupcheck.id,radgroupcheck.GroupName,radgroupcheck.Attribute,radgroupcheck.Value,radgroupcheck.op  FROM radgroupcheck,radusergroup WHERE radusergroup.Username = '000400320001:0106001cf09d7167' AND radusergroup.GroupName = radgroupcheck.GroupName ORDER BY radgroupcheck.id
[sql] User found in group phys2
[sql]   expand: SELECT radgroupreply.id,radgroupreply.GroupName,radgroupreply.Attribute,radgroupreply.Value,radgroupreply.op  FROM radgroupreply,radusergroup WHERE radusergroup.Username = '%{SQL-User-Name}' AND radusergroup.GroupName = radgroupreply.GroupName ORDER BY radgroupreply.id -> SELECT radgroupreply.id,radgroupreply.GroupName,radgroupreply.Attribute,radgroupreply.Value,radgroupreply.op  FROM radgroupreply,radusergroup WHERE radusergroup.Username = '000400320001:0106001cf09d7167' AND radusergroup.GroupName = radgroupreply.GroupName ORDER BY radgroupreply.id
rlm_sql (sql): Released sql socket id: 4
++[sql] returns ok
++[expiration] returns noop
++[logintime] returns noop
++[pap] returns updated
Found Auth-Type = PAP
# Executing group from file /usr/local/etc/raddb/sites-enabled/default
+- entering group PAP {...}
[pap] login attempt with password "ISG"
[pap] Using clear text password "ISG"
[pap] User authenticated successfully
++[pap] returns ok
Login OK: [000400320001:0106001cf09d7167] (from client 81.20.192.51 port 62736)
# Executing section post-auth from file /usr/local/etc/raddb/sites-enabled/default
+- entering group post-auth {...}
[sql]   expand: %{User-Name} -> 000400320001:0106001cf09d7167
[sql] sql_set_user escaped user --> '000400320001:0106001cf09d7167'
++[sql] returns noop
[sql_log] Processing sql_log_postauth
[sql_log]       expand: %{User-Name} -> 000400320001:0106001cf09d7167
[sql_log]       expand: %{%{User-Name}:-DEFAULT} -> 000400320001:0106001cf09d7167
[sql_log] sql_set_user escaped user --> '000400320001:0106001cf09d7167'
[sql_log] WARNING: Deprecated conditional expansion ":-".  See "man unlang" for details
[sql_log]       expand: INSERT INTO radpostauth                          (username, pass, reply, authdate) VALUES                        ('%{User-Name}', '%{User-Password:-Chap-Password}',                  '%{reply:Packet-Type}', '%S'); -> INSERT INTO radpostauth                       (username, pass, reply, authdate) VALUES                             ('000400320001:0106001cf09d7167', 'ISG',                'Access-Accept', '2011-10-05 14:57:47');
[sql_log]       expand: /usr/local/var/log/radius/radacct/sql-relay -> /usr/local/var/log/radius/radacct/sql-relay
++[sql_log] returns ok
++[exec] returns noop
Sending Access-Accept of id 236 to 81.20.192.51 port 1645
        Cisco-Account-Info += "A30720"
        Service-Type = Framed-User
        Cisco-AVPair = "lcp:interface-config=description Test oldswitch"
Finished request 0.
Going to the next request
Waking up in 4.9 seconds.
Cleaning up request 0 ID 236 with timestamp +16
Ready to process requests.
rad_recv: Access-Request packet from host 81.20.192.51 port 1645, id=237, length=301
        User-Name = "000400320001:0106001cf09d7167"
        User-Password = "ISG"
        NAS-Port-Type = PPPoEoQinQ
        Cisco-NAS-Port = "0/0/2/50.1957"
        NAS-Port = 62737
        NAS-Port-Id = "0/0/2/50.1957"
        Cisco-AVPair = "circuit-id-tag=000400320001"
        Cisco-AVPair = "remote-id-tag=0106001cf09d7167"
        Cisco-AVPair = "vendor-class-id-tag=MSFT 5.0"
        Service-Type = Outbound-User
        NAS-IP-Address = 81.20.192.51
        Acct-Session-Id = "0/0/2/50.1957_780000000000F511"
        NAS-Identifier = "ctd-c5-ISG.ctd-c5.sc.ru"
        Event-Timestamp = "Oct  5 2011 14:57:59 MSD"
# Executing section authorize from file /usr/local/etc/raddb/sites-enabled/default
+- entering group authorize {...}
++[preprocess] returns ok
[auth_log]      expand: /usr/local/var/log/radius/radacct/%{Client-IP-Address}/auth-detail-%Y%m%d -> /usr/local/var/log/radius/radacct/81.20.192.51/auth-detail-20111005
[auth_log] /usr/local/var/log/radius/radacct/%{Client-IP-Address}/auth-detail-%Y%m%d expands to /usr/local/var/log/radius/radacct/81.20.192.51/auth-detail-20111005
[auth_log]      expand: %t -> Wed Oct  5 14:57:59 2011
++[auth_log] returns ok
++[chap] returns noop
++[mschap] returns noop
++[files] returns noop
[sql]   expand: %{User-Name} -> 000400320001:0106001cf09d7167
[sql] sql_set_user escaped user --> '000400320001:0106001cf09d7167'
Closing socket 3 as its lifetime has been exceeded
rlm_sql (sql): Trying to (re)connect unconnected handle 3..
rlm_sql (sql): Attempting to connect rlm_sql_oracle #3
rlm_sql (sql): Connected new DB handle, #3
rlm_sql (sql): Reserving sql socket id: 3
rlm_sql (sql): got socket 3 after skipping 0 unconnected handles, tried to reconnect 1 though
[sql]   expand: SELECT id,UserName,Attribute,Value,op FROM radcheck WHERE Username = '%{SQL-User-Name}' ORDER BY id -> SELECT id,UserName,Attribute,Value,op FROM radcheck WHERE Username = '000400320001:0106001cf09d7167' ORDER BY id
[sql] User found in radcheck table
[sql]   expand: SELECT id,UserName,Attribute,Value,op FROM radreply WHERE Username = '%{SQL-User-Name}' ORDER BY id -> SELECT id,UserName,Attribute,Value,op FROM radreply WHERE Username = '000400320001:0106001cf09d7167' ORDER BY id
[sql]   expand: SELECT GroupName FROM radusergroup WHERE UserName='%{SQL-User-Name}' -> SELECT GroupName FROM radusergroup WHERE UserName='000400320001:0106001cf09d7167'
[sql]   expand: SELECT radgroupcheck.id,radgroupcheck.GroupName,radgroupcheck.Attribute,radgroupcheck.Value,radgroupcheck.op  FROM radgroupcheck,radusergroup WHERE radusergroup.Username = '%{SQL-User-Name}' AND radusergroup.GroupName = radgroupcheck.GroupName ORDER BY radgroupcheck.id -> SELECT radgroupcheck.id,radgroupcheck.GroupName,radgroupcheck.Attribute,radgroupcheck.Value,radgroupcheck.op  FROM radgroupcheck,radusergroup WHERE radusergroup.Username = '000400320001:0106001cf09d7167' AND radusergroup.GroupName = radgroupcheck.GroupName ORDER BY radgroupcheck.id
[sql] User found in group phys2
[sql]   expand: SELECT radgroupreply.id,radgroupreply.GroupName,radgroupreply.Attribute,radgroupreply.Value,radgroupreply.op  FROM radgroupreply,radusergroup WHERE radusergroup.Username = '%{SQL-User-Name}' AND radusergroup.GroupName = radgroupreply.GroupName ORDER BY radgroupreply.id -> SELECT radgroupreply.id,radgroupreply.GroupName,radgroupreply.Attribute,radgroupreply.Value,radgroupreply.op  FROM radgroupreply,radusergroup WHERE radusergroup.Username = '000400320001:0106001cf09d7167' AND radusergroup.GroupName = radgroupreply.GroupName ORDER BY radgroupreply.id
rlm_sql (sql): Released sql socket id: 3
++[sql] returns ok
++[expiration] returns noop
++[logintime] returns noop
++[pap] returns updated
Found Auth-Type = PAP
# Executing group from file /usr/local/etc/raddb/sites-enabled/default
+- entering group PAP {...}
[pap] login attempt with password "ISG"
[pap] Using clear text password "ISG"
[pap] User authenticated successfully
++[pap] returns ok
Login OK: [000400320001:0106001cf09d7167] (from client 81.20.192.51 port 62737)
# Executing section post-auth from file /usr/local/etc/raddb/sites-enabled/default
+- entering group post-auth {...}
[sql]   expand: %{User-Name} -> 000400320001:0106001cf09d7167
[sql] sql_set_user escaped user --> '000400320001:0106001cf09d7167'
++[sql] returns noop
[sql_log] Processing sql_log_postauth
[sql_log]       expand: %{User-Name} -> 000400320001:0106001cf09d7167
[sql_log]       expand: %{%{User-Name}:-DEFAULT} -> 000400320001:0106001cf09d7167
[sql_log] sql_set_user escaped user --> '000400320001:0106001cf09d7167'
[sql_log] WARNING: Deprecated conditional expansion ":-".  See "man unlang" for details
[sql_log]       expand: INSERT INTO radpostauth                          (username, pass, reply, authdate) VALUES                        ('%{User-Name}', '%{User-Password:-Chap-Password}',                  '%{reply:Packet-Type}', '%S'); -> INSERT INTO radpostauth                       (username, pass, reply, authdate) VALUES                             ('000400320001:0106001cf09d7167', 'ISG',                'Access-Accept', '2011-10-05 14:57:59');
[sql_log]       expand: /usr/local/var/log/radius/radacct/sql-relay -> /usr/local/var/log/radius/radacct/sql-relay
++[sql_log] returns ok
++[exec] returns noop
Sending Access-Accept of id 237 to 81.20.192.51 port 1645
        Cisco-Account-Info += "A30720"
        Service-Type = Framed-User
        Cisco-AVPair = "lcp:interface-config=description Test oldswitch"
Finished request 1.
Going to the next request
Waking up in 4.9 seconds.















rad_recv: Access-Request packet from host 81.20.192.51 port 1645, id=239, length=304
        User-Name = "000400a20004:00063408043a3fb0"
        User-Password = "ISG"
        NAS-Port-Type = PPPoEoQinQ
        Cisco-NAS-Port = "0/0/2/162.1954"
        NAS-Port = 62739
        NAS-Port-Id = "0/0/2/162.1954"
        Cisco-AVPair = "circuit-id-tag=000400a20004"
        Cisco-AVPair = "remote-id-tag=00063408043a3fb0"
        Cisco-AVPair = "vendor-class-id-tag=MSFT 5.0"
        Service-Type = Outbound-User
        NAS-IP-Address = 81.20.192.51
        Acct-Session-Id = "0/0/2/162.1954_780000000000F513"
        NAS-Identifier = "ctd-c5-ISG.ctd-c5.sc.ru"
        Event-Timestamp = "Oct  5 2011 14:58:34 MSD"
# Executing section authorize from file /usr/local/etc/raddb/sites-enabled/default
+- entering group authorize {...}
++[preprocess] returns ok
[auth_log]      expand: /usr/local/var/log/radius/radacct/%{Client-IP-Address}/auth-detail-%Y%m%d -> /usr/local/var/log/radius/radacct/81.20.192.51/auth-detail-20111005
[auth_log] /usr/local/var/log/radius/radacct/%{Client-IP-Address}/auth-detail-%Y%m%d expands to /usr/local/var/log/radius/radacct/81.20.192.51/auth-detail-20111005
[auth_log]      expand: %t -> Wed Oct  5 14:58:34 2011
++[auth_log] returns ok
++[chap] returns noop
++[mschap] returns noop
++[files] returns noop
[sql]   expand: %{User-Name} -> 000400a20004:00063408043a3fb0
[sql] sql_set_user escaped user --> '000400a20004:00063408043a3fb0'
Closing socket 1 as its lifetime has been exceeded
rlm_sql (sql): Trying to (re)connect unconnected handle 1..
rlm_sql (sql): Attempting to connect rlm_sql_oracle #1
rlm_sql (sql): Connected new DB handle, #1
rlm_sql (sql): Reserving sql socket id: 1
rlm_sql (sql): got socket 1 after skipping 0 unconnected handles, tried to reconnect 1 though
[sql]   expand: SELECT id,UserName,Attribute,Value,op FROM radcheck WHERE Username = '%{SQL-User-Name}' ORDER BY id -> SELECT id,UserName,Attribute,Value,op FROM radcheck WHERE Username = '000400a20004:00063408043a3fb0' ORDER BY id
[sql] User found in radcheck table
[sql]   expand: SELECT id,UserName,Attribute,Value,op FROM radreply WHERE Username = '%{SQL-User-Name}' ORDER BY id -> SELECT id,UserName,Attribute,Value,op FROM radreply WHERE Username = '000400a20004:00063408043a3fb0' ORDER BY id
[sql]   expand: SELECT GroupName FROM radusergroup WHERE UserName='%{SQL-User-Name}' -> SELECT GroupName FROM radusergroup WHERE UserName='000400a20004:00063408043a3fb0'
[sql]   expand: SELECT radgroupcheck.id,radgroupcheck.GroupName,radgroupcheck.Attribute,radgroupcheck.Value,radgroupcheck.op  FROM radgroupcheck,radusergroup WHERE radusergroup.Username = '%{SQL-User-Name}' AND radusergroup.GroupName = radgroupcheck.GroupName ORDER BY radgroupcheck.id -> SELECT radgroupcheck.id,radgroupcheck.GroupName,radgroupcheck.Attribute,radgroupcheck.Value,radgroupcheck.op  FROM radgroupcheck,radusergroup WHERE radusergroup.Username = '000400a20004:00063408043a3fb0' AND radusergroup.GroupName = radgroupcheck.GroupName ORDER BY radgroupcheck.id
[sql] User found in group phys2
[sql]   expand: SELECT radgroupreply.id,radgroupreply.GroupName,radgroupreply.Attribute,radgroupreply.Value,radgroupreply.op  FROM radgroupreply,radusergroup WHERE radusergroup.Username = '%{SQL-User-Name}' AND radusergroup.GroupName = radgroupreply.GroupName ORDER BY radgroupreply.id -> SELECT radgroupreply.id,radgroupreply.GroupName,radgroupreply.Attribute,radgroupreply.Value,radgroupreply.op  FROM radgroupreply,radusergroup WHERE radusergroup.Username = '000400a20004:00063408043a3fb0' AND radusergroup.GroupName = radgroupreply.GroupName ORDER BY radgroupreply.id
rlm_sql (sql): Released sql socket id: 1
++[sql] returns ok
++[expiration] returns noop
++[logintime] returns noop
++[pap] returns updated
Found Auth-Type = PAP
# Executing group from file /usr/local/etc/raddb/sites-enabled/default
+- entering group PAP {...}
[pap] login attempt with password "ISG"
[pap] Using clear text password "ISG"
[pap] User authenticated successfully
++[pap] returns ok
Login OK: [000400a20004:00063408043a3fb0] (from client 81.20.192.51 port 62739)
# Executing section post-auth from file /usr/local/etc/raddb/sites-enabled/default
+- entering group post-auth {...}
[sql]   expand: %{User-Name} -> 000400a20004:00063408043a3fb0
[sql] sql_set_user escaped user --> '000400a20004:00063408043a3fb0'
++[sql] returns noop
[sql_log] Processing sql_log_postauth
[sql_log]       expand: %{User-Name} -> 000400a20004:00063408043a3fb0
[sql_log]       expand: %{%{User-Name}:-DEFAULT} -> 000400a20004:00063408043a3fb0
[sql_log] sql_set_user escaped user --> '000400a20004:00063408043a3fb0'
[sql_log] WARNING: Deprecated conditional expansion ":-".  See "man unlang" for details
[sql_log]       expand: INSERT INTO radpostauth                          (username, pass, reply, authdate) VALUES                        ('%{User-Name}', '%{User-Password:-Chap-Password}',                  '%{reply:Packet-Type}', '%S'); -> INSERT INTO radpostauth                       (username, pass, reply, authdate) VALUES                             ('000400a20004:00063408043a3fb0', 'ISG',                'Access-Accept', '2011-10-05 14:58:34');
[sql_log]       expand: /usr/local/var/log/radius/radacct/sql-relay -> /usr/local/var/log/radius/radacct/sql-relay
++[sql_log] returns ok
++[exec] returns noop
Sending Access-Accept of id 239 to 81.20.192.51 port 1645
        Cisco-AVPair += "subscriber:accounting-list=ISG-AUTH-1"
        Cisco-Account-Info += "A20480"
        Service-Type = Framed-User
Finished request 3.
Going to the next request
Waking up in 4.9 seconds.

rad_recv: Accounting-Request packet from host 81.20.192.51 port 1646, id=118, length=366
        Acct-Session-Id = "0/0/2/162.1954_780000000000F513"
        Framed-Protocol = PPP
        User-Name = "000400a20004:00063408043a3fb0"
        Cisco-AVPair = "connect-progress=Call Up"
        Cisco-Control-Info = "I0;0"
        Cisco-Control-Info = "O0;0"
        Acct-Authentic = Local
        Acct-Status-Type = Start
        NAS-Port-Type = PPPoEoQinQ
        Cisco-NAS-Port = "0/0/2/162.1954"
        NAS-Port = 62739
        NAS-Port-Id = "0/0/2/162.1954"
        Cisco-AVPair = "circuit-id-tag=000400a20004"
        Cisco-AVPair = "remote-id-tag=00063408043a3fb0"
        Cisco-AVPair = "vendor-class-id-tag=MSFT 5.0"
        Service-Type = Framed-User
        NAS-IP-Address = 81.20.192.51
        Event-Timestamp = "Oct  5 2011 14:58:34 MSD"
        NAS-Identifier = "ctd-c5-ISG.ctd-c5.sc.ru"
        Acct-Delay-Time = 0
# Executing section preacct from file /usr/local/etc/raddb/sites-enabled/default
+- entering group preacct {...}
++[preprocess] returns ok
[acct_unique] Hashing 'NAS-Port = 62739,Client-IP-Address = 81.20.192.51,NAS-IP-Address = 81.20.192.51,Acct-Session-Id = "0/0/2/162.1954_780000000000F513",User-Name = "000400a20004:00063408043a3fb0"'
[acct_unique] Acct-Unique-Session-ID = "09c99fe0badbb88d".
++[acct_unique] returns ok
++[files] returns noop
# Executing section accounting from file /usr/local/etc/raddb/sites-enabled/default
+- entering group accounting {...}
[detail]        expand: /usr/local/var/log/radius/radacct/%{Client-IP-Address}/detail-%Y%m%d -> /usr/local/var/log/radius/radacct/81.20.192.51/detail-20111005
[detail] /usr/local/var/log/radius/radacct/%{Client-IP-Address}/detail-%Y%m%d expands to /usr/local/var/log/radius/radacct/81.20.192.51/detail-20111005
[detail]        expand: %t -> Wed Oct  5 14:58:34 2011
++[detail] returns ok
++[unix] returns ok
[sradutmp]      expand: /usr/local/var/log/radius/sradutmp -> /usr/local/var/log/radius/sradutmp
[sradutmp]      expand: %{User-Name} -> 000400a20004:00063408043a3fb0
++[sradutmp] returns ok
[sql]   expand: %{User-Name} -> 000400a20004:00063408043a3fb0
[sql] sql_set_user escaped user --> '000400a20004:00063408043a3fb0'
[sql]   expand: INSERT into radacct (RadAcctId, AcctSessionId, AcctUniqueId, UserName, Realm, NASIPAddress, NASPortId, NASPortType, AcctStartTime, AcctStopTime, AcctSessionTime, AcctAuthentic, ConnectInfo_start, ConnectInfo_stop, AcctInputOctets, AcctOutputOctets, CalledStationId, CallingStationId, AcctTerminateCause, ServiceType, FramedProtocol, FramedIPAddress, AcctStartDelay, AcctStopDelay, XAscendSessionSvrKey)  VALUES('', '%{Acct-Session-Id}', '%{Acct-Unique-Session-Id}', '%{SQL-User-Name}', '%{Realm}', '%{NAS-IP-Address}', '%{NAS-Port-Id}', '%{NAS-Port-Type}', TO_DATE('%S','yyyy-mm-dd hh24:mi:ss'), NULL, '0', '%{Acct-Authentic}', '%{Connect-Info}', '', '0', '0', '%{Called-Station-Id}', '%{Calling-Station-Id}', '', '%{Service-Type}', '%{Framed-Protocol}', '%{Framed-IP-Address}', '%{Acct-Delay-Time}', '0', '%{X-Ascend-Session-Svr-Key}') -> INSERT into radacct (RadAcctId, AcctSessionId, AcctUniqueId, UserName, Realm, NASIPAddress, NASPortId, NASPortType, AcctStartTime, AcctStopTime, AcctSessionTime, AcctAu
Closing socket 0 as its lifetime has been exceeded
rlm_sql (sql): Trying to (re)connect unconnected handle 0..
rlm_sql (sql): Attempting to connect rlm_sql_oracle #0
rlm_sql (sql): Connected new DB handle, #0
rlm_sql (sql): Reserving sql socket id: 0
rlm_sql (sql): got socket 0 after skipping 0 unconnected handles, tried to reconnect 1 though
rlm_sql (sql): Released sql socket id: 0
++[sql] returns ok
[sql_log] Processing sql_log_accounting
[sql_log]       expand: %{User-Name} -> 000400a20004:00063408043a3fb0
[sql_log]       expand: %{%{User-Name}:-DEFAULT} -> 000400a20004:00063408043a3fb0
[sql_log] sql_set_user escaped user --> '000400a20004:00063408043a3fb0'
[sql_log]       expand: INSERT INTO radacct (AcctSessionId, UserName,    NASIPAddress, FramedIPAddress, AcctStartTime, AcctStopTime,     AcctSessionTime, AcctTerminateCause) VALUES                          ('%{Acct-Session-Id}', '%{User-Name}', '%{NAS-IP-Address}',     '%{Framed-IP-Address}', '%S', '0', '0', ''); -> INSERT INTO radacct (AcctSessionId, UserName,        NASIPAddress, FramedIPAddress, AcctStartTime, AcctStopTime,     AcctSessionTime, AcctTerminateCause) VALUES                          ('0/0/2/162.1954_780000000000F513', '000400a20004:00063408043a3fb0', '81.20.192.51',    '', '2011-10-05 14:58:34', '0', '0', '');
[sql_log]       expand: /usr/local/var/log/radius/radacct/sql-relay -> /usr/local/var/log/radius/radacct/sql-relay
++[sql_log] returns ok
++[exec] returns noop
[attr_filter.accounting_response]       expand: %{User-Name} -> 000400a20004:00063408043a3fb0
 attr_filter: Matched entry DEFAULT at line 12
++[attr_filter.accounting_response] returns updated
Sending Accounting-Response of id 118 to 81.20.192.51 port 1646
Finished request 4.
Cleaning up request 4 ID 118 with timestamp +63
Going to the next request
Waking up in 4.6 seconds.







rad_recv: Accounting-Request packet from host 81.20.192.51 port 1646, id=119, length=375
        Acct-Session-Id = "0/0/2/162.1954_780000000000F514"
        Framed-Protocol = PPP
        Cisco-Service-Info = "N20480"
        Cisco-AVPair = "parent-session-id=0/0/2/162.1954_780000000000F513"
        User-Name = "000400a20004:00063408043a3fb0"
        Acct-Status-Type = Start
        NAS-Port-Type = PPPoEoQinQ
        Cisco-NAS-Port = "0/0/2/162.1954"
        NAS-Port = 62739
        NAS-Port-Id = "0/0/2/162.1954"
        Cisco-AVPair = "circuit-id-tag=000400a20004"
        Cisco-AVPair = "remote-id-tag=00063408043a3fb0"
        Cisco-AVPair = "vendor-class-id-tag=MSFT 5.0"
        Service-Type = Framed-User
        NAS-IP-Address = 81.20.192.51
        Event-Timestamp = "Oct  5 2011 14:58:34 MSD"
        NAS-Identifier = "ctd-c5-ISG.ctd-c5.sc.ru"
        Acct-Delay-Time = 0
# Executing section preacct from file /usr/local/etc/raddb/sites-enabled/default
+- entering group preacct {...}
++[preprocess] returns ok
[acct_unique] Hashing 'NAS-Port = 62739,Client-IP-Address = 81.20.192.51,NAS-IP-Address = 81.20.192.51,Acct-Session-Id = "0/0/2/162.1954_780000000000F514",User-Name = "000400a20004:00063408043a3fb0"'
[acct_unique] Acct-Unique-Session-ID = "bdd96fe6fbd8692b".
++[acct_unique] returns ok
++[files] returns noop
# Executing section accounting from file /usr/local/etc/raddb/sites-enabled/default
+- entering group accounting {...}
[detail]        expand: /usr/local/var/log/radius/radacct/%{Client-IP-Address}/detail-%Y%m%d -> /usr/local/var/log/radius/radacct/81.20.192.51/detail-20111005
[detail] /usr/local/var/log/radius/radacct/%{Client-IP-Address}/detail-%Y%m%d expands to /usr/local/var/log/radius/radacct/81.20.192.51/detail-20111005
[detail]        expand: %t -> Wed Oct  5 14:58:35 2011
++[detail] returns ok
++[unix] returns ok
[sradutmp]      expand: /usr/local/var/log/radius/sradutmp -> /usr/local/var/log/radius/sradutmp
[sradutmp]      expand: %{User-Name} -> 000400a20004:00063408043a3fb0
++[sradutmp] returns ok
[sql]   expand: %{User-Name} -> 000400a20004:00063408043a3fb0
[sql] sql_set_user escaped user --> '000400a20004:00063408043a3fb0'
[sql]   expand: INSERT into radacct (RadAcctId, AcctSessionId, AcctUniqueId, UserName, Realm, NASIPAddress, NASPortId, NASPortType, AcctStartTime, AcctStopTime, AcctSessionTime, AcctAuthentic, ConnectInfo_start, ConnectInfo_stop, AcctInputOctets, AcctOutputOctets, CalledStationId, CallingStationId, AcctTerminateCause, ServiceType, FramedProtocol, FramedIPAddress, AcctStartDelay, AcctStopDelay, XAscendSessionSvrKey)  VALUES('', '%{Acct-Session-Id}', '%{Acct-Unique-Session-Id}', '%{SQL-User-Name}', '%{Realm}', '%{NAS-IP-Address}', '%{NAS-Port-Id}', '%{NAS-Port-Type}', TO_DATE('%S','yyyy-mm-dd hh24:mi:ss'), NULL, '0', '%{Acct-Authentic}', '%{Connect-Info}', '', '0', '0', '%{Called-Station-Id}', '%{Calling-Station-Id}', '', '%{Service-Type}', '%{Framed-Protocol}', '%{Framed-IP-Address}', '%{Acct-Delay-Time}', '0', '%{X-Ascend-Session-Svr-Key}') -> INSERT into radacct (RadAcctId, AcctSessionId, AcctUniqueId, UserName, Realm, NASIPAddress, NASPortId, NASPortType, AcctStartTime, AcctStopTime, AcctSessionTime, AcctAu
Closing socket 4 as its lifetime has been exceeded
rlm_sql (sql): Trying to (re)connect unconnected handle 4..
rlm_sql (sql): Attempting to connect rlm_sql_oracle #4
rlm_sql (sql): Connected new DB handle, #4
rlm_sql (sql): Reserving sql socket id: 4
rlm_sql (sql): got socket 4 after skipping 0 unconnected handles, tried to reconnect 1 though
rlm_sql (sql): Released sql socket id: 4
++[sql] returns ok
[sql_log] Processing sql_log_accounting
[sql_log]       expand: %{User-Name} -> 000400a20004:00063408043a3fb0
[sql_log]       expand: %{%{User-Name}:-DEFAULT} -> 000400a20004:00063408043a3fb0
[sql_log] sql_set_user escaped user --> '000400a20004:00063408043a3fb0'
[sql_log]       expand: INSERT INTO radacct (AcctSessionId, UserName,    NASIPAddress, FramedIPAddress, AcctStartTime, AcctStopTime,     AcctSessionTime, AcctTerminateCause) VALUES                          ('%{Acct-Session-Id}', '%{User-Name}', '%{NAS-IP-Address}',     '%{Framed-IP-Address}', '%S', '0', '0', ''); -> INSERT INTO radacct (AcctSessionId, UserName,        NASIPAddress, FramedIPAddress, AcctStartTime, AcctStopTime,     AcctSessionTime, AcctTerminateCause) VALUES                          ('0/0/2/162.1954_780000000000F514', '000400a20004:00063408043a3fb0', '81.20.192.51',    '', '2011-10-05 14:58:35', '0', '0', '');
[sql_log]       expand: /usr/local/var/log/radius/radacct/sql-relay -> /usr/local/var/log/radius/radacct/sql-relay
++[sql_log] returns ok
++[exec] returns noop
[attr_filter.accounting_response]       expand: %{User-Name} -> 000400a20004:00063408043a3fb0
 attr_filter: Matched entry DEFAULT at line 12
++[attr_filter.accounting_response] returns updated
Sending Accounting-Response of id 119 to 81.20.192.51 port 1646
Finished request 5.
Cleaning up request 5 ID 119 with timestamp +64
Going to the next request
Waking up in 4.5 seconds.
Cleaning up request 3 ID 239 with timestamp +63
Ready to process requests.



















rad_recv: Access-Request packet from host 81.20.192.51 port 1645, id=240, length=301
        User-Name = "000400320001:0106001cf09d7167"
        User-Password = "ISG"
        NAS-Port-Type = PPPoEoQinQ
        Cisco-NAS-Port = "0/0/2/50.1957"
        NAS-Port = 62741
        NAS-Port-Id = "0/0/2/50.1957"
        Cisco-AVPair = "circuit-id-tag=000400320001"
        Cisco-AVPair = "remote-id-tag=0106001cf09d7167"
        Cisco-AVPair = "vendor-class-id-tag=MSFT 5.0"
        Service-Type = Outbound-User
        NAS-IP-Address = 81.20.192.51
        Acct-Session-Id = "0/0/2/50.1957_780000000000F515"
        NAS-Identifier = "ctd-c5-ISG.ctd-c5.sc.ru"
        Event-Timestamp = "Oct  5 2011 14:58:54 MSD"
# Executing section authorize from file /usr/local/etc/raddb/sites-enabled/default
+- entering group authorize {...}
++[preprocess] returns ok
[auth_log]      expand: /usr/local/var/log/radius/radacct/%{Client-IP-Address}/auth-detail-%Y%m%d -> /usr/local/var/log/radius/radacct/81.20.192.51/auth-detail-20111005
[auth_log] /usr/local/var/log/radius/radacct/%{Client-IP-Address}/auth-detail-%Y%m%d expands to /usr/local/var/log/radius/radacct/81.20.192.51/auth-detail-20111005
[auth_log]      expand: %t -> Wed Oct  5 14:58:55 2011
++[auth_log] returns ok
++[chap] returns noop
++[mschap] returns noop
++[files] returns noop
[sql]   expand: %{User-Name} -> 000400320001:0106001cf09d7167
[sql] sql_set_user escaped user --> '000400320001:0106001cf09d7167'
Closing socket 3 as its lifetime has been exceeded
rlm_sql (sql): Trying to (re)connect unconnected handle 3..
rlm_sql (sql): Attempting to connect rlm_sql_oracle #3
rlm_sql (sql): Connected new DB handle, #3
rlm_sql (sql): Reserving sql socket id: 3
rlm_sql (sql): got socket 3 after skipping 0 unconnected handles, tried to reconnect 1 though
[sql]   expand: SELECT id,UserName,Attribute,Value,op FROM radcheck WHERE Username = '%{SQL-User-Name}' ORDER BY id -> SELECT id,UserName,Attribute,Value,op FROM radcheck WHERE Username = '000400320001:0106001cf09d7167' ORDER BY id
[sql] User found in radcheck table
[sql]   expand: SELECT id,UserName,Attribute,Value,op FROM radreply WHERE Username = '%{SQL-User-Name}' ORDER BY id -> SELECT id,UserName,Attribute,Value,op FROM radreply WHERE Username = '000400320001:0106001cf09d7167' ORDER BY id
[sql]   expand: SELECT GroupName FROM radusergroup WHERE UserName='%{SQL-User-Name}' -> SELECT GroupName FROM radusergroup WHERE UserName='000400320001:0106001cf09d7167'
[sql]   expand: SELECT radgroupcheck.id,radgroupcheck.GroupName,radgroupcheck.Attribute,radgroupcheck.Value,radgroupcheck.op  FROM radgroupcheck,radusergroup WHERE radusergroup.Username = '%{SQL-User-Name}' AND radusergroup.GroupName = radgroupcheck.GroupName ORDER BY radgroupcheck.id -> SELECT radgroupcheck.id,radgroupcheck.GroupName,radgroupcheck.Attribute,radgroupcheck.Value,radgroupcheck.op  FROM radgroupcheck,radusergroup WHERE radusergroup.Username = '000400320001:0106001cf09d7167' AND radusergroup.GroupName = radgroupcheck.GroupName ORDER BY radgroupcheck.id
[sql] User found in group phys2
[sql]   expand: SELECT radgroupreply.id,radgroupreply.GroupName,radgroupreply.Attribute,radgroupreply.Value,radgroupreply.op  FROM radgroupreply,radusergroup WHERE radusergroup.Username = '%{SQL-User-Name}' AND radusergroup.GroupName = radgroupreply.GroupName ORDER BY radgroupreply.id -> SELECT radgroupreply.id,radgroupreply.GroupName,radgroupreply.Attribute,radgroupreply.Value,radgroupreply.op  FROM radgroupreply,radusergroup WHERE radusergroup.Username = '000400320001:0106001cf09d7167' AND radusergroup.GroupName = radgroupreply.GroupName ORDER BY radgroupreply.id
rlm_sql (sql): Released sql socket id: 3
++[sql] returns ok
++[expiration] returns noop
++[logintime] returns noop
++[pap] returns updated
Found Auth-Type = PAP
# Executing group from file /usr/local/etc/raddb/sites-enabled/default
+- entering group PAP {...}
[pap] login attempt with password "ISG"
[pap] Using clear text password "ISG"
[pap] User authenticated successfully
++[pap] returns ok
Login OK: [000400320001:0106001cf09d7167] (from client 81.20.192.51 port 62741)
# Executing section post-auth from file /usr/local/etc/raddb/sites-enabled/default
+- entering group post-auth {...}
[sql]   expand: %{User-Name} -> 000400320001:0106001cf09d7167
[sql] sql_set_user escaped user --> '000400320001:0106001cf09d7167'
++[sql] returns noop
[sql_log] Processing sql_log_postauth
[sql_log]       expand: %{User-Name} -> 000400320001:0106001cf09d7167
[sql_log]       expand: %{%{User-Name}:-DEFAULT} -> 000400320001:0106001cf09d7167
[sql_log] sql_set_user escaped user --> '000400320001:0106001cf09d7167'
[sql_log] WARNING: Deprecated conditional expansion ":-".  See "man unlang" for details
[sql_log]       expand: INSERT INTO radpostauth                          (username, pass, reply, authdate) VALUES                        ('%{User-Name}', '%{User-Password:-Chap-Password}',                  '%{reply:Packet-Type}', '%S'); -> INSERT INTO radpostauth                       (username, pass, reply, authdate) VALUES                             ('000400320001:0106001cf09d7167', 'ISG',                'Access-Accept', '2011-10-05 14:58:55');
[sql_log]       expand: /usr/local/var/log/radius/radacct/sql-relay -> /usr/local/var/log/radius/radacct/sql-relay
++[sql_log] returns ok
++[exec] returns noop
Sending Access-Accept of id 240 to 81.20.192.51 port 1645
        Cisco-Account-Info += "A30720"
        Service-Type = Framed-User
        Cisco-AVPair = "lcp:interface-config=description Test oldswitch"
Finished request 6.
Going to the next request
Waking up in 4.9 seconds.
Cleaning up request 6 ID 240 with timestamp +84
Ready to process requests.










rad_recv: Access-Request packet from host 81.20.192.51 port 1645, id=241, length=301
        User-Name = "000400320001:0106001cf09d7167"
        User-Password = "ISG"
        NAS-Port-Type = PPPoEoQinQ
        Cisco-NAS-Port = "0/0/2/50.1957"
        NAS-Port = 62742
        NAS-Port-Id = "0/0/2/50.1957"
        Cisco-AVPair = "circuit-id-tag=000400320001"
        Cisco-AVPair = "remote-id-tag=0106001cf09d7167"
        Cisco-AVPair = "vendor-class-id-tag=MSFT 5.0"
        Service-Type = Outbound-User
        NAS-IP-Address = 81.20.192.51
        Acct-Session-Id = "0/0/2/50.1957_780000000000F516"
        NAS-Identifier = "ctd-c5-ISG.ctd-c5.sc.ru"
        Event-Timestamp = "Oct  5 2011 14:59:02 MSD"
# Executing section authorize from file /usr/local/etc/raddb/sites-enabled/default
+- entering group authorize {...}
++[preprocess] returns ok
[auth_log]      expand: /usr/local/var/log/radius/radacct/%{Client-IP-Address}/auth-detail-%Y%m%d -> /usr/local/var/log/radius/radacct/81.20.192.51/auth-detail-20111005
[auth_log] /usr/local/var/log/radius/radacct/%{Client-IP-Address}/auth-detail-%Y%m%d expands to /usr/local/var/log/radius/radacct/81.20.192.51/auth-detail-20111005
[auth_log]      expand: %t -> Wed Oct  5 14:59:03 2011
++[auth_log] returns ok
++[chap] returns noop
++[mschap] returns noop
++[files] returns noop
[sql]   expand: %{User-Name} -> 000400320001:0106001cf09d7167
[sql] sql_set_user escaped user --> '000400320001:0106001cf09d7167'
Closing socket 2 as its lifetime has been exceeded
rlm_sql (sql): Trying to (re)connect unconnected handle 2..
rlm_sql (sql): Attempting to connect rlm_sql_oracle #2
rlm_sql (sql): Connected new DB handle, #2
rlm_sql (sql): Reserving sql socket id: 2
rlm_sql (sql): got socket 2 after skipping 0 unconnected handles, tried to reconnect 1 though
[sql]   expand: SELECT id,UserName,Attribute,Value,op FROM radcheck WHERE Username = '%{SQL-User-Name}' ORDER BY id -> SELECT id,UserName,Attribute,Value,op FROM radcheck WHERE Username = '000400320001:0106001cf09d7167' ORDER BY id
[sql] User found in radcheck table
[sql]   expand: SELECT id,UserName,Attribute,Value,op FROM radreply WHERE Username = '%{SQL-User-Name}' ORDER BY id -> SELECT id,UserName,Attribute,Value,op FROM radreply WHERE Username = '000400320001:0106001cf09d7167' ORDER BY id
[sql]   expand: SELECT GroupName FROM radusergroup WHERE UserName='%{SQL-User-Name}' -> SELECT GroupName FROM radusergroup WHERE UserName='000400320001:0106001cf09d7167'
[sql]   expand: SELECT radgroupcheck.id,radgroupcheck.GroupName,radgroupcheck.Attribute,radgroupcheck.Value,radgroupcheck.op  FROM radgroupcheck,radusergroup WHERE radusergroup.Username = '%{SQL-User-Name}' AND radusergroup.GroupName = radgroupcheck.GroupName ORDER BY radgroupcheck.id -> SELECT radgroupcheck.id,radgroupcheck.GroupName,radgroupcheck.Attribute,radgroupcheck.Value,radgroupcheck.op  FROM radgroupcheck,radusergroup WHERE radusergroup.Username = '000400320001:0106001cf09d7167' AND radusergroup.GroupName = radgroupcheck.GroupName ORDER BY radgroupcheck.id
[sql] User found in group phys2
[sql]   expand: SELECT radgroupreply.id,radgroupreply.GroupName,radgroupreply.Attribute,radgroupreply.Value,radgroupreply.op  FROM radgroupreply,radusergroup WHERE radusergroup.Username = '%{SQL-User-Name}' AND radusergroup.GroupName = radgroupreply.GroupName ORDER BY radgroupreply.id -> SELECT radgroupreply.id,radgroupreply.GroupName,radgroupreply.Attribute,radgroupreply.Value,radgroupreply.op  FROM radgroupreply,radusergroup WHERE radusergroup.Username = '000400320001:0106001cf09d7167' AND radusergroup.GroupName = radgroupreply.GroupName ORDER BY radgroupreply.id
rlm_sql (sql): Released sql socket id: 2
++[sql] returns ok
++[expiration] returns noop
++[logintime] returns noop
++[pap] returns updated
Found Auth-Type = PAP
# Executing group from file /usr/local/etc/raddb/sites-enabled/default
+- entering group PAP {...}
[pap] login attempt with password "ISG"
[pap] Using clear text password "ISG"
[pap] User authenticated successfully
++[pap] returns ok
Login OK: [000400320001:0106001cf09d7167] (from client 81.20.192.51 port 62742)
# Executing section post-auth from file /usr/local/etc/raddb/sites-enabled/default
+- entering group post-auth {...}
[sql]   expand: %{User-Name} -> 000400320001:0106001cf09d7167
[sql] sql_set_user escaped user --> '000400320001:0106001cf09d7167'
++[sql] returns noop
[sql_log] Processing sql_log_postauth
[sql_log]       expand: %{User-Name} -> 000400320001:0106001cf09d7167
[sql_log]       expand: %{%{User-Name}:-DEFAULT} -> 000400320001:0106001cf09d7167
[sql_log] sql_set_user escaped user --> '000400320001:0106001cf09d7167'
[sql_log] WARNING: Deprecated conditional expansion ":-".  See "man unlang" for details
[sql_log]       expand: INSERT INTO radpostauth                          (username, pass, reply, authdate) VALUES                        ('%{User-Name}', '%{User-Password:-Chap-Password}',                  '%{reply:Packet-Type}', '%S'); -> INSERT INTO radpostauth                       (username, pass, reply, authdate) VALUES                             ('000400320001:0106001cf09d7167', 'ISG',                'Access-Accept', '2011-10-05 14:59:03');
[sql_log]       expand: /usr/local/var/log/radius/radacct/sql-relay -> /usr/local/var/log/radius/radacct/sql-relay
++[sql_log] returns ok
++[exec] returns noop
Sending Access-Accept of id 241 to 81.20.192.51 port 1645
        Cisco-Account-Info += "A30720"
        Service-Type = Framed-User
        Cisco-AVPair = "lcp:interface-config=description Test oldswitch"
Finished request 7.
Going to the next request
Waking up in 4.9 seconds.
Cleaning up request 7 ID 241 with timestamp +92
Ready to process requests.






rad_recv: Access-Request packet from host 81.20.192.51 port 1645, id=242, length=301
        User-Name = "000400320001:0106001cf09d7167"
        User-Password = "ISG"
        NAS-Port-Type = PPPoEoQinQ
        Cisco-NAS-Port = "0/0/2/50.1957"
        NAS-Port = 62743
        NAS-Port-Id = "0/0/2/50.1957"
        Cisco-AVPair = "circuit-id-tag=000400320001"
        Cisco-AVPair = "remote-id-tag=0106001cf09d7167"
        Cisco-AVPair = "vendor-class-id-tag=MSFT 5.0"
        Service-Type = Outbound-User
        NAS-IP-Address = 81.20.192.51
        Acct-Session-Id = "0/0/2/50.1957_780000000000F517"
        NAS-Identifier = "ctd-c5-ISG.ctd-c5.sc.ru"
        Event-Timestamp = "Oct  5 2011 14:59:19 MSD"
# Executing section authorize from file /usr/local/etc/raddb/sites-enabled/default
+- entering group authorize {...}
++[preprocess] returns ok
[auth_log]      expand: /usr/local/var/log/radius/radacct/%{Client-IP-Address}/auth-detail-%Y%m%d -> /usr/local/var/log/radius/radacct/81.20.192.51/auth-detail-20111005
[auth_log] /usr/local/var/log/radius/radacct/%{Client-IP-Address}/auth-detail-%Y%m%d expands to /usr/local/var/log/radius/radacct/81.20.192.51/auth-detail-20111005
[auth_log]      expand: %t -> Wed Oct  5 14:59:20 2011
++[auth_log] returns ok
++[chap] returns noop
++[mschap] returns noop
++[files] returns noop
[sql]   expand: %{User-Name} -> 000400320001:0106001cf09d7167
[sql] sql_set_user escaped user --> '000400320001:0106001cf09d7167'
Closing socket 1 as its lifetime has been exceeded
rlm_sql (sql): Trying to (re)connect unconnected handle 1..
rlm_sql (sql): Attempting to connect rlm_sql_oracle #1
rlm_sql (sql): Connected new DB handle, #1
rlm_sql (sql): Reserving sql socket id: 1
rlm_sql (sql): got socket 1 after skipping 0 unconnected handles, tried to reconnect 1 though
[sql]   expand: SELECT id,UserName,Attribute,Value,op FROM radcheck WHERE Username = '%{SQL-User-Name}' ORDER BY id -> SELECT id,UserName,Attribute,Value,op FROM radcheck WHERE Username = '000400320001:0106001cf09d7167' ORDER BY id
[sql] User found in radcheck table
[sql]   expand: SELECT id,UserName,Attribute,Value,op FROM radreply WHERE Username = '%{SQL-User-Name}' ORDER BY id -> SELECT id,UserName,Attribute,Value,op FROM radreply WHERE Username = '000400320001:0106001cf09d7167' ORDER BY id
[sql]   expand: SELECT GroupName FROM radusergroup WHERE UserName='%{SQL-User-Name}' -> SELECT GroupName FROM radusergroup WHERE UserName='000400320001:0106001cf09d7167'
[sql]   expand: SELECT radgroupcheck.id,radgroupcheck.GroupName,radgroupcheck.Attribute,radgroupcheck.Value,radgroupcheck.op  FROM radgroupcheck,radusergroup WHERE radusergroup.Username = '%{SQL-User-Name}' AND radusergroup.GroupName = radgroupcheck.GroupName ORDER BY radgroupcheck.id -> SELECT radgroupcheck.id,radgroupcheck.GroupName,radgroupcheck.Attribute,radgroupcheck.Value,radgroupcheck.op  FROM radgroupcheck,radusergroup WHERE radusergroup.Username = '000400320001:0106001cf09d7167' AND radusergroup.GroupName = radgroupcheck.GroupName ORDER BY radgroupcheck.id
[sql] User found in group phys2
[sql]   expand: SELECT radgroupreply.id,radgroupreply.GroupName,radgroupreply.Attribute,radgroupreply.Value,radgroupreply.op  FROM radgroupreply,radusergroup WHERE radusergroup.Username = '%{SQL-User-Name}' AND radusergroup.GroupName = radgroupreply.GroupName ORDER BY radgroupreply.id -> SELECT radgroupreply.id,radgroupreply.GroupName,radgroupreply.Attribute,radgroupreply.Value,radgroupreply.op  FROM radgroupreply,radusergroup WHERE radusergroup.Username = '000400320001:0106001cf09d7167' AND radusergroup.GroupName = radgroupreply.GroupName ORDER BY radgroupreply.id
rlm_sql (sql): Released sql socket id: 1
++[sql] returns ok
++[expiration] returns noop
++[logintime] returns noop
++[pap] returns updated
Found Auth-Type = PAP
# Executing group from file /usr/local/etc/raddb/sites-enabled/default
+- entering group PAP {...}
[pap] login attempt with password "ISG"
[pap] Using clear text password "ISG"
[pap] User authenticated successfully
++[pap] returns ok
Login OK: [000400320001:0106001cf09d7167] (from client 81.20.192.51 port 62743)
# Executing section post-auth from file /usr/local/etc/raddb/sites-enabled/default
+- entering group post-auth {...}
[sql]   expand: %{User-Name} -> 000400320001:0106001cf09d7167
[sql] sql_set_user escaped user --> '000400320001:0106001cf09d7167'
++[sql] returns noop
[sql_log] Processing sql_log_postauth
[sql_log]       expand: %{User-Name} -> 000400320001:0106001cf09d7167
[sql_log]       expand: %{%{User-Name}:-DEFAULT} -> 000400320001:0106001cf09d7167
[sql_log] sql_set_user escaped user --> '000400320001:0106001cf09d7167'
[sql_log] WARNING: Deprecated conditional expansion ":-".  See "man unlang" for details
[sql_log]       expand: INSERT INTO radpostauth                          (username, pass, reply, authdate) VALUES                        ('%{User-Name}', '%{User-Password:-Chap-Password}',                  '%{reply:Packet-Type}', '%S'); -> INSERT INTO radpostauth                       (username, pass, reply, authdate) VALUES                             ('000400320001:0106001cf09d7167', 'ISG',                'Access-Accept', '2011-10-05 14:59:20');
[sql_log]       expand: /usr/local/var/log/radius/radacct/sql-relay -> /usr/local/var/log/radius/radacct/sql-relay
++[sql_log] returns ok
++[exec] returns noop
Sending Access-Accept of id 242 to 81.20.192.51 port 1645
        Cisco-Account-Info += "A30720"
        Service-Type = Framed-User
        Cisco-AVPair = "lcp:interface-config=description Test oldswitch"
Finished request 8.
Going to the next request
Waking up in 4.9 seconds.
Cleaning up request 8 ID 242 with timestamp +109
Ready to process requests.

































  Oct  5 11:43:43.175: DHCPD: Sending notification of DISCOVER:
Oct  5 11:43:43.175:   DHCPD: htype 1 chaddr 001d.60d7.6879
Oct  5 11:43:43.175:   DHCPD: remote id 0106001cf09d7167
Oct  5 11:43:43.175:   DHCPD: circuit id 000400320001
Oct  5 11:43:43.175:   DHCPD: interface = GigabitEthernet0/0/2.195750
Oct  5 11:43:43.175:   DHCPD: class id 4d53465420352e30
Oct  5 11:43:43.175: DHCPD: Sending notification of DISCOVER:
Oct  5 11:43:43.175:   DHCPD: htype 1 chaddr 001d.60d7.6879
Oct  5 11:43:43.175:   DHCPD: remote id 0106001cf09d7167
Oct  5 11:43:43.175:   DHCPD: circuit id 000400320001
Oct  5 11:43:43.175:   DHCPD: interface = GigabitEthernet0/0/2.195750
Oct  5 11:43:43.175:   DHCPD: class id 4d53465420352e30
Oct  5 11:43:43.176: AAA/BIND(00006C3D): Bind i/f  
Oct  5 11:43:43.176: AAA/BIND(00006C3D): Bind i/f GigabitEthernet0/0/2.195750 
Oct  5 11:43:43.177: AAA/AUTHOR (0x6C3D): Pick method list 'ISG-AUTH-1'
Oct  5 11:43:43.177: RADIUS/ENCODE(00006C3D):Orig. component type = Iedge IP SIP
Oct  5 11:43:43.177: RADIUS: Format E value 0xF651 for character U with bitmask 0xFFFFFFFF
Oct  5 11:43:43.177: RADIUS: Format E port 0xF651 with bit 32 processed
Oct  5 11:43:43.177: RADIUS(00006C3D): Config NAS IP: 0.0.0.0
Oct  5 11:43:43.178: RADIUS(00006C3D): Config NAS IPv6: ::
Oct  5 11:43:43.178: RADIUS/ENCODE(00006C3D): acct_session_id: 63057
Oct  5 11:43:43.178: RADIUS/ENCODE(00006C3D): Acct-session-id pre-pended with Nas Port = 0/0/2/50.1957
Oct  5 11:43:43.178: RADIUS(00006C3D): Config NAS IP: 0.0.0.0
Oct  5 11:43:43.178: RADIUS(00006C3D): sending
Oct  5 11:43:43.178: RADIUS/ENCODE: Best Local IP-Address 81.20.192.51 for Radius-Server 81.20.192.57
Oct  5 11:43:43.178: RADIUS(00006C3D): Send Access-Request to 81.20.192.57:1812 id 1645/81, len 301
Oct  5 11:43:43.178: RADIUS:  authenticator 49 99 FA A7 D7 89 D0 F2 - C5 67 40 B3 FA 45 13 4A
Oct  5 11:43:43.178: RADIUS:  User-Name           [1]   31  "000400320001:0106001cf09d7167"
Oct  5 11:43:43.178: RADIUS:  User-Password       [2]   18  *
Oct  5 11:43:43.178: RADIUS:  NAS-Port-Type       [61]  6   PPPoEoQinQ                [34]
Oct  5 11:43:43.178: RADIUS:  Vendor, Cisco       [26]  21  
Oct  5 11:43:43.178: RADIUS:   cisco-nas-port     [2]   15  "0/0/2/50.1957"
Oct  5 11:43:43.178: RADIUS:  NAS-Port            [5]   6   63057                     
Oct  5 11:43:43.178: RADIUS:  NAS-Port-Id         [87]  15  "0/0/2/50.1957"
Oct  5 11:43:43.178: RADIUS:  Vendor, Cisco       [26]  35  
Oct  5 11:43:43.178: RADIUS:   Cisco AVpair       [1]   29  "circuit-id-tag=000400320001"
Oct  5 11:43:43.178: RADIUS:  Vendor, Cisco       [26]  38  
Oct  5 11:43:43.178: RADIUS:   Cisco AVpair       [1]   32  "remote-id-tag=0106001cf09d7167"
Oct  5 11:43:43.178: RADIUS:  Vendor, Cisco       [26]  36  
Oct  5 11:43:43.178: RADIUS:   Cisco AVpair       [1]   30  "vendor-class-id-tag=MSFT 5.0"
Oct  5 11:43:43.178: RADIUS:  Service-Type        [6]   6   Outbound                  [5]
Oct  5 11:43:43.178: RADIUS:  NAS-IP-Address      [4]   6   81.20.192.51              
Oct  5 11:43:43.178: RADIUS:  Acct-Session-Id     [44]  32  "0/0/2/50.1957_780000000000F651"
Oct  5 11:43:43.178: RADIUS:  Nas-Identifier      [32]  25  "ctd-c5-ISG.ctd-c5.sc.ru"
Oct  5 11:43:43.178: RADIUS:  Event-Timestamp     [55]  6   1317815023                
Oct  5 11:43:43.178: RADIUS(00006C3D): Sending a IPv4 Radius
                                        Packet
Oct  5 11:43:43.178: RADIUS(00006C3D): Started 5 sec timeout
Oct  5 11:43:43.219: RADIUS: Received from id 1645/81 81.20.192.57:1812, Access-Accept, len 95
Oct  5 11:43:43.219: RADIUS:  authenticator 1C B8 E0 39 65 EF 84 DC - 67 30 00 44 A5 B2 A2 FB
Oct  5 11:43:43.219: RADIUS:  Vendor, Cisco       [26]  14  
Oct  5 11:43:43.219: RADIUS:   ssg-account-info   [250] 8   "A30720"
Oct  5 11:43:43.219: RADIUS:  Service-Type        [6]   6   Framed                    [2]
Oct  5 11:43:43.219: RADIUS:  Vendor, Cisco       [26]  55  
Oct  5 11:43:43.219: RADIUS:   Cisco AVpair       [1]   49  "lcp:interface-config=description Test oldswitch"
Oct  5 11:43:43.219: RADIUS(00006C3D): Received from id 1645/81
Oct  5 11:43:43.220: SVM [30720]: needs downloading
Oct  5 11:43:43.220: SVM [3A000601/30720]: allocated version 1
Oct  5 11:43:43.220: SVM [3A000601/30720]: [1F000143]: client queued
Oct  5 11:43:43.220: SVM [3A000601/30720]: [PM-Download:1F000143] locked 0->1
Oct  5 11:43:43.220: SVM [3A000601/30720]: [AAA-Download:44294A5C] locked 0->1
Oct  5 11:43:43.220: AAA/AUTHOR (0x6C3D): Pick method list 'default'
Oct  5 11:43:43.222: SVM [55000602/30720]: added child
Oct  5 11:43:43.223: SVM [3A000601/30720]: TC created
Oct  5 11:43:43.223: SVM [3A000601/30720]: [TC-Child:44C8B0F8] locked 0->1
Oct  5 11:43:43.223: SVM [55000602/CHILD/30720]: [TC-Parent:44C8B17C] locked 0->1
Oct  5 11:43:43.223: SVM [3A000601/30720]: TC svc_info found
Oct  5 11:43:43.223: SVM [55000602/CHILD/30720]: set accounting handle
Oct  5 11:43:43.223: SVM [3A000601/30720]: downloaded first version
Oct  5 11:43:43.223: SVM [3A000601/30720]: [1F000143]: client download ok
Oct  5 11:43:43.223: SVM [3A000601/30720]: [SVM-to-client-msg:1F000143] locked 0->1
Oct  5 11:43:43.223: SVM [3A000601/30720]: [AAA-Download:44294A5C] unlocked 1->0
Oct  5 11:43:43.223: SVM [3A000601/30720]: alloc feature info
Oct  5 11:43:43.223: SVM [3A000601/30720]: [SVM-Feature-Info:44B1834C] locked 0->1
Oct  5 11:43:43.223: SVM [3A000601/30720]: has Policy info
Oct  5 11:43:43.223: SVM [3A000601/30720]: [PM-Info:44C473B4] locked 0->1
Oct  5 11:43:43.223: SVM [3A000601/30720]: populated client
Oct  5 11:43:43.223: SVM [3A000601/30720]: [PM-Download:1F000143] unlocked 1->0
Oct  5 11:43:43.223: SVM [3A000601/30720]: [SVM-to-client-msg:1F000143] unlocked 1->0
Oct  5 11:43:43.223: SVM [3A000601/30720]: [PM-Service:44CBCF90] locked 0->1
Oct  5 11:43:43.224: SVM [3A000601/30720]: [SVM-Feature-Info:44B1834C] unlocked 1->0
Oct  5 11:43:43.224: DHCPD: Callback for workspace (ID=0xA0000B2)
Oct  5 11:43:43.224: DHCPD: No authentication required. Continue
Oct  5 11:43:43.224: DHCPD: Callback: class '' now specified for client 0100.1d60.d768.79
Oct  5 11:43:43.224: DHCPD: Callback: class error returns for client
Oct  5 11:43:43.224: SVM [3A000601/30720]: already downloaded; sharing
Oct  5 11:43:43.224: SVM [3A000601/30720]: [PM-Service:44CBCF90] unlocked 1->0
Oct  5 11:43:43.224: SVM [3A000601/30720]: [PM-Info:44C473B4] unlocked 1->0
Oct  5 11:43:43.224: SVM [3A000601/30720]: breaking parent-child lock
Oct  5 11:43:43.224: SVM [55000602/CHILD/30720]: breaking parent-child lock
Oct  5 11:43:43.224: SVM [55000602/CHILD/30720]: destroy
Oct  5 11:43:43.224: SVM ERROR: unknown handle 55000602
Oct  5 11:43:43.224: SVM [3A000601/30720]: destroy
Oct  5 11:43:43.224: SVM ERROR: unknown handle 3A000601
Oct  5 11:43:44.994: DHCPD: input i/f override GigabitEthernet0/0/2.1951137 for client
Oct  5 11:43:44.994: DHCPD: Sending notification of ASSIGNMENT:
Oct  5 11:43:44.994:  DHCPD: address 172.20.124.210 mask 255.255.224.0
Oct  5 11:43:44.994:   DHCPD: htype 1 chaddr 001d.920b.3a04
Oct  5 11:43:44.994:   DHCPD: remote id 0006f07d682d0320
Oct  5 11:43:44.994:   DHCPD: circuit id 000400890001
Oct  5 11:43:44.994:   DHCPD: lease time remaining (secs) = 300
Oct  5 11:43:44.994:   DHCPD: interface = GigabitEthernet0/0/2.1951137
Oct  5 11:43:44.994: DHCPD: Updating DPM hdl in DHCP binding for 172.20.124.210 
Oct  5 11:43:44.994:  DHCPD: lease time = 300
Oct  5 11:43:44.994: DHCPD: dhcpd_lookup_route: host = 172.20.124.210
Oct  5 11:43:44.994: DHCPD: dhcpd_lookup_route: index = 22
Oct  5 11:43:44.994: DHCPD: unicast BOOTREPLY output i/f override GigabitEthernet0/0/2.1951137
Oct  5 11:43:46.133: DHCPD: input i/f override GigabitEthernet0/0/2.1954162 for client
Oct  5 11:43:46.133: DHCPD: Sending notification of ASSIGNMENT:
Oct  5 11:43:46.133:  DHCPD: address 172.20.99.17 mask 255.255.224.0
Oct  5 11:43:46.133:   DHCPD: htype 1 chaddr f46d.047f.8959
Oct  5 11:43:46.133:   DHCPD: remote id 00063408043a3fb0
Oct  5 11:43:46.133:   DHCPD: circuit id 000400a20004
Oct  5 11:43:46.133:   DHCPD: lease time remaining (secs) = 300
Oct  5 11:43:46.133:   DHCPD: interface = GigabitEthernet0/0/2.1954162
Oct  5 11:43:46.134: DHCPD: Updating DPM hdl in DHCP binding for 172.20.99.17 
Oct  5 11:43:46.134:  DHCPD: lease time = 300
Oct  5 11:43:46.134: DHCPD: dhcpd_lookup_route: host = 172.20.99.17
Oct  5 11:43:46.134: DHCPD: dhcpd_lookup_route: index = 202
Oct  5 11:43:46.134: DHCPD: unicast BOOTREPLY output i/f override GigabitEthernet0/0/2.1954162
Oct  5 11:43:46.365: DHCPD: input i/f override GigabitEthernet0/0/2.1951132 for client
Oct  5 11:43:46.365: DHCPD: Sending notification of ASSIGNMENT:
Oct  5 11:43:46.365:  DHCPD: address 172.20.98.218 mask 255.255.224.0
Oct  5 11:43:46.365:   DHCPD: htype 1 chaddr 0024.8c7c.4617
Oct  5 11:43:46.365:   DHCPD: remote id 0006f07d682c96a0
Oct  5 11:43:46.365:   DHCPD: circuit id 000400840012
Oct  5 11:43:46.365:   DHCPD: lease time remaining (secs) = 300
Oct  5 11:43:46.365:   DHCPD: interface = GigabitEthernet0/0/2.1951132
Oct  5 11:43:46.365: DHCPD: Updating DPM hdl in DHCP binding for 172.20.98.218 
Oct  5 11:43:46.365:  DHCPD: lease time = 300
Oct  5 11:43:46.366: DHCPD: dhcpd_lookup_route: host = 172.20.98.218
Oct  5 11:43:46.366: DHCPD: dhcpd_lookup_route: index = 0
Oct  5 11:43:46.366: DHCPD: unicast BOOTREPLY output i/f override GigabitEthernet0/0/2.1951132
Oct  5 11:43:47.406: DHCPD: input i/f override GigabitEthernet0/0/2.1950109 for client
Oct  5 11:43:47.406: DHCPD: Sending notification of ASSIGNMENT:
Oct  5 11:43:47.406:  DHCPD: address 172.20.98.235 mask 255.255.224.0
Oct  5 11:43:47.406:   DHCPD: htype 1 chaddr 1c6f.65ac.546d
Oct  5 11:43:47.406:   DHCPD: remote id 0006f07d682c9360
Oct  5 11:43:47.406:   DHCPD: circuit id 0004006d0001
Oct  5 11:43:47.406:   DHCPD: lease time remaining (secs) = 300
Oct  5 11:43:47.406:   DHCPD: interface = GigabitEthernet0/0/2.1950109
Oct  5 11:43:47.406: DHCPD: Updating DPM hdl in DHCP binding for 172.20.98.235 
Oct  5 11:43:47.406:  DHCPD: lease time = 300
Oct  5 11:43:47.406: DHCPD: dhcpd_lookup_route: host = 172.20.98.235
Oct  5 11:43:47.406: DHCPD: dhcpd_lookup_route: index = 49
Oct  5 11:43:47.407: DHCPD: unicast BOOTREPLY output i/f override GigabitEthernet0/0/2.1950109
Oct  5 11:43:50.175: DHCPD: Sending notification of DISCOVER:
Oct  5 11:43:50.175:   DHCPD: htype 1 chaddr 001d.60d7.6879
Oct  5 11:43:50.175:   DHCPD: remote id 0106001cf09d7167
Oct  5 11:43:50.175:   DHCPD: circuit id 000400320001
Oct  5 11:43:50.175:   DHCPD: interface = GigabitEthernet0/0/2.195750
Oct  5 11:43:50.175:   DHCPD: class id 4d53465420352e30
Oct  5 11:43:50.175: DHCPD: Sending notification of DISCOVER:
Oct  5 11:43:50.175:   DHCPD: htype 1 chaddr 001d.60d7.6879
Oct  5 11:43:50.175:   DHCPD: remote id 0106001cf09d7167
Oct  5 11:43:50.175:   DHCPD: circuit id 000400320001
Oct  5 11:43:50.175:   DHCPD: interface = GigabitEthernet0/0/2.195750
Oct  5 11:43:50.175:   DHCPD: class id 4d53465420352e30
Oct  5 11:43:50.176: AAA/BIND(00006C3E): Bind i/f  
Oct  5 11:43:50.176: AAA/BIND(00006C3E): Bind i/f GigabitEthernet0/0/2.195750 
Oct  5 11:43:50.177: AAA/AUTHOR (0x6C3E): Pick method list 'ISG-AUTH-1'
Oct  5 11:43:50.177: RADIUS/ENCODE(00006C3E):Orig. component type = Iedge IP SIP
Oct  5 11:43:50.177: RADIUS: Format E value 0xF652 for character U with bitmask 0xFFFFFFFF
Oct  5 11:43:50.177: RADIUS: Format E port 0xF652 with bit 32 processed
Oct  5 11:43:50.177: RADIUS(00006C3E): Config NAS IP: 0.0.0.0
Oct  5 11:43:50.177: RADIUS(00006C3E): Config NAS IPv6: ::
Oct  5 11:43:50.177: RADIUS/ENCODE(00006C3E): acct_session_id: 63058
Oct  5 11:43:50.177: RADIUS/ENCODE(00006C3E): Acct-session-id pre-pended with Nas Port = 0/0/2/50.1957
Oct  5 11:43:50.178: RADIUS(00006C3E): Config NAS IP: 0.0.0.0
Oct  5 11:43:50.178: RADIUS(00006C3E): sending
Oct  5 11:43:50.178: RADIUS/ENCODE: Best Local IP-Address 81.20.192.51 for Radius-Server 81.20.192.57
Oct  5 11:43:50.178: RADIUS(00006C3E): Send Access-Request to 81.20.192.57:1812 id 1645/82, len 301
Oct  5 11:43:50.178: RADIUS:  authenticator C7 9F 5A D0 50 5A 26 19 - 9B BD D3 43 50 D4 43 87
Oct  5 11:43:50.178: RADIUS:  User-Name           [1]   31  "000400320001:0106001cf09d7167"
Oct  5 11:43:50.178: RADIUS:  User-Password       [2]   18  *
Oct  5 11:43:50.178: RADIUS:  NAS-Port-Type       [61]  6   PPPoEoQinQ                [34]
Oct  5 11:43:50.178: RADIUS:  Vendor, Cisco       [26]  21  
Oct  5 11:43:50.178: RADIUS:   cisco-nas-port     [2]   15  "0/0/2/50.1957"
Oct  5 11:43:50.178: RADIUS:  NAS-Port            [5]   6   63058                     
Oct  5 11:43:50.178: RADIUS:  NAS-Port-Id         [87]  15  "0/0/2/50.1957"
Oct  5 11:43:50.178: RADIUS:  Vendor, Cisco       [26]  35  
Oct  5 11:43:50.178: RADIUS:   Cisco AVpair       [1]   29  "circuit-id-tag=000400320001"
Oct  5 11:43:50.178: RADIUS:  Vendor, Cisco       [26]  38  
Oct  5 11:43:50.178: RADIUS:   Cisco AVpair       [1]   32  "remote-id-tag=0106001cf09d7167"
Oct  5 11:43:50.178: RADIUS:  Vendor, Cisco       [26]  36  
Oct  5 11:43:50.178: RADIUS:   Cisco AVpair       [1]   30  "vendor-class-id-tag=MSFT 5.0"
Oct  5 11:43:50.178: RADIUS:  Service-Type        [6]   6   Outbound                  [5]
Oct  5 11:43:50.178: RADIUS:  NAS-IP-Address      [4]   6   81.20.192.51              
Oct  5 11:43:50.178: RADIUS:  Acct-Session-Id     [44]  32  "0/0/2/50.1957_780000000000F652"
Oct  5 11:43:50.178: RADIUS:  Nas-Identifier      [32]  25  "ctd-c5-ISG.ctd-c5.sc.ru"
Oct  5 11:43:50.178: RADIUS:  Event-Timestamp     [55]  6   1317815030                
Oct  5 11:43:50.178: RADIUS(00006C3E): Sending a IPv4 Radius
                                        Packet
Oct  5 11:43:50.178: RADIUS(00006C3E): Started 5 sec timeout
Oct  5 11:43:50.210: RADIUS: Received from id 1645/82 81.20.192.57:1812, Access-Accept, len 95
Oct  5 11:43:50.210: RADIUS:  authenticator 95 67 AD 45 25 D7 1F 2A - A0 FD E7 85 F4 D5 BA CD
Oct  5 11:43:50.210: RADIUS:  Vendor, Cisco       [26]  14  
Oct  5 11:43:50.210: RADIUS:   ssg-account-info   [250] 8   "A30720"
Oct  5 11:43:50.210: RADIUS:  Service-Type        [6]   6   Framed                    [2]
Oct  5 11:43:50.210: RADIUS:  Vendor, Cisco       [26]  55  
Oct  5 11:43:50.210: RADIUS:   Cisco AVpair       [1]   49  "lcp:interface-config=description Test oldswitch"
Oct  5 11:43:50.211: RADIUS(00006C3E): Received from id 1645/82
Oct  5 11:43:50.212: SVM [30720]: needs downloading
Oct  5 11:43:50.212: SVM [9C000603/30720]: allocated version 1
Oct  5 11:43:50.212: SVM [9C000603/30720]: [6D000232]: client queued
Oct  5 11:43:50.212: SVM [9C000603/30720]: [PM-Download:6D000232] locked 0->1
Oct  5 11:43:50.212: SVM [9C000603/30720]: [AAA-Download:44A81468] locked 0->1
Oct  5 11:43:50.212: AAA/AUTHOR (0x6C3E): Pick method list 'default'
Oct  5 11:43:50.214: SVM [59000604/30720]: added child
Oct  5 11:43:50.214: SVM [9C000603/30720]: TC created
Oct  5 11:43:50.214: SVM [9C000603/30720]: [TC-Child:44C8B0F8] locked 0->1
Oct  5 11:43:50.214: SVM [59000604/CHILD/30720]: [TC-Parent:44C8B17C] locked 0->1
Oct  5 11:43:50.214: SVM [9C000603/30720]: TC svc_info found
Oct  5 11:43:50.214: SVM [59000604/CHILD/30720]: set accounting handle
Oct  5 11:43:50.214: SVM [9C000603/30720]: downloaded first version
Oct  5 11:43:50.214: SVM [9C000603/30720]: [6D000232]: client download ok
Oct  5 11:43:50.214: SVM [9C000603/30720]: [SVM-to-client-msg:6D000232] locked 0->1
Oct  5 11:43:50.215: SVM [9C000603/30720]: [AAA-Download:44A81468] unlocked 1->0
Oct  5 11:43:50.215: SVM [9C000603/30720]: alloc feature info
Oct  5 11:43:50.215: SVM [9C000603/30720]: [SVM-Feature-Info:44B1834C] locked 0->1
Oct  5 11:43:50.215: SVM [9C000603/30720]: has Policy info
Oct  5 11:43:50.215: SVM [9C000603/30720]: [PM-Info:44C3D098] locked 0->1
Oct  5 11:43:50.215: SVM [9C000603/30720]: populated client
Oct  5 11:43:50.215: SVM [9C000603/30720]: [PM-Download:6D000232] unlocked 1->0
Oct  5 11:43:50.215: SVM [9C000603/30720]: [SVM-to-client-msg:6D000232] unlocked 1->0
Oct  5 11:43:50.215: SVM [9C000603/30720]: [PM-Service:44CBCF90] locked 0->1
Oct  5 11:43:50.215: SVM [9C000603/30720]: [SVM-Feature-Info:44B1834C] unlocked 1->0
Oct  5 11:43:50.215: DHCPD: Callback for workspace (ID=0x380000B3)
Oct  5 11:43:50.215: DHCPD: No authentication required. Continue
Oct  5 11:43:50.215: DHCPD: Callback: class '' now specified for client 0100.1d60.d768.79
Oct  5 11:43:50.215: DHCPD: Callback: class error returns for client
Oct  5 11:43:50.215: SVM [9C000603/30720]: already downloaded; sharing
Oct  5 11:43:50.215: SVM [9C000603/30720]: [PM-Service:44CBCF90] unlocked 1->0
Oct  5 11:43:50.216: SVM [9C000603/30720]: [PM-Info:44C3D098] unlocked 1->0
Oct  5 11:43:50.216: SVM [9C000603/30720]: breaking parent-child lock
Oct  5 11:43:50.216: SVM [59000604/CHILD/30720]: breaking parent-child lock
Oct  5 11:43:50.216: SVM [59000604/CHILD/30720]: destroy
Oct  5 11:43:50.216: SVM ERROR: unknown handle 59000604
Oct  5 11:43:50.216: SVM [9C000603/30720]: destroy
Oct  5 11:43:50.216: SVM ERROR: unknown handle 9C000603

{% endraw %}