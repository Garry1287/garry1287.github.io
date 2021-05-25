---
layout: post
title:  "plan-sapph"
date:   2013-11-17 18:19:46 +0400
categories: PSI
tags: PSI
---

# plan-sapph

iptables
Ntp-server          (x)
ssh                     (x)
Syslog-ng
ipsec/raccon    нах не нужен
dns                     (x)
dhcp для локалки
rpcbind
snmp                        (x)
nmbd (samba)
bgpd
ospfd
openvpn                 (x)
pptp
tftp                            (x)
radius                          (x)
postfix                         (x)

Настроить now
tftp
radius
openvpn
bgpd
snmp
dhcp
dns
?ipsec
syslog-ng
ssh


В процессе  -  завести интерфейсы их все в shut
iptables сделать( применить)


1.Список интерфейсов для переноса
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
2: enp5s1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UNKNOWN qlen 1000
    link/ether 00:e0:4c:b0:e6:74 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.11/24 brd 192.168.1.255 scope global enp5s1
       valid_lft forever preferred_lft forever
3: enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 6000 qdisc pfifo_fast state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
4: tunl0@NONE: <NOARP> mtu 1480 qdisc noop state DOWN qlen 1000
    link/ipip 0.0.0.0 brd 0.0.0.0
5: enp2s0.134@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 2000 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 10.148.2.1/23 brd 10.148.3.255 scope global enp2s0.134
       valid_lft forever preferred_lft forever
6: enp2s0.134.134@enp2s0.134: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
7: vlan10@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 81.20.192.19/27 brd 81.20.192.31 scope global vlan10
       valid_lft forever preferred_lft forever
11: vlan21@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.112.1/24 brd 192.168.112.255 scope global vlan21
       valid_lft forever preferred_lft forever
12: vlan22@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.113.1/24 brd 192.168.113.255 scope global vlan22
       valid_lft forever preferred_lft forever
13: vlan23@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.116.1/24 brd 192.168.116.255 scope global vlan23
       valid_lft forever preferred_lft forever
14: vlan24@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.117.1/24 brd 192.168.117.255 scope global vlan24
       valid_lft forever preferred_lft forever
15: vlan25@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.118.1/24 brd 192.168.118.255 scope global vlan25
       valid_lft forever preferred_lft forever
16: vlan26@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.120.1/24 brd 192.168.120.255 scope global vlan26
       valid_lft forever preferred_lft forever
17: vlan27@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.121.1/24 brd 192.168.121.255 scope global vlan27
       valid_lft forever preferred_lft forever
18: vlan28@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.122.1/24 brd 192.168.122.255 scope global vlan28
       valid_lft forever preferred_lft forever
19: vlan29@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.248.1/24 brd 192.168.248.255 scope global vlan29
       valid_lft forever preferred_lft forever
    inet 172.17.1.1/30 brd 172.17.1.3 scope global vlan29
       valid_lft forever preferred_lft forever
20: vlan30@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.123.1/24 brd 192.168.123.255 scope global vlan30
       valid_lft forever preferred_lft forever
21: vlan34@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.124.1/22 brd 192.168.127.255 scope global vlan34
       valid_lft forever preferred_lft forever
22: vlan36@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.115.1/24 brd 192.168.115.255 scope global vlan36
       valid_lft forever preferred_lft forever
23: vlan37@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 172.28.0.8/24 brd 172.28.0.255 scope global vlan37
       valid_lft forever preferred_lft forever
24: vlan39@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.60.1/24 brd 192.168.60.255 scope global vlan39
       valid_lft forever preferred_lft forever
25: vlan40@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.140.1/24 brd 192.168.140.255 scope global vlan40
       valid_lft forever preferred_lft forever
26: vlan90@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.253.68/29 brd 192.168.253.71 scope global vlan90
       valid_lft forever preferred_lft forever
27: vlan99@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.253.22/30 brd 192.168.253.23 scope global vlan99
       valid_lft forever preferred_lft forever
28: vlan133@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 10.148.0.33/27 brd 10.148.0.63 scope global vlan133
       valid_lft forever preferred_lft forever
29: vlan201@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 10.192.10.190/30 brd 10.192.10.191 scope global vlan201
       valid_lft forever preferred_lft forever
30: vlan209@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 172.16.77.22/30 brd 172.16.77.23 scope global vlan209
       valid_lft forever preferred_lft forever
31: vlan217@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.114.66/30 brd 192.168.114.67 scope global vlan217
       valid_lft forever preferred_lft forever
34: vlan676@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.169.25/29 brd 192.168.169.31 scope global vlan676
       valid_lft forever preferred_lft forever
36: vlan875@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 10.48.0.4/26 brd 10.48.0.63 scope global vlan875
       valid_lft forever preferred_lft forever
39: vlan1035@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.253.1/30 brd 192.168.253.3 scope global vlan1035
       valid_lft forever preferred_lft forever
40: vlan1037@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.169.1/30 brd 192.168.169.3 scope global vlan1037
       valid_lft forever preferred_lft forever
41: vlan1038@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.71.1/30 brd 192.168.71.3 scope global vlan1038
       valid_lft forever preferred_lft forever
42: vlan1150@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.253.9/29 brd 192.168.253.15 scope global vlan1150
       valid_lft forever preferred_lft forever
43: vlan1892@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 2000 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
44: vlan1901@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 10.148.0.8/28 brd 10.148.0.15 scope global vlan1901
       valid_lft forever preferred_lft forever
45: vlan2002@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 10.11.12.14/24 brd 10.11.12.255 scope global vlan2002
       valid_lft forever preferred_lft forever
46: vlan2999@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.200.18/24 brd 192.168.200.255 scope global vlan2999
       valid_lft forever preferred_lft forever
47: vlan3151@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.253.41/29 brd 192.168.253.47 scope global vlan3151
       valid_lft forever preferred_lft forever
48: vlan3997@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.50.1/30 brd 192.168.50.3 scope global vlan3997
       valid_lft forever preferred_lft forever
73: vlan41@vlan1892: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.169.9/29 brd 192.168.169.15 scope global vlan41
       valid_lft forever preferred_lft forever
    inet 192.168.169.17/29 brd 192.168.169.23 scope global vlan41:0
       valid_lft forever preferred_lft forever
74: dummy0: <BROADCAST,NOARP> mtu 1500 qdisc noop state DOWN qlen 1000
    link/ether ca:e6:a5:46:64:97 brd ff:ff:ff:ff:ff:ff
78: vlan401@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 6000 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.253.49/29 brd 192.168.253.55 scope global vlan401
       valid_lft forever preferred_lft forever
79: vlan402@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 6000 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 192.168.253.249/30 brd 192.168.253.251 scope global vlan402
       valid_lft forever preferred_lft forever
82: vlan1112@enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 6000 qdisc noqueue state UP qlen 1000
    link/ether 00:23:54:6b:88:2b brd ff:ff:ff:ff:ff:ff
    inet 172.31.255.218/30 brd 172.31.255.219 scope global vlan1112
       valid_lft forever preferred_lft forever
98: tun2: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UNKNOWN qlen 100
    link/none 
    inet 192.168.132.129/25 brd 192.168.132.255 scope global tun2
       valid_lft forever preferred_lft forever
99: tun1: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UNKNOWN qlen 100
    link/none 
    inet 192.168.133.1 peer 192.168.133.2/32 scope global tun1
       valid_lft forever preferred_lft forever
101: tun0: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UNKNOWN qlen 100
    link/none 
    inet 192.168.132.1 peer 192.168.132.2/32 scope global tun0
       valid_lft forever preferred_lft forever



2.Настройка iptables

3.Настройка radius

4. Настройка openvpn

5. Настройка Quagga

6.Настройка named

7. Настройка tftp

8. Настройка rsyslog

9.posfix

10.ntp


-------------------------------------------------
1.перенос vpn nlmk (как есть) Перенести фейк интерфейс, потом заменить

2. Другой интерфейс повесить для whatup
3. перенос радиус для комбината
4. Физиков оставить
5. Логины пароли поменять на 113, 115
6. NTP настроить
7.


shorewall
shorewall check
shorewall clear
shorewall restart

[https://losst.ru/nastrojka-shorewall-dlya-nachinayushhih](https://losst.ru/nastrojka-shorewall-dlya-nachinayushhih)
[http://www.opennet.ru/base/net/shorewall.txt.html](http://www.opennet.ru/base/net/shorewall.txt.html)
