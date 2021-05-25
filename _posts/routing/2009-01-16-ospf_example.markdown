---
layout: post
title:  "ospf_example"
date:   2009-01-16 08:30:49 +0300
categories: routing
tags: routing
---

# ospf_example
router ospf 110
 router-id 81.20.192.22
 log-adjacency-changes
 redistribute connected metric 1 subnets
 redistribute static metric 1 metric-type 1 subnets
 redistribute bgp 20866 metric 1 metric-type 1 subnets route-map bgp2ospf
 passive-interface default
 no passive-interface GigabitEthernet0/0.10
 no passive-interface GigabitEthernet0/0.68
 no passive-interface GigabitEthernet0/0.69
 no passive-interface GigabitEthernet0/0.115
 no passive-interface GigabitEthernet0/0.117
 no passive-interface GigabitEthernet0/0.122
 no passive-interface GigabitEthernet0/0.450
 no passive-interface GigabitEthernet0/0.660
 no passive-interface GigabitEthernet0/0.661
 no passive-interface GigabitEthernet0/0.804
 no passive-interface GigabitEthernet0/0.806
 no passive-interface GigabitEthernet0/0.824
 no passive-interface GigabitEthernet0/0.825
 no passive-interface GigabitEthernet0/0.861
 no passive-interface GigabitEthernet0/0.862
 no passive-interface GigabitEthernet0/0.3009
 no passive-interface GigabitEthernet0/0.3046
 network 81.20.192.0 0.0.0.31 area 0
 network 81.20.192.100 0.0.0.3 area 0
 network 81.20.193.120 0.0.0.3 area 0
 network 81.20.193.144 0.0.0.3 area 0
 network 81.20.196.168 0.0.0.3 area 0
 network 81.20.196.172 0.0.0.3 area 0
 network 81.20.196.192 0.0.0.3 area 0
 network 81.20.196.200 0.0.0.3 area 0
 network 81.20.196.208 0.0.0.3 area 0
 network 81.20.197.248 0.0.0.3 area 0
 network 81.20.197.252 0.0.0.3 area 0
 network 81.20.200.144 0.0.0.3 area 0
 network 81.20.200.148 0.0.0.3 area 0
 network 81.20.202.100 0.0.0.3 area 0
 network 81.20.202.108 0.0.0.3 area 0
 network 172.20.0.0 0.0.3.255 area 0
 network 172.24.0.0 0.0.3.255 area 0
 neighbor 81.20.200.150
 neighbor 81.20.200.146
 neighbor 81.20.196.210
 neighbor 81.20.196.194
 neighbor 81.20.193.146
 neighbor 81.20.193.122
 default-information originate metric 1
 distribute-list prefix no-sc-local-distribution out






ffd


router ospf 110
 router-id 81.20.196.194
 log-adjacency-changes












interface GigabitEthernet0/0.3517
192.168.9.1
 redistribute connected metric 1 subnets
 redistribute static metric 1 metric-type 1 subnets
 passive-interface default
 no passive-interface FastEthernet0/0
 network 81.20.196.192 0.0.0.3 area 0
 neighbor 81.20.196.193
 distribute-list prefix no-local-distribution out

ip prefix-list no-local-distribution seq 1 deny 10.0.0.0/8 le 32
ip prefix-list no-local-distribution seq 10 deny 172.16.0.0/12 le 32
ip prefix-list no-local-distribution seq 20 deny 192.168.0.0/16 le 32
ip prefix-list no-local-distribution seq 50 permit 0.0.0.0/0 le 32





 description # Otrada-Gen downlink # Woland 24.10.06 #LN 4512_79
 bandwidth 256
 encapsulation dot1Q 117
 ip address 81.20.196.193 255.255.255.252
 ip verify unicast reverse-path
 ip flow ingress
 ip ospf network non-broadcast
 no cdp enable






interface FastEthernet0/0
 description # Uplink to PSI via RAD RIC-E1
 ip address 81.20.200.106 255.255.255.252
 ip access-group 100 in
 no ip proxy-arp
 ip route-cache flow
 ip ospf network non-broadcast
 load-interval 30
 duplex auto
 speed auto
 no cdp enable
 h323-gateway voip interface

 access-class 10 in
 exec-timeout 0 30
 transport input telnet


download firmware_fromTFTP 10.90.90.1 DES-3200R_1.50.B010.had image_id 1
download cfg_fromTFTP 10.90.90.1 /opt3/prishvina13-s1.sc.int


# STP                                                                                                                                                        
                                                                                                                                                             
 config stp version rstp                                                                                                                                     
 config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 3 fbpdu disable hellotime 2 lbd enable lbd_recover_timer 60                                     
 config stp priority 32768 instance_id 0                                                                                                                     
 config stp mst_config_id name 5C:D9:98:3E:9B:00 revision_level 0                                                                                            
 disable stp                                                                                                                                                 
 config stp ports 1-27 externalCost auto  edge false p2p auto state enable lbd disable                                                                       
 config stp mst_ports 1-27 instance_id 0 internalCost auto priority 128                                                                                      
config stp ports 1-27 fbpdu disable                                                                                                                          
                                                                                                                                                             
# BPDU_TUNNEL                                                                                                                                                
                                                                                                                                                             
 config bpdu_tunnel ports all type none                                                                                                                      
disable bpdu_tunnel                                                                                                                                          
                     



# SNTP                                                                                                                                                       
                                                                                                                                                             
disable sntp                                                                                                                                                 
config time_zone operator + hour 0 min 0                                                                                                                     
config sntp primary 0.0.0.0 secondary 0.0.0.0 poll-interval 720                                                                                              
config dst disable 




# MBA                                                                                                                                                        
                                                                                                                                                             
disable mac_based_access_control                                                                                                                             
config mac_based_access_control ports 1-27 state disable                                                                                                     
config mac_based_access_control ports  1-27 mode host_based                                                                                                  
config mac_based_access_control method local                                                                                                                 
config mac_based_access_control password default 




# SYSLOG                                                                                                                                                     
                                                                                                                                                             
disable syslog                                                                                                                                               
config system_severity log information                                                                                                                       
config system_severity trap information                                                                                                                      
config log_save_timing on_demand  








config stp priority 16384 instance_id 0
enable stp
config stp ports 1-2 externalCost auto edge false p2p auto state enable lbd disable
config stp ports 1-2 fbpdu enable

DGS-3612G:5#show stp
Command: show stp

STP Bridge Global Settings
—————————
STP Status : Enabled
STP Version : RSTP
Max Age : 20
Hello Time : 2
Forward Delay : 15
Max Hops : 20
TX Hold Count : 3
Forwarding BPDU : Enabled
Loopback Detection : Enabled
LBD Recover Time : 60



Отключаем на абонентских портах stp
DES-3526:admin# config stp ports 1-24 externalCost auto edge true p2p auto state disable
DES-3526:admin# config stp ports 1-24 fbpdu disableх
DES-3526:admin# config stp ports 1-24 restricted_role true
DES-3526:admin# config stp ports 1-24 restricted_tcn true




Настройки RSTP на магистральных портах
DES-3526:admin# config stp ports 25-26 externalCost auto edge false p2p auto state enable
DES-3526:admin# config stp ports 25-26 fbpdu enable
DES-3526:admin# config stp ports 25-26 restricted_role false
DES-3526:admin# config stp ports 25-26 restricted_tcn false
















Включаем отсылку трапов в случае изменения root кольца
DES-3028:4# config stp trap new_root enable topo_change enable

Отключаем на абонентских портах stp
DES-3028:4# config stp ports 1-24 externalCost auto edge true p2p auto state disable lbd disable
DES-3028:4# config stp ports 1-24 fbpdu disable
DES-3028:4# config stp ports 1-24 restricted_role true
DES-3028:4# config stp ports 1-24 restricted_tcn true

Настройки RSTP на магистральных портах
DES-3028:4# config stp ports 25-28 externalCost auto edge false p2p auto state enable lbd disable
DES-3028:4# config stp ports 25-28 fbpdu enable
DES-3028:4# config stp ports 25-28 restricted_role false
DES-3028:4# config stp ports 25-28 restricted_tcn false






Если все сделали правильно, то вывод команды на DES-3526 или DES-3028 show stp instance_id должна иметь такой вид, где Designated Root Bridge : 16384/00-1C-F0-25-81-80 мак адрес DGS-3612 :

DES-3526:admin# show stp instance_id
Command: show stp instance_id

STP Instance Settings
—————————
Instance Type          : CIST
Instance Status        : Enabled
Instance Priority      : 32768(bridge priority : 32768, sys ID ext : 0 )

STP Instance Operational Status
——————————–
Designated Root Bridge : 16384/00-1C-F0-25-81-80
External Root Cost     : 80000
Regional Root Bridge   : 32768/00-1C-F0-D3-E6-AF
Internal Root Cost     : 0
Designated Bridge      : 32768/00-1C-F0-D3-E7-19
Root Port              : 25
Max Age                : 20
Forward Delay          : 15
Last Topology Change   : 20643
Topology Changes Count : 1



3200
disable stp
config stp version rstp
config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 6 fbpdu enable hellotime 2
config stp priority 32768 instance_id 0 
config stp mst_config_id name 1C:BD:B9:64:94:60 revision_level 0
config stp ports 1-28 externalCost auto edge auto p2p auto state enable
config stp mst_ports 1-28 instance_id 0 internalCost auto priority 128
config stp ports 1-28 fbpdu enable
config stp ports 1-28 restricted_role false
config stp ports 1-28 restricted_tcn false





3627

# STP                                                                           
                                                                                
 config stp version rstp                                                        
 config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 3 fbpdu disable hellotime 2 lbd enable lbd_recover_timer 60
 config stp priority 16384 instance_id 0                                        
 config stp mst_config_id name 00:22:B0:1B:EC:00 revision_level 0               
 disable stp                                                                    
 config stp ports 1-27 externalCost auto  edge false p2p auto state enable lbd disable
 config stp mst_ports 1-27 instance_id 0 internalCost auto priority 128         
config stp ports 1-27 fbpdu disable                                             
                                                                                
# BPDU_TUNNEL                                                                   
                                                                                
 config bpdu_tunnel ports all type none                                         
disable bpdu_tunnel 












DSG3627


 config stp version rstp                                                        
 config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 3 fbpdu disable hellotime 2 lbd enable lbd_recover_timer 60
 config stp priority 16384 instance_id 0 
enable stp
config stp ports 24 externalCost auto edge true p2p auto state disable lbd disable
config stp ports 22-23 externalCost auto edge false p2p auto state enable lbd disable
config stp ports 22-23 fbpdu enable



config stp version rstp
config stp maxage 20 maxhops 20 forwarddelay 15 txholdcount 6 fbpdu enable hellotime 2
config stp priority 32768 instance_id 0 
enable stp

3200
config stp ports 1-24 externalCost auto edge true p2p auto state disable
config stp ports 1-24 fbpdu disable
config stp ports 1-24 restricted_role true
config stp ports 1-24 restricted_tcn true

config stp ports 25-28 externalCost auto edge false p2p auto state enable 
config stp ports 25-28 fbpdu enable
config stp ports 25-28 restricted_role false
config stp ports 25-28 restricted_tcn false




                                                                    
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
config stp ports 25-28 restricted_tcn false 




VID             : 1          VLAN Name       : default
VLAN Type       : static    
Member ports    : 21-26               
Static ports    : 21-26               
Tagged ports    :                     
Untagged ports  : 21-26               

VID             : 22         VLAN Name       : mngt
VLAN Type       : static    
Member ports    : 6,20,23-24          
Static ports    : 6,20,23-24          
Tagged ports    : 6,23-24             
Untagged ports  : 20                  

VID             : 24         VLAN Name       : MNG-phys
VLAN Type       : static    
Member ports    : 23-24               
Static ports    : 23-24               
Tagged ports    : 23-24               
Untagged ports  :                     
                                                                                
VID             : 417        VLAN Name       : Smurgisa-INET
VLAN Type       : static    
Member ports    : 14-17,23-24         
Static ports    : 14-17,23-24         
Tagged ports    : 17,23-24            
Untagged ports  : 14-16               

interface Vlan417
 description # SMURGISA11 Inet # Woland 18.12.08
 ip address 172.20.130.33 255.255.255.224
 ip helper-address 172.31.3.2
 no ip redirects
 ip local-proxy-arp
 ip route-cache same-interface
end






VID             : 444        VLAN Name       : Antipenko-Inet
VLAN Type       : static    
Member ports    : 23-24               
Static ports    : 23-24               
Tagged ports    : 23-24               
Untagged ports  :   

interface GigabitEthernet0/0.444
 description # Antipenko home inet @ Smurgisa, 11 # Woland 20.12.2008
 bandwidth 2048
 encapsulation dot1Q 444
 ip address 81.20.193.253 255.255.255.252
 ip flow ingress
 rate-limit input 8192000 1545000 3091000 conform-action transmit exceed-action drop
 rate-limit output 8192000 1545000 3091000 conform-action transmit exceed-action drop
end




                  

VID             : 446        VLAN Name       : Beketov-INET
VLAN Type       : static    
Member ports    : 2,23-24             
Static ports    : 2,23-24             
Tagged ports    : 23-24               
Untagged ports  : 2   

interface GigabitEthernet0/0.446
 description # IP Beketov inet @ Vodopiyanova, 21 # Woland 06.05.2009
 bandwidth 2048
 encapsulation dot1Q 446
 ip address 81.20.193.229 255.255.255.252
 ip flow ingress
 rate-limit input 2048000 386000 772000 conform-action transmit exceed-action drop
 rate-limit output 2048000 386000 772000 conform-action transmit exceed-action drop
end




                
                                                                                
VID             : 671        VLAN Name       : RSHB-GLD
VLAN Type       : static    
Member ports    : 3,23-24             
Static ports    : 3,23-24             
Tagged ports    : 23-24               
Untagged ports  : 3                   

VID             : 3005       VLAN Name       : Flinstone-Voip
VLAN Type       : static    
Member ports    : 4,23-24             
Static ports    : 4,23-24             
Tagged ports    : 23-24               
Untagged ports  : 4    

interface GigabitEthernet0/0.3005
 description #Flinstone #pheonix 11.08.2010
 encapsulation dot1Q 3005
 ip address 192.168.130.65 255.255.255.252
 ip flow ingress
 no cdp enable
end


               

VID             : 3023       VLAN Name       : MUP-LGTK
VLAN Type       : static    
Member ports    : 24-25               
Static ports    : 24-25               
Tagged ports    : 24-25               
Untagged ports  :          

interface GigabitEthernet0/0.3023
 description #Lipetskaya Ipetechnaya korp #garry 19.01.2011
 encapsulation dot1Q 3023
 ip unnumbered Loopback2
 ip verify unicast reverse-path
 no ip proxy-arp
 ip flow ingress
 rate-limit input 2048000 384000 768000 conform-action transmit exceed-action drop
 rate-limit output 2048000 384000 768000 conform-action transmit exceed-action drop
 no cdp enable
end


           
                                                                                
VID             : 3037       VLAN Name       : MUP_LGTK_2_Pobedy_85
VLAN Type       : static    
Member ports    : 5,23-24             
Static ports    : 5,23-24             
Tagged ports    : 23-24               
Untagged ports  : 5                   

interface GigabitEthernet0/0.3037
 description # MUP_LGTK_2 Pobedy 85
 encapsulation dot1Q 3037
 ip unnumbered Loopback2
 ip verify unicast reverse-path
 no ip proxy-arp
 ip flow ingress
 rate-limit input 4096000 768000 1536000 conform-action transmit exceed-action drop
 rate-limit output 4096000 768000 1536000 conform-action transmit exceed-action drop
 no cdp enable
end




VID             : 3039       VLAN Name       : SalonKrasoty
VLAN Type       : static    
Member ports    : 6,23-24             
Static ports    : 6,23-24             
Tagged ports    : 6,23-24             
Untagged ports  :                     

interface GigabitEthernet0/0.3039
 description #IP_Pronina #kaktus 17.08.2011
 encapsulation dot1Q 3039
 ip unnumbered Loopback5
 ip flow ingress
 ip flow egress
 rate-limit input 2048000 585000 1170000 conform-action transmit exceed-action drop
 rate-limit output 2048000 585000 1170000 conform-action transmit exceed-action drop
 no cdp enable
end
