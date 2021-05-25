---
layout: post
title:  "dhcp_gryazi-log"
date:   2018-01-23 13:41:06 +0300
categories: PSI
tags: PSI
---

# dhcp_gryazi-log
#484 Behteeva 10(2)
subnet 172.20.138.64 netmask 255.255.255.224 {
        range 172.20.138.66 172.20.138.94;
        option subnet-mask 255.255.255.224;
        option domain-name "Behteeva10_3.home.loc";
        option broadcast-address 172.20.138.95;
        option routers 172.20.138.65;
        option domain-name-servers 81.20.192.16,81.20.195.33;
        option ms-classless-static-routes 32, 172, 31, 3, 1, 172, 20, 137, 65, 16, 172 ,20, 172, 20, 137, 65, 16, 172, 24, 172, 20, 137, 65, 19, 195, 34, 224
, 172, 20, 137, 65, 20, 81, 20, 192, 172, 20, 137, 65, 18, 93, 180, 0, 172, 20, 137, 65, 12, 172, 16, 172, 20, 137, 65, 17, 95, 179, 0, 172, 20, 137, 65, 16,
 10, 1, 172, 20, 137, 65, 32, 195, 191, 182, 2, 172, 20, 137, 65, 16, 178, 234, 172, 20, 137, 65;
        option rfc3442-classless-static-routes 32, 172, 31, 3, 1, 172, 20, 137, 65, 16, 172 ,20, 172, 20, 137, 65, 16, 172, 24, 172, 20, 137, 65, 19, 195, 34
, 224, 172, 20, 137, 65, 20, 81, 20, 192, 172, 20, 137, 65, 18, 93, 180, 0, 172, 20, 137, 65, 12, 172, 16, 172, 20, 137, 65, 17, 95, 179, 0, 172, 20, 137, 65
, 16, 10, 1, 172, 20, 137, 65, 32, 195, 191, 182, 2, 172, 20, 137, 65, 16, 178, 234, 172, 20, 137, 65;
}


-A forward_int -s 10.0.16.0/22 -d 192.168.1.30/32 -i vlan10 -o ipip1 -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT 
-A forward_int -s 10.0.16.0/22 -i vlan10 -o ipip1 -j DROP





 -A PREROUTING -d 81.20.192.33/32 -p tcp -m tcp --dport 80 -j DNAT --to-destination 192.168.1.30:7780

billing.promsvyaz.ru has address 81.20.192.33





Dec  8 13:22:30 gryazy-gw1 dhcpd: DHCPOFFER on 172.28.16.2 to 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:22:47 gryazy-gw1 dhcpd: DHCPDISCOVER from 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:22:47 gryazy-gw1 dhcpd: DHCPOFFER on 172.28.16.2 to 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:23:23 gryazy-gw1 dhcpd: DHCPDISCOVER from 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:23:23 gryazy-gw1 dhcpd: DHCPOFFER on 172.28.16.2 to 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:23:23 gryazy-gw1 dhcpd: DHCPREQUEST for 172.28.16.2 (172.28.0.4) from 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:23:23 gryazy-gw1 dhcpd: DHCPACK on 172.28.16.2 to 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:24:39 gryazy-gw1 kernel: [1899866.164842] martian source 172.28.0.4 from 192.168.117.38, on dev ipip1
Dec  8 13:24:39 gryazy-gw1 kernel: [1899866.164847] ll header: 45:00:00:60:00:00:40:00:14:04:78:3f:51:14:c0:13:3e:21:9f:12:45:00:00:4c:92:8a:00:00:1d:11:29:28:c0:a8:75:26:ac:1c:00:04:00:7b:00:7b:00:38:11:99:0b:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:01:08:00:06:04:00:01:00:15:17:f1:10:35:ac:1c:00:00:00:15:17:f1:10:35:00:27:0d:e9:c3:c1:08:00:45:00:00:3c:c1:45:00:00:7e:01:fd:96:ac:1c:10:02:01:00:00:00
Dec  8 13:25:01 gryazy-gw1 /usr/sbin/cron[6188]: (root) CMD (/bin/ping 192.168.1.11 -c 1)















Dec  8 13:28:23 gryazy-gw1 dhcpd: DHCPREQUEST for 172.28.16.2 from 00:44:aa:77:11:22 (iptech) via vlan10
Dec  8 13:28:23 gryazy-gw1 dhcpd: DHCPACK on 172.28.16.2 to 00:44:aa:77:11:22 (iptech) via vlan10
Dec  8 13:30:01 gryazy-gw1 /usr/sbin/cron[6200]: (root) CMD (/bin/ping 192.168.1.11 -c 1)









Dec  8 13:33:23 gryazy-gw1 dhcpd: DHCPREQUEST for 172.28.16.2 from 00:44:aa:77:11:22 (iptech) via vlan10
Dec  8 13:33:23 gryazy-gw1 dhcpd: DHCPACK on 172.28.16.2 to 00:44:aa:77:11:22 (iptech) via vlan10
Dec  8 13:33:26 gryazy-gw1 dhcpd: DHCPREQUEST for 172.28.16.2 from 00:44:aa:77:11:22 (iptech) via vlan10
Dec  8 13:33:26 gryazy-gw1 dhcpd: DHCPACK on 172.28.16.2 to 00:44:aa:77:11:22 (iptech) via vlan10
Dec  8 13:35:01 gryazy-gw1 /usr/sbin/cron[6224]: (root) CMD (/bin/ping 192.168.1.11 -c 1)
Dec  8 13:35:58 gryazy-gw1 dhcpd: DHCPINFORM from 172.28.16.2 via 172.28.16.1
Dec  8 13:35:58 gryazy-gw1 dhcpd: DHCPACK to 172.28.16.2 (00:44:aa:77:11:22) via vlan10
Dec  8 13:36:01 gryazy-gw1 dhcpd: DHCPINFORM from 172.28.16.2 via 172.28.16.1
Dec  8 13:36:01 gryazy-gw1 dhcpd: DHCPACK to 172.28.16.2 (00:44:aa:77:11:22) via vlan10
Dec  8 13:36:39 gryazy-gw1 kernel: [1900586.185577] martian source 172.28.0.4 from 192.168.117.38, on dev ipip1
Dec  8 13:36:39 gryazy-gw1 kernel: [1900586.185582] ll header: 45:00:00:60:00:00:40:00:14:04:78:3f:51:14:c0:13:3e:21:9f:12:45:00:00:4c:92:8e:00:00:1d:11:29:24:c0:a8:75:26:ac:1c:00:04:00:7b:00:7b:00:38:11:99:0b:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:0d:e9:c3:c8:00:15:17:f1:10:35:08:00:45:00:00:50:00:00:40:00:1d:04:6f:4f:3e:21:9f:12:51:14:c0:13:45:00:00:3c:7b:99:00:00:1d:01:b4:16:ac:1c:00:2b:01:00:00:00
Dec  8 13:37:15 gryazy-gw1 dhcpd: DHCPREQUEST for 172.28.16.2 from 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:37:15 gryazy-gw1 dhcpd: DHCPACK on 172.28.16.2 to 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:37:57 gryazy-gw1 dhcpd: DHCPREQUEST for 172.28.16.2 from 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:37:57 gryazy-gw1 dhcpd: DHCPACK on 172.28.16.2 to 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:38:01 gryazy-gw1 dhcpd: DHCPREQUEST for 172.28.16.2 from 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:38:01 gryazy-gw1 dhcpd: DHCPACK on 172.28.16.2 to 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:38:08 gryazy-gw1 dhcpd: DHCPREQUEST for 172.28.16.2 from 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:38:08 gryazy-gw1 dhcpd: DHCPACK on 172.28.16.2 to 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:38:24 gryazy-gw1 dhcpd: DHCPDISCOVER from 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:38:24 gryazy-gw1 dhcpd: DHCPOFFER on 172.28.16.2 to 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:38:27 gryazy-gw1 dhcpd: DHCPDISCOVER from 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:38:27 gryazy-gw1 dhcpd: DHCPOFFER on 172.28.16.2 to 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:38:35 gryazy-gw1 dhcpd: DHCPDISCOVER from 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:38:35 gryazy-gw1 dhcpd: DHCPOFFER on 172.28.16.2 to 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:38:50 gryazy-gw1 dhcpd: DHCPDISCOVER from 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:38:50 gryazy-gw1 dhcpd: DHCPOFFER on 172.28.16.2 to 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:39:27 gryazy-gw1 dhcpd: DHCPDISCOVER from 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:39:27 gryazy-gw1 dhcpd: DHCPOFFER on 172.28.16.2 to 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:39:27 gryazy-gw1 dhcpd: DHCPREQUEST for 172.28.16.2 (172.28.0.4) from 00:44:aa:77:11:22 (iptech) via 172.28.16.1
Dec  8 13:39:27 gryazy-gw1 dhcpd: DHCPACK on 172.28.16.2 to 00:44:aa:77:11:22 (iptech) via 172.28.16.1
