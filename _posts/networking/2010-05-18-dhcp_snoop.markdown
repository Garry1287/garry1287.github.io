---
layout: post
title:  "dhcp_snoop"
date:   2010-05-18 19:19:14 +0400
categories: Networking
tags: Networking
---

# dhcp_snoop
enable dhcp_local_relay  - без вланов рубит бродкаст запросы в dhcp серверу


Фильтр dhcp - серверов

config filter dhcp_server ports 1-24 state enable



Для каждого коммутатора


config address_binding ip_mac ports 1-24 state enable
config address_binding ip_mac ports 1-24 allow_zeroip enable 
config address_binding ip_mac ports 1-24 state enable strict 

enable address_binding dhcp_snoop
config address_binding dhcp_snoop max_entry ports 1-24 limit 2
config address_binding ip_mac ports 1-24 state enable strict allow_zeroip enable forward_dhcppkt enable 






disable address_binding dhcp_snoop
disable address_binding trap_log
^Mdisable address_binding arp_inspection
config address_binding ip_mac ports 1-28 state disable allow_zeroip disable forward_dhcppkt enable
^Mconfig address_binding ip_mac ports 1-28 mode arp stop_learning_threshold 500
config address_binding dhcp_snoop max_entry ports 1-28 limit 5




 match-hw-address

Класс в котором проверяется МАК-адрес, номер порта и номер влана

class "match_vlan_2236_port4_0:14:22:8d:ca:a6"
{
      match if (
        binary-to-ascii(10, 16, "",  substring(option agent.circuit-id, 2, 2)) = "2236"
        and binary-to-ascii(10, 16, "",  substring(option agent.circuit-id, 4, 2)) = "4"
        and binary-to-ascii(16,  8, ":", substring(hardware,                1, 6)) = "0:14:22:8d:ca:a6"
    );
}




 match-remote-id

Класс в котром проверяется номер влана, номер порта, МАК-адрес и ID коммутатора. В примере ID коммутатора совпадает с его IP хотя фактически - является просто строкой, и может принимать любые строковые значения.

class "match_vlan_2236_port2_0:14:22:8d:ca:a6_sw_172.29.14.122"
{
      match if (
        binary-to-ascii(10, 16, "",  substring(option agent.circuit-id, 2, 2)) = "2236"
        and binary-to-ascii(10, 16, "",  substring(option agent.circuit-id, 4, 2)) = "2"
        and binary-to-ascii(16,  8, ":", substring(hardware,                1, 6)) = "0:14:22:8d:ca:a6"
        and substring(option agent.remote-id, 2, 15) = "172.29.14.122"
    );
}


        pool {
            range 192.168.201.5;
            allow members of "match_vlan_2236_port2_0:14:22:8d:ca:a6_sw_172.29.14.122";
        }







 Логгирование

if exists agent.circuit-id
  {
  log(info, concat("Lease"
                   ," IP ",     binary-to-ascii(10,  8, ".", leased-address)
                   ," MAC ",    binary-to-ascii(16,  8, ":", substring(hardware,                1, 6))
                   ," switch ", substring(option agent.remote-id, 2, 15)
                   ," port ",   binary-to-ascii(10, 16, "",  substring(option agent.circuit-id, 4, 2))
                   ," VLAN ",   binary-to-ascii(10, 16, "",  substring(option agent.circuit-id, 2, 2))
                  )
     );
  }








config dhcp_relay add ipif System 172.16.0.1
config dhcp_relay option_82 state enable
config dhcp_relay option_82 policy replace
enable dhcp_relay 

enable address_binding dhcp_snoop 
config address_binding dhcp_snoop max_entry ports 1-6 limit 2
config address_binding ip_mac ports 1-24 state enable forward_dhcppkt enable allow_zeroip enable




config address_binding ip_mac ports 1-6 state enable
config address_binding ip_mac ports 1-6 allow_zeroip enable 
config address_binding ip_mac ports 1-6 state enable strict 


Jun 30 13:55:31 ruby dhcpd: DHCPDISCOVER from 00:aa:66:44:77:88 (iptech) via 172.20.140.1
Jun 30 13:55:32 ruby dhcpd: DHCPOFFER on 172.20.140.29 to 00:aa:66:44:77:88 (iptech) via 172.20.140.1
Jun 30 13:55:32 ruby dhcpd: DHCPREQUEST for 172.20.140.29 (81.20.192.6) from 00:aa:66:44:77:88 (iptech) via 172.20.140.1
Jun 30 13:55:32 ruby dhcpd: DHCPACK on 172.20.140.29 to 00:aa:66:44:77:88 (iptech) via 172.20.140.1




Jun 30 14:07:55 ruby dhcpd: DHCPDISCOVER from 00:aa:66:44:77:88 (iptech) via 172.20.140.1
Jun 30 14:07:55 ruby dhcpd: DHCPDISCOVER from 00:aa:66:44:77:88 via 192.168.113.201: network 192.168.113/24: no free leases
Jun 30 14:07:56 ruby dhcpd: DHCPOFFER on 172.20.140.29 to 00:aa:66:44:77:88 via 172.20.140.1
Jun 30 14:07:56 ruby dhcpd: DHCPREQUEST for 172.20.140.29 (81.20.192.6) from 00:aa:66:44:77:88 via 172.20.140.1
Jun 30 14:07:56 ruby dhcpd: DHCPACK on 172.20.140.29 to 00:aa:66:44:77:88 (iptech) via 172.20.140.1
Jun 30 14:07:56 ruby dhcpd: DHCPREQUEST for 172.20.140.29 (172.20.140.1) from 00:aa:66:44:77:88 (iptech) via 192.168.113.201: wrong network.
Jun 30 14:07:56 ruby dhcpd: DHCPNAK on 172.20.140.29 to 00:aa:66:44:77:88 via 192.168.113.201





Jun 30 14:51:28 ruby dhcpd: DHCPDISCOVER from 00:aa:66:44:77:88 (iptech) via 172.20.140.1
Jun 30 14:51:28 ruby dhcpd: DHCPOFFER on 172.20.140.29 to 00:aa:66:44:77:88 (iptech) via 172.20.140.1
Jun 30 14:51:29 ruby dhcpd: DHCPDISCOVER from 00:aa:66:44:77:88 via 192.168.113.201: network 192.168.113/24: no free leases
Jun 30 14:51:29 ruby dhcpd: DHCPREQUEST for 172.20.140.29 (172.20.140.1) from 00:aa:66:44:77:88 via 192.168.113.201: wrong network.








#500 DHCP test
subnet 172.20.140.0 netmask 255.255.255.224 {
        range 172.20.140.2 172.20.135.30;
        option subnet-mask 255.255.255.224;
        option domain-name "test_dhcp.home.loc";
        option broadcast-address 172.20.140.31;
        option routers 172.20.140.1;
        option domain-name-servers 81.20.192.16,81.20.195.33;
        option ms-classless-static-routes 32, 172, 31, 3, 1, 172, 20, 140, 1, 16, 172 ,20, 172, 20, 140, 1, 16, 172, 24, 172, 20, 140, 1, 19, 195, 34, 224, 172, 20, 140, 1, 20, 81, 20, 192, 172, 20, 140, 1, 18, 93, 180, 0, 172, 20, 140, 1, 12, 172, 16, 172, 20, 140, 1, 17, 95, 179, 0, 172, 20, 140, 1, 16, 10, 1, 172, 20, 140, 1, 32, 195, 191, 182, 2, 172, 20, 140, 1, 16, 178, 234, 172, 20, 140, 1;
        option rfc3442-classless-static-routes 32, 172, 31, 3, 1, 172, 20, 140, 1, 16, 172 ,20, 172, 20, 140, 1, 16, 172, 24, 172, 20, 140, 1, 19, 195, 34, 224, 172, 20, 140, 1, 20, 81, 20, 192, 172, 20, 140, 1, 18, 93, 180, 0, 172, 20, 140, 1, 12, 172, 16, 172, 20, 140, 1, 17, 95, 179, 0, 172, 20, 140, 1, 16, 10, 1, 172, 20, 140, 1, 32, 195, 191, 182, 2, 172, 20, 140, 1, 16, 178, 234, 172, 20, 140, 1;
}




00-1E-58-A3-61-65



class "match_vlan_500_port1_00:1E:58:A3:61:65_sw_192.168.113.201"
{
      match if (
        binary-to-ascii(10, 16, "",  substring(option agent.circuit-id, 2, 2)) = "500"
        and binary-to-ascii(10, 16, "",  substring(option agent.circuit-id, 4, 2)) = "1"
        and binary-to-ascii(16,  8, ":", substring(hardware,                1, 6)) = "00:1E:58:A3:61:65"
        and substring(option agent.remote-id, 2, 15) = "192.168.113.201"
    );
}


        pool {
            range 172.20.140.5;
            option subnet-mask 255.255.255.224;
            option domain-name "opt82_dhcp.home.loc";
            option broadcast-address 172.20.140.31;
            option routers 172.20.140.1;
            option domain-name-servers 81.20.192.16,81.20.195.33;
            option ms-classless-static-routes 32, 172, 31, 3, 1, 172, 20, 140, 1, 16, 172 ,20, 172, 20, 140, 1, 16, 172, 24, 172, 20, 140, 1, 19, 195, 34, 224, 172, 20, 140, 1, 20, 81, 20, 192, 172, 20, 140, 1, 18, 93, 180, 0, 172, 20, 140, 1, 12, 172, 16, 172, 20, 140, 1, 17, 95, 179, 0, 172, 20, 140, 1, 16, 10, 1, 172, 20, 140, 1, 32, 195, 191, 182, 2, 172, 20, 140, 1, 16, 178, 234, 172, 20, 140, 1;
            option rfc3442-classless-static-routes 32, 172, 31, 3, 1, 172, 20, 140, 1, 16, 172 ,20, 172, 20, 140, 1, 16, 172, 24, 172, 20, 140, 1, 19, 195, 34, 224, 172, 20, 140, 1, 20, 81, 20, 192, 172, 20, 140, 1, 18, 93, 180, 0, 172, 20, 140, 1, 12, 172, 16, 172, 20, 140, 1, 17, 95, 179, 0, 172, 20, 140, 1, 16, 10, 1, 172, 20, 140, 1, 32, 195, 191, 182, 2, 172, 20, 140, 1, 16, 178, 234, 172, 20, 140, 1;
            
        pool {
            range 172.20.140.5;
	    allow members of "match_vlan_500_port1_00:1E:58:A3:61:65_sw_192.168.113.201";
        }






и много много таких запросов




config address_binding ip_mac ports 1-24 state enable strict allow_zeroip enable forward_dhcppkt enable
config address_binding ip_mac ports 1-28 mode arp stop_learning_threshold 500
config address_binding dhcp_snoop max_entry ports 1-24 limit 2
config address_binding ip_mac ports 25-28 state disable allow_zeroip disable forward_dhcppkt enable
config address_binding dhcp_snoop max_entry ports 25-28 limit 5























Jun 16 11:19:03.256: DHCPD: Sending notification of DISCOVER:
Jun 16 11:19:03.256:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:03.256:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:03.256:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:03.256:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:03.256: DHCPD: Sending notification of DISCOVER:
Jun 16 11:19:03.256:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:03.256:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:03.256:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:03.256:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:03.256: DHCPD: there is no address pool for 192.168.120.105.
Jun 16 11:19:03.256: DHCPD: Sending notification of ASSIGNMENT FAILURE:
Jun 16 11:19:03.256:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:03.257:   DHCPD: remote id 020a00005114c0330200000d
Jun 16 11:19:03.257:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:03.257:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:03.257:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:03.257: DHCPD: Sending notification of ASSIGNMENT_FAILURE:
Jun 16 11:19:03.257:  DHCPD: due to: NO POOL
Jun 16 11:19:03.257:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:03.257:   DHCPD: remote id 020a00005114c0330200000d
Jun 16 11:19:03.257:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:03.257:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:03.257:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:03.257: DHCPD: Sending notification of DISCOVER:
Jun 16 11:19:03.257:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:03.257:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:03.257:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:03.257:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:03.257: DHCPD: Sending notification of DISCOVER:
Jun 16 11:19:03.257:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:03.257:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:03.257:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:03.257:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:03.257: DHCPD: there is no address pool for 192.168.120.105.
Jun 16 11:19:03.257: DHCPD: Sending notification of ASSIGNMENT FAILURE:
Jun 16 11:19:03.257:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:03.257:   DHCPD: remote id 020a00005114c0330200000d
Jun 16 11:19:03.257:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:03.257:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:03.257:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:03.257: DHCPD: Sending notification of ASSIGNMENT_FAILURE:
Jun 16 11:19:03.257:  DHCPD: due to: NO POOL
Jun 16 11:19:03.257:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:03.257:   DHCPD: remote id 020a00005114c0330200000d
Jun 16 11:19:03.257:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:03.257:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:03.257:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:07.255: DHCPD: Sending notification of DISCOVER:
Jun 16 11:19:07.255:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:07.255:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:07.255:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:07.255:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:07.255: DHCPD: Sending notification of DISCOVER:
Jun 16 11:19:07.255:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:07.255:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:07.255:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:07.255:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:07.255: DHCPD: there is no address pool for 192.168.120.105.
Jun 16 11:19:07.255: DHCPD: Sending notification of ASSIGNMENT FAILURE:
Jun 16 11:19:07.255:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:07.255:   DHCPD: remote id 020a00005114c0330200000d
Jun 16 11:19:07.255:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:07.255:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:07.255:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:07.255: DHCPD: Sending notification of ASSIGNMENT_FAILURE:
Jun 16 11:19:07.255:  DHCPD: due to: NO POOL
Jun 16 11:19:07.255:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:07.255:   DHCPD: remote id 020a00005114c0330200000d
Jun 16 11:19:07.255:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:07.255:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:07.255:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:07.256: DHCPD: Sending notification of DISCOVER:
Jun 16 11:19:07.256:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:07.256:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:07.256:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:07.256:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:07.256: DHCPD: Sending notification of DISCOVER:
Jun 16 11:19:07.256:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:07.256:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:07.256:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:07.256:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:07.256: DHCPD: there is no address pool for 192.168.120.105.
Jun 16 11:19:07.256: DHCPD: Sending notification of ASSIGNMENT FAILURE:
Jun 16 11:19:07.256:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:07.256:   DHCPD: remote id 020a00005114c0330200000d
Jun 16 11:19:07.256:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:07.256:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:07.256:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:07.256: DHCPD: Sending notification of ASSIGNMENT_FAILURE:
Jun 16 11:19:07.256:  DHCPD: due to: NO POOL
Jun 16 11:19:07.256:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:07.256:   DHCPD: remote id 020a00005114c0330200000d
Jun 16 11:19:07.256:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:07.256:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:07.256:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:14.255: DHCPD: Sending notification of DISCOVER:
Jun 16 11:19:14.255:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:14.255:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:14.255:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:14.255:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:14.255: DHCPD: Sending notification of DISCOVER:
Jun 16 11:19:14.255:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:14.255:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:14.255:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:14.255:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:14.255: DHCPD: there is no address pool for 192.168.120.105.
Jun 16 11:19:14.255: DHCPD: Sending notification of ASSIGNMENT FAILURE:
Jun 16 11:19:14.255:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:14.255:   DHCPD: remote id 020a00005114c0330200000d
Jun 16 11:19:14.255:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:14.255:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:14.255:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:14.255: DHCPD: Sending notification of ASSIGNMENT_FAILURE:
Jun 16 11:19:14.255:  DHCPD: due to: NO POOL
Jun 16 11:19:14.255:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:14.255:   DHCPD: remote id 020a00005114c0330200000d
Jun 16 11:19:14.255:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:14.255:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:14.255:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:14.256: DHCPD: Sending notification of DISCOVER:
Jun 16 11:19:14.256:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:14.256:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:14.256:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:14.256:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:14.256: DHCPD: Sending notification of DISCOVER:
Jun 16 11:19:14.256:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:14.256:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:14.256:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:14.256:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:14.256: DHCPD: there is no address pool for 192.168.120.105.
Jun 16 11:19:14.256: DHCPD: Sending notification of ASSIGNMENT FAILURE:
Jun 16 11:19:14.256:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:14.256:   DHCPD: remote id 020a00005114c0330200000d
Jun 16 11:19:14.256:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:14.256:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:14.256:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:14.256: DHCPD: Sending notification of ASSIGNMENT_FAILURE:
Jun 16 11:19:14.256:  DHCPD: due to: NO POOL
Jun 16 11:19:14.256:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:14.256:   DHCPD: remote id 020a00005114c0330200000d
Jun 16 11:19:14.256:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:14.256:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:14.256:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:30.257: DHCPD: Sending notification of DISCOVER:
Jun 16 11:19:30.257:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:30.257:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:30.257:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:30.257:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:30.257: DHCPD: Sending notification of DISCOVER:
Jun 16 11:19:30.257:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:30.257:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:30.257:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:30.257:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:30.257: DHCPD: there is no address pool for 192.168.120.105.
Jun 16 11:19:30.257: DHCPD: Sending notification of ASSIGNMENT FAILURE:
Jun 16 11:19:30.257:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:30.257:   DHCPD: remote id 020a00005114c0330200000d
Jun 16 11:19:30.257:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:30.257:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:30.257:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:30.257: DHCPD: Sending notification of ASSIGNMENT_FAILURE:
Jun 16 11:19:30.257:  DHCPD: due to: NO POOL
Jun 16 11:19:30.257:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:30.257:   DHCPD: remote id 020a00005114c0330200000d
Jun 16 11:19:30.257:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:30.257:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:30.257:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:30.258: DHCPD: Sending notification of DISCOVER:
Jun 16 11:19:30.258:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:30.258:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:30.258:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:30.258:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:30.259: DHCPD: Sending notification of DISCOVER:
Jun 16 11:19:30.259:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:30.259:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:30.259:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:30.259:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:30.259: DHCPD: there is no address pool for 192.168.120.105.
Jun 16 11:19:30.259: DHCPD: Sending notification of ASSIGNMENT FAILURE:
Jun 16 11:19:30.259:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:30.259:   DHCPD: remote id 020a00005114c0330200000d
Jun 16 11:19:30.259:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:30.259:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:30.259:   DHCPD: class id 4d53465420352e30
Jun 16 11:19:30.259: DHCPD: Sending notification of ASSIGNMENT_FAILURE:
Jun 16 11:19:30.259:  DHCPD: due to: NO POOL
Jun 16 11:19:30.259:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 16 11:19:30.259:   DHCPD: remote id 020a00005114c0330200000d
Jun 16 11:19:30.259:   DHCPD: giaddr = 192.168.120.105
Jun 16 11:19:30.259:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 16 11:19:30.259:   DHCPD: class id 4d53465420352e30



config dhcp_local_relay option_82 ports 1-24 policy replace
config dhcp_local_relay option_82 ports 25-26 policy keep




















Jun 17 06:11:51.015: DHCPD: input i/f override GigabitEthernet0/0/2.52 for client
Jun 17 06:11:51.015: DHCPD: Sending notification of DISCOVER:
Jun 17 06:11:51.015:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:11:51.015:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:11:51.015:   DHCPD: circuit id 000400340002
Jun 17 06:11:51.015:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:11:51.015:   DHCPD: class id 4d53465420352e30
Jun 17 06:11:51.016: DHCPD: Sending notification of DISCOVER:
Jun 17 06:11:51.016:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:11:51.016:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:11:51.016:   DHCPD: circuit id 000400340002
Jun 17 06:11:51.016:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:11:51.016:   DHCPD: class id 4d53465420352e30
Jun 17 06:11:51.025: DHCPD: Callback for workspace (ID=0x64000007)
Jun 17 06:11:51.025: DHCPD: No authentication required. Continue
Jun 17 06:11:51.025: DHCPD: Callback: class '' now specified for client 0100.1d60.d768.79
Jun 17 06:11:51.025: DHCPD: Sending notification of DISCOVER:
Jun 17 06:11:51.025:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:11:51.025:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:11:51.025:   DHCPD: circuit id 000400340002
Jun 17 06:11:51.025:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:11:51.025:   DHCPD: class id 4d53465420352e30
Jun 17 06:11:51.025: DHCPD: Removing previous server binding
Jun 17 06:11:51.025: DHCPD: Sending notification of TERMINATION:
Jun 17 06:11:51.025:  DHCPD: address 172.20.96.7 mask 255.255.224.0
Jun 17 06:11:51.025:  DHCPD: reason flags: noalloc 
Jun 17 06:11:51.025:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:11:51.025:   DHCPD: lease time remaining (secs) = 291
Jun 17 06:11:51.026: DHCPD: returned 172.20.96.7 to address pool private.
Jun 17 06:11:51.026: DHCPD: requested address 169.254.87.195 is not on subnet 172.20.96.0.
Jun 17 06:11:51.026: DHCPD: Adding binding to radix tree (172.20.96.8)
Jun 17 06:11:51.026: DHCPD: Adding binding to hash tree
Jun 17 06:11:51.027: DHCPD: assigned IP address 172.20.96.8 to client 0100.1d60.d768.79.
Jun 17 06:11:53.026: DHCPD: Sending notification of DISCOVER:
Jun 17 06:11:53.026:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:11:53.026:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:11:53.026:   DHCPD: circuit id 000400340002
Jun 17 06:11:53.026:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:11:53.027:   DHCPD: class id 4d53465420352e30
Jun 17 06:11:53.027: DHCPD: Found previous server binding
Jun 17 06:11:53.027: DHCPD: requested address 169.254.87.195 is not on subnet 172.20.96.0.
Jun 17 06:11:53.027: DHCPD: DHCPOFFER notify setup address 172.20.96.8 mask 255.255.224.0
Jun 17 06:11:53.047: DHCPD: Flagging binding 172.20.96.8 255.255.224.0 for force termination
Jun 17 06:11:55.001: DHCPD: input i/f override GigabitEthernet0/0/2.52 for client
Jun 17 06:11:55.001: DHCPD: Sending notification of DISCOVER:
Jun 17 06:11:55.001:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:11:55.001:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:11:55.001:   DHCPD: circuit id 000400340002
Jun 17 06:11:55.001:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:11:55.001:   DHCPD: class id 4d53465420352e30
Jun 17 06:11:55.001: DHCPD: Sending notification of DISCOVER:
Jun 17 06:11:55.001:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:11:55.001:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:11:55.001:   DHCPD: circuit id 000400340002
Jun 17 06:11:55.001:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:11:55.001:   DHCPD: class id 4d53465420352e30
Jun 17 06:11:55.011: DHCPD: Callback for workspace (ID=0xA7000008)
Jun 17 06:11:55.011: DHCPD: No authentication required. Continue
Jun 17 06:11:55.011: DHCPD: Callback: class '' now specified for client 0100.1d60.d768.79
Jun 17 06:11:55.011: DHCPD: Sending notification of DISCOVER:
Jun 17 06:11:55.011:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:11:55.011:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:11:55.011:   DHCPD: circuit id 000400340002
Jun 17 06:11:55.011:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:11:55.011:   DHCPD: class id 4d53465420352e30
Jun 17 06:11:55.011: DHCPD: Removing previous server binding
Jun 17 06:11:55.011: DHCPD: Sending notification of TERMINATION:
Jun 17 06:11:55.011:  DHCPD: address 172.20.96.8 mask 255.255.224.0
Jun 17 06:11:55.011:  DHCPD: reason flags: noalloc 
Jun 17 06:11:55.011:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:11:55.011:   DHCPD: lease time remaining (secs) = 298
Jun 17 06:11:55.012: DHCPD: returned 172.20.96.8 to address pool private.
Jun 17 06:11:55.012: DHCPD: requested address 169.254.87.195 is not on subnet 172.20.96.0.
Jun 17 06:11:55.012: DHCPD: Adding binding to radix tree (172.20.96.9)
Jun 17 06:11:55.012: DHCPD: Adding binding to hash tree
Jun 17 06:11:55.012: DHCPD: assigned IP address 172.20.96.9 to client 0100.1d60.d768.79.
Jun 17 06:11:57.011: DHCPD: Sending notification of DISCOVER:
Jun 17 06:11:57.011:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:11:57.011:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:11:57.011:   DHCPD: circuit id 000400340002
Jun 17 06:11:57.011:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:11:57.012:   DHCPD: class id 4d53465420352e30
Jun 17 06:11:57.012: DHCPD: Found previous server binding
Jun 17 06:11:57.012: DHCPD: requested address 169.254.87.195 is not on subnet 172.20.96.0.
Jun 17 06:11:57.012: DHCPD: DHCPOFFER notify setup address 172.20.96.9 mask 255.255.224.0
Jun 17 06:11:57.028: DHCPD: Flagging binding 172.20.96.9 255.255.224.0 for force termination
Jun 17 06:12:03.001: DHCPD: input i/f override GigabitEthernet0/0/2.52 for client
Jun 17 06:12:03.001: DHCPD: Sending notification of DISCOVER:
Jun 17 06:12:03.001:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:12:03.001:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:12:03.001:   DHCPD: circuit id 000400340002
Jun 17 06:12:03.001:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:12:03.001:   DHCPD: class id 4d53465420352e30
Jun 17 06:12:03.002: DHCPD: Sending notification of DISCOVER:
Jun 17 06:12:03.002:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:12:03.002:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:12:03.002:   DHCPD: circuit id 000400340002
Jun 17 06:12:03.002:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:12:03.002:   DHCPD: class id 4d53465420352e30
Jun 17 06:12:03.011: DHCPD: Callback for workspace (ID=0x98000009)
Jun 17 06:12:03.011: DHCPD: No authentication required. Continue
Jun 17 06:12:03.011: DHCPD: Callback: class '' now specified for client 0100.1d60.d768.79
Jun 17 06:12:03.011: DHCPD: Sending notification of DISCOVER:
Jun 17 06:12:03.011:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:12:03.011:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:12:03.011:   DHCPD: circuit id 000400340002
Jun 17 06:12:03.011:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:12:03.011:   DHCPD: class id 4d53465420352e30
Jun 17 06:12:03.011: DHCPD: Removing previous server binding
Jun 17 06:12:03.011: DHCPD: Sending notification of TERMINATION:
Jun 17 06:12:03.011:  DHCPD: address 172.20.96.9 mask 255.255.224.0
Jun 17 06:12:03.011:  DHCPD: reason flags: noalloc 
Jun 17 06:12:03.011:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:12:03.011:   DHCPD: lease time remaining (secs) = 294
Jun 17 06:12:03.012: DHCPD: returned 172.20.96.9 to address pool private.
Jun 17 06:12:03.012: DHCPD: requested address 169.254.87.195 is not on subnet 172.20.96.0.
Jun 17 06:12:03.013: DHCPD: Adding binding to radix tree (172.20.96.10)
Jun 17 06:12:03.013: DHCPD: Adding binding to hash tree
Jun 17 06:12:03.013: DHCPD: assigned IP address 172.20.96.10 to client 0100.1d60.d768.79.
Jun 17 06:12:05.012: DHCPD: Sending notification of DISCOVER:
Jun 17 06:12:05.012:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:12:05.012:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:12:05.012:   DHCPD: circuit id 000400340002
Jun 17 06:12:05.012:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:12:05.013:   DHCPD: class id 4d53465420352e30
Jun 17 06:12:05.013: DHCPD: Found previous server binding
Jun 17 06:12:05.013: DHCPD: requested address 169.254.87.195 is not on subnet 172.20.96.0.
Jun 17 06:12:05.013: DHCPD: DHCPOFFER notify setup address 172.20.96.10 mask 255.255.224.0
Jun 17 06:12:05.029: DHCPD: Flagging binding 172.20.96.10 255.255.224.0 for force termination
Jun 17 06:12:19.001: DHCPD: input i/f override GigabitEthernet0/0/2.52 for client
Jun 17 06:12:19.001: DHCPD: Sending notification of DISCOVER:
Jun 17 06:12:19.001:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:12:19.001:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:12:19.001:   DHCPD: circuit id 000400340002
Jun 17 06:12:19.001:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:12:19.001:   DHCPD: class id 4d53465420352e30
Jun 17 06:12:19.002: DHCPD: Sending notification of DISCOVER:
Jun 17 06:12:19.002:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:12:19.002:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:12:19.002:   DHCPD: circuit id 000400340002
Jun 17 06:12:19.002:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:12:19.002:   DHCPD: class id 4d53465420352e30
Jun 17 06:12:19.011: DHCPD: Callback for workspace (ID=0x5F00000A)
Jun 17 06:12:19.012: DHCPD: No authentication required. Continue
Jun 17 06:12:19.012: DHCPD: Callback: class '' now specified for client 0100.1d60.d768.79
Jun 17 06:12:19.012: DHCPD: Sending notification of DISCOVER:
Jun 17 06:12:19.012:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:12:19.012:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:12:19.012:   DHCPD: circuit id 000400340002
Jun 17 06:12:19.012:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:12:19.012:   DHCPD: class id 4d53465420352e30
Jun 17 06:12:19.012: DHCPD: Removing previous server binding
Jun 17 06:12:19.012: DHCPD: Sending notification of TERMINATION:
Jun 17 06:12:19.012:  DHCPD: address 172.20.96.10 mask 255.255.224.0
Jun 17 06:12:19.012:  DHCPD: reason flags: noalloc 
Jun 17 06:12:19.012:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:12:19.012:   DHCPD: lease time remaining (secs) = 286
Jun 17 06:12:19.013: DHCPD: returned 172.20.96.10 to address pool private.
Jun 17 06:12:19.013: DHCPD: requested address 169.254.87.195 is not on subnet 172.20.96.0.
Jun 17 06:12:19.013: DHCPD: Adding binding to radix tree (172.20.96.11)
Jun 17 06:12:19.013: DHCPD: Adding binding to hash tree
Jun 17 06:12:19.013: DHCPD: assigned IP address 172.20.96.11 to client 0100.1d60.d768.79.
Jun 17 06:12:21.012: DHCPD: Sending notification of DISCOVER:
Jun 17 06:12:21.012:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:12:21.012:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:12:21.012:   DHCPD: circuit id 000400340002
Jun 17 06:12:21.012:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:12:21.013:   DHCPD: class id 4d53465420352e30
Jun 17 06:12:21.013: DHCPD: Found previous server binding
Jun 17 06:12:21.013: DHCPD: requested address 169.254.87.195 is not on subnet 172.20.96.0.
Jun 17 06:12:21.013: DHCPD: DHCPOFFER notify setup address 172.20.96.11 mask 255.255.224.0
Jun 17 06:12:21.029: DHCPD: Flagging binding 172.20.96.11 255.255.224.0 for force termination
Jun 17 06:12:56.955: DHCPD: input i/f override GigabitEthernet0/0/2.52 for client
Jun 17 06:12:56.955: DHCPD: Sending notification of DISCOVER:
Jun 17 06:12:56.955:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:12:56.955:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:12:56.955:   DHCPD: circuit id 000400340002
Jun 17 06:12:56.955:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:12:56.955:   DHCPD: class id 4d53465420352e30
Jun 17 06:12:56.955: DHCPD: Sending notification of DISCOVER:
Jun 17 06:12:56.955:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:12:56.955:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:12:56.955:   DHCPD: circuit id 000400340002
Jun 17 06:12:56.955:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:12:56.955:   DHCPD: class id 4d53465420352e30
Jun 17 06:12:56.965: DHCPD: Callback for workspace (ID=0x9E00000B)
Jun 17 06:12:56.965: DHCPD: No authentication required. Continue
Jun 17 06:12:56.965: DHCPD: Callback: class '' now specified for client 0100.1d60.d768.79
Jun 17 06:12:56.965: DHCPD: Sending notification of DISCOVER:
Jun 17 06:12:56.965:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:12:56.965:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:12:56.965:   DHCPD: circuit id 000400340002
Jun 17 06:12:56.965:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:12:56.965:   DHCPD: class id 4d53465420352e30
Jun 17 06:12:56.965: DHCPD: Removing previous server binding
Jun 17 06:12:56.965: DHCPD: Sending notification of TERMINATION:
Jun 17 06:12:56.965:  DHCPD: address 172.20.96.11 mask 255.255.224.0
Jun 17 06:12:56.965:  DHCPD: reason flags: noalloc 
Jun 17 06:12:56.965:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:12:56.965:   DHCPD: lease time remaining (secs) = 265
Jun 17 06:12:56.966: DHCPD: returned 172.20.96.11 to address pool private.
Jun 17 06:12:56.966: DHCPD: requested address 169.254.87.195 is not on subnet 172.20.96.0.
Jun 17 06:12:56.967: DHCPD: Adding binding to radix tree (172.20.96.12)
Jun 17 06:12:56.967: DHCPD: Adding binding to hash tree
Jun 17 06:12:56.967: DHCPD: assigned IP address 172.20.96.12 to client 0100.1d60.d768.79.
Jun 17 06:12:58.966: DHCPD: Sending notification of DISCOVER:
Jun 17 06:12:58.966:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:12:58.966:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:12:58.966:   DHCPD: circuit id 000400340002
Jun 17 06:12:58.967:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:12:58.967:   DHCPD: class id 4d53465420352e30
Jun 17 06:12:58.967: DHCPD: Found previous server binding
Jun 17 06:12:58.967: DHCPD: requested address 169.254.87.195 is not on subnet 172.20.96.0.
Jun 17 06:12:58.967: DHCPD: DHCPOFFER notify setup address 172.20.96.12 mask 255.255.224.0
Jun 17 06:12:58.983: DHCPD: Flagging binding 172.20.96.12 255.255.224.0 for force termination
Jun 17 06:12:59.954: DHCPD: input i/f override GigabitEthernet0/0/2.52 for client
Jun 17 06:12:59.954: DHCPD: Sending notification of DISCOVER:
Jun 17 06:12:59.954:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:12:59.954:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:12:59.954:   DHCPD: circuit id 000400340002
Jun 17 06:12:59.954:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:12:59.954:   DHCPD: class id 4d53465420352e30
Jun 17 06:12:59.955: DHCPD: Sending notification of DISCOVER:
Jun 17 06:12:59.955:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:12:59.955:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:12:59.955:   DHCPD: circuit id 000400340002
Jun 17 06:12:59.955:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:12:59.955:   DHCPD: class id 4d53465420352e30
Jun 17 06:12:59.964: DHCPD: Callback for workspace (ID=0x9200000C)
Jun 17 06:12:59.964: DHCPD: No authentication required. Continue
Jun 17 06:12:59.964: DHCPD: Callback: class '' now specified for client 0100.1d60.d768.79
Jun 17 06:12:59.964: DHCPD: Sending notification of DISCOVER:
Jun 17 06:12:59.964:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:12:59.964:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:12:59.964:   DHCPD: circuit id 000400340002
Jun 17 06:12:59.964:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:12:59.964:   DHCPD: class id 4d53465420352e30
Jun 17 06:12:59.964: DHCPD: Removing previous server binding
Jun 17 06:12:59.964: DHCPD: Sending notification of TERMINATION:
Jun 17 06:12:59.964:  DHCPD: address 172.20.96.12 mask 255.255.224.0
Jun 17 06:12:59.964:  DHCPD: reason flags: noalloc 
Jun 17 06:12:59.964:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:12:59.964:   DHCPD: lease time remaining (secs) = 299
Jun 17 06:12:59.966: DHCPD: returned 172.20.96.12 to address pool private.
Jun 17 06:12:59.966: DHCPD: requested address 169.254.87.195 is not on subnet 172.20.96.0.
Jun 17 06:12:59.966: DHCPD: Adding binding to radix tree (172.20.96.13)
Jun 17 06:12:59.966: DHCPD: Adding binding to hash tree
Jun 17 06:12:59.966: DHCPD: assigned IP address 172.20.96.13 to client 0100.1d60.d768.79.
Jun 17 06:13:01.965: DHCPD: Sending notification of DISCOVER:
Jun 17 06:13:01.965:   DHCPD: htype 1 chaddr 001d.60d7.6879
Jun 17 06:13:01.965:   DHCPD: remote id 00061cbdb965fae0
Jun 17 06:13:01.965:   DHCPD: circuit id 000400340002
Jun 17 06:13:01.965:   DHCPD: interface = GigabitEthernet0/0/2.52
Jun 17 06:13:01.966:   DHCPD: class id 4d53465420352e30
Jun 17 06:13:01.966: DHCPD: Found previous server binding
Jun 17 06:13:01.966: DHCPD: requested address 169.254.87.195 is not on subnet 172.20.96.0.
Jun 17 06:13:01.966: DHCPD: DHCPOFFER notify setup address 172.20.96.13 mask 255.255.224.0
Jun 17 06:13:01.982: DHCPD: Flagging binding 172.20.96.13 255.255.224.0 for force termination





ip dhcp pool private
 network 172.20.96.0 255.255.224.0
 dns-server 81.20.192.16 
 default-router 172.20.96.1 
 lease 0 2




ip dhcp pool block
 network 10.90.0.0 255.255.224.0
 dns-server 81.20.192.16 
 default-router 10.90.0.1 


ip dhcp pool public
 network 81.20.199.240 255.255.255.248
 dns-server 81.20.192.16 
 default-router 81.20.199.241
 lease 0 0 5



iptables -t nat -A POSTROUTING -s 10.90.0.0/19  -d 81.20.192.9/32 -o vlan10 -j SNAT --to-source 81.20.198.190 
iptables -t nat -A POSTROUTING -s 10.90.0.0/19  -d 81.20.192.33/32 -o vlan10 -j SNAT --to-source 81.20.198.190 

-A forward_ext -d 10.90.0.0/19 -i vlan10 -o vlan1021 -m state --state RELATED,ESTABLISHED -j ACCEPT 
-A forward_ext -d 10.90.0.0/19 -i vlan10 -o vlan11 -m state --state RELATED,ESTABLISHED -j ACCEPT 
-A forward_ext -d 10.90.0.0/19 -i vlan10 -o eth0 -m state --state RELATED,ESTABLISHED -j ACCEPT 
-A forward_ext -d 10.90.0.0/19 -i vlan10 -o eth1 -m state --state RELATED,ESTABLISHED -j ACCEPT 


-A forward_int -s 10.90.0.0/19 -i vlan1021 -o vlan10 -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT 
-A forward_int -s 10.90.0.0/19 -i vlan11 -o vlan10 -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT 
-A forward_int -s 10.90.0.0/19 -i eth0 -o vlan10 -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT 
-A forward_int -s 10.90.0.0/19 -i eth1 -o vlan10 -m state --state NEW,RELATED,ESTABLISHED -j ACCEPT 



ip dhcp excluded-address 10.254.0.1

ip dhcp pool block
 network 10.254.0.0 255.255.224.0
 default-router 10.90.0.1 
 dns-server 81.20.192.16 
 lease 0 0 5


!         
interface Loopback1
 description #Pool Block Address
 ip address 10.254.0.1 255.255.224.0




interface GigabitEthernet0/0/2.195151
 encapsulation dot1Q 1951 second-dot1q 51
 ip unnumbered Loopback2
 service-policy type control ISG-CUSTOMERS-POLICY
 ip subscriber l2-connected
  initiator dhcp class-aware











Jun 17 10:35:06.069: DHCPD: checking for expired leases.
Jun 17 10:35:20.844: DHCPD: dhcpd_lookup_route: host = 172.20.96.9
Jun 17 10:35:20.844: DHCPD: dhcpd_lookup_route: index = 209
Jun 17 10:35:20.844: DHCPD: Binding output intf GigabitEthernet0/0/2.13 is updated to GigabitEthernet0/0/2.51
Jun 17 10:35:20.844: DHCPD: dhcpd_lookup_route: host = 172.20.96.9
Jun 17 10:35:20.844: DHCPD: dhcpd_lookup_route: index = 209
Jun 17 10:35:20.844:  DHCPD: Deleting existing route to host 172.20.96.9
Jun 17 10:35:20.844: DHCPD: dhcpd_delete_route: index = 209
Jun 17 10:35:20.845: DHCPD: dhcpd_create_and_hash_route: host = 172.20.96.9
Jun 17 10:35:20.845: DHCPD: dhcpd_create_and_hash_route index = 209
Jun 17 10:35:20.845: DHCPD: dhcpd_add_route: lease = 149 
Jun 17 10:35:20.845: DHCPD: input i/f override GigabitEthernet0/0/2.51 for client
Jun 17 10:35:20.845: DHCPD: Sending notification of ASSIGNMENT:
Jun 17 10:35:20.845:  DHCPD: address 172.20.96.9 mask 255.255.224.0
Jun 17 10:35:20.845:   DHCPD: htype 1 chaddr 00dd.fdfd.ca11
Jun 17 10:35:20.845:   DHCPD: remote id 00061cbdb965fb60
Jun 17 10:35:20.845:   DHCPD: circuit id 000400330001
Jun 17 10:35:20.845:   DHCPD: lease time remaining (secs) = 300
Jun 17 10:35:20.845:   DHCPD: interface = GigabitEthernet0/0/2.51
Jun 17 10:35:20.845: DHCPD: Updating DPM hdl in DHCP binding for 172.20.96.9 
Jun 17 10:35:20.845:  DHCPD: lease time = 300
Jun 17 10:35:20.845: DHCPD: dhcpd_lookup_route: host = 172.20.96.9
Jun 17 10:35:20.845: DHCPD: dhcpd_lookup_route: index = 209
Jun 17 10:35:20.845: DHCPD: unicast BOOTREPLY output i/f override GigabitEthernet0/0/2.51
Jun 17 10:35:20.849: DHCPD: dhcpd_lookup_route: host = 172.20.96.9
Jun 17 10:35:20.849: DHCPD: dhcpd_lookup_route: index = 209
Jun 17 10:35:20.849: DHCPD: Binding output intf GigabitEthernet0/0/2.51 is updated to GigabitEthernet0/0/2.13
Jun 17 10:35:20.849: DHCPD: dhcpd_lookup_route: host = 172.20.96.9
Jun 17 10:35:20.849: DHCPD: dhcpd_lookup_route: index = 209
Jun 17 10:35:20.849:  DHCPD: Deleting existing route to host 172.20.96.9
Jun 17 10:35:20.849: DHCPD: dhcpd_delete_route: index = 209
Jun 17 10:35:20.849: DHCPD: dhcpd_create_and_hash_route: host = 172.20.96.9
Jun 17 10:35:20.849: DHCPD: dhcpd_create_and_hash_route index = 209
Jun 17 10:35:20.849: DHCPD: dhcpd_add_route: lease = 300 
Jun 17 10:35:20.849: DHCPD: input i/f override GigabitEthernet0/0/2.13 for client
Jun 17 10:35:20.849: DHCPD: Sending notification of ASSIGNMENT:
Jun 17 10:35:20.849:  DHCPD: address 172.20.96.9 mask 255.255.224.0
Jun 17 10:35:20.849:   DHCPD: htype 1 chaddr 00dd.fdfd.ca11
Jun 17 10:35:20.849:   DHCPD: remote id 00061cbdb965fb60
Jun 17 10:35:20.849:   DHCPD: circuit id 000400330001
Jun 17 10:35:20.849:   DHCPD: lease time remaining (secs) = 300
Jun 17 10:35:20.849:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 17 10:35:20.850: DHCPD: Updating DPM hdl in DHCP binding for 172.20.96.9 
Jun 17 10:35:20.850: DHCPD: unicast BOOTREPLY output i/f override GigabitEthernet0/0/2.13
Jun 17 10:35:20.850: DHCPD: input i/f override GigabitEthernet0/0/2.13 for client
Jun 17 10:35:20.850: DHCPD: Sending notification of ASSIGNMENT:
Jun 17 10:35:20.850:  DHCPD: address 172.20.96.9 mask 255.255.224.0
Jun 17 10:35:20.850:   DHCPD: htype 1 chaddr 00dd.fdfd.ca11
Jun 17 10:35:20.850:   DHCPD: remote id 00061cbdb965fb60
Jun 17 10:35:20.850:   DHCPD: circuit id 000400330001
Jun 17 10:35:20.850:   DHCPD: lease time remaining (secs) = 300
Jun 17 10:35:20.850:   DHCPD: interface = GigabitEthernet0/0/2.13
Jun 17 10:35:20.850: DHCPD: Updating DPM hdl in DHCP binding for 172.20.96.9 
Jun 17 10:35:20.850: DHCPD: unicast BOOTREPLY output i/f override GigabitEthernet0/0/2.13




access-list 131 deny   udp any any eq bootps
access-list 131 permit   ip any any
access-list 131 deny   udp 10.0.16.0 0.0.3.255 any eq bootps
access-list 131 permit ip 172.28.16.0 0.0.3.255 any
access-list 131 permit ip 10.0.16.0 0.0.3.255 any
access-list 131 deny   ip any any









access-list 131 deny   udp any any eq bootps
access-list 131 permit ip any any

access-list 150 permit tcp 10.254.0.0 0.0.255.255 host 81.20.192.9 eq www
access-list 150 permit tcp 10.254.0.0 0.0.255.255 host 81.20.192.33 eq www
access-list 150 permit udp 10.254.0.0 0.0.255.255 host 81.20.192.16 eq 5
access-list 150 permit udp 10.254.0.0 0.0.255.255 host 81.20.192.17 eq www
access-list 150 deny ip 10.254.0.0 0.0.255.255 any
access-list 150 permit   ip any any





aaa group server radius ISG-RADIUS
 server 81.20.192.30 auth-port 1812 acct-port 1813

server 81.20.192.6

radius-server host 81.20.192.30 auth-port 1812 acct-port 1813 key 7 111D1C16031B050B557878

radius-server host 81.20.192.6 auth-port 1645 acct-port 1646 non-standard


dhcp_local_relay на dlink
access-list на dhcp















