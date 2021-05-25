---
layout: post
title:  "arp-parametr"
date:   2013-06-19 08:35:07 +0400
categories: Networking
tags: Networking
---

# arp-parametr
[http://habrahabr.ru/post/108240/](http://habrahabr.ru/post/108240/)

net.ipv4.neigh.default.gc_thresh1=2048
net.ipv4.neigh.default.gc_thresh2=4096
net.ipv4.neigh.default.gc_thresh3=8192






если нет необходимости в conntrack его тоже надо отрубить
*raw
-A PREROUTING -j NOTRACK
COMMIT

увеличить очередь
ifconfig eth0 txqueuelen 10000

потом смотреть ошибки и по необходимости увеличить буфер
ethtool -G eth0 rx 1024

если надо conntrack то увеличивать
net.ipv4.netfilter.ip_conntrack_max и /sys/module/ip_conntrack/parameters/hashsize
и уменьшать интервалы
net.ipv4.netfilter.ip_conntrack_icmp_timeout
net.ipv4.netfilter.ip_conntrack_udp_timeout_stream
net.ipv4.netfilter.ip_conntrack_udp_timeout
net.ipv4.netfilter.ip_conntrack_tcp_timeout_close
net.ipv4.netfilter.ip_conntrack_tcp_timeout_time_wait
net.ipv4.netfilter.ip_conntrack_tcp_timeout_last_ack
net.ipv4.netfilter.ip_conntrack_tcp_timeout_close_wait
net.ipv4.netfilter.ip_conntrack_tcp_timeout_fin_wait
net.ipv4.netfilter.ip_conntrack_tcp_timeout_established
net.ipv4.netfilter.ip_conntrack_tcp_timeout_syn_recv
net.ipv4.netfilter.ip_conntrack_tcp_timeout_syn_sent

уменьшать количество правил iptables, если надо много однотипных списков то использовать ipset

и пр. пр. пр. 









create access_profile ethernet source_mac FF-FF-FF-FF-FF-FF profile_id 20
config access_profile profile_id 20 add access_id 21 ethernet source_mac 68-9C-5E-B9-15-BF port 1 deny

link-detect 


ip ospf hello-interval 20
ip ospf dead-interval 40
ip ospf retransmit-interval 20
ip ospf transmit-delay 20



 ip ospf transmit-delay

To set the estimated time required to send a link-state update packet on the interface, use the ip ospf transmit-delay command in interface configuration mode. To return to the default value, use the no form of this command.

ip ospf transmit-delay seconds

no ip ospf transmit-delay
Syntax Description

seconds
	
Time (in seconds) required to send a link-state update. The range is from 1 to 65535 seconds. The default is 1 second. 






 ip ospf retransmit-interval

To specify the time between link-state advertisement (LSA) retransmissions for adjacencies belonging to the interface, use the ip ospf retransmit-interval command in interface configuration mode. To return to the default value, use the no form of this command.

ip ospf retransmit-interval seconds

no ip ospf retransmit-interval
Syntax Description

seconds
	

Time (in seconds) between retransmissions. The range is from 1 to 65535 seconds. The default is 5 seconds.

Defaults

5 seconds 

link-mtu 
tun-mtu 
fixmss

fragmen 1400
mssfix



00:26:18:95:72:ff

00:26:18:95:72:bb


ospfTrapNbrStateChange trap sent: 81.20.192.10 now Init/DROther

ospfTrapNbrStateChange trap sent: 81.20.192.10 now 2-Way/DROther

 ip ospf hello-interval 8
 ip ospf dead-interval 24
 ip ospf retransmit-interval 4 
link-detect


2013/11/12 15:30:57 OSPF: DR-Election[1st]: DR     81.20.192.22
2013/11/12 15:32:45 OSPF: nsm_change_state(81.20.192.22, Full -> Init): scheduling new router-LSA origination
2013/11/12 15:32:45 OSPF: DR-Election[1st]: Backup 81.20.192.5
2013/11/12 15:32:45 OSPF: DR-Election[1st]: DR     81.20.192.5
2013/11/12 15:32:48 OSPF: nsm_change_state(81.20.192.5, Full -> Init): scheduling new router-LSA origination
2013/11/12 15:32:48 OSPF: DR-Election[1st]: Backup 81.20.192.12
2013/11/12 15:32:48 OSPF: DR-Election[1st]: DR     81.20.192.12
2013/11/12 15:33:07 OSPF: Link State Update: Neighbor[81.20.192.5] state Init is less than Exchange
2013/11/12 15:33:10 OSPF: Link State Acknowledgment: Neighbor[81.20.192.22] state Init is less than Exchange
2013/11/12 15:33:26 OSPF: Link State Update: Neighbor[81.20.192.5] state Init is less than Exchange
2013/11/12 15:33:27 OSPF: Link State Update: Neighbor[81.20.192.22] state Init is less than Exchange
2013/11/12 15:33:27 OSPF: Link State Update: Neighbor[81.20.192.5] state Init is less than Exchange
2013/11/12 15:33:29 OSPF: Link State Acknowledgment: Neighbor[81.20.192.22] state Init is less than Exchange
2013/11/12 15:33:30 OSPF: Link State Acknowledgment: Neighbor[81.20.192.5] state Init is less than Exchange
2013/11/12 15:33:35 OSPF: Link State Update: Neighbor[81.20.192.22] state Init is less than Exchange
2013/11/12 15:33:37 OSPF: Link State Acknowledgment: Neighbor[81.20.192.5] state Init is less than Exchange
2013/11/12 15:33:42 OSPF: ospfTrapNbrStateChange trap sent: 81.20.192.22 now Init/DROther
2013/11/12 15:33:42 OSPF: DR-Election[1st]: Backup 81.20.192.12
2013/11/12 15:33:42 OSPF: DR-Election[1st]: DR     81.20.192.22
2013/11/12 15:33:44 OSPF: Packet[DD]: Neighbor 81.20.192.22 Negotiation done (Slave).
2013/11/12 15:33:44 OSPF: nsm_change_state(81.20.192.22, Loading -> Full): scheduling new router-LSA origination
2013/11/12 15:33:47 OSPF: Link State Acknowledgment: Neighbor[81.20.192.5] state Init is less than Exchange
2013/11/12 15:33:52 OSPF: Link State Acknowledgment: Neighbor[81.20.192.5] state Init is less than Exchange
2013/11/12 15:33:59 OSPF: ospfTrapNbrStateChange trap sent: 81.20.192.5 now Init/DROther


FULL to DOWN, Neighbor Down: Dead timer expired
Это обусловлено тем, что значения параметров  hello-interval и dead-interval должны совпадать на обоих концах линка. 


>Hello 30sec
>Dead 120sec
>Wait 120sec
>Retransmit 5sec


Interface Command: ip ospf retransmit-interval <1-65535> {}
Interface Command: no ip ospf retransmit interval {}
  Устанавливает значение в секундах для RxmtInterval timer. Этот таймер используется при повторных передачах базы данных описаний и запросов состояния соединения. Значение по умолчанию - 5 секунд.

Interface Command: ip ospf transmit-delay {}
Interface Command: no ip ospf transmit-delay {}
  Устанавливает значение в секундах для InfTransDelay. Возраст LSA должен быть увеличен на это значение при передаче. Значение по умолчанию - 1 секунда.
