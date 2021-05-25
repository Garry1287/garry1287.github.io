---
layout: post
title:  "spoofing_linux"
date:   2010-11-24 16:22:23 +0300
categories: linux
tags: linux
---

# spoofing_linux
-A input_ext -p tcp -m limit --limit 3/min -m tcp --dport 53 --tcp-flags FIN,SYN,RST,ACK SYN -j LOG --log-prefix "SFW2-INext-ACC-TCP " --log-tcp-options --log-ip-options
-A input_ext -p tcp -m tcp --dport 53 -j ACCEPT
-A input_ext -p udp -m udp --dport 53 -j ACCEPT


-A INPUT -j input_ext


-A input_int -p tcp -m limit --limit 3/min -m tcp --dport 22 --tcp-flags FIN,SYN,RST,ACK SYN -j LOG --log-prefix "SFW2-INint-ACC-TCP " --log-tcp-options --log-ip-options


iptables -I POSTROUTING  4 -p tcp -m limit --limit 3/min -s 172.20.96.0/22 -o vlan10 -j LOG --log-prefix "NAt 96.0 " --log-tcp-options --log-ip-options

iptables -I FORWARD 4 -p tcp -m limit --limit 3/min -i lo -o vlan1021 -j -j LOG --log-prefix "Loopback " --log-tcp-options --log-ip-options
iptables -I FORWARD 5 -i lo -o vlan1012 -j ACCEPT

[http://armanenshaft-linux.blogspot.ru/2010/09/linux_8449.html](http://armanenshaft-linux.blogspot.ru/2010/09/linux_8449.html)
[http://xgu.ru/wiki/IP-spoofing](http://xgu.ru/wiki/IP-spoofing)

Нужен 0 - выключение

for i in /proc/sys/net/ipv4/conf/*/rp_filter ; do  echo 2 > $i; done




sysctl -w net.ipv4.conf.eth0.rp_filter=2
sysctl -w net.ipv4.conf.eth1.rp_filter=2
sysctl -w net.ipv4.conf.lo.rp_filter=2
sysctl -w net.ipv4.conf.vlan10.rp_filter=2
sysctl -w net.ipv4.conf.vlan1021.rp_filter=2
sysctl -w net.ipv4.conf.vlan27.rp_filter=2
sysctl -w net.ipv4.conf.all.rp_filter=2
sysctl -w net.ipv4.conf.default.rp_filter=2

eth0  eth1  lo  vlan10  vlan1021  vlan27
