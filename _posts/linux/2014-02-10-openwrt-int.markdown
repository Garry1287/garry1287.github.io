---
layout: post
title:  "openwrt-int"
date:   2014-02-10 13:41:24 +0400
categories: linux
tags: linux
---

# openwrt-int
config interface 'loopback'
        option ifname 'lo'
        option proto 'static'
        option ipaddr '127.0.0.1'
        option netmask '255.0.0.0'

config globals 'globals'
        option ula_prefix 'fd86:fc02:d1b9::/48'

config interface 'lan'
        option ifname 'eth0.1'
        option force_link '1'
        option type 'bridge'
        option proto 'static'
        option netmask '255.255.255.0'
        option ip6assign '60'
        option ipaddr '192.168.0.1'

config interface 'wan'
        option ifname 'eth0.2'
        option _orig_ifname 'eth0.2'
        option _orig_bridge 'false'
        option proto 'pppoe'
        option username '72390-1060'
        option password '27FsROx3'

config interface 'wan6'
        option ifname 'eth0.2'
        option proto 'dhcpv6'

config switch
        option name 'switch0'
        option reset '1'
        option enable_vlan '1'

config switch_vlan
        option device 'switch0'
        option vlan '1'
        option ports '1 2 3 4 5t'

config switch_vlan
        option device 'switch0'
        option vlan '2'
        option ports '0 5t'

config interface 'VPN'
        option proto 'none'
        option ifname 'tun0'









br-lan    Link encap:Ethernet  HWaddr 64:70:02:A1:CA:5E  
          inet addr:192.168.0.1  Bcast:192.168.0.255  Mask:255.255.255.0
          inet6 addr: fd86:fc02:d1b9::1/60 Scope:Global
          inet6 addr: fe80::6670:2ff:fea1:ca5e/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:69111621 errors:0 dropped:0 overruns:0 frame:0
          TX packets:120234313 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:5552695328 (5.1 GiB)  TX bytes:166904846307 (155.4 GiB)

eth0      Link encap:Ethernet  HWaddr 64:70:02:A1:CA:5E  
          inet6 addr: fe80::6670:2ff:fea1:ca5e/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:128722070 errors:0 dropped:7 overruns:113 frame:0
          TX packets:76345578 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:1669099693 (1.5 GiB)  TX bytes:3888203843 (3.6 GiB)
          Interrupt:4 

eth0.1    Link encap:Ethernet  HWaddr 64:70:02:A1:CA:5E  
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:444784 errors:0 dropped:0 overruns:0 frame:0
          TX packets:1721337 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:241349625 (230.1 MiB)  TX bytes:572021703 (545.5 MiB)

eth0.2    Link encap:Ethernet  HWaddr 64:70:02:A1:CA:5E  
          inet6 addr: fe80::6670:2ff:fea1:ca5e/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:128277278 errors:0 dropped:2811743 overruns:0 frame:0
          TX packets:74685297 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:166614476969 (155.1 GiB)  TX bytes:7310835416 (6.8 GiB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:28826 errors:0 dropped:0 overruns:0 frame:0
          TX packets:28826 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:1840794 (1.7 MiB)  TX bytes:1840794 (1.7 MiB)

pppoe-wan Link encap:Point-to-Point Protocol  
          inet addr:178.234.51.63  P-t-P:178.234.48.1  Mask:255.255.255.255
          UP POINTOPOINT RUNNING NOARP MULTICAST  MTU:1480  Metric:1
          RX packets:223 errors:0 dropped:0 overruns:0 frame:0
          TX packets:241 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:3 
          RX bytes:28916 (28.2 KiB)  TX bytes:29775 (29.0 KiB)

tun0      Link encap:UNSPEC  HWaddr 00-00-00-00-00-00-00-00-00-00-00-00-00-00-00-00  
          inet addr:192.168.132.50  P-t-P:192.168.132.49  Mask:255.255.255.255
          UP POINTOPOINT RUNNING NOARP MULTICAST  MTU:1500  Metric:1
          RX packets:1870 errors:0 dropped:0 overruns:0 frame:0
          TX packets:2747 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:100 
          RX bytes:423279 (413.3 KiB)  TX bytes:200337 (195.6 KiB)

wlan0     Link encap:Ethernet  HWaddr 64:70:02:A1:CA:5E  
          inet6 addr: fe80::6670:2ff:fea1:ca5e/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:69144049 errors:0 dropped:0 overruns:0 frame:0
          TX packets:121029148 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:2282848576 (2.1 GiB)  TX bytes:1458797128 (1.3 GiB)


root@Dz-router:/etc/config# brctl show
bridge name     bridge id               STP enabled     interfaces
br-lan          7fff.647002a1ca5e       no              eth0.1
                                                                             wlan0

[http://wiki.openwrt.org/ru/doc/uci/network/switch](http://wiki.openwrt.org/ru/doc/uci/network/switch)
[https://habrahabr.ru/post/128451/](https://habrahabr.ru/post/128451/)


--------------------------------------------------------------------------------
                                                                               
eth0(для подключения программного комммутатора) - фактически представляет из себя все ethernet порты роутера
wlan0 (для wifi)                           
     br0(создаётся из eth0.1 и wlan0) для локалки   -  eth0.1 - влан 1
    eth0.2 (2 влан) создан для wan                         
            
            Порты роутера (лановские и wan порт) представлены как программый
            свитч, который подключен и openwrt через eth0  
            
           Можно настроить каждый физический порт как eth интерфейс, просто это
           нахер не нужно    (потом собирать их в бридж, плюс сложности запихивания портов в один влан)    
           
           
           Настройка свитча
           У свитча 6 портов - 0-5, 0 - это wan, 1-4 - lan порты, 5 - порт, программный, который подключен к eth0
           0 порт (wan) мы помещаем во 2 влан
           1-4 в 1 влан
           5 - тегированный
           
        в eth0 приходит 2 влана, на интерфейсе со вторым вланом eth0.2 поднимаем pppoe (можно сделать любое подключение)
        поэтому существует интерфейс pppoe-wan
        tun0 - интерфейс для openvp
        Фактически на порту 1194 pppoe интерфейса работает openvpn, который расшифровывает трафик и отправляет его на особый интерфейс (программные сетевые устройства) tun0 (L3). И уже с tun0 данными обменивается конкретный процесс.
        
Для firewall соответственно имеет смысл рассматривать следующие интерфейсы
br-lan   - порт локалки
pppoe-wan и eth0.2 - wan порты
tun0 - порт для vpn траффика (пропускать всё, что получаем из конторы)




nat
raw
mangle
filter


root@Dz-router:/etc/config# iptables-save
# Generated by iptables-save v1.4.21 on Wed May 17 23:56:18 2017
*nat
:PREROUTING ACCEPT [3004:151195]
:INPUT ACCEPT [1394:63928]
:OUTPUT ACCEPT [308:19208]
:POSTROUTING ACCEPT [0:0]
:delegate_postrouting - [0:0]
:delegate_prerouting - [0:0]
:postrouting_lan_rule - [0:0]
:postrouting_openvpn_rule - [0:0]
:postrouting_rule - [0:0]
:postrouting_wan_rule - [0:0]
:prerouting_lan_rule - [0:0]
:prerouting_openvpn_rule - [0:0]
:prerouting_rule - [0:0]
:prerouting_wan_rule - [0:0]
:zone_lan_postrouting - [0:0]
:zone_lan_prerouting - [0:0]
:zone_openvpn_postrouting - [0:0]
:zone_openvpn_prerouting - [0:0]
:zone_wan_postrouting - [0:0]
:zone_wan_prerouting - [0:0]
-A PREROUTING -j delegate_prerouting
-A POSTROUTING -o tun0 -j MASQUERADE                                                        !!!!!!!!!!!!!!!             рабочее правило
-A POSTROUTING -j delegate_postrouting
-A delegate_postrouting -m comment --comment "user chain for postrouting" -j postrouting_rule
-A delegate_postrouting -o br-lan -j zone_lan_postrouting                                                       !!!!!!!!
-A delegate_postrouting -o pppoe-wan -j zone_wan_postrouting                                            !!!!!!!!
-A delegate_postrouting -o eth0.2 -j zone_wan_postrouting                                                   !!!!!!!!
-A delegate_postrouting -o tun0 -j zone_openvpn_postrouting                                             !!!!!!!
-A delegate_prerouting -m comment --comment "user chain for prerouting" -j prerouting_rule
-A delegate_prerouting -i br-lan -j zone_lan_prerouting                                                             !!!!!!!!
-A delegate_prerouting -i pppoe-wan -j zone_wan_prerouting                                                  !!!!
-A delegate_prerouting -i eth0.2 -j zone_wan_prerouting                                                             !!!!!!!
-A delegate_prerouting -i tun0 -j zone_openvpn_prerouting                                                           !!!!!
-A zone_lan_postrouting -m comment --comment "user chain for postrouting" -j postrouting_lan_rule
-A zone_lan_prerouting -m comment --comment "user chain for prerouting" -j prerouting_lan_rule
-A zone_openvpn_postrouting -m comment --comment "user chain for postrouting" -j postrouting_openvpn_rule
-A zone_openvpn_prerouting -m comment --comment "user chain for prerouting" -j prerouting_openvpn_rule
-A zone_wan_postrouting -m comment --comment "user chain for postrouting" -j postrouting_wan_rule
-A zone_wan_postrouting -j MASQUERADE                                                                                                                                       !!!!!!!!!!!!!!!!!!!!!!!   рабочее правило
-A zone_wan_prerouting -m comment --comment "user chain for prerouting" -j prerouting_wan_rule
COMMIT
# Completed on Wed May 17 23:56:18 2017
# Generated by iptables-save v1.4.21 on Wed May 17 23:56:18 2017
*raw
:PREROUTING ACCEPT [116940:82587195]
:OUTPUT ACCEPT [6167:1263994]
:delegate_notrack - [0:0]
-A PREROUTING -j delegate_notrack
COMMIT
# Completed on Wed May 17 23:56:18 2017
# Generated by iptables-save v1.4.21 on Wed May 17 23:56:18 2017
*mangle
:PREROUTING ACCEPT [116940:82587195]
:INPUT ACCEPT [7296:605865]
:FORWARD ACCEPT [109584:81975990]
:OUTPUT ACCEPT [6167:1263994]
:POSTROUTING ACCEPT [115751:83239984]
:fwmark - [0:0]
:mssfix - [0:0]
-A PREROUTING -j fwmark
-A FORWARD -j mssfix
-A mssfix -o pppoe-wan -p tcp -m tcp --tcp-flags SYN,RST SYN -m comment --comment "wan (mtu_fix)" -j TCPMSS --clamp-mss-to-pmtu
-A mssfix -o eth0.2 -p tcp -m tcp --tcp-flags SYN,RST SYN -m comment --comment "wan (mtu_fix)" -j TCPMSS --clamp-mss-to-pmtu
COMMIT
# Completed on Wed May 17 23:56:18 2017
# Generated by iptables-save v1.4.21 on Wed May 17 23:56:18 2017
*filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
:delegate_forward - [0:0]
:delegate_input - [0:0]
:delegate_output - [0:0]
:forwarding_lan_rule - [0:0]
:forwarding_openvpn_rule - [0:0]
:forwarding_rule - [0:0]
:forwarding_wan_rule - [0:0]
:input_lan_rule - [0:0]
:input_openvpn_rule - [0:0]
:input_rule - [0:0]
:input_wan_rule - [0:0]
:output_lan_rule - [0:0]
:output_openvpn_rule - [0:0]
:output_rule - [0:0]
:output_wan_rule - [0:0]
:reject - [0:0]
:syn_flood - [0:0]
:zone_lan_dest_ACCEPT - [0:0]
:zone_lan_forward - [0:0]
:zone_lan_input - [0:0]
:zone_lan_output - [0:0]
:zone_lan_src_ACCEPT - [0:0]
:zone_openvpn_dest_ACCEPT - [0:0]
:zone_openvpn_forward - [0:0]
:zone_openvpn_input - [0:0]
:zone_openvpn_output - [0:0]
:zone_openvpn_src_ACCEPT - [0:0]
:zone_wan_dest_ACCEPT - [0:0]
:zone_wan_dest_REJECT - [0:0]
:zone_wan_forward - [0:0]
:zone_wan_input - [0:0]
:zone_wan_output - [0:0]
:zone_wan_src_REJECT - [0:0]

Вот такая цепочка
INPUT  - delegate_input - zone_lan_input (ACCEPT 2222) - zone_lan_src_ACCEPT   --------- -A zone_lan_src_ACCEPT -i br-lan -j ACCEPT


-A INPUT -i tun0 -p tcp -m tcp --dport 2222 -j ACCEPT                                                                               !!!!!!!!!!!!!!! рабочее правило
-A INPUT -i tun0 -p tcp -m tcp --dport 80 -j ACCEPT                                                                                     !!!!!!!!!!   рабочее правило   
-A INPUT -j delegate_input
-A FORWARD -j delegate_forward
-A OUTPUT -j delegate_output

-A delegate_forward -m comment --comment "user chain for forwarding" -j forwarding_rule
-A delegate_forward -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A delegate_forward -i br-lan -j zone_lan_forward
-A delegate_forward -i pppoe-wan -j zone_wan_forward
-A delegate_forward -i eth0.2 -j zone_wan_forward
-A delegate_forward -i tun0 -j zone_openvpn_forward

-A delegate_input -i lo -j ACCEPT
-A delegate_input -m comment --comment "user chain for input" -j input_rule
-A delegate_input -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A delegate_input -p tcp -m tcp --tcp-flags FIN,SYN,RST,ACK SYN -j syn_flood
-A delegate_input -i br-lan -j zone_lan_input
-A delegate_input -i pppoe-wan -j zone_wan_input
-A delegate_input -i eth0.2 -j zone_wan_input
-A delegate_input -i tun0 -j zone_openvpn_input


-A delegate_output -o lo -j ACCEPT
-A delegate_output -m comment --comment "user chain for output" -j output_rule
-A delegate_output -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A delegate_output -o br-lan -j zone_lan_output
-A delegate_output -o pppoe-wan -j zone_wan_output
-A delegate_output -o eth0.2 -j zone_wan_output
-A delegate_output -o tun0 -j zone_openvpn_output

-A reject -p tcp -j REJECT --reject-with tcp-reset                                                                                                          !!!!!!!!!!!!!!!!!!!вспом правила
-A reject -j REJECT --reject-with icmp-port-unreachable                                                                                                !!!!!!!!!!!!!! 

-A syn_flood -p tcp -m tcp --tcp-flags FIN,SYN,RST,ACK SYN -m limit --limit 25/sec --limit-burst 50 -j RETURN          !!!!!!!!!!!
-A syn_flood -j DROP                                                                                                                                                                        !!!!!!!!!!!  вспом правила            

-A zone_lan_forward -m comment --comment "user chain for forwarding" -j forwarding_lan_rule
-A zone_lan_forward -m comment --comment "forwarding lan -> wan" -j zone_wan_dest_ACCEPT
-A zone_lan_forward -m comment --comment "forwarding lan -> openvpn" -j zone_openvpn_dest_ACCEPT
-A zone_lan_forward -m conntrack --ctstate DNAT -m comment --comment "Accept port forwards" -j ACCEPT                       !!!!!!!!!!!!!!!!!!!!!!!!!! Проброс порта

-A zone_lan_forward -j zone_lan_dest_ACCEPT

-A zone_lan_input -m comment --comment "user chain for input" -j input_lan_rule
-A zone_lan_input -p tcp -m tcp --dport 2222 -m comment --comment Allow-ssh -j ACCEPT                                                             !!!!!!!!!!!!!!!!! Все, что с лана, разрешаем 2222 порт  
-A zone_lan_input -m conntrack --ctstate DNAT -m comment --comment "Accept port redirections" -j ACCEPT
-A zone_lan_input -j zone_lan_src_ACCEPT


-A zone_lan_output -m comment --comment "user chain for output" -j output_lan_rule
-A zone_lan_output -j zone_lan_dest_ACCEPT


-A zone_lan_src_ACCEPT -i br-lan -j ACCEPT

-A zone_openvpn_dest_ACCEPT -o tun0 -j ACCEPT


-A zone_openvpn_forward -m comment --comment "user chain for forwarding" -j forwarding_openvpn_rule
-A zone_openvpn_forward -m comment --comment "forwarding openvpn -> lan" -j zone_lan_dest_ACCEPT
-A zone_openvpn_forward -m conntrack --ctstate DNAT -m comment --comment "Accept port forwards" -j ACCEPT
-A zone_openvpn_forward -j zone_openvpn_dest_ACCEPT

-A zone_openvpn_input -m comment --comment "user chain for input" -j input_openvpn_rule
-A zone_openvpn_input -m conntrack --ctstate DNAT -m comment --comment "Accept port redirections" -j ACCEPT
-A zone_openvpn_input -j zone_openvpn_src_ACCEPT

-A zone_openvpn_output -m comment --comment "user chain for output" -j output_openvpn_rule
-A zone_openvpn_output -j zone_openvpn_dest_ACCEPT

-A zone_openvpn_src_ACCEPT -i tun0 -j ACCEPT

-A zone_wan_dest_ACCEPT -o pppoe-wan -j ACCEPT
-A zone_wan_dest_ACCEPT -o eth0.2 -j ACCEPT
-A zone_wan_dest_REJECT -o pppoe-wan -j reject
-A zone_wan_dest_REJECT -o eth0.2 -j reject

-A zone_wan_forward -m comment --comment "user chain for forwarding" -j forwarding_wan_rule
-A zone_wan_forward -p esp -m comment --comment "@rule[7]" -j zone_lan_dest_ACCEPT
-A zone_wan_forward -p udp -m udp --dport 500 -m comment --comment "@rule[8]" -j zone_lan_dest_ACCEPT
-A zone_wan_forward -m conntrack --ctstate DNAT -m comment --comment "Accept port forwards" -j ACCEPT
-A zone_wan_forward -j zone_wan_dest_REJECT

-A zone_wan_input -m comment --comment "user chain for input" -j input_wan_rule
-A zone_wan_input -p udp -m udp --dport 68 -m comment --comment Allow-DHCP-Renew -j ACCEPT
-A zone_wan_input -p icmp -m icmp --icmp-type 8 -m comment --comment Allow-Ping -j ACCEPT
-A zone_wan_input -p igmp -m comment --comment Allow-IGMP -j ACCEPT
-A zone_wan_input -m conntrack --ctstate DNAT -m comment --comment "Accept port redirections" -j ACCEPT
-A zone_wan_input -j zone_wan_src_REJECT

-A zone_wan_output -m comment --comment "user chain for output" -j output_wan_rule
-A zone_wan_output -j zone_wan_dest_ACCEPT

-A zone_wan_src_REJECT -i pppoe-wan -j reject
-A zone_wan_src_REJECT -i eth0.2 -j reject
COMMIT
# Completed on Wed May 17 23:56:22 2017
