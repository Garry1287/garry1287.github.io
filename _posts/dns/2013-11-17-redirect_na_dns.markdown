---
layout: post
title:  "redirect_na_dns"
date:   2013-11-17 23:52:58 +0400
categories: dns
tags: dns
---

# redirect_na_dns
15: vlan418@bond0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP 
    link/ether 00:15:17:6a:0e:64 brd ff:ff:ff:ff:ff:ff
    inet 192.168.253.89/29 brd 192.168.253.95 scope global vlan418


Заворачивать весь траффик на emerald
418 влан


iptables -t nat -A PREROUTING -p udp -m udp --dport 53 -j DNAT --to-destination 81.20.192.16:53




iptables -t nat -A PREROUTING -i <IP_VPN_SERVER> -p udp --dport 53 -j DNAT --to-destination <IP_DNS_SERVER>
iptables -t nat -A PREROUTING -i <IP_VPN_SERVER> -p tcp --dport 53 -j DNAT --to-destination <IP_DNS_SERVER>

iptables -t nat -A POSTROUTING -p tcp --dst <IP_DNS_SERVER> --dport 53 -j SNAT --to-source <IP_VPN_SERVER>
iptables -t nat -A POSTROUTING -p udp --dst <IP_DNS_SERVER> --dport 53 -j SNAT --to-source <IP_VPN_SERVER>


iptables -t nat -A PREROUTING -p udp --dport 53 -s 192.168.253.90 -j DNAT --to 81.20.192.16:53


selfip="10.0.0.11"
dnsip="10.0.0.4"
nw="10.0.0.0/24"
iptables -t nat -A PREROUTING -s $nw -p udp --dport 53 -j DNAT --to-destination $dnsip
iptables -t nat -A PREROUTING -s $nw -p tcp --dport 53 -j DNAT --to-destination $dnsip
iptables -t nat -A POSTROUTING -p tcp --dst $dnsip --dport 53 -j SNAT --to-source $selfip
iptables -t nat -A POSTROUTING -p udp --dst $dnsip --dport 53 -j SNAT --to-source $selfip




-A POSTROUTING -s 10.4.4.83/32 -o vlan13 -j SNAT --to-source 81.20.192.53
-A POSTROUTING -s 192.168.170.0/24 -o vlan13 -j SNAT --to-source 81.20.196.9
-A POSTROUTING -s 192.168.171.0/24 -o vlan13 -j SNAT --to-source 81.20.196.9
-A POSTROUTING -s 192.168.253.88/29 -o vlan13 -j SNAT --to-source 81.20.196.9



REDIRECT для RKN
iptables -A FORWARD -s 192.168.253.90 -d 81.20.192.16 -p udp --dport 53  -j ACCEPT
iptables -A FORWARD -s 192.168.253.90 -d 81.20.192.16 -p udp --dport 53  -j ACCEPT
iptables -A FORWARD -s 192.168.253.90 -p udp --dport 53 -j DROP
iptables -A FORWARD -s 192.168.253.90 -p tcp --dport 53 -j DROP


iptables -t nat -A PREROUTING -s 192.168.253.90 -p udp --dport 53 -j DNAT --to-destination 81.20.192.16
iptables -t nat -A PREROUTING -s 192.168.253.90 -p tcp --dport 53 -j DNAT --to-destination 81.20.192.16

iptables -t nat -A POSTROUTING -p tcp --dst 81.20.192.16 --dport 53 -j SNAT --to-source 81.20.196.9
iptables -t nat -A POSTROUTING -p udp --dst 81.20.192.16 --dport 53 -j SNAT --to-source 81.20.196.9








TEST NA SAPPHIRE
iptables -I FORWARD 1 -s 192.168.1.141 -d 81.20.192.19 -p udp --dport 53  -j ACCEPT
iptables -I FORWARD 2 -s 192.168.1.141 -d 81.20.192.19 -p udp --dport 53  -j ACCEPT
iptables -I FORWARD 3 -s 192.168.1.141 -p udp --dport 53 -j DROP
iptables -I FORWARD 4 -s 192.168.1.141 -p tcp --dport 53 -j DROP

iptables -t nat -I PREROUTING 1 -s 192.168.1.141 -p udp --dport 53 -j DNAT --to-destination 81.20.192.19
iptables -t nat -I PREROUTING 2 -s 192.168.1.141 -p tcp --dport 53 -j DNAT --to-destination 81.20.192.19
iptables -t nat -I POSTROUTING 1 -p tcp --dst 81.20.192.19 --dport 53 -j SNAT --to-source 81.20.192.32
iptables -t nat -I POSTROUTING 2 -p udp --dst 81.20.192.19 --dport 53 -j SNAT --to-source 81.20.192.32



iptables -t nat -D PREROUTING -s 192.168.1.141 -p udp --dport 53 -j DNAT --to-destination 81.20.192.19
iptables -t nat -D PREROUTING -s 192.168.1.141 -p tcp --dport 53 -j DNAT --to-destination 81.20.192.19
iptables -t nat -D POSTROUTING -p tcp --dst 81.20.192.19 --dport 53 -j SNAT --to-source 81.20.192.32
iptables -t nat -D POSTROUTING -p udp --dst 81.20.192.19 --dport 53 -j SNAT --to-source 81.20.192.32

iptables -D FORWARD -s 192.168.1.141 -d 81.20.192.19 -p udp --dport 53  -j ACCEPT
iptables -D FORWARD -s 192.168.1.141 -d 81.20.192.19 -p udp --dport 53  -j ACCEPT
iptables -D FORWARD -s 192.168.1.141 -p udp --dport 53 -j DROP
iptables -D FORWARD -s 192.168.1.141 -p tcp --dport 53 -j DROP

[http://forum.nag.ru/forum/index.php?showtopic=124678&st=0](http://forum.nag.ru/forum/index.php?showtopic=124678&st=0)
