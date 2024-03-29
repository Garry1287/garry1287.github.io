---
layout: post
title:  "tcpdump-ex"
date:   2017-05-11 09:22:59 +0300
categories: Networking
tags: Networking
---

# tcpdump-ex
See the list of interfaces on which tcpdump can listen:

tcpdump -D
Listen on interface eth0:

tcpdump -i eth0
Listen on any available interface (cannot be done in promiscuous mode. Requires Linux kernel 2.2 or greater):

tcpdump -i any
Be verbose while capturing packets:

tcpdump -v
Be more verbose while capturing packets:

tcpdump -vv
Be very verbose while capturing packets:

tcpdump -vvv
Be less verbose (than the default) while capturing packets:

tcpdump -q
Limit the capture to 100 packets:

tcpdump -c 100
Record the packet capture to a file called capture.cap:

tcpdump -w capture.cap
Record the packet capture to a file called capture.cap but display on-screen how many packets have been captured in real-time:

tcpdump -v -w capture.cap
Display the packets of a file called capture.cap:

tcpdump -r capture.cap
Display the packets using maximum detail of a file called capture.cap:

tcpdump -vvv -r capture.cap
Display IP addresses and port numbers instead of domain and service names when capturing packets:

tcpdump -n
Capture any packets where the destination host is 192.168.1.1. Display IP addresses and port numbers:

tcpdump -n dst host 192.168.1.1
Capture any packets where the source host is 192.168.1.1. Display IP addresses and port numbers:

tcpdump -n src host 192.168.1.1
Capture any packets where the source or destination host is 192.168.1.1. Display IP addresses and port numbers:

tcpdump -n host 192.168.1.1
Capture any packets where the destination network is 192.168.1.0/24. Display IP addresses and port numbers:

tcpdump -n dst net 192.168.1.0/24
Capture any packets where the source network is 192.168.1.0/24. Display IP addresses and port numbers:

tcpdump -n src net 192.168.1.0/24
Capture any packets where the source or destination network is 192.168.1.0/24. Display IP addresses and port numbers:

tcpdump -n net 192.168.1.0/24
Capture any packets where the destination port is 23. Display IP addresses and port numbers:

tcpdump -n dst port 23
Capture any packets where the destination port is is between 1 and 1023 inclusive. Display IP addresses and port numbers:

tcpdump -n dst portrange 1-1023
Capture only TCP packets where the destination port is is between 1 and 1023 inclusive. Display IP addresses and port numbers:

tcpdump -n tcp dst portrange 1-1023
Capture only UDP packets where the destination port is is between 1 and 1023 inclusive. Display IP addresses and port numbers:

tcpdump -n udp dst portrange 1-1023
Capture any packets with destination IP 192.168.1.1 and destination port 23. Display IP addresses and port numbers:

tcpdump -n "dst host 192.168.1.1 and dst port 23"
Capture any packets with destination IP 192.168.1.1 and destination port 80 or 443. Display IP addresses and port numbers:

tcpdump -n "dst host 192.168.1.1 and (dst port 80 or dst port 443)"
Capture any ICMP packets:

tcpdump -v icmp
Capture any ARP packets:

tcpdump -v arp
Capture either ICMP or ARP packets:

tcpdump -v "icmp or arp"
Capture any packets that are broadcast or multicast:

tcpdump -n "broadcast or multicast"
Capture 500 bytes of data for each packet rather than the default of 68 bytes:

tcpdump -s 500
Capture all bytes of data within the packet:

tcpdump -s 0

[http://docs.carbonsoft.ru/pages/viewpage.action?pageId=7241735](http://docs.carbonsoft.ru/pages/viewpage.action?pageId=7241735)
[http://openmaniak.com/tcpdump.php](http://openmaniak.com/tcpdump.php)
[http://kb.pert.geant.net/PERTKB/TcpdumpExamples](http://kb.pert.geant.net/PERTKB/TcpdumpExamples)
[http://www.appkubos.com/linux/Tcpdump.html](http://www.appkubos.com/linux/Tcpdump.html)
[http://yuyusaitanus.blogspot.ru/2010/07/tcpdump-filters.html](http://yuyusaitanus.blogspot.ru/2010/07/tcpdump-filters.html)
[http://www.workrobot.com/sysadmin/security/tcpdump_expressions.html](http://www.workrobot.com/sysadmin/security/tcpdump_expressions.html)
[http://www.protocols.ru/modules.php?name=News&file=article&sid=125](http://www.protocols.ru/modules.php?name=News&file=article&sid=125)
[http://danielmiessler.com/study/tcpdump/](http://danielmiessler.com/study/tcpdump/)
[http://mccltd.net/blog/?p=1199](http://mccltd.net/blog/?p=1199)
[http://www.k-max.name/linux/tcpdump-v-primerax/](http://www.k-max.name/linux/tcpdump-v-primerax/)
[http://alexof.ru/page/tcpdump](http://alexof.ru/page/tcpdump)