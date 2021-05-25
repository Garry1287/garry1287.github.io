---
layout: post
title:  "osfp_nets_psi"
date:   2016-09-02 22:06:01 +0300
categories: routing
tags: routing
---

# osfp_nets_psi
O IA     192.168.200.0/29 
192.168.253. (мнжм к ебургу)
192.168.221.0/29  (ТЕСТ, нах не нужна
192.168.200.0/24  (нах)
192.168.70.0/24 (нах)
192.168.45.0/24 (нах)
 78.25.66.220 MEGAFON (нах)
 87.245.241.132  RETN (нах)
 
192.168.253.0/24

91.190.64.0/20
81.20.192.0/20
192.168.130.0/24
192.168.131.0/24
 193.104.11.0/24  - Индезит
 
172.20.0.0/14
 172.24.0.0/24
 172.28.0.0/24
 172.31.0.0/16

 
 
 
no ip prefix-list no-sc-local-distribution
ip prefix-list no-sc-local-distribution seq 5 permit 172.20.0.0/14 le 32
ip prefix-list no-sc-local-distribution seq 10 permit 172.31.0.0/16 le 32
ip prefix-list no-sc-local-distribution seq 11 permit 172.24.0.0/24 le 32
ip prefix-list no-sc-local-distribution seq 12 permit 172.28.0.0/24 le 32
ip prefix-list no-sc-local-distribution seq 15 permit 192.168.130.0/23 le 32
ip prefix-list no-sc-local-distribution seq 20 permit 81.20.192.0/20 le 32
ip prefix-list no-sc-local-distribution seq 25 permit 91.190.64.0/20 le 32
ip prefix-list no-sc-local-distribution seq 30 permit 193.104.11.0/24 le 32
ip prefix-list no-sc-local-distribution seq 35 permit 192.168.253.0/24 le 32
ip prefix-list no-sc-local-distribution seq 40 permit 0.0.0.0/0
ip prefix-list no-sc-local-distribution seq 100 deny 0.0.0.0/0 le 32
 
 policy-options {                        
      policy-statement no-sc-local-distribution {
        term net_1 {                    
            from {                      
                route-filter 192.168.0.0/16 orlonger;
            }                           
            then reject;                
        }                               
    }                                   

 set  policy-options policy-statement no-sc-local-distribution term net_1 from route-filter 172.20.0.0/14 orlonger
 set  policy-options policy-statement no-sc-local-distribution term net_1 from route-filter 172.31.0.0/16 orlonger
  set  policy-options policy-statement no-sc-local-distribution term net_1 from route-filter 172.24.0.0/24 orlonger
 set  policy-options policy-statement no-sc-local-distribution term net_1 from route-filter 172.28.0.0/24 orlonger
 set  policy-options policy-statement no-sc-local-distribution term net_1 from route-filter 192.168.130.0/23 orlonger
 set  policy-options policy-statement no-sc-local-distribution term net_1 from route-filter 81.20.192.0/20 orlonger
 set  policy-options policy-statement no-sc-local-distribution term net_1 from route-filter 91.190.64.0/20 orlonger
 set  policy-options policy-statement no-sc-local-distribution term net_1 from route-filter 193.104.11.0/24 orlonger
 set  policy-options policy-statement no-sc-local-distribution term net_1 from route-filter 192.168.253.0/24 orlonger
 
 set  policy-options policy-statement no-sc-local-distribution term net_1 from route-filter 0.0.0.0/0 exact

 set  policy-options policy-statement no-sc-local-distribution term net_1 from route-filter 192.168.0.0/16 orlonger

 delete  policy-options policy-statement no-sc-local-distribution term net_1 from route-filter 172.20.0.0/14 orlonger
 delete  policy-options policy-statement no-sc-local-distribution term net_1 from route-filter 172.31.0.0/16 orlonger
delete policy-options policy-statement no-sc-local-distribution term net_1 from route-filter 172.24.0.0/24 orlonger
delete policy-options policy-statement no-sc-local-distribution term net_1 from route-filter 172.28.0.0/24 orlonger
 delete  policy-options policy-statement no-sc-local-distribution term net_1 from route-filter 192.168.130.0/23 orlonger
 delete  policy-options policy-statement no-sc-local-distribution term net_1 from route-filter 81.20.192.0/20 orlonger
 delete policy-options policy-statement no-sc-local-distribution term net_1 from route-filter 91.190.64.0/20 orlonger
 delete policy-options policy-statement no-sc-local-distribution term net_1 from route-filter 193.104.11.0/24 orlonger
 delete  policy-options policy-statement no-sc-local-distribution term net_1 from route-filter 192.168.253.0/24 orlonger

 protocols {                             
    ospf {                              
        traceoptions {                  
            file debug-ospf size 1m files 5;
            flag all;                   
        }                               
        export [ STATIC-TO-OSPF DIRECT-TO-OSPF no-199-net ];
        import no-sc-local-distribution;
        area 0.0.0.0 {                  
            interface vlan.10 {         
                priority 0;             
            }                           
            interface vlan.13 {         
                priority 0;             
            }                           
            interface vlan.38 {         
                priority 0;             
            }                           
        }                               

 
Архаизм
8: vlan9@eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP 
    link/ether 00:25:90:0e:d1:16 brd ff:ff:ff:ff:ff:ff
    inet 10.255.9.10/30 brd 10.255.9.11 scope global vlan9
Connect VOIP test

Нахер 192.168.0.0
O E2  192.168.0.0/24 [110/1] via 81.20.192.12, 6w2d, GigabitEthernet0/2.10



      172.24.0.0/24 is subnetted, 1 subnets
O        172.24.0.0 [110/2] via 81.20.192.13, 7w0d, GigabitEthernet0/2.10


      172.28.0.0/24 is subnetted, 1 subnets
O E2     172.28.0.0 [110/0] via 81.20.192.8, 7w0d, GigabitEthernet0/2.10

      172.31.0.0/16 is variably subnetted, 4 subnets, 2 masks
O E1     172.31.2.20/30 [110/3] via 81.20.192.8, 2w2d, GigabitEthernet0/2.10
O E1     172.31.2.44/30 [110/3] via 81.20.192.8, 2w2d, GigabitEthernet0/2.10
O E1     172.31.2.72/29 [110/3] via 81.20.192.8, 2w2d, GigabitEthernet0/2.10
O E1     172.31.2.84/30 [110/3] via 81.20.192.8, 2w2d, GigabitEthernet0/2.10

