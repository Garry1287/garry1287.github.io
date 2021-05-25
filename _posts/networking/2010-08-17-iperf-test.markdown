---
layout: post
title:  "iperf-test"
date:   2010-08-17 21:25:36 +0400
categories: Networking
tags: Networking
---

# iperf-test

wget --user=wantst --password=speedTSTwan ftp://10.170.0.14/test.psi100  /dev/null
  524  iperf -c 10.170.0.14 -n 50m -P 30 -p 65005
  525  iperf -c 10.170.0.14 -n 50m -P 20 -p 65005
  526  iperf -c 10.170.0.14 -n 50m -P 25 -p 65005
  527  iperf -c 10.170.0.14  -P 25 -p 65005
  528  iperf -u -c 10.170.0.14 -n 100m -b 100M  -p 65006
  529  iperf -u -c 10.170.0.14 -n 1000m -b 100M  -p 65006
  530  iperf -c 10.170.0.14 -n 50m -w 0,5 -p 65005 
  531  iperf -c 10.170.0.14 -n 50m -w 512 -p 65005 
  532  iperf -c 10.170.0.14 -n 50m -w 512KB -p 65005 
  533  iperf -c 10.170.0.14 -n 50m -w 244KB -p 65005 
  534  iperf -u -c 10.170.0.14 -b 100M  -p 65006
  535  iperf -u -c 10.170.0.14 -b 100M  -p 65006
  536  iperf -u -c 10.170.0.14 -p 65006
  537  iperf -c 10.170.0.14 -p 65005
  538  iperf -c 10.170.0.14 -P 10 -p 65005
  539  iperf -c 10.170.0.14 -P 20 -p 65005
  540  iperf -c 10.170.0.14 -n 50m -P 25 -p 65005
  541  iperf -c 10.170.0.14 -P 20 -p 65005
  542  iperf -c 10.170.0.14 -w 244KB -p 65005
  543  iperf -c 10.170.0.14 -w 512KB -p 65005
  515  iperf -c 10.170.0.14 -n 50m -p 65005 

  516  iperf -c 10.170.0.14 -n 50m -P 10 -p 65005
  517  iperf -c 10.170.0.14 -n 50m -P 20 -p 65005
  518  iperf -c 10.170.0.14 -n 50m -P 30 -p 65005


[garry@quartz ~]$ iperf -u -c 10.170.0.14 -b 100M -t 30 -i 10 -p 65006
------------------------------------------------------------
Client connecting to 10.170.0.14, UDP port 65006
Sending 1470 byte datagrams
UDP buffer size:   122 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 47487 connected with 10.170.0.14 port 65006
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-10.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 10.0-20.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 20.0-30.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-30.0 sec    359 MBytes    101 Mbits/sec
[  3] Sent 256412 datagrams
[  3] Server Report:
[ ID] Interval       Transfer     Bandwidth       Jitter   Lost/Total Datagrams
[  3]  0.0-30.0 sec    340 MBytes  95.2 Mbits/sec  0.009 ms 13554/256412 (5.3%)
[  3]  0.0-30.0 sec  2 datagrams received out-of-order
[garry@quartz ~]$ iperf -u -c 10.170.0.14 -b 100M -t 100 -i 10 -p 65006
------------------------------------------------------------
Client connecting to 10.170.0.14, UDP port 65006
Sending 1470 byte datagrams
UDP buffer size:   122 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 54714 connected with 10.170.0.14 port 65006
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-10.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 10.0-20.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 20.0-30.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 30.0-40.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 40.0-50.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 50.0-60.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 60.0-70.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 70.0-80.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 80.0-90.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 90.0-100.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-100.0 sec  1.17 GBytes    101 Mbits/sec
[  3] Sent 854702 datagrams
[  3] Server Report:
[ ID] Interval       Transfer     Bandwidth       Jitter   Lost/Total Datagrams
[  3]  0.0-100.0 sec  1.11 GBytes  95.3 Mbits/sec  0.023 ms 44589/854702 (5.2%)
[  3]  0.0-100.0 sec  1 datagrams received out-of-order
[garry@quartz ~]$ iperf -c 10.170.0.14 -t 100 -i 10 -p 65005
------------------------------------------------------------
Client connecting to 10.170.0.14, TCP port 65005
TCP window size: 18.6 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 42380 connected with 10.170.0.14 port 65005
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-10.0 sec  23.7 MBytes  19.9 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 10.0-20.0 sec  37.1 MBytes  31.1 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 20.0-30.0 sec  40.1 MBytes  33.6 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 30.0-40.0 sec  26.9 MBytes  22.6 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 40.0-50.0 sec  22.8 MBytes  19.1 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 50.0-60.0 sec  17.9 MBytes  15.0 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 60.0-70.0 sec  27.1 MBytes  22.8 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 70.0-80.0 sec  28.9 MBytes  24.2 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 80.0-90.0 sec  41.5 MBytes  34.8 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 90.0-100.0 sec  34.0 MBytes  28.6 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-100.1 sec    300 MBytes  25.2 Mbits/sec
[garry@quartz ~]$ iperf -u -c 10.170.0.14 -b 1024000 -t 100 -i 10 -p 65006
------------------------------------------------------------
Client connecting to 10.170.0.14, UDP port 65006
Sending 1470 byte datagrams
UDP buffer size:   122 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 50686 connected with 10.170.0.14 port 65006
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-10.0 sec  1.22 MBytes  1.02 Mbits/sec
^C[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-15.2 sec  1.85 MBytes  1.02 Mbits/sec
[  3] Sent 1320 datagrams
[  3] Server Report:
[ ID] Interval       Transfer     Bandwidth       Jitter   Lost/Total Datagrams
[  3]  0.0-15.2 sec  1.85 MBytes  1.02 Mbits/sec  0.259 ms    0/ 1320 (0%)
[garry@quartz ~]$ iperf -u -c 10.170.0.14 -b 1024000b -t 100 -i 10 -p 65006
------------------------------------------------------------
Client connecting to 10.170.0.14, UDP port 65006
Sending 1470 byte datagrams
UDP buffer size:   122 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 39324 connected with 10.170.0.14 port 65006
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-10.0 sec  1.22 MBytes  1.02 Mbits/sec
^C[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-11.8 sec  1.44 MBytes  1.02 Mbits/sec
[  3] Sent 1029 datagrams
[  3] Server Report:
[ ID] Interval       Transfer     Bandwidth       Jitter   Lost/Total Datagrams
[  3]  0.0-11.8 sec  1.44 MBytes  1.02 Mbits/sec  0.113 ms    0/ 1029 (0%)
[garry@quartz ~]$ iperf -u -c 10.170.0.14 -b 100M -t 100 -i 10 -p 65006
------------------------------------------------------------
Client connecting to 10.170.0.14, UDP port 65006
Sending 1470 byte datagrams
UDP buffer size:   122 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 56963 connected with 10.170.0.14 port 65006
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-10.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 10.0-20.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 20.0-30.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 30.0-40.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 40.0-50.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 50.0-60.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 60.0-70.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 70.0-80.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 80.0-90.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 90.0-100.0 sec    120 MBytes    101 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-100.0 sec  1.17 GBytes    101 Mbits/sec
[  3] Sent 854702 datagrams
[  3] Server Report:
[ ID] Interval       Transfer     Bandwidth       Jitter   Lost/Total Datagrams
[  3]  0.0-100.0 sec  1.11 GBytes  95.3 Mbits/sec  0.016 ms 44172/854702 (5.2%)
[  3]  0.0-100.0 sec  2 datagrams received out-of-order
[garry@quartz ~]$ iperf -u -c 10.170.0.14 -b 102400000 -t 100 -i 10 -p 65006
------------------------------------------------------------
Client connecting to 10.170.0.14, UDP port 65006
Sending 1470 byte datagrams
UDP buffer size:   122 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 57387 connected with 10.170.0.14 port 65006
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-10.0 sec    123 MBytes    103 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 10.0-20.0 sec    123 MBytes    103 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 20.0-30.0 sec    123 MBytes    103 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 30.0-40.0 sec    123 MBytes    103 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 40.0-50.0 sec    123 MBytes    103 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 50.0-60.0 sec    123 MBytes    103 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 60.0-70.0 sec    123 MBytes    103 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 70.0-80.0 sec    123 MBytes    103 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 80.0-90.0 sec    123 MBytes    103 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3] 90.0-100.0 sec    123 MBytes    103 Mbits/sec
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-100.0 sec  1.20 GBytes    103 Mbits/sec
[  3] Sent 877194 datagrams
[  3] Server Report:
[ ID] Interval       Transfer     Bandwidth       Jitter   Lost/Total Datagrams
[  3]  0.0-100.0 sec  1.11 GBytes  95.3 Mbits/sec  0.019 ms 66925/877194 (7.6%)
[  3]  0.0-100.0 sec  3 datagrams received out-of-order
[garry@quartz ~]$ iperf -u -c 10.170.0.14 -b 102400000  -p 65006
------------------------------------------------------------
Client connecting to 10.170.0.14, UDP port 65006
Sending 1470 byte datagrams
UDP buffer size:   122 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 36530 connected with 10.170.0.14 port 65006
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-10.0 sec    123 MBytes    103 Mbits/sec
[  3] Sent 87721 datagrams
[  3] Server Report:
[ ID] Interval       Transfer     Bandwidth       Jitter   Lost/Total Datagrams
[  3]  0.0-10.0 sec    114 MBytes  95.2 Mbits/sec  0.057 ms 6659/87721 (7.6%)
[garry@quartz ~]$ iperf -u -c 10.170.0.14 -b 102400000  -p 65006
------------------------------------------------------------
Client connecting to 10.170.0.14, UDP port 65006
Sending 1470 byte datagrams
UDP buffer size:   122 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 40484 connected with 10.170.0.14 port 65006
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-10.0 sec    123 MBytes    103 Mbits/sec
[  3] Sent 87721 datagrams
[  3] Server Report:
[ ID] Interval       Transfer     Bandwidth       Jitter   Lost/Total Datagrams
[  3]  0.0-10.2 sec    114 MBytes  92.9 Mbits/sec  14.640 ms 6753/87721 (7.7%)
[garry@quartz ~]$ iperf -u -c 10.170.0.14 -b 102400000  -p 65006 >> /home/garry/iperf-test.txt
[garry@quartz ~]$ iperf -u -c 10.170.0.14 -b 102400000  -p 65006 >> /home/garry/iperf-test.txt
[garry@quartz ~]$ iperf -u -c 10.170.0.14 -b 102400000  -p 65006 >> /home/garry/iperf-test.txt
[garry@quartz ~]$ cat /home/garry/iperf-test.txt
------------------------------------------------------------
Client connecting to 10.170.0.14, UDP port 65006
Sending 1470 byte datagrams
UDP buffer size:   122 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 45955 connected with 10.170.0.14 port 65006
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-10.0 sec    123 MBytes    103 Mbits/sec
[  3] Sent 87721 datagrams
[  3] Server Report:
[ ID] Interval       Transfer     Bandwidth       Jitter   Lost/Total Datagrams
[  3]  0.0-10.0 sec    114 MBytes  95.2 Mbits/sec  0.022 ms 6634/87721 (7.6%)
[  3]  0.0-10.0 sec  1 datagrams received out-of-order
------------------------------------------------------------
Client connecting to 10.170.0.14, UDP port 65006
Sending 1470 byte datagrams
UDP buffer size:   122 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 49298 connected with 10.170.0.14 port 65006
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-10.0 sec    123 MBytes    103 Mbits/sec
[  3] Sent 87721 datagrams
[  3] Server Report:
[ ID] Interval       Transfer     Bandwidth       Jitter   Lost/Total Datagrams
[  3]  0.0-21.0 sec    114 MBytes  45.5 Mbits/sec  0.040 ms 6621/87721 (7.5%)
[  3]  0.0-21.0 sec  3 datagrams received out-of-order
------------------------------------------------------------
Client connecting to 10.170.0.14, UDP port 65006
Sending 1470 byte datagrams
UDP buffer size:   122 KByte (default)
------------------------------------------------------------
[  3] local 10.192.10.230 port 34955 connected with 10.170.0.14 port 65006
[ ID] Interval       Transfer     Bandwidth
[  3]  0.0-10.0 sec    123 MBytes    103 Mbits/sec
[  3] Sent 87721 datagrams
[  3] Server Report:
[ ID] Interval       Transfer     Bandwidth       Jitter   Lost/Total Datagrams
[  3]  0.0-10.0 sec    114 MBytes  95.2 Mbits/sec  0.015 ms 6625/87721 (7.6%)
[  3]  0.0-10.0 sec  1 datagrams received out-of-order
