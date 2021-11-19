---
layout: post
title:  "Iptables - старые правила"
date:   2011-11-24 07:02:35 +0400
categories: firewall
tags: firewall
---

# iptables_for

```
-A FORWARD -s 192.168.1.0/24 -d 192.168.1.9/32 -i eth1 -o eth1 -p tcp -m tcp --dport 3128 -j ACCEPT 
-A FORWARD -s 192.168.1.0/24 -d 91.203.193.18/32 -j gambler 
-A FORWARD -s 192.168.1.0/24 -d 80.75.131.78/32 -j Axaptamtt 
-A FORWARD -s 80.75.131.78/32 -j Axaptamtt 
-A FORWARD -d 64.12.0.0/16 -j icq 
-A FORWARD -d 152.163.0.0/16 -j icq 
-A FORWARD -d 205.188.0.0/16 -j icq 
-A FORWARD -d 192.168.1.30/32 -p tcp -m tcp --dport 7780 -j ACCEPT 
-A FORWARD -p udp -m udp --dport 161 -j ACCEPT 
-A FORWARD -s 192.168.253.10/32 -d 192.168.1.15/32 -p tcp -m tcp --dport 7780 -j ACCEPT 
-A FORWARD -s 192.168.1.0/24 -d 192.168.169.2/32 -m conntrack --ctstate NEW,RELATED,ESTABLISHED -m limit --limit 3/min -j LOG --log-prefix "To 1C " --log-tcp-options --log-ip-options 
-A FORWARD -s 192.168.1.0/24 -d 192.168.169.2/32 -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT 
-A FORWARD -s 192.168.169.2/32 -d 192.168.1.0/24 -m conntrack --ctstate ESTABLISHED -m limit --limit 3/min -j LOG --log-prefix "From 1C " --log-tcp-options --log-ip-options 
-A FORWARD -s 192.168.169.2/32 -d 192.168.1.0/24 -m conntrack --ctstate ESTABLISHED -j ACCEPT 
-A FORWARD -s 192.168.169.2/32 -d 192.168.1.0/24 -p udp -m multiport --dports 53,69 -j ACCEPT 
-A FORWARD -s 192.168.169.2/32 -m limit --limit 3/min -j LOG --log-prefix "MTT atack from 1c to LAN " --log-tcp-options --log-ip-options 
-A FORWARD -s 192.168.169.2/32 -j DROP 
```

81.20.192.4 - Проверить как Глуховский

81.20.196.100 - pj9997 Тоже Глухов

```
:PREROUTING ACCEPT [15593758:1110960968]
:OUTPUT ACCEPT [749220:61948738]
:POSTROUTING ACCEPT [3049925:200069938]
:squid - [0:0]
-A PREROUTING -d 81.20.192.19/32 -p tcp -m tcp --dport 8880 -j DNAT --to-destination 192.168.1.15:7781 
-A FORWARD -d 192.168.1.15/32 -p tcp -m tcp --dport 7781 -j ACCEPT

-A PREROUTING -s 81.20.193.251/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 3389 -j DNAT --to-destination 192.168.1.169:3389
-A FORWARD -d 192.168.1.15/32 -p tcp -m tcp --dport 7781 -j ACCEPT


## Удалить не нужное правило
-A PREROUTING -s 81.20.199.208/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 3389 -j DNAT --to-destination 192.168.1.35:3389 



-A PREROUTING -s 91.190.76.53/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 3389 -j LOG --log-prefix "from MTT To 1C " --log-tcp-options --log-ip-options 
-A PREROUTING -s 91.190.76.53/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 3389 -j DNAT --to-destination 192.168.1.35:3389 
-A FORWARD -s 91.190.76.53/32 -d 192.168.1.35/32 -p tcp -m tcp --dport 3389 -j ACCEPT


-A PREROUTING -s 77.233.199.98/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 8880 -j DNAT --to-destination 192.168.1.14:80
-A FORWARD -s 77.233.199.98/32 -d 192.168.1.14/32 -p tcp -m tcp --dport 80 -j ACCEPT

-A PREROUTING -s 77.233.199.98/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 8080 -j DNAT --to-destination 192.168.1.14:8080 
-A FORWARD -s 77.233.199.98/32 -d 192.168.1.14/32 -p tcp -m tcp --dport 8080 -j ACCEPT

-A PREROUTING -s 77.233.199.98/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 22 -j DNAT --to-destination 192.168.1.14:22 
-A FORWARD -s 77.233.199.98/32 -d 192.168.1.14/32 -p tcp -m tcp --dport 22 -j ACCEPT

-A PREROUTING -s 77.233.199.98/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 443 -j DNAT --to-destination 192.168.1.14:443 
-A FORWARD -s 77.233.199.98/32 -d 192.168.1.14/32 -p tcp -m tcp --dport 443 -j ACCEPT

#Удалить не нужное правило
-A PREROUTING -s 81.20.192.4/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 3389 -j DNAT --to-destination 192.168.1.175:3389


-A PREROUTING -s 192.168.130.110/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 514 -j DNAT --to-destination 192.168.1.178:514
-A FORWARD -s 192.168.130.110/32 -d 192.168.1.178/32 -p tcp -m tcp --dport 514 -j ACCEPT
-A PREROUTING -s 192.168.130.110/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 514 -j DNAT --to-destination 192.168.1.160:514
-A FORWARD -s 192.168.130.110/32 -d 192.168.1.160/32 -p tcp -m tcp --dport 514 -j ACCEPT

-A PREROUTING -s 195.34.240.24/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 443 -j DNAT --to-destination 192.168.1.30:4461
-A FORWARD -s 195.34.240.24/32 -d 192.168.1.30/32 -p tcp -m tcp --dport 4461 -j ACCEPT

-A PREROUTING -d 81.20.192.33/32 -p tcp -m tcp --dport 443 -j DNAT --to-destination 192.168.1.30:4459
-A FORWARD -d 192.168.1.30/32 -p tcp -m tcp --dport 4459 -j ACCEPT

-A PREROUTING -d 81.20.192.33/32 -p tcp -m tcp --dport 11194 -j DNAT --to-destination 192.168.1.14:1194
-A FORWARD -d 192.168.1.30/32 -p tcp -m tcp --dport 1194 -j ACCEPT

-A PREROUTING -d 81.20.192.33/32 -p udp -m udp --dport 11194 -j DNAT --to-destination 192.168.1.14:1194
-A FORWARD -d 192.168.1.30/32 -p udp -m udp --dport 1194 -j ACCEPT

-A PREROUTING -s 81.20.199.22/32 -d 81.20.192.19/32 -p tcp -m tcp --dport 4389 -j DNAT --to-destination 192.168.1.34:3389
-A FORWARD -s 81.20.199.22/32 -d 192.168.1.34/32 -p tcp -m tcp --dport 3389 -j ACCEPT

-A PREROUTING -s 81.20.199.22/32 -d 81.20.192.19/32 -p tcp -m tcp --dport 2222 -j DNAT --to-destination 192.168.1.188:22
-A FORWARD -s 81.20.199.22/32 -d 192.168.1.188/32 -p tcp -m tcp --dport 22 -j ACCEPT


-A PREROUTING -s 81.20.198.8/32 -d 81.20.192.19/32 -p tcp -m tcp --dport 2222 -j DNAT --to-destination 192.168.1.188:22
-A FORWARD -s 81.20.198.8/32 -d 192.168.1.188/32 -p tcp -m tcp --dport 22 -j ACCEPT

-A PREROUTING -s 109.172.41.150/32 -d 81.20.192.19/32 -p tcp -m tcp --dport 2222 -j DNAT --to-destination 192.168.1.188:22
-A FORWARD -s 109.172.41.150/32 -d 192.168.1.188/32 -p tcp -m tcp --dport 22 -j ACCEPT


-A PREROUTING -s 109.172.41.150/32 -d 81.20.192.19/32 -p tcp -m tcp --dport 4389 -j DNAT --to-destination 192.168.1.34:3389 
-A FORWARD -s 109.172.41.150/32 -d 192.168.1.34/32 -p tcp -m tcp --dport 3389 -j ACCEPT

-A PREROUTING -s 109.172.41.150/32 -d 81.20.192.19/32 -p tcp -m tcp --dport 5901 -j DNAT --to-destination 192.168.1.188:5901 
-A FORWARD -s 109.172.41.150/32 -d 192.168.1.188/32 -p tcp -m tcp --dport 5901 -j ACCEPT

#Удалить не нужное правило
-A PREROUTING -s 81.20.196.100/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 3389 -j DNAT --to-destination 192.168.1.175:3389 


-A PREROUTING -s 81.20.192.53/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 22 -j DNAT --to-destination 192.168.1.178:22
-A FORWARD -s 81.20.192.53/32 -d 192.168.1.178/32 -p tcp -m tcp --dport 22 -j ACCEPT

-A PREROUTING -s 81.20.192.57/32 -d 81.20.192.19/32 -p tcp -m tcp --dport 15210 -j DNAT --to-destination 192.168.1.30:1521
-A FORWARD -s 81.20.192.57/32 -d 192.168.1.30/32 -p tcp -m tcp --dport 1521 -j ACCEPT

-A PREROUTING -s 81.20.192.6/32 -d 81.20.192.19/32 -p tcp -m tcp --dport 15211 -j DNAT --to-destination 192.168.1.30:1521
-A FORWARD -s 81.20.192.6/32 -d 192.168.1.30/32 -p tcp -m tcp --dport 1521 -j ACCEPT

#Удалить не нужное правило
-A PREROUTING -s 81.20.192.170/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 22 -j DNAT --to-destination 192.168.1.45:22


-A PREROUTING -d 81.20.192.33/32 -p tcp -m tcp --dport 8888 -j DNAT --to-destination 192.168.1.15:7780
-A FORWARD -d 192.168.1.15/32 -p tcp -m tcp --dport 7780 -j ACCEPT

-A PREROUTING -d 81.20.192.33/32 -p tcp -m tcp --dport 80 -j DNAT --to-destination 192.168.1.30:7780
-A FORWARD --d 192.168.1.30/32 -p tcp -m tcp --dport 7780 -j ACCEPT

-A PREROUTING -s 66.199.231.152/29 -d 81.20.192.33/32 -p udp -m udp --dport 161 -j DNAT --to-destination 192.168.113.20:161 
-A FORWARD -s 66.199.231.152/29 -d 192.168.113.20/32 -p tcp -m tcp --dport 161 -j ACCEPT

-A PREROUTING -s 107.22.218.106/32 -d 81.20.192.33/32 -p udp -m udp --dport 161 -j DNAT --to-destination 192.168.113.20:161
-A FORWARD -s 107.22.218.106/32 -d 192.168.113.20/32 -p tcp -m tcp --dport 161 -j ACCEPT

#Удалить не нужное правило
-A PREROUTING -d 81.20.192.33/32 -p tcp -m tcp --dport 4022 -j DNAT --to-destination 192.168.1.97:4022


-A PREROUTING -s 81.20.198.8/32 -d 81.20.192.19/32 -p tcp -m tcp --dport 4389 -j DNAT --to-destination 192.168.1.34:3389

-A PREROUTING -s 192.168.1.0/24 -p tcp -m tcp --dport 80 -j squid 
-A FORWARD -s 192.168.1.0/24 -d 192.168.1.9/32 -p tcp -m tcp --dport 3128 -j ACCEPT

#Это для сквида
-A POSTROUTING -s 192.168.1.0/24 -d 192.168.1.9/32 -j SNAT --to-source 192.168.1.11

#Это для Виктории
-A POSTROUTING -s 192.168.1.0/24 -d 192.168.250.0/24 -o vlan12 -j SNAT --to-source 192.168.251.2
-A FORWARD -s 192.168.1.0/24 -d 192.168.250.0/24 -i eth1 -o vlan12 -j ACCEPT

-A POSTROUTING -s 192.168.1.0/24 -d 192.168.9.0/24 -o vlan16 -j SNAT --to-source 192.168.8.2
-A FORWARD -s 192.168.1.0/24 -d 192.168.9.0/24 -i eth1 -o vlan16 -j ACCEPT

-A POSTROUTING -s 192.168.1.0/24 -d 192.168.10.0/24 -o vlan16 -j SNAT --to-source 192.168.8.2
-A FORWARD -s 192.168.1.0/24 -d 192.168.10.0/24 -i eth1 -o vlan16 -j ACCEPT

-A POSTROUTING -s 192.168.1.0/24 -d 192.168.252.0/24 -o vlan15 -j SNAT --to-source 192.168.251.6
-A FORWARD -s 192.168.1.0/24 -d 192.168.252.0/24 -i eth1 -o vlan15 -j ACCEPT

-A POSTROUTING -s 192.168.1.0/24 -d 10.0.48.0/24 -o vlan250 -j SNAT --to-source 10.0.48.18
-A FORWARD -s 192.168.1.0/24 -d 10.0.48.0/24 -i eth1 -o vlan250 -j ACCEPT

-A POSTROUTING -s 192.168.1.0/24 -d 10.10.120.0/24 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.10.120.0/24 -i eth1 -o vlan201 -j ACCEPT


-A POSTROUTING -s 192.168.0.0/16 -d 10.90.0.0/16 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.90.0.0/16 -i eth1 -o vlan201 -j ACCEPT

-A POSTROUTING -s 192.168.0.0/16 -d 10.192.3.8/29 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.192.3.8/29 -i eth1 -o vlan201 -j ACCEPT

-A POSTROUTING -s 192.168.0.0/16 -d 10.82.0.0/16 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.192.3.8/29 -i eth1 -o vlan201 -j ACCEPT

-A POSTROUTING -s 192.168.0.0/16 -d 10.192.10.0/24 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.192.3.8/29 -i eth1 -o vlan201 -j ACCEPT

-A POSTROUTING -s 192.168.0.0/16 -d 10.192.1.0/24 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.192.1.0/24 -i eth1 -o vlan201 -j ACCEPT

-A POSTROUTING -s 192.168.0.0/16 -d 10.33.0.0/24 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.33.0.0/24 -i eth1 -o vlan201 -j ACCEPT
 
-A POSTROUTING -s 192.168.0.0/16 -d 10.50.0.0/16 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.50.0.0/16 -i eth1 -o vlan201 -j ACCEPT

-A POSTROUTING -s 192.168.0.0/16 -d 10.66.0.0/24 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.66.0.0/24 -i eth1 -o vlan201 -j ACCEPT
 
-A POSTROUTING -s 192.168.0.0/16 -d 10.194.0.0/24 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.194.0.0/24 -i eth1 -o vlan201 -j ACCEPT

-A POSTROUTING -s 192.168.0.0/16 -d 10.210.0.0/16 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.210.0.0/16 -i eth1 -o vlan201 -j ACCEPT

-A POSTROUTING -s 192.168.0.0/16 -d 10.186.0.0/16 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.186.0.0/16 -i eth1 -o vlan201 -j ACCEPT

-A POSTROUTING -s 192.168.0.0/16 -d 10.17.0.0/24 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.17.0.0/24 -i eth1 -o vlan201 -j ACCEPT

-A POSTROUTING -s 192.168.0.0/16 -d 10.28.11.0/30 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.28.11.0/30 -i eth1 -o vlan201 -j ACCEPT


-A POSTROUTING -s 192.168.0.0/16 -d 10.28.12.0/30 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.28.12.0/30 -i eth1 -o vlan201 -j ACCEPT

-A POSTROUTING -s 192.168.0.0/16 -d 10.74.0.0/24 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.74.0.0/24 -i eth1 -o vlan201 -j ACCEPT
 
-A POSTROUTING -s 192.168.0.0/16 -d 10.0.0.0/24 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.0.0.0/24 -i eth1 -o vlan201 -j ACCEPT

-A POSTROUTING -s 192.168.0.0/16 -d 10.98.0.0/16 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.98.0.0/16 -i eth1 -o vlan201 -j ACCEPT

-A POSTROUTING -s 192.168.0.0/16 -d 10.26.0.0/16 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.26.0.0/16 -i eth1 -o vlan201 -j ACCEPT

#Удалить не нужное правило
-A POSTROUTING -s 192.168.1.0/24 -d 192.168.114.0/24 -o vlan10 -j SNAT --to-source 192.168.114.1

-A POSTROUTING -s 192.168.0.0/16 -d 192.168.130.0/24 -o vlan10 -j SNAT --to-source 81.20.192.19
-A FORWARD -s 192.168.1.0/24 -d 192.168.130.0/24 -i eth1 -o vlan10 -j ACCEPT

#Удалить не нужное правило
-A POSTROUTING -s 192.168.0.0/16 -d 192.168.114.0/24 -o vlan10 -j SNAT --to-source 81.20.192.19

-A POSTROUTING -s 192.168.0.0/16 -d 192.168.116.0/24 -o vlan23 -j SNAT --to-source 192.168.116.1
-A FORWARD -s 192.168.1.0/24 -d 192.168.116.0/24 -i eth1 -o vlan23 -j ACCEPT


-A POSTROUTING -s 192.168.0.0/16 -d 192.168.83.0/24 -o vlan10 -j SNAT --to-source 81.20.192.19
-A FORWARD -s 192.168.1.0/24 -d 192.168.83.0/24 -i eth1 -o vlan10 -j ACCEPT

-A POSTROUTING -s 192.168.1.0/24 -d 172.16.97.216/30 -o vlan250 -j SNAT --to-source 10.0.48.18
-A FORWARD -s 192.168.1.0/24 -d 172.16.97.216/30 -i eth1 -o vlan250 -j ACCEPT

-A POSTROUTING -s 192.168.0.0/16 -d 192.168.112.0/24 -o vlan21 -j SNAT --to-source 192.168.112.1
-A FORWARD -s 192.168.1.0/24 -d 192.168.112.0/24 -i eth1 -o vlan21 -j ACCEPT

-A POSTROUTING -s 192.168.0.0/16 -d 172.16.0.0/15 -o vlan10 -j SNAT --to-source 81.20.192.19
-A FORWARD -s 192.168.1.0/24 -d 172.16.0.0/15 -i eth1 -o vlan10 -j ACCEPT

-A POSTROUTING -s 192.168.0.0/16 -d 10.29.0.0/16 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.29.0.0/16 -i eth1 -o vlan201 -j ACCEPT

-A POSTROUTING -d 192.168.1.30/32 -p tcp -m tcp --dport 7780 -j SNAT --to-source 192.168.1.11
-A POSTROUTING -d 192.168.1.30/32 -p tcp -m tcp --dport 4459 -j SNAT --to-source 192.168.1.11

-A POSTROUTING -s 192.168.1.0/24 -d 10.110.0.0/16 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.110.0.0/24 -i eth1 -o vlan201 -j ACCEPT

#Нахера
-A POSTROUTING -s 192.168.1.0/24 -d 192.168.50.0/30 -o vlan3997 -j SNAT --to-source 192.168.50.1
-A FORWARD -s 192.168.1.0/24 -d 192.168.50.0/24 -i eth1 -o vlan3997 -j ACCEPT

-A POSTROUTING -s 192.168.1.0/24 -d 172.19.4.0/22 -o vlan201 -j SNAT --to-source 10.192.10.190 
-A FORWARD -s 192.168.1.0/24 -d 172.19.4.0/22 -i eth1 -o vlan201 -j ACCEPT

-A POSTROUTING -s 192.168.1.0/24 -d 192.168.5.0/27 -o vlan201 -j SNAT --to-source 10.192.10.190 
-A FORWARD -s 192.168.1.0/24 -d 192.168.5.0/27 -i eth1 -o vlan201 -j ACCEPT

-A POSTROUTING -s 192.168.1.0/24 -d 10.90.19.0/24 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.90.19.0/24 -i eth1 -o vlan201 -j ACCEPT

-A POSTROUTING -s 192.168.1.0/24 -o vlan2002 -j SNAT --to-source 10.11.12.14
-A FORWARD -s 192.168.1.0/24 -i eth1 -o vlan2002 -j ACCEPT
 
-A POSTROUTING -s 192.168.1.0/24 -d 192.168.120.0/24 -o vlan26 -j SNAT --to-source 192.168.120.1
-A FORWARD -s 192.168.1.0/24 -d 192.168.120.0/24 -i eth1 -o vlan26 -j ACCEPT

-A POSTROUTING -s 192.168.0.0/16 -d 192.168.131.0/24 -o vlan10 -j SNAT --to-source 81.20.192.19
-A FORWARD -s 192.168.1.0/24 -d 192.168.131.0/24 -i eth1 -o vlan10 -j ACCEPT

-A POSTROUTING -s 192.168.1.0/24 -d 192.168.113.0/24 -o vlan22 -j SNAT --to-source 192.168.113.1
-A FORWARD -s 192.168.1.0/24 -d 192.168.131.0/24 -i eth1 -o vlan22 -j ACCEPT

-A POSTROUTING -s 192.168.1.0/24 -d 192.168.121.0/24 -o vlan27 -j SNAT --to-source 192.168.121.1
-A FORWARD -s 192.168.1.0/24 -d 192.168.121.0/24 -i eth1 -o vlan27 -j ACCEPT

-A POSTROUTING -s 192.168.1.0/24 -d 192.168.128.0/24 -o vlan1027 -j SNAT --to-source 192.168.128.1
-A FORWARD -s 192.168.1.0/24 -d 192.168.128.0/24 -i eth1 -o vlan1027 -j ACCEPT

-A POSTROUTING -s 192.168.1.0/24 -d 192.168.248.0/24 -o vlan29 -j SNAT --to-source 192.168.248.1
-A FORWARD -s 192.168.1.0/24 -d 192.168.248.0/24 -i eth1 -o vlan29 -j ACCEPT

-A POSTROUTING -s 192.168.0.0/16 -d 192.168.70.0/24 -o vlan10 -j SNAT --to-source 81.20.192.19
-A FORWARD -s 192.168.1.0/24 -d 192.168.70.0/24 -i eth1 -o vlan10 -j ACCEPT
 
-A POSTROUTING -s 192.168.121.0/24 -o vlan10 -j SNAT --to-source 81.20.192.19
-A FORWARD -s 192.168.1.0/24 -d 192.168.121.0/24 -i eth1 -o vlan10 -j ACCEPT

-A POSTROUTING -s 192.168.0.0/16 -d 10.138.0.0/16 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.138.0.0/16 -i eth1 -o vlan201 -j ACCEPT

-A POSTROUTING -s 192.168.1.0/24 -d 10.192.11.0/24 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.192.11.0/24 -i eth1 -o vlan201 -j ACCEPT

-A POSTROUTING -s 192.168.1.0/24 -d 10.100.0.0/16 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.100.0.0/16 -i eth1 -o vlan201 -j ACCEPT

-A POSTROUTING -s 192.168.1.0/24 ! -d 192.168.0.0/16 -o vlan10 -j SNAT --to-source 81.20.192.32
-A FORWARD -s 192.168.1.0/24 ! -d 192.168.0.0/16 -i eth1 -o vlan10 -j ACCEPT

# Надо удалить 2 записи
-A POSTROUTING -s 192.168.168.0/24 ! -d 192.168.0.0/16 -o vlan10 -j SNAT --to-source 81.20.192.32

-A POSTROUTING -s 192.168.1.0/24 -d 192.168.200.0/24 -o vlan2502 -j SNAT --to-source 192.168.200.18
-A FORWARD -s 192.168.1.0/24 -d 192.168.200.0/24 -i eth1 -o vlan2502 -j ACCEPT

-A POSTROUTING -s 192.168.1.0/24 -d 10.150.0.0/24 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.150.0.0/24 -i eth1 -o vlan201 -j ACCEPT
 
-A POSTROUTING -s 192.168.1.0/24 -d 10.150.4.0/24 -o vlan201 -j SNAT --to-source 10.192.10.190
-A FORWARD -s 192.168.1.0/24 -d 10.150.4.0/24 -i eth1 -o vlan201 -j ACCEPT

-A POSTROUTING -s 192.168.248.101/32 -o vlan10 -j SNAT --to-source 81.20.192.32
-A FORWARD -s 192.168.248.101/32 -i eth1 -o vlan10 -j ACCEPT

-A POSTROUTING -s 192.168.248.102/32 -o vlan10 -j SNAT --to-source 81.20.192.32
-A FORWARD -s 192.168.248.102/32 -i eth1 -o vlan10 -j ACCEPT

-A POSTROUTING -s 192.168.1.0/24 -d 172.28.0.0/24 -o vlan37 -j SNAT --to-source 172.28.0.8 
-A FORWARD -s 192.168.1.0/24 -d 172.28.0.0/24 -i eth1 -o vlan37 -j ACCEPT

-A POSTROUTING -s 192.168.1.0/24 -d 10.146.0.0/16 -o vlan201 -j SNAT --to-source 10.192.10.190 
-A FORWARD -s 192.168.1.0/24 -d 10.146.0.0/16 -i eth1 -o vlan201 -j ACCEPT

-A POSTROUTING -s 192.168.1.0/24 -d 10.186.250.0/29 -o vlan1030 -j SNAT --to-source 10.186.250.5
-A FORWARD -s 192.168.1.0/24 -d 10.186.250.0/29 -i eth1 -o vlan1030 -j ACCEPT

-A POSTROUTING -s 192.168.248.100/32 -o vlan10 -j SNAT --to-source 81.20.192.32 
-A FORWARD -s 192.168.248.100/32 -i eth1 -o vlan10 -j ACCEPT
```

```
-A squid -s 192.168.1.9/32 -j ACCEPT 
-A squid -s 192.168.1.66/32 -j ACCEPT 
-A squid -s 192.168.1.64/32 -j ACCEPT 
-A squid -s 192.168.1.96/32 -j ACCEPT 
-A squid -s 192.168.1.65/32 -j ACCEPT 
-A squid -s 192.168.1.188/32 -j ACCEPT 
-A squid -s 192.168.1.150/32 -j ACCEPT 
-A squid -s 192.168.1.229/32 -j ACCEPT 
-A squid -s 192.168.1.191/32 -j ACCEPT 
-A squid -s 192.168.1.152/32 -j ACCEPT 
-A squid -s 192.168.1.160/32 -j ACCEPT 
-A squid -s 192.168.1.33/32 -j ACCEPT 
-A squid -s 192.168.1.200/32 -j ACCEPT 
-A squid -s 192.168.1.141/32 -j ACCEPT 
-A squid -s 192.168.1.169/32 -j ACCEPT 
-A squid -s 192.168.1.187/32 -j ACCEPT 
-A squid -s 192.168.1.170/32 -j ACCEPT 
-A squid -s 192.168.1.178/32 -j ACCEPT 
-A squid -p tcp -m tcp --dport 80 -j DNAT --to-destination 192.168.1.9:3128 
COMMIT
# Completed on Mon Aug 20 12:16:54 2012
```


```
LAN
Unisprint 192.168.2.1
OUT (19)
REDIRECT (33)
NUT (32)
VICTORIA  Vlan12
BOST-MGMT-MPLS Vlan15
UNISPRINT-MGMT Vlan16
RADIO-MGMT Vlan21
MNGT22-113 Vlan22
MNGT23-RADIO Vlan23
MNGT24-117 vlan24
MNGT25-118 vlan25
MNGT26-120 vlan26
MNGT27-121
MNGT28-122
MNGT29-248
MNGT30-123
MNGT34-124
MNGT36-115
MNGT37-GRYAZI
VPN-NLMK 201
STTC-PSI 209
SUCDEN 250
START-ONIMA 875
BRAS-RADIUS 1027
FSB-BILL 1035
SAPPHIRE-1C-DMZ 1037
vpn_MGTU-Voip - 2002
l2vpn-voip-grz 2999 (телефония карамышево-грязи)
pppoe_nlmk 3997  (dslam на заводе)
```


```
vlan12    Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:192.168.251.2  Bcast:192.168.251.3  Mask:255.255.255.252
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:687264 errors:0 dropped:0 overruns:0 frame:0
          TX packets:1278193 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:98797034 (94.2 Mb)  TX bytes:82297272 (78.4 Mb)

vlan15    Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:192.168.251.6  Bcast:192.168.251.7  Mask:255.255.255.252
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:9828 errors:0 dropped:0 overruns:0 frame:0
          TX packets:22506 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:584002 (570.3 Kb)  TX bytes:3942056 (3.7 Mb)

vlan16    Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:192.168.8.2  Bcast:192.168.8.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:1771115 errors:0 dropped:0 overruns:0 frame:0
          TX packets:2085282 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:160285895 (152.8 Mb)  TX bytes:174062459 (165.9 Mb)

vlan21    Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:192.168.112.1  Bcast:192.168.112.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:9163581 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11366723 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:600865666 (573.0 Mb)  TX bytes:745571244 (711.0 Mb)

vlan22    Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:192.168.113.1  Bcast:192.168.113.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:50224825 errors:0 dropped:0 overruns:0 frame:0
          TX packets:46690986 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:933850641 (890.5 Mb)  TX bytes:3623270172 (3455.4 Mb)

vlan22:0  Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:192.168.192.1  Bcast:192.168.192.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1

vlan23    Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:192.168.116.1  Bcast:192.168.116.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:40724929 errors:0 dropped:0 overruns:0 frame:0
          TX packets:43185217 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:2402547229 (2291.2 Mb)  TX bytes:4012274449 (3826.4 Mb)

vlan24    Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:192.168.117.1  Bcast:192.168.117.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:14087345 errors:0 dropped:0 overruns:0 frame:0
          TX packets:13716404 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:1496206106 (1426.8 Mb)  TX bytes:1254391198 (1196.2 Mb)

vlan25    Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:192.168.118.1  Bcast:192.168.118.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:21974549 errors:0 dropped:0 overruns:0 frame:0
          TX packets:20700124 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:1904790033 (1816.5 Mb)  TX bytes:1296685747 (1236.6 Mb)

vlan26    Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:192.168.120.1  Bcast:192.168.120.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:859892534 errors:0 dropped:0 overruns:0 frame:0
          TX packets:42079932 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:1658649217 (1581.8 Mb)  TX bytes:2459833754 (2345.8 Mb)

vlan27    Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:192.168.121.1  Bcast:192.168.121.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:4185453 errors:0 dropped:0 overruns:0 frame:0
          TX packets:1742884 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:1581242775 (1507.9 Mb)  TX bytes:156184634 (148.9 Mb)

vlan28    Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:192.168.122.1  Bcast:192.168.122.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:17709881 errors:0 dropped:0 overruns:0 frame:0
          TX packets:22952552 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:1052875016 (1004.0 Mb)  TX bytes:1268367908 (1209.6 Mb)

vlan29    Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:192.168.248.1  Bcast:192.168.248.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:30510624 errors:0 dropped:0 overruns:0 frame:0
          TX packets:28060182 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:170305959 (162.4 Mb)  TX bytes:246683628 (235.2 Mb)

vlan30    Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:192.168.123.1  Bcast:192.168.123.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:20066947 errors:0 dropped:0 overruns:0 frame:0
          TX packets:22376067 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:1212988734 (1156.7 Mb)  TX bytes:1358205640 (1295.2 Mb)

vlan34    Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:192.168.124.1  Bcast:192.168.127.255  Mask:255.255.252.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:644693951 errors:0 dropped:0 overruns:0 frame:0
          TX packets:32108676 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:562037017 (536.0 Mb)  TX bytes:1909510996 (1821.0 Mb)

vlan36    Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:192.168.115.1  Bcast:192.168.115.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:1201207 errors:0 dropped:0 overruns:0 frame:0
          TX packets:1526447 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:243818136 (232.5 Mb)  TX bytes:112892987 (107.6 Mb)

vlan37    Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:172.28.0.8  Bcast:172.28.0.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:17588355 errors:0 dropped:0 overruns:0 frame:0
          TX packets:17447047 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:1284298162 (1224.8 Mb)  TX bytes:1170347932 (1116.1 Mb)

vlan201   Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:10.192.10.190  Bcast:10.192.10.191  Mask:255.255.255.252
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:27092031 errors:0 dropped:0 overruns:0 frame:0
          TX packets:25456083 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:2327726058 (2219.8 Mb)  TX bytes:2369328953 (2259.5 Mb)

vlan209   Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:172.16.77.22  Bcast:172.16.77.23  Mask:255.255.255.252
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:72922 errors:0 dropped:0 overruns:0 frame:0
          TX packets:33630 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:6556329 (6.2 Mb)  TX bytes:4384694 (4.1 Mb)

vlan250   Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:10.0.48.18  Bcast:10.0.48.19  Mask:255.255.255.252
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:2925 errors:0 dropped:0 overruns:0 frame:0
          TX packets:13380 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:181542 (177.2 Kb)  TX bytes:3339287 (3.1 Mb)

vlan875   Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:10.48.0.4  Bcast:10.48.0.63  Mask:255.255.255.192
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:12247 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:0 (0.0 b)  TX bytes:3234155 (3.0 Mb)

vlan1027  Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:192.168.128.1  Bcast:192.168.128.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:110460 errors:0 dropped:0 overruns:0 frame:0
          TX packets:13772 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:5084478 (4.8 Mb)  TX bytes:3314076 (3.1 Mb)

vlan1035  Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:192.168.253.9  Bcast:192.168.253.11  Mask:255.255.255.252
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:887071 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11197 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:41928467 (39.9 Mb)  TX bytes:3061307 (2.9 Mb)

vlan1037  Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:192.168.169.1  Bcast:192.168.169.3  Mask:255.255.255.252
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:12920 errors:0 dropped:0 overruns:0 frame:0
          TX packets:25899 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:3249806 (3.0 Mb)  TX bytes:4059868 (3.8 Mb)

vlan2002  Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:10.11.12.14  Bcast:10.11.12.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:6427 errors:0 dropped:0 overruns:0 frame:0
          TX packets:19229 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:302975 (295.8 Kb)  TX bytes:3830064 (3.6 Mb)

vlan2999  Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:192.168.200.18  Bcast:192.168.200.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:29522 errors:0 dropped:0 overruns:0 frame:0
          TX packets:24418 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:1359879 (1.2 Mb)  TX bytes:3745397 (3.5 Mb)

vlan3997  Link encap:Ethernet  HWaddr 00:23:54:6B:88:2B  
          inet addr:192.168.50.1  Bcast:192.168.50.3  Mask:255.255.255.252
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:427548 errors:0 dropped:0 overruns:0 frame:0
          TX packets:317734 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:189154621 (180.3 Mb)  TX bytes:29775653 (28.3 Mb)
```



```
-A INPUT -i vlan1021 -j input_int
-A INPUT -i vlan11 -j input_int
-A INPUT -i bond0 -j input_dmz
-A INPUT -i bond1 -j input_dmz
-A INPUT -i eth0 -j input_dmz
-A INPUT -i eth1 -j input_dmz
-A INPUT -i eth2 -j input_dmz
-A INPUT -i eth3 -j input_dmz
```

```
-A FORWARD -i vlan1021 -j forward_int
-A FORWARD -i vlan11 -j forward_int
-A FORWARD -i vlan13 -j forward_ext
-A FORWARD -i bond0 -j forward_dmz
-A FORWARD -i bond1 -j forward_dmz
-A FORWARD -i eth0 -j forward_dmz
-A FORWARD -i eth1 -j forward_dmz
-A FORWARD -i eth2 -j forward_dmz
-A FORWARD -i eth3 -j forward_dmz
-A FORWARD -j DROP
```


```
-A forward_dmz -s 172.20.64.0/19 -i eth0 -o vlan13 -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
-A forward_dmz -s 172.20.64.0/19 -i eth1 -o vlan13 -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
-A forward_dmz -s 172.20.64.0/19 -i eth2 -o vlan13 -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
-A forward_dmz -s 172.20.64.0/19 -i eth3 -o vlan13 -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
-A forward_dmz -m pkttype --pkt-type multicast -j DROP
-A forward_dmz -m pkttype --pkt-type broadcast -j DROP
-A forward_dmz -p tcp -m limit --limit 3/min -m tcp --tcp-flags FIN,SYN,RST,ACK SYN -j LOG --log-prefix "SFW2-FWDdmz-DROP-DEFLT " --log-tcp-options --log-ip-options
-A forward_dmz -p icmp -m limit --limit 3/min -j LOG --log-prefix "SFW2-FWDdmz-DROP-DEFLT " --log-tcp-options --log-ip-options
-A forward_dmz -p udp -m limit --limit 3/min -m conntrack --ctstate NEW -j LOG --log-prefix "SFW2-FWDdmz-DROP-DEFLT " --log-tcp-options --log-ip-options
-A forward_dmz -j DROP
```

```
-A forward_ext -p icmp -m conntrack --ctstate RELATED,ESTABLISHED -m icmp --icmp-type 0 -j ACCEPT
-A forward_ext -p icmp -m conntrack --ctstate RELATED,ESTABLISHED -m icmp --icmp-type 3 -j ACCEPT
-A forward_ext -p icmp -m conntrack --ctstate RELATED,ESTABLISHED -m icmp --icmp-type 11 -j ACCEPT
-A forward_ext -p icmp -m conntrack --ctstate RELATED,ESTABLISHED -m icmp --icmp-type 12 -j ACCEPT
-A forward_ext -p icmp -m conntrack --ctstate RELATED,ESTABLISHED -m icmp --icmp-type 14 -j ACCEPT
-A forward_ext -p icmp -m conntrack --ctstate RELATED,ESTABLISHED -m icmp --icmp-type 18 -j ACCEPT
-A forward_ext -p icmp -m conntrack --ctstate RELATED,ESTABLISHED -m icmp --icmp-type 3/2 -j ACCEPT
-A forward_ext -p icmp -m conntrack --ctstate RELATED,ESTABLISHED -m icmp --icmp-type 5 -j ACCEPT
-A forward_ext -d 192.168.1.0/24 -i vlan13 -o vlan1021 -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A forward_ext -d 192.168.1.0/24 -i vlan13 -o vlan11 -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A forward_ext -d 192.168.1.0/24 -i vlan13 -o bond0 -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A forward_ext -d 192.168.1.0/24 -i vlan13 -o bond1 -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A forward_ext -d 192.168.1.0/24 -i vlan13 -o eth0 -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A forward_ext -d 192.168.1.0/24 -i vlan13 -o eth1 -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A forward_ext -d 192.168.1.0/24 -i vlan13 -o eth2 -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A forward_ext -d 192.168.1.0/24 -i vlan13 -o eth3 -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A forward_ext -m pkttype --pkt-type multicast -j DROP
-A forward_ext -m pkttype --pkt-type broadcast -j DROP
-A forward_ext -p tcp -m limit --limit 3/min -m tcp --tcp-flags FIN,SYN,RST,ACK SYN -j LOG --log-prefix "SFW2-FWDext-DROP-DEFLT " --log-tcp-options --log-ip-options
-A forward_ext -p icmp -m limit --limit 3/min -j LOG --log-prefix "SFW2-FWDext-DROP-DEFLT " --log-tcp-options --log-ip-options
-A forward_ext -p udp -m limit --limit 3/min -m conntrack --ctstate NEW -j LOG --log-prefix "SFW2-FWDext-DROP-DEFLT " --log-tcp-options --log-ip-options
-A forward_ext -j DROP
```


```
-A input_int -j reject_func
-A reject_func -p tcp -j REJECT --reject-with tcp-reset
-A reject_func -p udp -j REJECT --reject-with icmp-port-unreachable
-A reject_func -j REJECT --reject-with icmp-proto-unreachable
```



