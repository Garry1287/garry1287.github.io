---
layout: post
title:  "Vienna-test-speed"
date:   2015-07-22 04:49:36 +0300
categories: zavod
tags: zavod
---

# Vienna-test-speed
NLMK_admin
7rubrEra

https
193.80.22.64 tcp/4431 
193.80.22.64 tcp/4432  




as requested: 7rubrEra


 
Hi Danijel,
 
I would like to inform you I\u2019ve installed the console servers. The procedure to reach the devices via the console server is the following:

    Make an ssh connection to devices in the DC38 (firewall0, balancer0, switch0, CE0) using the IP address of 193.80.22.64 on port tcp/3333 

    to devices in the DC38 (firewall0, balancer0, switch0, CE0) using the IP address of 193.80.22.64 on port tcp/3333 
    to devices in the DC39 (firewall1, balancer1, switch1, CE1) using the IP address of 193.80.22.64 on port tcp/3334

    when they get a prompt use the username followed by the \u201c:\u201d

    username: NLMK_admin
    password: what we created for the devices itself

    there will be the manageable devices in the list on the screen, they have to enter what they wish to manage

  
After that they need to hit \u201cENTER\u201d once more to get the login prompt on the devices
Any question please feel free to ask
 
 
 
 
 
 
[root@quartz sysconfig]# iperf -c 10.170.0.14 -p 65005 
------------------------------------------------------------
Client connecting to 10.170.0.14, TCP port 65005
TCP window size: 18.6 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 41479 connected with 10.170.0.14 port 65005
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-10.0 sec  26.8 MBytes  22.4 Mbits/sec





[root@quartz sysconfig]# iperf -c 10.170.0.14 -p 65005 
------------------------------------------------------------
Client connecting to 10.170.0.14, TCP port 65005
TCP window size: 18.6 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 41480 connected with 10.170.0.14 port 65005
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-10.0 sec  27.6 MBytes  23.1 Mbits/sec






[  3] local 10.192.10.230 port 41485 connected with 10.170.0.14 port 65005
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-10.0 sec  73.4 MBytes  61.5 Mbits/sec
[root@quartz sysconfig]# iperf -c 10.170.0.14 -p 65005 




^[[A[root@quartz sysconfig]# iperf -c 10.170.0.14 -n 100m -p 65005 
------------------------------------------------------------
Client connecting to 10.170.0.14, TCP port 65005
TCP window size: 18.6 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 41488 connected with 10.170.0.14 port 65005
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-19.6 sec    100 MBytes  42.8 Mbits/sec



[root@quartz sysconfig]# iperf -c 10.170.0.14 -n 200m -p 65005 
------------------------------------------------------------
Client connecting to 10.170.0.14, TCP port 65005
TCP window size: 18.6 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 41489 connected with 10.170.0.14 port 65005
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-33.5 sec    200 MBytes  50.0 Mbits/sec
[root@quartz sysconfig]# iperf -c 10.170.0.14 -n 1000m -p 65005 






[root@quartz sysconfig]# iperf -c 10.170.0.14 -n 1000m -p 65005 
------------------------------------------------------------
Client connecting to 10.170.0.14, TCP port 65005
TCP window size: 18.6 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 41490 connected with 10.170.0.14 port 65005
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-106.9 sec  1000 MBytes  78.5 Mbits/sec






[root@quartz sysconfig]# iperf -c 10.170.0.14 -n 300m -p 65005 
------------------------------------------------------------
Client connecting to 10.170.0.14, TCP port 65005
TCP window size: 18.6 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 41491 connected with 10.170.0.14 port 65005
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-39.6 sec    300 MBytes  63.5 Mbits/se



[root@quartz sysconfig]# iperf -c 10.170.0.14 -n 500m -p 65005 
------------------------------------------------------------
Client connecting to 10.170.0.14, TCP port 65005
TCP window size: 18.6 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 41493 connected with 10.170.0.14 port 65005
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-56.4 sec    500 MBytes  74.4 Mbits/sec





[root@quartz sysconfig]# iperf -c 10.170.0.14 -n 1000m -p 65005 
------------------------------------------------------------
Client connecting to 10.170.0.14, TCP port 65005
TCP window size: 18.6 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 41494 connected with 10.170.0.14 port 65005
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-107.5 sec  1000 MBytes  78.0 Mbits/sec









[root@quartz sysconfig]# iperf -u -c 10.170.0.14 -n 1000m -b 100M -p 65006
------------------------------------------------------------
Client connecting to 10.170.0.14, UDP port 65006
Sending 1470 byte datagrams
UDP buffer size:   122 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 36851 connected with 10.170.0.14 port 65006


^C[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-657.5 sec  7.69 GBytes    101 Mbits/sec
[  3] Sent 5619298 datagrams
[  3] Server Report:
[ ID] Interval       Transfer     Bandwidth       Jitter   Lost/Total Datagrams
[  3]  0.0-657.5 sec  7.32 GBytes  95.6 Mbits/sec  0.016 ms 272839/5619298 (4.9%)
[  3]  0.0-657.5 sec  2 datagrams received out-of-order



 -w, --window n[KM]
              TCP window size (socket buffer size)
18.6 KByte

       -P, --parallel n
              number of parallel client threads to run









Vienna-Retn-CE0#sh int Gi0/0
GigabitEthernet0/0 is up, line protocol is up 
  Hardware is CN Gigabit Ethernet, address is 3c08.f612.f890 (bia 3c08.f612.f890)
  Description: NLMK_PE0 via Megafon/A1 (PR2 R02/01 EXAE 1402669)
  Internet address is 10.192.10.170/30
  MTU 1500 bytes, BW 102400 Kbit/sec, DLY 100 usec, 
     reliability 255/255, txload 1/255, rxload 223/255
  Encapsulation ARPA, loopback not set
  Keepalive set (10 sec)
  Full Duplex, 100Mbps, media type is RJ45
  output flow-control is unsupported, input flow-control is unsupported
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 00:00:00, output 00:00:00, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 89783000 bits/sec, 14319 packets/sec
  30 second output rate 146000 bits/sec, 32 packets/sec
     3520005521 packets input, 166510155 bytes, 0 no buffer
     Received 74 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles 
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     1960017621 packets output, 3028399704 bytes, 0 underruns
     0 output errors, 0 collisions, 2 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     1 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out














[root@quartz sysconfig]# iperf -c 10.170.0.14 -n 50m -p 65005 
------------------------------------------------------------
Client connecting to 10.170.0.14, TCP port 65005
TCP window size: 18.6 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 41497 connected with 10.170.0.14 port 65005
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-404.7 sec    500 MBytes  10.4 Mbits/



Vienna-Retn-CE0#sh int Gi0/0
GigabitEthernet0/0 is up, line protocol is up 
  Hardware is CN Gigabit Ethernet, address is 3c08.f612.f890 (bia 3c08.f612.f890)
  Description: NLMK_PE0 via Megafon/A1 (PR2 R02/01 EXAE 1402669)
  Internet address is 10.192.10.170/30
  MTU 1500 bytes, BW 102400 Kbit/sec, DLY 100 usec, 
     reliability 255/255, txload 1/255, rxload 245/255
  Encapsulation ARPA, loopback not set
  Keepalive set (10 sec)
  Full Duplex, 100Mbps, media type is RJ45
  output flow-control is unsupported, input flow-control is unsupported
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 00:00:00, output 00:00:00, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 98412000 bits/sec, 8157 packets/sec
  30 second output rate 189000 bits/sec, 51 packets/sec












UDP


 iperf -u -c 10.170.0.14 -n 1000m -b 100M -p 65006
------------------------------------------------------------
Client connecting to 10.170.0.14, UDP port 65006
Sending 1470 byte datagrams
UDP buffer size:   122 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 36851 connected with 10.170.0.14 port 65006


^C[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-657.5 sec  7.69 GBytes    101 Mbits/sec
[  3] Sent 5619298 datagrams
[  3] Server Report:
[ ID] Interval       Transfer     Bandwidth       Jitter   Lost/Total Datagrams
[  3]  0.0-657.5 sec  7.32 GBytes  95.6 Mbits/sec  0.016 ms 272839/5619298 (4.9%)
[  3]  0.0-657.5 sec  2 datagrams received out-of-order



10 FTP соединений
На интерфейсе

GigabitEthernet0/0 is up, line protocol is up 
  Hardware is CN Gigabit Ethernet, address is 3c08.f612.f890 (bia 3c08.f612.f890)
  Description: NLMK_PE0 via Megafon/A1 (PR2 R02/01 EXAE 1402669)
  Internet address is 10.192.10.170/30
  MTU 1500 bytes, BW 102400 Kbit/sec, DLY 100 usec, 
     reliability 255/255, txload 5/255, rxload 218/255
  Encapsulation ARPA, loopback not set
  Keepalive set (10 sec)
  Full Duplex, 100Mbps, media type is RJ45
  output flow-control is unsupported, input flow-control is unsupported
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 00:00:00, output 00:00:00, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  30 second input rate 87882000 bits/sec, 7672 packets/sec
  30 second output rate 2209000 bits/sec, 3995 packets/sec
     3524768269 packets input, 2480171772 bytes, 0 no buffer
     Received 74 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles 
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog, 0 multicast, 0 pause input
     1962589180 packets output, 3312359264 bytes, 0 underruns
     0 output errors, 0 collisions, 2 interface resets
     0 unknown protocol drops
     0 babbles, 0 late collision, 0 deferred
     1 lost carrier, 0 no carrier, 0 pause output
     0 output buffer failures, 0 output buffers swapped out

50















20 соединений
iperf -c 10.170.0.14 -P 20 -p 65005

------------------------------------------------------------
Client connecting to 10.170.0.14, TCP port 65005
TCP window size: 18.6 KByte (default)
------------------------------------------------------------
[ 22] local 10.192.10.230 port 41893 connected with 10.170.0.14 port 65005
[  8] local 10.192.10.230 port 41879 connected with 10.170.0.14 port 65005
[  6] local 10.192.10.230 port 41877 connected with 10.170.0.14 port 65005
[ 11] local 10.192.10.230 port 41881 connected with 10.170.0.14 port 65005
[  3] local 10.192.10.230 port 41876 connected with 10.170.0.14 port 65005
[  4] local 10.192.10.230 port 41874 connected with 10.170.0.14 port 65005
[ 12] local 10.192.10.230 port 41884 connected with 10.170.0.14 port 65005
[  5] local 10.192.10.230 port 41875 connected with 10.170.0.14 port 65005
[ 14] local 10.192.10.230 port 41883 connected with 10.170.0.14 port 65005
[ 10] local 10.192.10.230 port 41882 connected with 10.170.0.14 port 65005
[ 13] local 10.192.10.230 port 41885 connected with 10.170.0.14 port 65005
[ 16] local 10.192.10.230 port 41887 connected with 10.170.0.14 port 65005
[  9] local 10.192.10.230 port 41880 connected with 10.170.0.14 port 65005
[ 17] local 10.192.10.230 port 41888 connected with 10.170.0.14 port 65005
[ 15] local 10.192.10.230 port 41886 connected with 10.170.0.14 port 65005
[  7] local 10.192.10.230 port 41878 connected with 10.170.0.14 port 65005
[ 18] local 10.192.10.230 port 41889 connected with 10.170.0.14 port 65005
[ 21] local 10.192.10.230 port 41892 connected with 10.170.0.14 port 65005


[ ID] Interval       Transfer     Bandwidth
[  8]  0.0-10.0 sec  3.85 MBytes  3.23 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[ 13]  0.0-10.0 sec  3.66 MBytes  3.07 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[ 14]  0.0-10.0 sec  4.20 MBytes  3.52 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[ 10]  0.0-10.0 sec  4.12 MBytes  3.46 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  5]  0.0-10.0 sec  4.73 MBytes  3.97 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-10.0 sec  6.05 MBytes  5.07 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  7]  0.0-10.0 sec  3.48 MBytes  2.91 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  9]  0.0-10.0 sec  6.27 MBytes  5.24 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[ 11]  0.0-10.0 sec  3.16 MBytes  2.64 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[ 15]  0.0-10.0 sec  4.38 MBytes  3.65 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[ 12]  0.0-10.1 sec  3.11 MBytes  2.59 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[ 16]  0.0-10.1 sec  6.65 MBytes  5.55 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[ 19]  0.0-10.1 sec  4.90 MBytes  4.08 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  6]  0.0-10.1 sec  3.84 MBytes  3.20 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[ 22]  0.0-10.1 sec  4.42 MBytes  3.67 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  4]  0.0-10.1 sec  4.90 MBytes  4.06 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[ 20]  0.0-10.1 sec  7.05 MBytes  5.85 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[ 21]  0.0-10.1 sec  5.27 MBytes  4.37 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[ 17]  0.0-10.1 sec  5.58 MBytes  4.61 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[ 18]  0.0-10.2 sec  5.96 MBytes  4.91 Mbits/sec
[SUM]  0.0-10.2 sec  95.6 MBytes  78.8 Mbits/sec





