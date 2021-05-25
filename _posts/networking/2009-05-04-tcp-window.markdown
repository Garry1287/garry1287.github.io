---
layout: post
title:  "tcp-window"
date:   2009-05-04 10:11:58 +0400
categories: Networking
tags: Networking
---

# tcp-window
[http://bradhedlund.com/2008/12/19/how-to-calculate-tcp-throughput-for-long-distance-links/](http://bradhedlund.com/2008/12/19/how-to-calculate-tcp-throughput-for-long-distance-links/)
[http://it-portal.maglan.net/Tonkaya-Nastroyka-TCP.html](http://it-portal.maglan.net/Tonkaya-Nastroyka-TCP.html)
[http://dml.compkaluga.ru/forum/index.php?showtopic=27517](http://dml.compkaluga.ru/forum/index.php?showtopic=27517)


First lets convert the TCP window size from bytes to bits.  In this case we are using the standard 64KB TCP window size of a Windows machine.

64KB = 65536 Bytes.   65536 * 8 = 524288 bits

Next, lets take the TCP window in bits and divide it by the round trip latency of our link in seconds.  So if our latency is 30 milliseconds we will use 0.030 in our calculation.

524288 bits / 0.030 seconds = 17476266 bits per second throughput = 17.4 Mbps maximum possible throughput



throughput = TCP window size / RTT (roud trip time)

Assume that the TCP window size is 64KB and the RTT is 40ms, the throughput is:
65936 Bytes / 40 ms = 1.6 MBytes/s = 13 Mbits/s




[http://www.switch.ch/fr/network/tools/tcp_throughput/?do+new+calculation=do+new+calculation](http://www.switch.ch/fr/network/tools/tcp_throughput/?do+new+calculation=do+new+calculation)
11 Мбит/с