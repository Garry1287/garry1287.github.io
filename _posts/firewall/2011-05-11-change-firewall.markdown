---
layout: post
title:  "change-firewall"
date:   2011-05-11 19:00:56 +0400
categories: firewall
tags: firewall
---

# change-firewall
-A PREROUTING -s 81.20.192.90/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 2343 -j DNAT --to-destination 192.168.121.4:443    #asterisk
-A PREROUTING -d 81.20.192.19/32 -p tcp -m tcp --dport 23543 -j DNAT --to-destination 192.168.1.129:80      #zabbix for green

-A PREROUTING -d 81.20.192.19/32 -p tcp -m tcp --dport 8880 -j DNAT --to-destination 192.168.1.15:7781          #доступ к биллингу пользователям
-A PREROUTING -d 192.168.253.1/32 -p tcp -m tcp --dport 80 -j DNAT --to-destination 192.168.1.15:7780           #FSB биллинг

??????????????????????????????????????????????????????????????????????????????????????????? Удалил нах
-A PREROUTING -s 84.16.137.94/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 2323 -j LOG --log-prefix "from STAR To teleSORM " --log-tcp-options --log-ip-options  #NetbyNet to ast (23 порт) telnet  #УДАЛИТь НАХ
-A PREROUTING -s 84.16.137.94/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 2323 -j DNAT --to-destination 192.168.1.8:23
-A PREROUTING -s 83.136.235.94/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 3389 -j LOG --log-prefix "from Satikov To 1C " --log-tcp-options --log-ip-options   # To 1C   (удалим)
-A PREROUTING -s 91.190.76.53/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 3389 -j LOG --log-prefix "from MTT To 1C " --log-tcp-options --log-ip-options   #Наша сеть )


Удалил нах
-A PREROUTING -s 77.233.199.98/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 8880 -j DNAT --to-destination 192.168.1.14:80            #billing  MEGASVYAZ LLC
-A PREROUTING -s 77.233.199.98/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 8080 -j DNAT --to-destination 192.168.1.14:8080
-A PREROUTING -s 77.233.199.98/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 22 -j DNAT --to-destination 192.168.1.14:22
-A PREROUTING -s 77.233.199.98/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 443 -j DNAT --to-destination 192.168.1.14:443

Нахер
-A PREROUTING -s 192.168.130.110/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 514 -j DNAT --to-destination 192.168.1.178:514             #Логирование с 130.110 на 1.178, 1.160  Trans bank
-A PREROUTING -s 192.168.130.110/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 514 -j DNAT --to-destination 192.168.1.160:514


-A PREROUTING -d 81.20.192.33/32 -p tcp -m tcp --dport 11194 -j DNAT --to-destination 192.168.1.14:1194                             #проброс openvpn для биллинга

iptables -t nat -D PREROUTING -s 81.20.196.8/32 -d 81.20.192.19/32 -p tcp -m tcp --dport 4389 -j DNAT --to-destination 192.168.1.34:3389            #Проброст порта от физика (НАХ)

************************************************************************************************************************************************
-A PREROUTING -s 195.34.240.24/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 443 -j DNAT --to-destination 192.168.1.15:4461        #Проброс порта от ростелеком для биллинга

***************************************************************************************************************************
-A PREROUTING -d 81.20.192.33/32 -p tcp -m tcp --dport 443 -j DNAT --to-destination 192.168.1.15:4459                       #Проброс порта  для биллинга

-A PREROUTING -s 81.20.192.57/32 -d 81.20.192.19/32 -p tcp -m tcp --dport 15210 -j DNAT --to-destination 192.168.1.15:1521
-A PREROUTING -s 81.20.192.6/32 -d 81.20.192.19/32 -p tcp -m tcp --dport 15211 -j DNAT --to-destination 192.168.1.15:1521   #Oracle port

-A PREROUTING -d 81.20.192.33/32 -p tcp -m tcp --dport 80 -j DNAT --to-destination 192.168.1.15:7780

-A PREROUTING -s 81.20.196.8/32 -d 81.20.192.19/32 -p tcp -m tcp --dport 2222 -j DNAT --to-destination 192.168.1.188:22    #ВОва   (нах)
-A PREROUTING -s 81.20.192.53/32 -d 81.20.192.33/32 -p tcp -m tcp --dport 22 -j DNAT --to-destination 192.168.1.178:22 #Копалин  с NTP1 обращаемся к саппфиру    (наХ)

-A PREROUTING -d 81.20.192.33/32 -p tcp -m tcp --dport 8888 -j DNAT --to-destination 192.168.1.15:7780          #Проброс к биллингу
-A PREROUTING -s 10.222.0.10/32 -d 10.192.10.190/32 -p tcp -m tcp --dport 10051 -j DNAT --to-destination 192.168.1.129:10051    #Проброс для zabbix для комбината

-A PREROUTING -s 80.75.128.0/20 -d 81.20.192.19/32 -p tcp -m tcp --dport 3389 -j LOG --log-prefix "from M To 1C " --log-tcp-options --log-ip-options  #MTC 1c - нах их

forward к этим правилам
-A FORWARD -s 192.168.253.10/32 -d 10.148.0.14/32 -p tcp -m tcp --dport 22 -j ACCEPT


iptables -I FORWARD 1  -i vlan10 -s 81.20.192.90/32 -o vlan27 -d 192.168.121.4/32 -p tcp -m tcp --dport 2343  -j ACCEPT
разрешаем 81.20.192.90 к 192.168.121.4
iptables -I FORWARD 2 -i vlan10 -o enp5s1 -d 192.168.1.129/32 -p tcp -m tcp --dport 23543  -j ACCEPT
разрешаем зелёным к zabbix 192.168.1.129

iptables -I FORWARD 3 -i vlan10 -o enp5s1 -d 192.168.1.15/32 -p tcp -m tcp --dport 8880  -j ACCEPT
iptables -I FORWARD 4 -i vlan1035 -o enp5s1 -d 192.168.1.15/32 -p tcp -m tcp --dport 80  -j ACCEPT
разрешаем всем обращаться к 192.168.1.15
разрешаем 192.168.253.1 (fsb) r биллингу 192.168.1.15

разрешаем всем обращаться к 192.168.1.14
iptables -I FORWARD 6 -i vlan10 -o enp5s1 -d 192.168.1.14/32 -p tcp -m tcp --dport 11194  -j ACCEPT
iptables -I FORWARD 7 -i vlan10 -o enp5s1 -d 192.168.1.15/32 -p tcp -m tcp --dport 443  -j ACCEPT
iptables -I FORWARD 8 -i vlan10 -s 81.20.192.6/32 -o enp5s1 -d 192.168.1.15/32 -p tcp -m tcp --dport 15211  -j ACCEPT
iptables -I FORWARD 9 -i vlan10 -o enp5s1 -d 192.168.1.15/32 -p tcp -m tcp --dport 80  -j ACCEPT
iptables -I FORWARD 10 -i vlan10 -o enp5s1 -d 192.168.1.15/32 -p tcp -m tcp --dport 8888  -j ACCEPT
iptables -I FORWARD 11 -i vlan10 -s 10.222.0.10/32 -o enp5s1 -d 192.168.1.129/32 -p tcp -m tcp --dport 10051  -j ACCEPT

#iptables -A INPUT -p tcp -m tcp --dport 22 -m comment --comment "Разрешим доступ к SSH всем желающим" -j ACCEPT



из наших сетей в локалку
из наших сетей 





Проверяем INPUT, запрещем со всех
разрешаем радиус на  172.31.3.1
-A allowed_ports -s 192.168.0.0/16 -p udp -m udp --dport 1812 -j ACCEPT




---------------------------------------------------------------------------------------------------------------------------------------------------------
1)доступ с лан
            - nlmk
            - mngt сети
            - не явные mngt сети (ебург)
2)доступ в инет
3)инет через openvpn
4) особые правила

5) доступ с whatup
            - nlmk
            - mngt сети
            - не явные mngt сети (ебург)
6) доступ с whatup_green
            - mngt сети
---------------------------------------------------------------------------------------------------------------------------------------------------------
1)

 iptables -t nat -N POSTROUTING_INET
iptables -t nat -A POSTROUTING_INET -o vlan10 -j SNAT --to-source 81.20.192.32

iptables -t nat  -A POSTROUTING -s 192.168.1.0/24  -j POSTROUTING_INET


-A POSTROUTING -s 192.168.248.101/32 -o vlan10 -j SNAT --to-source 81.20.192.32
-A POSTROUTING -s 192.168.248.102/32 -o vlan10 -j SNAT --to-source 81.20.192.32
-A POSTROUTING -s 192.168.248.100/32 -o vlan10 -j SNAT --to-source 81.20.192.32


 PHYS
 iptables -t nat -N POSTROUTING_PHYS
 iptables -t nat -I POSTROUTING 2 -s 192.168.1.0/24 -j POSTROUTING_PHYS
 iptables -t nat -A POSTROUTING_PHYS  -d 192.168.117.0/24 -o vlan24 -j SNAT --to-source 192.168.117.1
 iptables -t nat -A POSTROUTING_PHYS -d 192.168.118.0/24 -o vlan25 -j SNAT --to-source 192.168.118.1
 iptables -t nat -A POSTROUTING_PHYS -d 192.168.120.0/24 -o vlan26 -j SNAT --to-source 192.168.120.1
 iptables -t nat -A POSTROUTING_PHYS -d 192.168.121.0/24 -o vlan27 -j SNAT --to-source 192.168.121.1
 iptables -t nat -A POSTROUTING_PHYS -d 192.168.122.0/24 -o vlan28 -j SNAT --to-source 192.168.122.1
 iptables -t nat -A POSTROUTING_PHYS -d 192.168.123.0/24 -o vlan30 -j SNAT --to-source 192.168.123.1
 iptables -t nat -A POSTROUTING_PHYS -d 192.168.124.0/22 -o vlan34 -j SNAT --to-source 192.168.124.1
 iptables -t nat -A POSTROUTING_PHYS -d 172.28.0.0/24 -o vlan37 -j SNAT --to-source 172.28.0.8
iptables -t nat -A POSTROUTING_PHYS -d 10.148.0.0/28 -o  vlan1901  -j SNAT --to-source 10.148.0.8
iptables -t nat -A POSTROUTING_PHYS -d 10.148.0.32/27 -o  vlan133  -j SNAT --to-source 10.148.0.33
iptables -t nat -A POSTROUTING_PHYS -d 10.148.2.0/23 -o enp2s0.134.134 -j SNAT --to-source 10.148.2.1
 
 iptables -t nat -N POSTROUTING_RADIO
iptables  -t nat -I POSTROUTING 3 -s 192.168.1.0/24 -j POSTROUTING_RADIO
iptables  -t nat -A POSTROUTING_RADIO -d 192.168.112.0/24 -o vlan21 -j SNAT --to-source 192.168.112.1
iptables -t nat -A POSTROUTING_RADIO -d 192.168.116.0/24 -o vlan23 -j SNAT --to-source 192.168.116.1
iptables -t nat -A POSTROUTING_RADIO -d 192.168.248.0/24 -o vlan29 -j SNAT --to-source 192.168.248.1
iptables -t nat -A POSTROUTING_RADIO -d 192.168.140.0/24 -o vlan40 -j SNAT --to-source 192.168.140.1


iptables -t nat -N POSTROUTING_MNGT
 iptables  -t nat -I POSTROUTING 4 -s 192.168.1.0/24 -j POSTROUTING_MNGT
iptables -t nat -A POSTROUTING_MNGT -d 192.168.113.0/24 -o vlan22 -j SNAT --to-source 192.168.113.1
iptables -t nat -A POSTROUTING_MNGT -d 192.168.115.0/24 -o vlan36 -j SNAT --to-source 192.168.115.1
iptables -t nat -A POSTROUTING_MNGT -d 192.168.60.0/24 -o vlan39 -j SNAT --to-source 192.168.60.1
iptables -t nat -A POSTROUTING_MNGT -d 192.168.253.68/29 -o vlan90 -j SNAT --to-source 192.168.253.68
iptables -t nat -A POSTROUTING_MNGT -d 192.168.253.20/30 -o vlan99 -j SNAT --to-source 192.168.253.22
iptables -t nat -A POSTROUTING_MNGT -d 192.168.253.8/29 -o  vlan1150  -j SNAT --to-source 192.168.253.9
iptables -t nat -A POSTROUTING_MNGT -d 192.168.200.0/24 -o  vlan2999  -j SNAT --to-source 192.168.200.18
iptables -t nat -A POSTROUTING_MNGT -d 192.168.253.40/29 -o  vlan3151 -j SNAT --to-source 192.168.253.41
iptables -t nat -A POSTROUTING_MNGT -d 192.168.50.0/30 -o  vlan3997 -j SNAT --to-source 192.168.50.1
iptables -t nat -A POSTROUTING_MNGT -d 192.168.253.48/29 -o  vlan401 -j SNAT --to-source 192.168.253.49

iptables -t nat -N POSTROUTING_VPN
iptables -t nat -I POSTROUTING 5 -s 192.168.1.0/24 -j POSTROUTING_VPN
iptables -t nat -A POSTROUTING_VPN -o vlan201 -j SNAT --to-source 10.192.10.190

iptables -t nat -N POSTROUTING_GREEN_WHATUP
iptables -t nat -I POSTROUTING 6 -s 192.168.1.0/24 -j POSTROUTING_GREEN_WHATUP
iptables -t nat -I POSTROUTING 7 -s 172.31.255.218/30 -j POSTROUTING_GREEN_WHATUP
iptables -t nat -A POSTROUTING_GREEN_WHATUP -d 192.168.253.248/30 -o  vlan402 -j SNAT --to-source 192.168.253.249

iptables -t nat -I POSTROUTING -s 192.168.1.0/24 -d 192.168.253.48/29 -o  vlan401 -j SNAT --to-source 192.168.253.49



iptables -t nat -N POSTROUTING_VOIP
iptables -t nat -I POSTROUTING 8 -s 192.168.1.0/24 -j POSTROUTING_VOIP
iptables  -t nat -A POSTROUTING_VOIP -d 192.168.130.0/24 -o vlan10 -j SNAT --to-source 81.20.192.32
iptables  -t nat -A  POSTROUTING_VOIP -d 172.16.0.0/16 -o vlan10 -j SNAT --to-source 81.20.192.32
iptables  -t nat -A POSTROUTING_VOIP -d 192.168.131.0/24 -o vlan10 -j SNAT --to-source 81.20.192.32


 iptables -t nat -N POSTROUTING_MNGT10VLAN
 iptables  -t nat -I POSTROUTING 10 -s 192.168.1.0/24 -j POSTROUTING_MNGT10VLAN
 iptables  -t nat -A POSTROUTING_MNGT10VLAN  -d 192.168.70.0/24 -o vlan10 -j SNAT --to-source 81.20.192.19
 iptables  -t nat -A POSTROUTING_MNGT10VLAN -d 192.168.83.0/24 -o vlan10 -j SNAT --to-source 81.20.192.19
 iptables  -t nat -A POSTROUTING_MNGT10VLAN -d 192.168.253.80/29 -o vlan10 -j SNAT --to-source 81.20.192.19

 
 
 
-A POSTROUTING -s 217.107.196.0/26 -d 192.168.121.2/32 -o vlan27 -j SNAT --to-source 192.168.121.1  #Green to 4900 cat
-A POSTROUTING -s 172.31.255.216/30 -d 192.168.121.2/32 -o vlan27 -j SNAT --to-source 192.168.121.1 # GREEN to 121
-A POSTROUTING -d 192.168.1.15/32 -p tcp -m tcp --dport 4459 -j SNAT --to-source 192.168.1.11 # Правила для работы биллинга из локалки
-A POSTROUTING -d 192.168.1.15/32 -p tcp -m tcp --dport 7780 -j SNAT --to-source 192.168.1.11 # # Правила для работы биллинга из локалки


 
LAN к mngt, инет
Whatup к mngt
Whatup_green к mngt
Green к mngt


vlan209 inet 172.16.77.22/30 
192.168.114.66/30 217
691  BSMP8mkrm-Poliklinika3

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Политика такова, если надо отфильтровать по какому нибудь признаку, заворачиваем в отдельную цепочку, там делаем все проверки, режем, разрешаем, что надо и в конце возвращаем в основную, либо дропаем

iptables -P FORWARD DROP
iptables -I FORWARD 1 -m conntrack --ctstate INVALID -j DROP
iptables -I FORWARD 2 -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
iptables -I FORWARD 3 -p tcp -m tcp --tcp-flags SYN,RST SYN -j TCPMSS --clamp-mss-to-pmtu

1)доступ с лан
            - nlmk
            - mngt сети
            - не явные mngt сети (ебург)
2)доступ в инет
3)инет через openvpn
4) особые правила

5) доступ с whatup
            - nlmk
            - mngt сети
            - не явные mngt сети (ебург)
6) доступ с whatup_green
            - mngt сети
            
1) Ходить в инет
2)Управлять mngt - nat правила (Управлять с lan и двух whatup)
3) Все должно инициироваться из LAN, Green, whatup, whatup2
4) c оборудования разрешить trap, syslog и ??? Посмотреть мониторинг (snmp, icmp, log, ntp, radius, ) 



-A FORWARD -p tcp -m tcp --tcp-flags SYN,RST SYN -j TCPMSS --clamp-mss-to-pmtu
Добавляем интерфейсы в forward
-A FORWARD -m limit --limit 3/min -j LOG --log-prefix "SFW2-FWD-ILL-ROUTING " --log-tcp-options --log-ip-options
-A FORWARD -j DROP


-A FORWARD -s 192.168.1.0/24 -i enp5s1 -j FORWARD_INET
-A FORWARD_INET -o vlan10 -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT



Из вне разрешаем
-A forward_dmz -p icmp -m conntrack --ctstate RELATED,ESTABLISHED -m icmp --icmp-type 0 -j ACCEPT
-A forward_dmz -p icmp -m conntrack --ctstate RELATED,ESTABLISHED -m icmp --icmp-type 3 -j ACCEPT
-A forward_dmz -p icmp -m conntrack --ctstate RELATED,ESTABLISHED -m icmp --icmp-type 11 -j ACCEPT
-A forward_dmz -p icmp -m conntrack --ctstate RELATED,ESTABLISHED -m icmp --icmp-type 12 -j ACCEPT
-A forward_dmz -p icmp -m conntrack --ctstate RELATED,ESTABLISHED -m icmp --icmp-type 14 -j ACCEPT
-A forward_dmz -p icmp -m conntrack --ctstate RELATED,ESTABLISHED -m icmp --icmp-type 18 -j ACCEPT
-A forward_dmz -p icmp -m conntrack --ctstate RELATED,ESTABLISHED -m icmp --icmp-type 3/2 -j ACCEPT
-A forward_dmz -p icmp -m conntrack --ctstate RELATED,ESTABLISHED -m icmp --icmp-type 5 -j ACCEPT


Из вне
-A forward_ext -d 192.168.1.0/24 -i vlan13 -o vlan27 -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT

Из доверенных сетей
-A forward_dmz -s 192.168.1.0/24 -i bond0.1953.1011 -o vlan13 -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT

В завершении следующие действия


iptables -A FORWARD -m pkttype --pkt-type multicast -j DROP
iptables -A FORWARD -m pkttype --pkt-type broadcast -j DROP
iptables -A FORWARD -p tcp -m limit --limit 3/min -m tcp --tcp-flags FIN,SYN,RST,ACK SYN -j LOG --log-prefix "FW-FWD-DROP-DEFLT " --log-tcp-options --log-ip-options
iptables -A FORWARD -p icmp -m limit --limit 3/min -j LOG --log-prefix "FW-FWD-DROP-DEFLT " --log-tcp-options --log-ip-options
iptables -A FORWARD -p udp -m limit --limit 3/min -m conntrack --ctstate NEW -j LOG --log-prefix "FW-FWDdmz-DROP-DEFLT " --log-tcp-options --log-ip-options




PREROUTING FOrward
-A FORWARD -s 81.20.192.90/32 -d 192.168.121.4/32 -i vlan10 -o vlan27 -p tcp -m tcp --dport 2343 -j ACCEPT
-A FORWARD -d 192.168.1.14/32 -i vlan10 -o enp5s1 -p tcp -m tcp --dport 11194 -j ACCEPT
-A FORWARD -d 192.168.1.15/32 -i vlan10 -o enp5s1 -p tcp -m tcp --dport 443 -j ACCEPT
-A FORWARD -s 81.20.192.6/32 -d 192.168.1.15/32 -i vlan10 -o enp5s1 -p tcp -m tcp --dport 15211 -j ACCEPT
-A FORWARD -d 192.168.1.15/32 -i vlan10 -o enp5s1 -p tcp -m tcp --dport 80 -j ACCEPT
-A FORWARD -d 192.168.1.15/32 -i vlan10 -o enp5s1 -p tcp -m tcp --dport 8888 -j ACCEPT
-A FORWARD -d 192.168.1.129/32 -i vlan10 -o enp5s1 -p tcp -m tcp --dport 23543 -j ACCEPT
-A FORWARD -d 192.168.1.15/32 -i vlan10 -o enp5s1 -p tcp -m tcp --dport 8880 -j ACCEPT
-A FORWARD -d 192.168.1.15/32 -i vlan1035 -o enp5s1 -p tcp -m tcp --dport 80 -j ACCEPT
---------------------FSB------------------
-A FORWARD -s 192.168.253.2/32 -d 192.168.1.15/32 -p tcp -m tcp --dport 7780 -j ACCEPT
-A FORWARD -d 192.168.1.15/32 -p tcp -m tcp --dport 7780 -j ACCEPT

-A FORWARD -s 10.222.0.10/32 -d 192.168.1.129/32 -i vlan10 -o enp5s1 -p tcp -m tcp --dport 10051 -j ACCEPT

FORWARD к INET, PHYS, RADIO, MNGT, NLMK

 iptables -N FORWARD_PHYS
 iptables -A  FORWARD_PHYS  -d 192.168.117.0/24 -o vlan24 -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
 iptables -A  FORWARD_PHYS -d 192.168.118.0/24 -o vlan25 -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
 iptables -A  FORWARD_PHYS -d 192.168.120.0/24 -o vlan26 -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
 iptables -A  FORWARD_PHYS -d 192.168.121.0/24 -o vlan27 -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
 iptables -A  FORWARD_PHYS -d 192.168.122.0/24 -o vlan28 -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
 iptables -A  FORWARD_PHYS -d 192.168.123.0/24 -o vlan30  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
 iptables -A  FORWARD_PHYS -d 192.168.124.0/22 -o vlan34  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
 iptables -A  FORWARD_PHYS -d 172.28.0.0/24 -o vlan37  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
iptables -A  FORWARD_PHYS -d 10.148.0.0/28 -o  vlan1901  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
 iptables -A  FORWARD_PHYS -d 10.148.0.32/27 -o  vlan133  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
 iptables -A  FORWARD_PHYS -d 10.148.2.0/23 -o enp2s0.134.134  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
 iptables -A FORWARD_PHYS -j RETURN
iptables -I FORWARD 5 -i enp5s1 -s 192.168.1.0/24 -j FORWARD_PHYS 
 
iptables -N FORWARD_RADIO
iptables -A FORWARD_RADIO -d 192.168.112.0/24 -o vlan21 -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
iptables -A FORWARD_RADIO -d 192.168.116.0/24 -o vlan23  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
iptables -A FORWARD_RADIO -d 192.168.248.0/24 -o vlan29  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
iptables -A FORWARD_RADIO -d 192.168.140.0/24 -o vlan40 -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
 iptables -A FORWARD_RADIO -j RETURN
iptables  -I FORWARD 6 -i enp5s1 -s 192.168.1.0/24 -j FORWARD_RADIO

iptables  -N FORWARD_MNGT
iptables  -A FORWARD_MNGT -d 192.168.113.0/24 -o vlan22  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
iptables  -A FORWARD_MNGT -d 192.168.115.0/24 -o vlan36  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
iptables  -A FORWARD_MNGT -d 192.168.60.0/24 -o vlan39  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
iptables  -A FORWARD_MNGT -d 192.168.253.68/29 -o vlan90  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
iptables  -A FORWARD_MNGT -d 192.168.253.20/30 -o vlan99  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
iptables  -A FORWARD_MNGT -d 192.168.253.8/29 -o  vlan1150  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
iptables  -A FORWARD_MNGT -d 192.168.200.0/24 -o  vlan2999  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
iptables  -A FORWARD_MNGT -d 192.168.253.40/29 -o  vlan3151  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
iptables  -A FORWARD_MNGT -d 192.168.50.0/30 -o  vlan3997  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
iptables  -A FORWARD_MNGT -d 192.168.253.48/29 -o  vlan401  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
iptables -A FORWARD_MNGT -j RETURN
 iptables  -I FORWARD 7 -s 192.168.1.0/24 -j FORWARD_MNGT

iptables  -N FORWARD_VPN
iptables  -A FORWARD_VPN -o vlan201  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
iptables -A FORWARD_VPN -j RETURN
iptables  -I FORWARD 8 -s 192.168.1.0/24 -j FORWARD_VPN



iptables  -N FORWARD_GREEN_WHATUP
iptables  -A FORWARD_GREEN_WHATUP -d 192.168.253.248/30 -o  vlan402  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
iptables -A FORWARD_GREEN_WHATUP -j RETURN
iptables  -I FORWARD 9 -s 192.168.1.0/24 -j FORWARD_GREEN_WHATUP
iptables  -I FORWARD 10 -s 172.31.255.218/30 -j FORWARD_GREEN_WHATUP


iptables -I FORWARD 11 -s 192.168.1.0/24 -d 192.168.253.48/29 -o  vlan401 -j ACCEPT

iptables  -N FORWARD_VOIP
iptables   -A FORWARD_VOIP -d 192.168.130.0/24 -o vlan10  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
iptables   -A  FORWARD_VOIP -d 172.16.0.0/16 -o vlan10  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
iptables   -A FORWARD_VOIP -d 192.168.131.0/24 -o vlan10  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
iptables -A FORWARD_VOIP -j RETURN

iptables  -I FORWARD 12 -s 192.168.1.0/24 -j FORWARD_VOIP


 iptables  -N FORWARD_MNGT10VLAN
 iptables   -A FORWARD_MNGT10VLAN  -d 192.168.70.0/24 -o vlan10  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
 iptables   -A FORWARD_MNGT10VLAN -d 192.168.83.0/24 -o vlan10  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
 iptables   -A FORWARD_MNGT10VLAN -d 192.168.253.80/29 -o vlan10  -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
iptables -A FORWARD_MNGT10VLAN -j RETURN

  iptables  -I FORWARD 13 -s 192.168.1.0/24 -j FORWARD_MNGT10VLAN

 
 
  Правила от исходящих интерфейсов сетей
 iptables -A FORWARD -i vlan -m state --state RELATED,ESTABLISHED -j ACCEPT
  
 
 
 
 ----------------------------------------------------------------------------------------------
-A FORWARD -s 10.210.0.0/22 -j GREEN
-A FORWARD -s 192.168.121.2/32 -j GREEN
-A FORWARD -s 172.28.0.0/24 -j GREEN
-A FORWARD -s 172.31.255.216/30 -j GREEN
-A FORWARD -s 172.31.255.212/30 -j GREEN
-A FORWARD -s 10.148.0.32/27 -j GREEN
-A FORWARD -s 10.148.2.0/23 -j GREEN
-A FORWARD -s 192.168.124.0/22 -j GREEN
-A FORWARD -s 192.168.122.0/23 -j GREEN
-A FORWARD -s 192.168.120.0/24 -j GREEN
-A FORWARD -s 192.168.118.0/24 -j GREEN
-A FORWARD -s 192.168.117.0/24 -j GREEN

A FORWARD -s 192.168.132.0/23 -i tun+ -j OPENVPN

-A FORWARD -s 192.168.253.10/32 -d 10.148.0.14/32 -p tcp -m tcp --dport 22 -j ACCEPT
-A FORWARD -s 192.168.253.10/32 -d 192.168.1.15/32 -p tcp -m tcp --dport 7780 -j ACCEPT

-A FORWARD -s 192.168.1.0/24 -d 192.168.169.2/32 -m conntrack --ctstate NEW,RELATED,ESTABLISHED -m limit --limit 3/min -j LOG --log-prefix "To 1C " --log-tcp-options --log-ip-options
-A FORWARD -s 192.168.1.0/24 -d 192.168.169.2/32 -m conntrack --ctstate NEW,RELATED,ESTABLISHED -j ACCEPT
-A FORWARD -s 192.168.169.2/32 -d 192.168.1.0/24 -m conntrack --ctstate ESTABLISHED -m limit --limit 3/min -j LOG --log-prefix "From 1C " --log-tcp-options --log-ip-options
-A FORWARD -s 192.168.169.2/32 -d 192.168.1.0/24 -m conntrack --ctstate ESTABLISHED -j ACCEPT
-A FORWARD -s 192.168.169.2/32 -d 192.168.1.0/24 -p udp -m multiport --dports 53,69 -j ACCEPT
-A FORWARD -s 192.168.169.2/32 -m limit --limit 3/min -j LOG --log-prefix "MTT atack from 1c to LAN " --log-tcp-options --log-ip-options
-A FORWARD -s 192.168.169.2/32 -j DROP




-A GREEN -p udp -m udp --dport 161 -j REJECT --reject-with icmp-port-unreachable
-A GREEN -s 192.168.121.2/32 -m state --state RELATED,ESTABLISHED -j ACCEPT
-A GREEN -d 192.168.121.2/32 -j ACCEPT
-A GREEN -s 172.28.0.0/24 -m state --state RELATED,ESTABLISHED -j ACCEPT
-A GREEN -d 172.28.0.0/24 -j ACCEPT
-A GREEN -s 192.168.117.124/32 -j ACCEPT
-A GREEN -s 192.168.117.137/32 -j ACCEPT
-A GREEN -s 192.168.117.143/32 -j ACCEPT
-A GREEN -s 192.168.117.132/32 -j ACCEPT
-A GREEN -s 192.168.117.123/32 -j ACCEPT
-A GREEN -s 192.168.117.126/32 -j ACCEPT
-A GREEN -s 192.168.117.120/32 -j ACCEPT
-A GREEN -s 192.168.117.130/32 -j ACCEPT
-A GREEN -s 192.168.117.138/32 -j ACCEPT
-A GREEN -d 192.168.253.248/30 -j ACCEPT
-A GREEN -s 10.148.0.32/27 -m state --state RELATED,ESTABLISHED -j ACCEPT
-A GREEN -d 10.148.0.32/27 -j ACCEPT
-A GREEN -s 10.148.2.0/23 -m state --state RELATED,ESTABLISHED -j ACCEPT
-A GREEN -d 10.148.2.0/23 -j ACCEPT
-A GREEN -s 192.168.124.0/22 -m state --state RELATED,ESTABLISHED -j ACCEPT
-A GREEN -d 192.168.124.0/22 -j ACCEPT
-A GREEN -s 192.168.122.0/23 -m state --state RELATED,ESTABLISHED -j ACCEPT
-A GREEN -d 192.168.122.0/23 -j ACCEPT
-A GREEN -s 192.168.120.0/24 -m state --state RELATED,ESTABLISHED -j ACCEPT
-A GREEN -d 192.168.120.0/24 -j ACCEPT
-A GREEN -s 192.168.118.0/24 -m state --state RELATED,ESTABLISHED -j ACCEPT
-A GREEN -d 192.168.118.0/24 -j ACCEPT
-A GREEN -s 192.168.117.0/24 -m state --state RELATED,ESTABLISHED -j ACCEPT
-A GREEN -d 192.168.117.0/24 -j ACCEPT
-A GREEN -j REJECT --reject-with icmp-port-unreachable
117 cеть разрешить к астериску 81.20.192.20
















 #LAN for phys
-A POSTROUTING -s 192.168.1.0/24 -d 192.168.120.0/24 -o vlan26 -j SNAT --to-source 192.168.120.1

-A POSTROUTING -s 192.168.1.0/24 -d 192.168.128.0/24 -o vlan1027 -j SNAT --to-source 192.168.128.1
-A POSTROUTING -s 192.168.1.0/24 ! -d 192.168.0.0/16 -o vlan1901 -j SNAT --to-source 10.148.0.8


iptables -I POSTROUTING -s 192.168.132.88/30 -o vlan10 -j SNAT --to-source 81.20.192.32
iptables -I POSTROUTING -s 192.168.132.40/30 -o vlan10 -j SNAT --to-source 81.20.192.32
iptables -I POSTROUTING -s 192.168.132.68/30 -o vlan10 -j SNAT --to-source 81.20.192.32
iptables -I POSTROUTING -s 192.168.132.72/30 -o vlan10 -j SNAT --to-source 81.20.192.32
iptables -A POSTROUTING -s 192.168.132.4/30 -o vlan10 -j SNAT --to-source 81.20.192.32
iptables -A POSTROUTING -s 192.168.132.60/30 -o vlan10 -j SNAT --to-source 81.20.192.32

iptables -A POSTROUTING -s 192.168.1.0/24 -d 192.168.253.80/29 -o vlan10 -j SNAT --to-source 81.20.192.32 
iptables -A POSTROUTING -s 192.168.1.0/24 -d 192.168.50.0/30 -o vlan3997 -j SNAT --to-source 192.168.50.1
iptables -A POSTROUTING -s 192.168.1.0/24 -d 192.168.253.64/29 -o vlan90 -j SNAT --to-source 192.168.253.68  #Доступ к хранилищам
iptables -A POSTROUTING -s 192.168.1.0/24 -o vlan99 -j SNAT --to-source 192.168.253.22       #MNGT ats к Victori





iptables -A POSTROUTING -d 192.168.1.15/32 -p tcp -m tcp --dport 4459 -j SNAT --to-source 192.168.1.11
iptables -A POSTROUTING -d 192.168.1.15/32 -p tcp -m tcp --dport 7780 -j SNAT --to-source 192.168.1.11

Разрешить только нужным пацанам
iptables -I FORWARD 12 -i enp5s1 -s 192.168.1.0/24  -o vlan10  -j ACCEPT
iptables -I FORWARD 12 -i enp5s1 -s 192.168.1.0/24 -o vlan875 -j ACCEPT
iptables -I FORWARD 12 -i tun0 -s 192.168.132.0/24 -o vlan10 -j ACCEPT
iptables -I FORWARD 12 -i enp5s1 -s 192.168.1.0/24 -d 192.168.253.80/29 -o vlan10 -j ACCEPT

iptables -I   FORWARD_PUBLIC 1  -d  !192.168.0.0/24 -o vlan10 -j ACCEPT
iptables -I   FORWARD_PUBLIC 2  -d  !10.0.0.0/8 -o vlan10 -j ACCEPT
iptables -I   FORWARD_PUBLIC 3  -d  !172.16.0.0/12 -o vlan10 -j ACCEPT
iptables -I   FORWARD_PUBLIC 4  -j RETURN

iptables -I FORWARD 12 -i enp5s1 -s 192.168.1.141/24 -j IPTECH_FORWARD
iptables -I FORWARD 12 -i enp5s1 -s 192.168.1.188/24 -j IPTECH_FORWARD

iptables -I FORWARD 12 -i enp5s1 -s 192.168.1.1xx/24 -j VOIP_FORWARD
iptables -I VOIP_FORWARD 1 -d 192.168.130.0/24 -o vlan10 -j ACCEPT
iptables -I VOIP_FORWARD 1 -d 172.16.0.0/16 -o vlan10 -j ACCEPT
iptables -I VOIP_FORWARD 1 -d 192.168.131.0/24 -o vlan10 -j ACCEPT

iptables -I FORWARD 12 -i enp5s1 -s 192.168.1.1xx/24 -j RADIO_FORWARD

iptables -I IPTECH_FORWARD 1 -o vlan201 -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o enp2s0.134.134  -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan12  -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan15  -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan21  -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan22  -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan23  -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan24  -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan25  -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan26  -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan27  -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan28  -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan29  -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan30  -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan34  -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan36  -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan37  -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan39  -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan40  -j ACCEPT
iptables -I IPTECH_FORWARD 1  -d  192.168.253.64/29 -o vlan90  -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan99  -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan133  -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan201 -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan1035 -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan1037 -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan1038 -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan1150 -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan1901 -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan2999 -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan3151 -j ACCEPT
iptables -I IPTECH_FORWARD 1 -d 192.168.50.0/30 -o vlan3997 -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan401 -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan402 -j ACCEPT
iptables -I IPTECH_FORWARD 1 -o vlan41 -j ACCEPT

-A POSTROUTING -s 192.168.1.0/24 -d 192.168.116.0/24 -o vlan23 -j SNAT --to-source 192.168.116.1 #LAN for phys
-A POSTROUTING -s 192.168.1.0/24 -d 192.168.112.0/24 -o vlan21 -j SNAT --to-source 192.168.112.1 #LAN for phys
-A POSTROUTING -s 192.168.1.0/24 -d 192.168.116.0/24 -o vlan23 -j SNAT --to-source 192.168.116.1 #LAN for phys
-A POSTROUTING -s 192.168.1.0/24 -d 192.168.112.0/24 -o vlan21 -j SNAT --to-source 192.168.112.1 #LAN for phys
-A POSTROUTING -s 192.168.1.0/24 -d 192.168.120.0/24 -o vlan26 -j SNAT --to-source 192.168.120.1
-A POSTROUTING -s 192.168.1.0/24 -d 192.168.113.0/24 -o vlan22 -j SNAT --to-source 192.168.113.1
-A POSTROUTING -s 192.168.1.0/24 -d 192.168.128.0/24 -o vlan1027 -j SNAT --to-source 192.168.128.1
-A POSTROUTING -s 192.168.1.0/24 ! -d 192.168.0.0/16 -o vlan1901 -j SNAT --to-source 10.148.0.8






Интерфейсы 250 и 16 2002  убить





1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet 81.20.192.33/32 brd 81.20.192.33 scope global lo:0
       valid_lft forever preferred_lft forever
    inet 81.20.192.32/32 brd 81.20.192.32 scope global lo:1
       valid_lft forever preferred_lft forever
    inet 81.20.196.53/32 brd 81.20.196.53 scope global lo:2
       valid_lft forever preferred_lft forever
    inet 10.192.10.252/32 brd 10.192.10.252 scope global lo:3
       valid_lft forever preferred_lft forever
    inet 172.31.3.3/32 brd 172.31.3.3 scope global lo:4
       valid_lft forever preferred_lft forever
2: enp5s1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UNKNOWN qlen 1000                      #LAN
    link/ether 00:e0:4c:b0:e6:74 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.11/24 brd 192.168.1.255 scope global enp5s1
       valid_lft forever preferred_lft forever
3: enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 6000 qdisc pfifo_fast state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
4: tunl0@NONE: <NOARP> mtu 1480 qdisc noop state DOWN qlen 1000
    link/ipip 0.0.0.0 brd 0.0.0.0
5: enp2s0.134@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 2000 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
6: enp2s0.134.134@enp2s0.134: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                   #MNGT 16d
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 10.148.2.1/23 brd 10.148.3.255 scope global enp2s0.134.134
       valid_lft forever preferred_lft forever
7: vlan10@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                           #Backbone
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 81.20.192.19/27 brd 81.20.192.31 scope global vlan10
       valid_lft forever preferred_lft forever
8: vlan12@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                           #MNGT Victoria
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.251.2/30 brd 192.168.251.3 scope global vlan12
       valid_lft forever preferred_lft forever
9: vlan15@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                           #MNGT
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.251.6/30 brd 192.168.251.7 scope global vlan15
       valid_lft forever preferred_lft forever
11: vlan21@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                             #RADIO 
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.112.1/24 brd 192.168.112.255 scope global vlan21
       valid_lft forever preferred_lft forever
12: vlan22@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                 #113  
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.113.1/24 brd 192.168.113.255 scope global vlan22
       valid_lft forever preferred_lft forever
13: vlan23@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                  #Wimax
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.116.1/24 brd 192.168.116.255 scope global vlan23
       valid_lft forever preferred_lft forever
14: vlan24@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                  #Phys
        link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.117.1/24 brd 192.168.117.255 scope global vlan24
       valid_lft forever preferred_lft forever
15: vlan25@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                  #Phys
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.118.1/24 brd 192.168.118.255 scope global vlan25
       valid_lft forever preferred_lft forever
16: vlan26@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                  #Phys
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.120.1/24 brd 192.168.120.255 scope global vlan26
       valid_lft forever preferred_lft forever
17: vlan27@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                   #MNGT servers mngt backbone                                                   
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.121.1/24 brd 192.168.121.255 scope global vlan27
       valid_lft forever preferred_lft forever
18: vlan28@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                      #Phys
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.122.1/24 brd 192.168.122.255 scope global vlan28
       valid_lft forever preferred_lft forever
19: vlan29@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                         #Pashki tel 
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.248.1/24 brd 192.168.248.255 scope global vlan29
       valid_lft forever preferred_lft forever
20: vlan30@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                          #Phys
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.123.1/24 brd 192.168.123.255 scope global vlan30
       valid_lft forever preferred_lft forever
21: vlan34@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                              #Phys
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.124.1/22 brd 192.168.127.255 scope global vlan34
       valid_lft forever preferred_lft forever
22: vlan36@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                              #Ur mngt 2
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.115.1/24 brd 192.168.115.255 scope global vlan36
       valid_lft forever preferred_lft forever
23: vlan37@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                                 #Gryazi mngt 
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 172.28.0.8/24 brd 172.28.0.255 scope global vlan37
       valid_lft forever preferred_lft forever
24: vlan39@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                                  #MNGT dovatora, второй ip нах
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.60.1/24 brd 192.168.60.255 scope global vlan39
       valid_lft forever preferred_lft forever
    inet 172.31.255.214/30 brd 172.31.255.215 scope global vlan39
       valid_lft forever preferred_lft forever
25: vlan40@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                                  #Ubiquti mngt
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.140.1/24 brd 192.168.140.255 scope global vlan40
       valid_lft forever preferred_lft forever
26: vlan90@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                                  #ISCI mngt
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.253.68/29 brd 192.168.253.71 scope global vlan90
       valid_lft forever preferred_lft forever
27: vlan99@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                                  mngt ats
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.253.22/30 brd 192.168.253.23 scope global vlan99
       valid_lft forever preferred_lft forever
28: vlan133@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                                 mngt 16 agg
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 10.148.0.33/27 brd 10.148.0.63 scope global vlan133
       valid_lft forever preferred_lft forever
29: vlan201@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen  1000                                                            NLMK
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 10.192.10.190/30 brd 10.192.10.191 scope global vlan201
       valid_lft forever preferred_lft forever
30: vlan209@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                                 #Start DEL
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 172.16.77.22/30 brd 172.16.77.23 scope global vlan209
       valid_lft forever preferred_lft forever
31: vlan217@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                                 #Start mngt
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.114.66/30 brd 192.168.114.67 scope global vlan217
       valid_lft forever preferred_lft forever
34: vlan676@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                                 #Telemir-GKMetallurg  ??????????
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.169.25/29 brd 192.168.169.31 scope global vlan676
       valid_lft forever preferred_lft forever
35: vlan691@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                             #BSMP8mkrm-Poliklinika3 ???????????
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 10.0.90.1/24 brd 10.0.90.255 scope global vlan691
       valid_lft forever preferred_lft forever
36: vlan875@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                                # Start-Onima Пока надо
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 10.48.0.4/26 brd 10.48.0.63 scope global vlan875
       valid_lft forever preferred_lft forever
37: vlan1027@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                            #RadiusVlan
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.128.1/24 brd 192.168.128.255 scope global vlan1027
       valid_lft forever preferred_lft forever
38: vlan1030@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                            test-ftp-nmlk3G
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 10.186.250.5/30 brd 10.186.250.7 scope global vlan1030
       valid_lft forever preferred_lft forever
39: vlan1035@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                                FSB-BILL
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.253.1/30 brd 192.168.253.3 scope global vlan1035
       valid_lft forever preferred_lft forever
40: vlan1037@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                                sapphire-1C-dmz
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.169.1/30 brd 192.168.169.3 scope global vlan1037
       valid_lft forever preferred_lft forever
41: vlan1038@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                                sap-k6-c0-mn-sw
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.71.1/30 brd 192.168.71.3 scope global vlan1038
       valid_lft forever preferred_lft forever
42: vlan1150@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                                Enforta-Regard-PPR
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.253.9/29 brd 192.168.253.15 scope global vlan1150
       valid_lft forever preferred_lft forever
43: vlan1892@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 2000 qdisc noqueue state UP qlen 1000                                                                TRradio
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
44: vlan1901@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                                   mngtBras-Start
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 10.148.0.8/28 brd 10.148.0.15 scope global vlan1901
       valid_lft forever preferred_lft forever
45: vlan2002@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                                    vpn_MGTU-Voip
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 10.11.12.14/24 brd 10.11.12.255 scope global vlan2002
       valid_lft forever preferred_lft forever
46: vlan2999@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                                    l2vpn-voip-grz
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.200.18/24 brd 192.168.200.255 scope global vlan2999
       valid_lft forever preferred_lft forever
47: vlan3151@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                                        malina
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.253.41/29 brd 192.168.253.47 scope global vlan3151
       valid_lft forever preferred_lft forever
48: vlan3997@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                                        pppoe_nlmk
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.50.1/30 brd 192.168.50.3 scope global vlan3997
       valid_lft forever preferred_lft forever
72: tun1: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UNKNOWN qlen 100
    link/none 
    inet 192.168.133.1 peer 192.168.133.2/32 scope global tun1
       valid_lft forever preferred_lft forever
73: vlan41@vlan1892: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000                                                                        1892:41
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.169.9/29 brd 192.168.169.15 scope global vlan41
       valid_lft forever preferred_lft forever
    inet 192.168.169.17/29 brd 192.168.169.23 scope global vlan41:0
       valid_lft forever preferred_lft forever
74: dummy0: <BROADCAST,NOARP> mtu 1500 qdisc noop state DOWN qlen 1000
    link/ether ca:e6:a5:46:64:97 brd ff:ff:ff:ff:ff:ff  
78: vlan401@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 6000 qdisc noqueue state UP qlen 1000                                                                 whatup-start
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.253.49/29 brd 192.168.253.55 scope global vlan401
       valid_lft forever preferred_lft forever
79: vlan402@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 6000 qdisc noqueue state UP qlen 1000                                                                     whatup-start-green
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.253.249/30 brd 192.168.253.251 scope global vlan402
       valid_lft forever preferred_lft forever
82: vlan1112@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 6000 qdisc noqueue state UP qlen 1000                                                                ZelenayaVL1112
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 172.31.255.218/30 brd 172.31.255.219 scope global vlan1112
       valid_lft forever preferred_lft forever
83: tun0: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UNKNOWN qlen 100
    link/none 
    inet 192.168.132.1 peer 192.168.132.2/32 scope global tun0
       valid_lft forever preferred_lft forever

Запрет FIN-сканирования
Linux> iptables -A INPUT –p tcp –m tcp –-tcp-flags FIN,ACK FIN -j DROP
# Запрет X-сканирования
Linux> iptables -A INPUT –p tcp –m tcp --tcp-flags FIN,SYN,RST,PSH,ACK,URG -j DROP
# Запрет N-сканирования
Linux> iptables -A INPUT –p tcp –m tcp -tcp-flags FIN,SYN,RST,PSH,ACK,URG NONE -j DROP

Linux> iptables -I INPUT -p tcp -m osf --genre NMAP -j DROP
 Борьба со сканированием с помощью iptables

# Проверка на стук в нерабочие порты (10 в час)
iptables -A INPUT -m recent --rcheck --seconds 3600 --hitcount 10 --rttl -j RETURN
# Вторая проверка на стук в нерабочие порты (2 в минуту)
iptables -A INPUT -m recent --rcheck --seconds 60 --hitcount 2 --rttl -j RETURN
# Заносим адреса стучащихся в список
iptables -A INPUT -m recent --set
# Отбрасываем пакеты всех, кто превысил лимит на
количество подключений



Запрет Icmp-сообщений

Хорошей практикой также является запрет ICMP-сообщений, которые могут выдать дополнительную информацию о хосте или
быть использованы для выполнения различных злонамеренных действий (например, модификации таблицы маршрутизации). Ниже приведена таблица со списком возможных типов ICMP-сообщений:

Типы ICMP-сообщений

    0 — echo reply (echo-ответ, пинг)
    3 — destination unreachable (адресат недосягаем)
    4 — source quench (подавление источника, просьба посылать пакеты медленнее)
    5 — redirect (редирект)
    8 — echo request (echo-запрос, пинг)
    9 — router advertisement (объявление маршрутизатора)
    10 — router solicitation (ходатайство маршрутизатора)
    11 — time-to-live exceeded (истечение срока жизни пакета)
    12 — IP header bad (неправильный IPзаголовок пакета)
    13 — timestamp request (запрос значения счетчика времени)
    14 — timestamp reply (ответ на запрос значения счетчика времени)
    15 — information request (запрос информации)
    16 — information reply (ответ на запрос информации)
    17 — address mask request (запрос маски сети)
    18 — address mask reply (ответ на запрос маски сети)

Как видишь, ответ на некоторые ICMP-сообщения может привести к разглашению некоторой информации о хосте, в то время как другие — привести к модификации таблицы маршрутизации, поэтому их необходимо запретить.
Обычно выход во внешний мир разрешают ICMP-сообщениям 0, 3, 4, 11 и 12, в то время как на вход принимают только 3, 8 и 12. Вот как это реализуется в различных брандмауэрах:

Запрет опасных ICMP-сообщений

Linux> iptables -A INPUT -p icmp -icmp-type 3,8,12 -j ACCEPT
Linux> iptables -A OUTPUT -p icmp -icmp-type 0,3,4,11,12 -j ACCEPT


 Можно указать стандартный числовой код или сообщение. Пропустить все входящие ICMP-эхо-запросы (пинги).

# iptables -I INPUT -p icmp --icmp-type 8 -j ACCEPT
# iptables -I INPUT -p icmp --icmp-type echo-request -j ACCEPT

Блокирует фрагменты ICMP-пакетов

iptables -I INPUT -p icmp -f -j DROP

Рекомендуемые правила для ICMP:

#!/bin/sh

IPT="/sbin/iptables"

$IPT -A INPUT -p icmp --icmp-type 3 -j ACCEPT # destination-unreachable 3/4
$IPT -A INPUT -p icmp --icmp-type 8 -j ACCEPT # echo request
$IPT -A INPUT -p icmp --icmp-type 12 -j ACCEPT # IP header bad 
$IPT -A OUTPUT -p icmp --icmp-type 0 -j ACCEPT #
$IPT -A OUTPUT -p icmp --icmp-type 3 -j ACCEPT #
$IPT -A OUTPUT -p icmp --icmp-type 4 -j ACCEPT #
$IPT -A OUTPUT -p icmp --icmp-type 11 -j ACCEPT #
$IPT -A OUTPUT -p icmp --icmp-type 12 -j ACCEPT #








-----------------------------------INPUT
netfilter:~# iptables -P INPUT DROP
netfilter:~# iptables -P OUTPUT DROP
netfilter:~# iptables -A INPUT -i lo -j ACCEPT 
netfilter:~# iptables -A OUTPUT -o lo -j ACCEPT
netfilter:~# iptables -A INPUT -p icmp --icmp-type 0 -j ACCEPT
netfilter:~# iptables -A INPUT -p icmp --icmp-type 8 -j ACCEPT
netfilter:~# iptables -A OUTPUT -p icmp -j ACCEPT
netfilter:~# cat /proc/sys/net/ipv4/ip_local_port_range
32768 61000
netfilter:~# iptables -A OUTPUT -p TCP --sport 32768:61000 -j ACCEPT
netfilter:~# iptables -A OUTPUT -p UDP --sport 32768:61000 -j ACCEPT
netfilter:~# iptables -A INPUT -p TCP -m state --state ESTABLISHED,RELATED -j ACCEPT
netfilter:~# iptables -A INPUT -p UDP -m state --state ESTABLISHED,RELATED -j ACCEPT



*filter
:INPUT DROP [7769:407175]
:FORWARD ACCEPT [12702685:10540656902]
:OUTPUT ACCEPT [91559:15294861]
:Axaptamtt - [0:0]
:GREEN - [0:0]
:OPENVPN - [0:0]
:OPENVPNLAN - [0:0]
:OPENVPNSIP - [0:0]
:OPENVPNWU - [0:0]
:allowed_ports - [0:0]
:apache - [0:0]
:blocked-sites - [0:0]
:ospf - [0:0]
:start-whatup - [0:0]
:voice - [0:0]

-A INPUT -p icmp -j ACCEPT
-A INPUT -i lo -j ACCEPT
-A INPUT -s 81.20.192.0/25 -i vlan10 -p tcp -m state --state NEW -m tcp --dport 22 -j ACCEPT
-A INPUT -s 192.168.1.0/24 -i enp5s1 -p tcp -m state --state NEW -m tcp --dport 22 -j ACCEPT
-A INPUT -p tcp -m tcp --dport 69 -j ACCEPT
-A INPUT -p udp -m udp --dport 69 -j ACCEPT
-A INPUT -p esp -j ACCEPT
-A INPUT -p ah -j ACCEPT

-A INPUT -s 217.107.196.0/22 -j DROP #НАХ
-A INPUT -i lo -j ACCEPT        №НАХ

-A INPUT -i enp2s0 -p ospf -j ACCEPT
-A INPUT -i enp5s1 -j ACCEPT


-A INPUT -i vlan10 -p ospf -j ACCEPT
-A INPUT -s 224.0.0.0/24 -j ACCEPT
-A INPUT -i vlan27 -j ACCEPT

-A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
-A INPUT -j allowed_ports
-A INPUT -j apache
-A INPUT -j ospf
-A INPUT -s 195.151.76.173/32 -j ACCEPT
-A INPUT -s 31.204.98.37/32 -j ACCEPT
-A INPUT -s 31.204.98.143/32 -j ACCEPT

-A INPUT -p udp -j ACCEPT
-A INPUT -s 81.20.192.24/32 -d 81.20.192.19/32 -j voice
-A INPUT -s 165.251.38.130/32 -d 81.20.192.19/32 -p udp -m multiport --sports 5060,16384:32767 -j voice
-A INPUT -s 165.251.38.130/32 -d 81.20.192.19/32 -p tcp -m multiport --sports 5060,16384:32767 -j voice
-A INPUT -s 80.75.131.78/32 -j ACCEPT
-A INPUT -s 80.75.128.2/32 -j ACCEPT
-A INPUT -i vlan201 -j ACCEPT
-A INPUT -d 81.20.192.19/32 -p gre -j ACCEPT
-A INPUT -s 81.20.192.0/20 -p udp -m udp --dport 514 -j ACCEPT
-A INPUT -s 192.168.0.0/16 -p udp -m udp --dport 514 -j ACCEPT
-A INPUT -i vlan1035 -j DROP
-A INPUT -i vlan1037 -j DROP
-A INPUT -s 172.16.77.17/32 -p tcp -m tcp --dport 22 -j DROP
-A INPUT -s 10.148.0.8/32 -p tcp -m tcp --dport 22 -j DROP

-A allowed_ports -s 81.20.192.0/20 -d 81.20.192.19/32 -p tcp -m multiport --dports 22,110,143,873,20,21,5901,5801,65001 -j ACCEPT
-A allowed_ports -s 81.20.192.19/32 -d 81.20.192.0/20 -p tcp -m multiport --dports 65001 -j ACCEPT
-A allowed_ports -s 195.34.224.0/19 -d 81.20.192.19/32 -p tcp -m multiport --dports 110,143 -j ACCEPT
-A allowed_ports -s 109.172.40.228/32 -d 81.20.192.19/32 -p tcp -m multiport --dports 65001,65002 -j ACCEPT
-A allowed_ports -s 81.20.192.19/32 -d 109.172.40.228/32 -p tcp -m multiport --dports 65001,65002 -j ACCEPT
-A allowed_ports -s 192.168.1.0/24 -d 192.168.1.11/32 -p tcp -m multiport --dports 22,110,143,873,20,21,5901,5801 -j ACCEPT
-A allowed_ports -s 192.168.168.0/24 -d 192.168.1.11/32 -p tcp -m multiport --dports 22,110,143,873,20,21,5901,5801 -j ACCEPT
-A allowed_ports -s 192.168.132.0/24 -d 192.168.1.11/32 -p tcp -m multiport --dports 22,110,143,873,20,21,5901,5801 -j ACCEPT
-A allowed_ports -s 81.20.192.0/20 -d 81.20.192.19/32 -p udp -m udp --dport 873 -j ACCEPT
-A allowed_ports -s 81.20.192.0/20 -d 81.20.192.19/32 -p tcp -m tcp --dport 53 -j ACCEPT
-A allowed_ports -s 192.168.1.0/24 -d 192.168.1.11/32 -p tcp -m tcp --dport 53 -j ACCEPT
-A allowed_ports -s 81.20.192.19/32 -d 81.20.192.0/20 -p tcp -m tcp --sport 53 -j ACCEPT
-A allowed_ports -s 81.20.192.19/32 -p tcp -m tcp --dport 53 -j ACCEPT
-A allowed_ports -s 81.20.192.19/32 -p tcp -m tcp --dport 53 -j ACCEPT
-A allowed_ports -s 172.24.0.0/14 -d 81.20.192.19/32 -p tcp -m multiport --dports 110,143 -j ACCEPT
-A allowed_ports -s 172.20.0.0/14 -d 81.20.192.19/32 -p tcp -m multiport --dports 110,143 -j ACCEPT
-A allowed_ports -s 81.20.192.0/20 -d 81.20.192.19/32 -p udp -m udp --dport 53 -j ACCEPT
-A allowed_ports -s 192.168.1.0/24 -d 192.168.1.11/32 -p udp -m udp --dport 53 -j ACCEPT
-A allowed_ports -s 81.20.192.19/32 -d 81.20.192.0/20 -p udp -m udp --sport 53 -j ACCEPT
-A allowed_ports -s 81.20.192.19/32 -p udp -m udp --dport 53 -j ACCEPT
-A allowed_ports -s 192.168.0.0/16 -p udp -m udp --dport 1812 -j ACCEPT
-A allowed_ports -s 81.20.192.19/32 -p udp -m udp --dport 53 -j ACCEPT

-A allowed_ports -s 81.20.192.19/32 -p udp -m udp --dport 123 -j ACCEPT
-A allowed_ports -d 81.20.192.19/32 -p udp -m udp --dport 123 -j ACCEPT
-A allowed_ports -d 192.168.253.49/32 -p tcp -m tcp --dport 123 -j ACCEPT
-A allowed_ports -s 192.168.253.49/32 -p tcp -m tcp --dport 123 -j ACCEPT
-A allowed_ports -d 192.168.253.49/32 -p udp -m udp --dport 123 -j ACCEPT
-A allowed_ports -s 192.168.253.49/32 -p udp -m udp --dport 123 -j ACCEPT
-A allowed_ports -d 81.20.192.19/32 -p tcp -m tcp --dport 123 -j ACCEPT
-A allowed_ports -s 81.20.192.19/32 -p tcp -m tcp --dport 123 -j ACCEPT

-A allowed_ports -s 81.20.195.194/32 -d 81.20.192.19/32 -p tcp -m multiport --dports 110,143 -j ACCEPT
-A allowed_ports -s 81.20.196.31/32 -d 81.20.192.19/32 -p tcp -m multiport --dports 110,143 -j ACCEPT
-A allowed_ports -d 81.20.192.19/32 -p tcp -m multiport --dports 110,143 -j ACCEPT

-A allowed_ports -s 10.29.5.0/24 -p tcp -m tcp --dport 22 -j ACCEPT
-A allowed_ports -s 10.9.0.0/24 -p tcp -m tcp --dport 22 -j ACCEPT
-A allowed_ports -s 10.9.0.0/24 -p tcp -m tcp --dport 80 -j ACCEPT
-A allowed_ports -s 10.9.0.0/24 -p tcp -m tcp --dport 21 -j ACCEPT
-A allowed_ports -s 10.192.10.0/24 -p tcp -m tcp --dport 21 -j ACCEPT
-A allowed_ports -s 10.9.0.0/24 -p tcp -m tcp --dport 20 -j ACCEPT
-A allowed_ports -s 10.9.254.10/32 -p tcp -m tcp --dport 20 -j ACCEPT
-A allowed_ports -s 10.9.254.10/32 -p tcp -m tcp --dport 21 -j ACCEPT
-A allowed_ports -d 81.20.192.32/32 -p udp -m udp --dport 1194 -j ACCEPT
-A allowed_ports -d 81.20.192.32/32 -p tcp -m tcp --dport 1194 -j ACCEPT
-A allowed_ports -p tcp -m tcp --dport 5001 -j ACCEPT
-A allowed_ports -p udp -m udp --dport 5001 -j ACCEPT
-A allowed_ports -s 192.168.1.0/24 -d 192.168.1.11/32 -p udp -m udp --dport 123 -j ACCEPT
-A allowed_ports -s 192.168.1.0/24 -p udp -m udp --dport 69 -j ACCEPT
-A allowed_ports -s 192.168.0.0/16 -p udp -m udp --dport 123 -j ACCEPT
-A allowed_ports -s 192.168.0.0/16 -p tcp -m tcp --dport 123 -j ACCEPT
-A apache -d 81.20.192.19/32 -p tcp -m tcp --dport 80 -j ACCEPT


-A blocked-sites -s 192.168.1.141/32 -j RETURN
-A blocked-sites -s 192.168.1.133/32 -j RETURN
-A blocked-sites -s 192.168.1.152/32 -j RETURN
-A blocked-sites -s 192.168.1.155/32 -j RETURN
-A blocked-sites -s 192.168.1.156/32 -j RETURN
-A blocked-sites -s 192.168.1.165/32 -j RETURN
-A blocked-sites -s 192.168.1.168/32 -j RETURN
-A blocked-sites -s 192.168.1.169/32 -j RETURN
-A blocked-sites -s 192.168.1.170/32 -j RETURN
-A blocked-sites -s 192.168.1.172/32 -j RETURN
-A blocked-sites -s 192.168.1.222/32 -j RETURN
-A blocked-sites -s 192.168.1.177/32 -j RETURN
-A blocked-sites -s 192.168.1.178/32 -j RETURN
-A blocked-sites -s 192.168.1.186/32 -j RETURN
-A blocked-sites -s 192.168.1.188/32 -j RETURN
-A blocked-sites -s 192.168.1.200/32 -j RETURN
-A blocked-sites -s 192.168.1.203/32 -j RETURN
-A blocked-sites -s 192.168.1.212/32 -j RETURN
-A blocked-sites -s 192.168.1.213/32 -j RETURN
-A blocked-sites -s 192.168.1.220/32 -j RETURN
-A blocked-sites -s 192.168.1.236/32 -j RETURN
-A blocked-sites -s 192.168.1.240/32 -j RETURN
-A blocked-sites -s 192.168.1.241/32 -j RETURN
-A blocked-sites -m string --string "vk.com" --algo kmp --to 65535 -j REJECT --reject-with icmp-proto-unreachable
-A blocked-sites -m string --string "vkontakte.ru" --algo kmp --to 65535 -j REJECT --reject-with icmp-proto-unreachable
-A blocked-sites -m string --string "ok.ru" --algo kmp --to 65535 -j REJECT --reject-with icmp-proto-unreachable
-A blocked-sites -m string --string "odnoklassniki.ru" --algo kmp --to 65535 -j REJECT --reject-with icmp-proto-unreachable
-A blocked-sites -j RETURN

-A ospf -s 81.20.192.0/27 -d 224.0.0.0/24 -j ACCEPT
-A ospf -s 81.20.192.0/27 -d 224.0.0.0/24 -j ACCEPT
-A voice -j ACCEPT



# Generated by iptables-save v1.4.7 on Thu Nov 16 15:05:48 2017
*filter
:INPUT DROP [0:0]
:FORWARD DROP [0:0]
:OUTPUT ACCEPT [15743932:14518834090]
:fail2ban-SSH - [0:0]
-A INPUT -s 192.168.1.0/24 -p tcp -m state --state NEW -m tcp --dport 25 -j ACCEPT 
-A INPUT -p tcp -m tcp --dport 2222 -j fail2ban-SSH 
-A INPUT -s 46.118.123.0/24 -j REJECT --reject-with icmp-port-unreachable 
-A INPUT -s 91.185.1.178/32 -j REJECT --reject-with icmp-port-unreachable 
-A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT 
-A INPUT -p icmp -j ACCEPT 
-A INPUT -i lo -j ACCEPT 
-A INPUT -s 192.168.1.0/24 -p tcp -m multiport --dports 110,143 -j ACCEPT 
-A INPUT -p udp -m udp --dport 1194 -j ACCEPT 
-A INPUT -p tcp -m tcp --dport 80 --tcp-flags FIN,SYN,RST,ACK SYN -m connlimit --connlimit-above 32 --connlimit-mask 32 -j REJECT --reject-with tcp-reset 
-A INPUT -p tcp -m state --state NEW -m tcp --dport 80 -j ACCEPT 
-A INPUT -p udp -m udp --dport 53 -j ACCEPT 
-A INPUT -p tcp -m tcp --dport 53 -j ACCEPT 
-A INPUT -s 192.168.1.0/24 -p tcp -m state --state NEW -m tcp --dport 2812 -j ACCEPT 
-A INPUT -p tcp -m state --state NEW -m tcp --dport 2222 -j ACCEPT 
-A INPUT -j REJECT --reject-with icmp-host-prohibited 
-A FORWARD -j REJECT --reject-with icmp-host-prohibited 
-A fail2ban-SSH -s 69.165.74.167/32 -j REJECT --reject-with icmp-port-unreachable 
-A fail2ban-SSH -s 91.185.1.178/32 -j REJECT --reject-with icmp-port-unreachable 
-A fail2ban-SSH -j RETURN 
COMMIT
# Completed on Thu Nov 16 15:05:48 2017




type(тип) 8-bit
code(код) 8-bit
0 — echo reply (echo-ответ, пинг)
3 — destination unreachable (адресат недосягаем)
4 — source quench (подавление источника, просьба посылать пакеты медленнее)
5 — redirect (редирект)
8 — echo request (echo-запрос, пинг)
9 — router advertisement (объявление маршрутизатора)
10 — router solicitation (ходатайство маршрутизатора)
11 — time-to-live exceeded (истечение срока жизни пакета)
12 — IP header bad (неправильный IPзаголовок пакета)
13 — timestamp request (запрос значения счетчика времени)
14 — timestamp reply (ответ на запрос значения счетчика времени)
15 — information request (запрос информации)
16 — information reply (ответ на запрос информации)
17 — address mask request (запрос маски сети)
18 — address mask reply (ответ на запрос маски сети)







netfilter:~# iptables -A INPUT -p icmp --icmp-type 0 -j ACCEPT
netfilter:~# iptables -A INPUT -p icmp --icmp-type 8 -j ACCEPT
iptables -A INPUT -p icmp --icmp-type echo-request -j REJECT


Как заблокировать PING на сервере с выводом сообщений об ошибке?
Таким образом, вы можете частично блокировать PING с выводом сообщения об ошибке «Destination Port Unreachable». Добавьте следующие правила Iptables чтобы заблокировать PING с выводом сообщения об ошибке:
 iptables -A INPUT -p icmp --icmp-type echo-request -j REJECT

Заблокировать PING на сервере без каких-либо сообщений об ошибках.
Для этого, используем команду для ИПтейбелс:

 iptables -A OUTPUT -p icmp --icmp-type echo-request -j DROP
 iptables -A INPUT -p icmp --icmp-type echo-reply -j DROP





Для сервера 
iptables -A INPUT -p icmp --icmp-type 3,8,12 -j ACCEPT
iptables -A OUTPUT -p icmp --icmp-type 0,3,4,11,12 -j ACCEPT

Для форварда всё разрешим


8 отправляем, 0 получаем

Чтобы запретить ping:
# iptables -A INPUT -p icmp --icmp-type echo-request -j DROP
# iptables -A INPUT -i eth1 -p icmp --icmp-type echo-request -j DROP

Разрешить для определенных сетей / хостов:
# iptables -A INPUT -s 192.168.1.0/24 -p icmp --icmp-type echo-request -j ACCEPT

Разрешить только часть ICMP запросов:
### ** предполагается, что политики по умолчанию для входящих установлены в DROP ** ###
# iptables -A INPUT -p icmp --icmp-type echo-reply -j ACCEPT
# iptables -A INPUT -p icmp --icmp-type destination-unreachable -j ACCEPT
# iptables -A INPUT -p icmp --icmp-type time-exceeded -j ACCEPT
## ** разрешим отвечать на запрос ** ##
# iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT 


-A INPUT -p icmp --icmp-type 8 -j ACCEPT 
-A INPUT -p icmp --icmp-type 8 -m limit --limit 3/minute --limit-burst 3 -j ACCEPT

iptables -N limit-icmp
iptables -A limit-icmp -j ACCEPT
iptables -A INPUT -p icmp --icmp-type 8 -m limit --limit 3/minute --limit-burst 3 -j limit-icmp
iptables -A INPUT -p icmp --icmp-type 8 -j DROP

iptables -N ICMP_packets
iptables -A INPUT -p icmp --icmp-type echo-request -m length --length 128 -j ICMP_packets
iptables -A ICMP_packets -m limit ! --limit 1000/s --limit-burst 1000 -j DROP
iptables -A ICMP_packets -m hashlimit --hashlimit-above 50/m --hashlimit-burst 50 --hashlimit-mode srcip --hashlimit-name icmp -j DROP

iptables -A ICMP_packets -j ACCEPT

$IPT -A INPUT -p icmp --icmp-type 8 -j ACCEPT # echo request

$IPT -A INPUT -p icmp --icmp-type 3 -j ACCEPT # destination-unreachable 3/4
icmp match options:
[!] --icmp-type typename        match icmp type
[!] --icmp-type type[/code]     (or numeric type or type/code)
Valid ICMP Types:
any


0  echo-reply (pong)
3  destination-unreachable
            network-unreachable
            host-unreachable
   protocol-unreachable
   port-unreachable
   fragmentation-needed
   source-route-failed
   network-unknown
   host-unknown
   network-prohibited
   host-prohibited
   TOS-network-unreachable
   TOS-host-unreachable
   communication-prohibited
   host-precedence-violation
   precedence-cutoff
source-quench
redirect
   network-redirect
   host-redirect
   TOS-network-redirect
   TOS-host-redirect
echo-request (ping)
router-advertisement
router-solicitation
time-exceeded (ttl-exceeded)
   ttl-zero-during-transit
   ttl-zero-during-reassembly
parameter-problem
   ip-header-bad
   required-option-missing
timestamp-request
timestamp-reply
address-mask-request
address-mask-reply



195.151.76.173


iptables -I INPUT 1 -p icmp --icmp-type 3,8,12 -j ACCEPT
iptables -I INPUT 2 -m state --state RELATED,ESTABLISHED -j ACCEPT

Сделать 3 цепочки
LAN
Вражеские сети
МНЖМ сети





-A INPUT -p icmp -j ACCEPT
-A INPUT -i lo -j ACCEPT
-A INPUT -s 81.20.192.0/25 -i vlan10 -p tcp -m state --state NEW -m tcp --dport 22 -j ACCEPT
-A INPUT -s 192.168.1.0/24 -i enp5s1 -p tcp -m state --state NEW -m tcp --dport 22 -j ACCEPT
-A INPUT -p tcp -m tcp --dport 69 -j ACCEPT
-A INPUT -p udp -m udp --dport 69 -j ACCEPT
-A INPUT -p esp -j ACCEPT
-A INPUT -p ah -j ACCEPT
-A INPUT -i lo -j ACCEPT
-A INPUT -i enp2s0 -p ospf -j ACCEPT
-A INPUT -i enp5s1 -j ACCEPT
-A INPUT -i vlan10 -p ospf -j ACCEPT
-A INPUT -s 224.0.0.0/24 -j ACCEPT

-A INPUT -j allowed_ports
-A INPUT -j apache
-A INPUT -j ospf
-A INPUT -d 81.20.192.19/32 -p gre -j ACCEPT
-A INPUT -s 81.20.192.0/20 -p udp -m udp --dport 514 -j ACCEPT
-A INPUT -s 192.168.0.0/16 -p udp -m udp --dport 514 -j ACCEPT

-A allowed_ports -s 81.20.192.0/20 -d 81.20.192.19/32 -p tcp -m multiport --dports 22,110,143,873,20,21,5901,5801,65001 -j ACCEPT
-A allowed_ports -s 81.20.192.19/32 -d 81.20.192.0/20 -p tcp -m multiport --dports 65001 -j ACCEPT
-A allowed_ports -s 195.34.224.0/19 -d 81.20.192.19/32 -p tcp -m multiport --dports 110,143 -j ACCEPT
-A allowed_ports -s 109.172.40.228/32 -d 81.20.192.19/32 -p tcp -m multiport --dports 65001,65002 -j ACCEPT
-A allowed_ports -s 81.20.192.19/32 -d 109.172.40.228/32 -p tcp -m multiport --dports 65001,65002 -j ACCEPT
-A allowed_ports -s 192.168.1.0/24 -d 192.168.1.11/32 -p tcp -m multiport --dports 22,110,143,873,20,21,5901,5801 -j ACCEPT
-A allowed_ports -s 192.168.168.0/24 -d 192.168.1.11/32 -p tcp -m multiport --dports 22,110,143,873,20,21,5901,5801 -j ACCEPT
-A allowed_ports -s 192.168.132.0/24 -d 192.168.1.11/32 -p tcp -m multiport --dports 22,110,143,873,20,21,5901,5801 -j ACCEPT
-A allowed_ports -s 81.20.192.0/20 -d 81.20.192.19/32 -p udp -m udp --dport 873 -j ACCEPT
-A allowed_ports -s 81.20.192.0/20 -d 81.20.192.19/32 -p tcp -m tcp --dport 53 -j ACCEPT
-A allowed_ports -s 192.168.1.0/24 -d 192.168.1.11/32 -p tcp -m tcp --dport 53 -j ACCEPT
-A allowed_ports -s 81.20.192.19/32 -d 81.20.192.0/20 -p tcp -m tcp --sport 53 -j ACCEPT
-A allowed_ports -s 81.20.192.19/32 -p tcp -m tcp --dport 53 -j ACCEPT
-A allowed_ports -s 81.20.192.19/32 -p tcp -m tcp --dport 53 -j ACCEPT
-A allowed_ports -s 81.20.192.0/20 -d 81.20.192.19/32 -p udp -m udp --dport 53 -j ACCEPT
-A allowed_ports -s 192.168.1.0/24 -d 192.168.1.11/32 -p udp -m udp --dport 53 -j ACCEPT
-A allowed_ports -s 81.20.192.19/32 -d 81.20.192.0/20 -p udp -m udp --sport 53 -j ACCEPT
-A allowed_ports -s 81.20.192.19/32 -p udp -m udp --dport 53 -j ACCEPT
-A allowed_ports -s 81.20.192.19/32 -p udp -m udp --dport 53 -j ACCEPT
-A allowed_ports -s 81.20.192.19/32 -p udp -m udp --dport 123 -j ACCEPT
-A allowed_ports -d 81.20.192.19/32 -p udp -m udp --dport 123 -j ACCEPT
-A allowed_ports -d 192.168.253.49/32 -p tcp -m tcp --dport 123 -j ACCEPT
-A allowed_ports -s 192.168.253.49/32 -p tcp -m tcp --dport 123 -j ACCEPT
-A allowed_ports -d 192.168.253.49/32 -p udp -m udp --dport 123 -j ACCEPT
-A allowed_ports -s 192.168.253.49/32 -p udp -m udp --dport 123 -j ACCEPT
-A allowed_ports -d 81.20.192.19/32 -p tcp -m tcp --dport 123 -j ACCEPT
-A allowed_ports -s 81.20.192.19/32 -p tcp -m tcp --dport 123 -j ACCEPT
-A allowed_ports -s 81.20.195.194/32 -d 81.20.192.19/32 -p tcp -m multiport --dports 110,143 -j ACCEPT
-A allowed_ports -s 81.20.196.31/32 -d 81.20.192.19/32 -p tcp -m multiport --dports 110,143 -j ACCEPT
-A allowed_ports -d 81.20.192.19/32 -p tcp -m multiport --dports 110,143 -j ACCEPT
-A allowed_ports -d 81.20.192.32/32 -p udp -m udp --dport 1194 -j ACCEPT
-A allowed_ports -d 81.20.192.32/32 -p tcp -m tcp --dport 1194 -j ACCEPT
-A allowed_ports -s 192.168.1.0/24 -d 192.168.1.11/32 -p udp -m udp --dport 123 -j ACCEPT
-A allowed_ports -s 192.168.0.0/16 -p udp -m udp --dport 123 -j ACCEPT
-A allowed_ports -s 192.168.0.0/16 -p tcp -m tcp --dport 123 -j ACCEPT
-A allowed_ports -s 192.168.1.0/24 -p udp -m udp --dport 69 -j ACCEPT
-A allowed_ports -s 192.168.0.0/16 -p udp -m udp --dport 1812 -j ACCEPT
-A allowed_ports -s 192.168.0.0/16 -p udp -m udp --dport 1813 -j ACCEPT
-A allowed_ports -s 10.148.0.0/16 -p udp -m udp --dport 1812 -j ACCEPT
-A allowed_ports -s 10.148.0.0/16 -p udp -m udp --dport 1813 -j ACCEPT
-A allowed_ports -s 10.0.0.0/8 -i vlan201 -p udp -m udp --dport 2012 -j ACCEPT
-A allowed_ports -s 10.0.0.0/8 -i vlan201 -p udp -m udp --dport 2013 -j ACCEPT
-A allowed_ports -s 172.28.0.0/24 -p udp -m udp --dport 1812 -j ACCEPT
-A allowed_ports -s 172.28.0.0/24 -p udp -m udp --dport 123 -j ACCEPT
-A allowed_ports -s 10.148.0.0/16 -p udp -m udp --dport 123 -j ACCEPT
-A apache -d 81.20.192.19/32 -p tcp -m tcp --dport 80 -j ACCEPT

-A ospf -s 81.20.192.0/27 -d 224.0.0.0/24 -j ACCEPT
-A ospf -s 81.20.192.0/27 -d 224.0.0.0/24 -j ACCEPT





ПРАВИЛА ДЛЯ ИНПУТ
gre (ipsec) 500
openvpn 1194
22 (ssh)
53,953 (dns)
514 
2812 monit
80
123 NTP
179 bgp
ospf !!!
25 
1812
1813
2012
2013 (udp)
67 -dhcp
69 (xinetd)
zabbix 10050
111,1019
37800 radiusd
41240 dhcpd


91.190.64.0/20
81.20.192.0/20

22
53
953
514
2812
80
123
179

25
953
           
1812
1813
2012
2013 
67
69 (xinetd)
1194
10050 - zabbix
500 - racoon
111 rpc
1019 rpcbind       

37800 radiusd
41240 dhcpd


tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      6746/master         
tcp        0      0 127.0.0.1:953           0.0.0.0:*               LISTEN      6626/named  
tcp        0      0 127.0.0.1:6379          0.0.0.0:*               LISTEN      5353/redis-server 1 








































1892:41 - wifi на 16 района для Мишлена



ПРАВИЛА ДЛЯ ИНПУТ
gre (ipsec) 500
openvpn 1194 --------------------------- ext, lan
22 (ssh) ------------------------------- lan
53,953 (dns) ------------------------------ psi, lan
514 ---------------------------------------------- dmz
2812 monit  -------------------------- lan
80 ------------------------------------------------ lan
123 NTP ------------------------------------- dmz, psi
179 bgp ------------------------------------ psi, dmz
ospf !!! ---------------------------------------- psi
25 
1812  -------------------------------------- dmz
1813  -------------------------------------- dmz
2012 ---------------------------------------- dmz
2013 (udp) ------------------------------- dmz
67 -dhcp   ----------- lan
69 (xinetd)
zabbix 10050 ----------------- (?????)
111,1019
37800 radiusd
41240 dhcpd


81.20.192.0/25  dmz
81.20.192.0/20  ext

81.20.192.0/25  - ospf,bgp,

iptables -I INPUT 9 -p esp -j ACCEPT
iptables -I INPUT 10 -p ah -j ACCEPT 
iptables  -I INPUT 10 -p ipencap -j ACCEPT

iptables -I INPUT 11 -p udp -m udp -s 195.151.76.173 -d 81.20.192.19 --dport 500 -m comment --comment "FROM UNISPRINT" -j ACCEPT
iptables -I INPUT 12 -i vlan10 -p ospfigp -j ACCEPT


iptables -D INPUT -s 81.20.192.0/25 -i vlan10 -p tcp -m state --state NEW -m tcp --dport 22 -j ACCEPT
iptables -D INPUT -s 192.168.1.0/24 -i enp5s1 -p tcp -m state --state NEW -m tcp --dport 22 -j ACCEPT




iptables -I INPUT 16 -i enp5s1 -j input_lan
iptables -I INPUT 17 -i tun+ -j input_lan 
tun+

iptables -I INPUT 18 -s 81.20.192.0/25 -i vlan 10  -j input_dmz

iptables -I INPUT 19 -i vlan401 -j input_dmz
iptables -I INPUT 20 -i vlan201 -j input_dmz
iptables -I INPUT 21 -i vlan402 -j input_dmz
iptables -I INPUT 22 -i vlan3997 -j input_dmz
iptables -I INPUT 23 -i vlan2999 -j input_dmz
iptables -I INPUT 24 -i vlan2002 -j input_dmz
iptables -I INPUT 25 -i vlan1901 -j input_dmz
iptables -I INPUT 26 -i vlan41 -j input_dmz
iptables -I INPUT 27 -i vlan1150 -j input_dmz
iptables -I INPUT 28 -i vlan1038 -j input_dmz
iptables -I INPUT 29 -i vlan1037 -j input_dmz
iptables -I INPUT 30 -i vlan1035 -j input_dmz
iptables -I INPUT 31 -i vlan676 -j input_dmz
iptables -I INPUT 32 -i vlan133 -j input_dmz
iptables -I INPUT 33 -i vlan99 -j input_dmz
iptables -I INPUT 34 -i vlan90 -j input_dmz
iptables -I INPUT 35 -i vlan40 -j input_dmz
iptables -I INPUT 36 -i vlan39 -j input_dmz
iptables -I INPUT 37 -i vlan37 -j input_dmz
iptables -I INPUT 38 -i vlan36 -j input_dmz
iptables -I INPUT 39 -i vlan34 -j input_dmz
iptables -I INPUT 40 -i vlan30 -j input_dmz
iptables -I INPUT 41 -i vlan29 -j input_dmz
iptables -I INPUT 42 -i vlan28 -j input_dmz
iptables -I INPUT 43 -i vlan27 -j input_dmz
iptables -I INPUT 44 -i vlan21 -j input_dmz
iptables -I INPUT 45 -i vlan22 -j input_dmz
iptables -I INPUT 46 -i vlan23 -j input_dmz
iptables -I INPUT 47 -i vlan24 -j input_dmz
iptables -I INPUT 48 -i vlan25 -j input_dmz
iptables -I INPUT 49 -i vlan26 -j input_dmz
iptables -I INPUT 50 -i vlan15 -j input_dmz
iptables -I INPUT 51 -i enp2s0.134.134 -j input_dmz
iptables -I INPUT 52 -i vlan12 -j input_dmz
iptables -I INPUT 53 -i vlan15 -j input_dmz


iptables -I INPUT 54 -i vlan10  -j input_ext
iptables -I INPUT 55 -i vlan1112 -j input_ext
iptables -I INPUT 56 -i vlan3151  -j input_ext
iptables -I INPUT 57 -i vlan875  -j input_ext
iptables -I INPUT 58 -i vlan217  -j input_ext
iptables -I INPUT 59 -i vlan209  -j input_ext


iptables -A INPUT -s 81.20.192.0/25 -i vlan10 -p tcp -m tcp --dport 22 -j ACCEPT
iptables -A INPUT -s 192.168.1.0/24 -i enp5s1 -p tcp -m tcp --dport 22 -j ACCEPT

iptables -N input_lan
iptables -A input_lan  -p tcp -m limit --limit 3/min -m tcp --dport 22 --tcp-flags FIN,SYN,RST,ACK SYN -j LOG --log-prefix "FW-INlan-ACC-TCP " --log-tcp-options --log-ip-options
iptables -A input_lan -p tcp -m tcp --dport 22 -j ACCEPT
iptables -A input_lan -p udp -m udp --dport 53 -j ACCEPT
iptables -A input_lan -p tcp -m tcp --dport 53 -j ACCEPT
iptables -A input_lan -p udp -m udp --dport 67 -j ACCEPT
iptables -A input_lan -p udp -m udp  --dport 1194 -j ACCEPT
iptables -A input_lan -p tcp -m tcp --dport 2812 -j ACCEPT
iptables -A input_lan -p tcp -m tcp --dport 80 -j ACCEPT
iptables -A input_lan -p tcp -m tcp --dport 2812 -j ACCEPT
iptables -A input_lan -p udp -m udp --dport 123 -j ACCEPT
iptables -A input_lan -p udp -m udp --dport 514 -j ACCEPT
iptables -A input_lan -p tcp -m tcp --dport 10500 -j ACCEPT
iptables -A input_lan -j DROP


iptables -N input_ext
iptables -A input_ext -p udp -m udp -d 81.20.192.32 --dport 1194 -j ACCEPT
iptables -A input_ext -s 81.20.192.0/25 -p tcp -m tcp --dport 22 -j ACCEPT
iptables -A input_ext -j DROP


iptables -N input_dmz

iptables -A input_dmz  -p tcp -m limit --limit 3/min -m tcp --dport 22 --tcp-flags FIN,SYN,RST,ACK SYN -j LOG --log-prefix "FW-INlan-ACC-TCP " --log-tcp-options --log-ip-options
iptables -A input_dmz -p udp -m udp --dport 53 -j ACCEPT
iptables -A input_dmz -p tcp -m tcp --dport 53 -j ACCEPT
iptables -A input_dmz -p udp -m udp --dport 123 -j ACCEPT
iptables -A input_dmz -p udp -m udp --dport 514 -j ACCEPT
iptables -A input_dmz -p tcp -m tcp --dport 179 -j ACCEPT
iptables -A input_dmz -p udp -m udp --dport 1812 -j ACCEPT
iptables -A input_dmz -p udp -m udp --dport 1813 -j ACCEPT
iptables -A input_dmz -p tcp -m tcp --dport 10500 -j ACCEPT
iptables -A input_dmz -s 10.0.0.0/8 -i vlan201 -p udp -m udp --dport 2012 -j ACCEPT
iptables -A input_dmz -s 10.0.0.0/8 -i vlan201 -p udp -m udp --dport 2013 -j ACCEPT
iptables -A input_dmz -j DROP


-A INPUT -i lo -j ACCEPT

iptables -I INPUT 2 -p icmp --icmp-type 3,8,12 -j ACCEPT
iptables -I INPUT 3 -m state --state RELATED,ESTABLISHED -j ACCEPT

-A INPUT -m conntrack --ctstate ESTABLISHED -j ACCEPT
iptables -A INPUT -p icmp --icmp-type 3,8,12 -j ACCEPT
-A INPUT -p icmp -m conntrack --ctstate RELATED -j ACCEPT
-A INPUT -i vlan10 -p ospfigp -j ACCEPT
-A INPUT -p esp -j ACCEPT
-A INPUT -p ah -j ACCEPT
-A INPUT -d 81.20.192.19/32 -p gre -j ACCEPT


?????????????????????????????????????
iptables -N ICMP_packets
iptables -A INPUT -p icmp --icmp-type echo-request -m length --length 128 -j ICMP_packets
iptables -A ICMP_packets -m limit ! --limit 1000/s --limit-burst 1000 -j DROP
iptables -A ICMP_packets -m hashlimit --hashlimit-above 50/m --hashlimit-burst 50 --hashlimit-mode srcip --hashlimit-name icmp -j DROP




iptables 

-A input_int -p udp -m pkttype --pkt-type broadcast -m udp --dport 67 -j ACCEPT
-A input_int -m pkttype --pkt-type broadcast -j DROP
-A input_int -p icmp -m icmp --icmp-type 8 -j ACCEPT

-A input_int -p tcp -m limit --limit 3/min -m tcp --dport 53 --tcp-flags FIN,SYN,RST,ACK SYN -j LOG --log-prefix "SFW2-INint-ACC-TCP " --log-tcp-options --log-ip-options
-A input_int -p tcp -m tcp --dport 53 -j ACCEPT
-A input_int -p tcp -m limit --limit 3/min -m tcp --dport 22 --tcp-flags FIN,SYN,RST,ACK SYN -j LOG --log-prefix "SFW2-INint-ACC-TCP " --log-tcp-options --log-ip-options
-A input_int -p tcp -m tcp --dport 22 -j ACCEPT
-A input_int -p tcp -m limit --limit 3/min -m tcp --dport 21 --tcp-flags FIN,SYN,RST,ACK SYN -j LOG --log-prefix "SFW2-INint-ACC-TCP " --log-tcp-options --log-ip-options
-A input_int -p tcp -m tcp --dport 21 -j ACCEPT
-A input_int -p tcp -m limit --limit 3/min -m tcp --dport 30000:30100 --tcp-flags FIN,SYN,RST,ACK SYN -j LOG --log-prefix "SFW2-INint-ACC-TCP " --log-tcp-options --log-ip-options
-A input_int -p tcp -m tcp --dport 30000:30100 -j ACCEPT
-A input_int -p udp -m udp --dport 10500 -j ACCEPT
-A input_int -p udp -m udp --dport 53 -j ACCEPT
-A input_int -p udp -m udp --dport 67 -j ACCEPT
-A input_int -s 192.168.121.0/24 -p udp -m udp --dport 161 -m conntrack --ctstate NEW -m limit --limit 3/min -j LOG --log-prefix "SFW2-INint-ACC " --log-tcp-options --log-ip-options
-A input_int -s 192.168.121.0/24 -p udp -m udp --dport 161 -j ACCEPT

-A input_int -m pkttype --pkt-type multicast -j DROP
-A input_int -m pkttype --pkt-type broadcast -j DROP
-A input_int -p tcp -m limit --limit 3/min -m tcp --tcp-flags FIN,SYN,RST,ACK SYN -j LOG --log-prefix "SFW2-INint-DROP-DEFLT " --log-tcp-options --log-ip-options
-A input_int -p icmp -m limit --limit 3/min -j LOG --log-prefix "SFW2-INint-DROP-DEFLT " --log-tcp-options --log-ip-options
-A input_int -p udp -m limit --limit 3/min -m conntrack --ctstate NEW -j LOG --log-prefix "SFW2-INint-DROP-DEFLT " --log-tcp-options --log-ip-options
-A input_int -j DROP



-A INPUT -s 81.20.199.240/29 -i vlan1021 -j ACCEPT
-A INPUT -d 81.20.199.240/29 -i vlan13 -j ACCEPT
-A INPUT -s 81.20.199.64/26 -i vlan1021 -j ACCEPT
-A INPUT -d 81.20.199.64/26 -i vlan13 -j ACCEPT

-A INPUT -i bond0.1953.1011 -j input_int
-A INPUT -i vlan1011 -j input_int
-A INPUT -i vlan1021 -j input_int
-A INPUT -i vlan222 -j input_int
-A INPUT -i vlan27 -j input_int
-A INPUT -i bond0 -j input_dmz
-A INPUT -i bond1 -j input_dmz
-A INPUT -i eth0 -j input_dmz
-A INPUT -i eth1 -j input_dmz
-A INPUT -i vlan1029 -j input_dmz
-A INPUT -i vlan1891 -j input_dmz
-A INPUT -i vlan1953 -j input_dmz
-A INPUT -i vlan2037 -j input_dmz
-A INPUT -i vlan215 -j input_dmz
-A INPUT -j input_ext


-A INPUT -m limit --limit 3/min -j LOG --log-prefix "SFW2-IN-ILL-TARGET " --log-tcp-options --log-ip-options
-A INPUT -j DROP





Вражеские

vlan1112
vlan3151
vlan10
vlan875
vlan217
vlan209


LAN
enp5s1
tun+



DMZ
vlan401
vlan201
vlan402
vlan3997
vlan2999
vlan2002
vlan1901
vlan41
vlan1150
vlan1038
vlan1037
vlan1035
vlan676
vlan133
vlan99
vlan90
vlan40
vlan39
vlan37
vlan36
vlan34
vlan30
vlan29
vlan28
vlan27
vlan21
vlan22
vlan23
vlan24
vlan25
vlan26
vlan15
enp2s0.134.134
vlan12
vlan15






Как предотвращать DDoS атаки с помощью iptables

Я уверена, что вы все знаете что такое DDoS. Чтобы не допустить этот, в последнее время очень популярный вид атаки, воспользуйтесь следующей командой:

 iptables -A INPUT -p tcp --dport 80 -m limit --limit 20/minute --limit-burst 100 -j ACCEPT 

, где

    —limit 20/minute — максимальная средняя частота положительных результатов. После числа можно указывать единицы: `/second’, `/minute’, `/hour’, `/day’; значение по умолчанию — 3/hour. Лимит настраивайте в зависимости от своих требований.
    —limit-burst number — ограничивает исходное число пропускаемых пакетов: это число увеличивается на единицу каждый раз когда ограничение на частоту положительных результатов не достигается. Это происходит столько раз, сколько указано в данном параметре. Значение по умолчанию — 5.
    
    
-------------------------------------------------------------------------------------------------------------
Блокировка сканирования порта используя iptables

Хакеры так и ждут возможности просканировать открытые порты на вашем сервере и взломать систему безопасности. Чтобы не допустить этого безобразия:

 sudo iptables -N block-scan 

 sudo iptables -A block-scan -p tcp —tcp-flags SYN,ACK,FIN,RST -m limit —limit 1/s -j RETURN 

 sudo iptables -A block-scan -j DROP 

где block-scan — это название новой цепочки.

Надеюсь, что этот пост был максимально полезным для вас!

Подписывайтесь на обновления нашего блога и оставайтесь в курсе новостей мира инфокоммуникаций!

[https://xakep.ru/2009/10/14/49752/](https://xakep.ru/2009/10/14/49752/)
