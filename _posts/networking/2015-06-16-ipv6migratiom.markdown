---
layout: post
title:  "ipv6migratiom"
date:   2015-06-16 10:31:30 +0300
categories: Networking
tags: Networking
---

# ipv6migratiom
[http://www.itcertnotes.com/2011/02/network-address-translation-protocol.html](http://www.itcertnotes.com/2011/02/network-address-translation-protocol.html)
[http://habrahabr.ru/post/159775/](http://habrahabr.ru/post/159775/)
[http://habrahabr.ru/post/169829/](http://habrahabr.ru/post/169829/)

[http://ipv6go.ru/](http://ipv6go.ru/)

[http://www.ashep.org/2011/bystryj-kurs-ipv6-v-linux/#.UXZGkVKPaYQ](http://www.ashep.org/2011/bystryj-kurs-ipv6-v-linux/#.UXZGkVKPaYQ)

[http://www.ixbt.com/soft/ipv6.shtml](http://www.ixbt.com/soft/ipv6.shtml)
[http://blog.ipv6go.ru/post/38704476718/ipv6](http://blog.ipv6go.ru/post/38704476718/ipv6)

[https://www.ipv6ready.org/](https://www.ipv6ready.org/)
[http://www.ipv6forum.com/](http://www.ipv6forum.com/)

[http://www.ripe.net/lir-services/training/material/IPv6-for-LIRs-Training-Course/IPv6_addr_plan4.pdf](http://www.ripe.net/lir-services/training/material/IPv6-for-LIRs-Training-Course/IPv6_addr_plan4.pdf)



[http://version6.ru/](http://version6.ru/)
[http://habrahabr.ru/post/169829/](http://habrahabr.ru/post/169829/)










[http://forum.nag.ru/forum/index.php?showtopic=76712](http://forum.nag.ru/forum/index.php?showtopic=76712)
[http://xgu.ru/wiki/IPv6](http://xgu.ru/wiki/IPv6)
[http://book.itep.ru/4/44/ip6_4411.htm](http://book.itep.ru/4/44/ip6_4411.htm)
[http://ru.wikipedia.org/wiki/IPv6_Rapid_Deployment](http://ru.wikipedia.org/wiki/IPv6_Rapid_Deployment)
[http://habrahabr.ru/post/119968/](http://habrahabr.ru/post/119968/)
[http://ru.wikipedia.org/wiki/%D0%9F%D0%B0%D0%BA%D0%B5%D1%82_IPv6](http://ru.wikipedia.org/wiki/%D0%9F%D0%B0%D0%BA%D0%B5%D1%82_IPv6)
[http://habrahabr.ru/post/245935/](http://habrahabr.ru/post/245935/)


[https://habrahabr.ru/post/245047/](https://habrahabr.ru/post/245047/)


Для начала
[https://habrahabr.ru/post/64592/](https://habrahabr.ru/post/64592/)
[https://habrahabr.ru/post/210100/](https://habrahabr.ru/post/210100/)
[https://habrahabr.ru/post/253803/](https://habrahabr.ru/post/253803/)

ospf, bgp параллельно

ipv6 for Linux
[http://www.tldp.org/HOWTO/pdf/Linux+IPv6-HOWTO.pdf](http://www.tldp.org/HOWTO/pdf/Linux+IPv6-HOWTO.pdf)

ospf v6
[http://www.omnisecu.com/cisco-certified-network-associate-ccna/how-to-configure-ospfv3-ipv6-routing-in-cisco-routers.php](http://www.omnisecu.com/cisco-certified-network-associate-ccna/how-to-configure-ospfv3-ipv6-routing-in-cisco-routers.php)

 Поднимаем упрощенную провайдерскую сеть дома 
 [https://habrahabr.ru/post/245047/](https://habrahabr.ru/post/245047/)
 
  IPv6 в Cisco или будущее уже рядом (Часть 2) 
 [https://habrahabr.ru/post/223523/](https://habrahabr.ru/post/223523/)
 
 Плавный переход сети компании на IPv6
 [https://habrahabr.ru/post/119968/](https://habrahabr.ru/post/119968/)
 
 
 Все технологии туннелирования IPv6 понятным языком
 [https://habrahabr.ru/post/207562/](https://habrahabr.ru/post/207562/)
 
 Распределение адресного пространства IPv6 для ISP
 [https://habrahabr.ru/post/169829/](https://habrahabr.ru/post/169829/)
 
 IPv6-адреса через EUI-64: Точки над i
 [https://habrahabr.ru/post/245323/](https://habrahabr.ru/post/245323/)
 
 
 dual stack bgp ipv6
 [http://mindless.gr/2011/07/dual_stack_bgp_configuration_quagga/](http://mindless.gr/2011/07/dual_stack_bgp_configuration_quagga/)
 [https://supportforums.cisco.com/t5/wan-routing-and-switching/bgp-dual-stack-ipv4-ipv6-configuration-guide/td-p/2673982](https://supportforums.cisco.com/t5/wan-routing-and-switching/bgp-dual-stack-ipv4-ipv6-configuration-guide/td-p/2673982)
 
 
 
 Самое толковое описание
 [https://nag.ru/articles/article/26964/tehnologii-dlya-migratsii-na-ipv6.html](https://nag.ru/articles/article/26964/tehnologii-dlya-migratsii-na-ipv6.html)
 
 
 1. Понять и делать 6to4 NAT                    v
 2.Тестовый ospf quagga  +  cisco  (дуал стек попробовать)          v
 3. Сделать тестовый BGP (должно же быть серое адресное пространство и серые AS для теста). Посмотреть анонсы и т д         v
 4. Включить ospf в нашем backbone, получить связность (предварительно распределить адресное пространство)   -  Выделяем блок адресов для клиентов /48 на бизнес-центр, первую и последюю резервируем, остальное клиентам
                            из резерва нарезаем /64 на линки клиентам. Ну вот и всё 
 5. DNS ipv6, проверка наших сайтов
 6. Попробовать на ASR тестовый BGP v6 совместно с существующими (ASR - k6-c0)  (DHCPv6 PD)
 6. Обратиться в RETN (router object)
 7. Проверить работу сети
 8. Попробовать с Соколовым.
 
 (/64 - лупбэки  выделять адреса /128 из них
 бэкбон - на core link предлагается использовать /127, /64 предлагают использовать на линк к клиенту
 /48 на бизнес центр (Доватора 2а)
 /56 клиенту Руле
 /64 на линк (влан))

 
 НА p2p интерфейсах надо выключать RA
 Правильная настройка интерфейса p2p
 interface xyz
ipv6 address ...
no ipv6 redirects
ipv6 nd ra suppress all


Интерфейс в сторону клиентов
interface xyz
ipv6 address ...
no ipv6 redirects


 Now we will enable SLAAC
interface e0/0
ipv6 address autoconfig default
no shutdown

 
 
 
 DNSSEC + AAAA
 
 
  2a0c:4280::/29
  
  
  2a0c:4280:0:0::/64
  
  [http://yar-ix.net/info/configs/](http://yar-ix.net/info/configs/)
  
  
  
  k6-c0
  router bgp 65502
 bgp router-id 172.16.1.2
 bgp log-neighbor-changes
 no bgp default ipv4-unicast
 neighbor 2A0C:4280:FFFF:FFFF::1 remote-as 65501
 neighbor 172.16.1.1 remote-as 65501
 !
 address-family ipv4
  redistribute connected
  neighbor 172.16.1.1 activate
 neighbor 172.16.1.1 route-map TEST-IPV4-PEER-OUT out
 exit-address-family
 !
 address-family ipv6
  redistribute connected
  neighbor 2A0C:4280:FFFF:FFFF::1  activate
  neighbor 2A0C:4280:FFFF:FFFF::1 route-map TEST-PEER-OUT out
 exit-address-family

 
 
ip prefix-list IPV4-PEER-OUT seq 10 permit 172.16.0.0/23 le 32
 
 ipv6 prefix-list PERMIT-OUR-NETS seq 1 permit 2A0C:4281::/32

 
route-map TEST-IPV4-PEER-OUT permit 10
 match ip address prefix-list IPV4-PEER-OUT
!
route-map TEST-PEER-OUT permit 5
 match ipv6 address prefix-list PERMIT-OUR-NETS
 
 
 
  TEST
 router bgp 65501
 bgp router-id 172.16.1.1
 bgp log-neighbor-changes
 no bgp default ipv4-unicast
 neighbor 2A0C:4280:FFFF:FFFF::2 remote-as 65502
 neighbor 172.16.1.2 remote-as 65502
 !
 address-family ipv4
  redistribute connected
  neighbor 2A0C:4280:FFFF:FFFF::2 activate
  neighbor 172.16.1.2 activate
  neighbor 172.16.1.2 route-map TEST-IPV4-PEER-OUT out
 exit-address-family
 !
 address-family ipv6
  redistribute connected
  neighbor 2A0C:4280:FFFF:FFFF::2 activate
  neighbor 2A0C:4280:FFFF:FFFF::2 route-map TEST-PEER-OUT out
 exit-address-family
 
 
 
ip prefix-list IPV4-PEER-OUT seq 10 permit 192.168.80.0/23 le 32
ip prefix-list IPV4-PEER-OUT seq 20 permit 10.0.0.0/30 le 32

ipv6 prefix-list PERMIT-OUR-NETS seq 1 permit 2A0C:4280::/32

!
route-map TEST-IPV4-PEER-OUT permit 10
 match ip address prefix-list IPV4-PEER-OUT
!
route-map TEST-PEER-OUT permit 5
 match ipv6 address prefix-list PERMIT-OUR-NETS
 
 
   redistribute ospf 1 match internal external 1 external 2
   
   
   

ipv6 prefix-list ANY permit ::/0 le 128



Информация по ipv6
[http://wiki.rsu.edu.ru/wiki/%D0%92%D0%BD%D0%B5%D0%B4%D1%80%D0%B5%D0%BD%D0%B8%D0%B5_IPv6](http://wiki.rsu.edu.ru/wiki/%D0%92%D0%BD%D0%B5%D0%B4%D1%80%D0%B5%D0%BD%D0%B8%D0%B5_IPv6)
[http://www.intuit.ru/studies/courses/11157/1119/info](http://www.intuit.ru/studies/courses/11157/1119/info)
[https://yarique.bitbucket.io/ipv6_ru/ipv6_ru.htm](https://yarique.bitbucket.io/ipv6_ru/ipv6_ru.htm)
[https://docs.google.com/file/d/0ByeFzvNZTBw4MURhSmV1OVlOSms/edit](https://docs.google.com/file/d/0ByeFzvNZTBw4MURhSmV1OVlOSms/edit)
[http://www.foxnetwork.ru/index.php/component/content/article/153-ipv6.html](http://www.foxnetwork.ru/index.php/component/content/article/153-ipv6.html)

Распределение адресов
[http://ip.v6net.ru/about/subnetting2](http://ip.v6net.ru/about/subnetting2)



OSPFv3
[https://protechgurus.com/configure-ospf-ipv6-ospfv3-cisco/](https://protechgurus.com/configure-ospf-ipv6-ospfv3-cisco/)
[http://blog.evgenybelkin.ru/2011/07/ospfv3-ipv6.html](http://blog.evgenybelkin.ru/2011/07/ospfv3-ipv6.html)
[https://www.cisco.com/c/en/us/support/docs/ip/ip-version-6-ipv6/112100-ospfv3-config-guide.html](https://www.cisco.com/c/en/us/support/docs/ip/ip-version-6-ipv6/112100-ospfv3-config-guide.html)
[https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/iproute_ospf/configuration/15-1sg/ip6-route-ospfv3.html](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/iproute_ospf/configuration/15-1sg/ip6-route-ospfv3.html)
[https://blog.philippklaus.de/2012/04/ipv6-dynamic-routing-with-quagga-and-ospf6d-ospfv3/](https://blog.philippklaus.de/2012/04/ipv6-dynamic-routing-with-quagga-and-ospf6d-ospfv3/)
[http://xmodulo.com/ipv6-bgp-peering-filtering-quagga-bgp-router.html](http://xmodulo.com/ipv6-bgp-peering-filtering-quagga-bgp-router.html)
[https://unquietwiki.com/tinc_quagga_ipv6.html](https://unquietwiki.com/tinc_quagga_ipv6.html)

ipv6 firewall
[https://www.sixxs.net/wiki/IPv6_Firewalling](https://www.sixxs.net/wiki/IPv6_Firewalling)
[https://lxadm.com/IPv6:_blocking_incoming_traffic_with_ip6tables](https://lxadm.com/IPv6:_blocking_incoming_traffic_with_ip6tables)
Ra guard
neighbor-cache

 Никакой статики никогда и нигде! Только PD + EUI-64 (тоже можно)!
  Вообще в IPv6 на линке может вообще не быть реальных адресов, достаточно link-local. Для трейсинга роутер может использовать лупбек, например. В RA будет link-local адрес, например. Тогда атаки на neighbour-cache тоже исключаются для линка. 
  
  
  PNI private peering 
  Private Network Interconnect (Прямой пиринг, как у нас с ростелеком или медиасетями)
  
  
  Домашний роутер
  [https://taczanowski.net/linux-box-as-an-ipv6-router-with-slaac-and-dhcpv6-pd/](https://taczanowski.net/linux-box-as-an-ipv6-router-with-slaac-and-dhcpv6-pd/)
  [https://superuser.com/questions/742792/how-do-i-deploy-ipv6-within-a-lan-using-a-debian-based-router-and-prefix-delegat](https://superuser.com/questions/742792/how-do-i-deploy-ipv6-within-a-lan-using-a-debian-based-router-and-prefix-delegat)
  [https://habrahabr.ru/post/192164/](https://habrahabr.ru/post/192164/)
  [https://h4cks4w.blogspot.ru/2015/04/ipv6-linux-2.html](https://h4cks4w.blogspot.ru/2015/04/ipv6-linux-2.html)
  [http://alter.org.ua/ru/docs/net/ipv6_isp/](http://alter.org.ua/ru/docs/net/ipv6_isp/)
  
  По адресации
  /64 на loopback
  /64 на 13 vlan
  /64 на DNS
  /40 на CTD-C5 /48 на Доватора /56 руле и /64 на линковочную сеть руле
  
  
  IPv6 for LIRs

    Each router and layer 3 switch will receive a /56 prefix. This provides space for 256 possible interfaces.
    For the infrastructure we set aside a /56 as well. There is room for 256 possible VLANs for our internal services.
    To be consistent, we use the same approach for the rest of the POP.
    Each of the service VLANs (www, mail, etc.) requires only one subnet, which is equal to one /64. The amount of devices connected to each subnet is completely irrelevant.
    Each point-to-point connection requires one /64 subnet.
    Every customer (colocation and the P2P links) will receive a /48 assignment, pushed down to their network using IPv6 Prefix Delegation.
    The customer base will not grow, so we set aside a /39 (= 512 x /48) for the colocation customers. If the amount of customers would increase, it would be a better idea to set aside a 4-bit boundary block, for example, a /36 (= 4096 x /48).
    
    
    
    
    
    
    
    
    
    
    Конфигурации для OSPFv3
    
ipv6 route 2A0C:4280:3::2/128 GigabitEthernet0/0.32                                                                                                                                     
ipv6 route 2A0C:4280::/32 Null0     

ipv6 router ospf 100                                                                                                                                                                    
 router-id 1.1.1.2                                                                                                                                                                      
 passive-interface default                                                                                                                                                              
 no passive-interface GigabitEthernet0/0.50                                                                                                                                             
 redistribute connected                                                                                                                                                                 
 redistribute static                                                                                                                                                                    
!                                                                                                                                                                                       
!                    

router bgp 65501                                                                                                                                                                        
 bgp router-id 172.16.1.1                                                                                                                                                               
 bgp log-neighbor-changes                                                                                                                                                               
 no bgp default ipv4-unicast                                                                                                                                                            
 neighbor 2A0C:4280:FFFF:FFFF::2 remote-as 65502                                                                                                                                        
 neighbor 172.16.1.2 remote-as 65502                                                                                                                                                    
 !                                                                                                                                                                                      
 address-family ipv4                                                                                                                                                                    
  redistribute connected                                                                                                                                                                
  neighbor 2A0C:4280:FFFF:FFFF::2 activate                                                                                                                                              
  neighbor 172.16.1.2 activate                                                                                                                                                          
  neighbor 172.16.1.2 route-map TEST-IPV4-PEER-OUT out                                                                                                                                  
 exit-address-family                                                                                                                                                                    
 !                                                                                                                                                                                      
 address-family ipv6                                                                                                                                                                    
  redistribute connected                                                                                                                                                                
  redistribute ospf 100 match internal external 1 external 2                                                                                                                            
  network 2A0C:4280::/32                                                                                                                                                                
  neighbor 2A0C:4280:FFFF:FFFF::2 activate                                                                                                                                              
  neighbor 2A0C:4280:FFFF:FFFF::2 route-map TEST-PEER-OUT out                                                                                                                           
 exit-address-family                                                                                                                                                                    
!                          









2a0c:4280::/29

loopback
2a0c:4280:0000:0000:0000:0000:d450:e8e7/128
81.20.192.16

13vlan
2a0c:4280:0000:0001:0000:0000:0000:00bd/64
81.20.192.50

Radium
2a0c:4280:0000:0001:0000:0000:0000:02bd/64

2a0c:4280:0000:0000:0000:0000:d450:4ad1/128


DNS
Добавить
listen-on-v6 { any; };          ---- нужно добавить (или перечислить только нужное вам)
allow-recursion { clients; };   ---как правило, уже есть
};

«прямыми» зонами просто, то есть к любой записи А добавляют запись АААА. 
Выделить ip адреса для bind из backone


Создать более специфичный inet6num /32
Создать route6
Создать domain для /32  (сначала надо настроить DNS)


reverse DNS
$TTL	1h
$ORIGIN 0.0.0.0.8.b.d.0.1.0.0.2.ip6.arpa.
@           IN SOA  ns1.example.org. root.example.org. (
			2012122101; serial
			24h; refresh
			2h; retry
			1000h; expire
			2d; minimum
			) 

	IN	NS	ns1.example.org.
	IN	NS	ns2.example.org.

1.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0	IN PTR server.example.org.





Подготовить
listen-on listen-on-v6
transfer-source
transfer-source-v6 
notify-source
notify-source-v6
query-source address 
query-source-v6 address.

notify yes;
also-notify { xxxx:xxxx:xxxx:xxxx::xxx5; x.x.x.5; };

zone "example.dev" {
    type slave;
    masters { xxxx:xxxx:xxxx:xxxx::xxx2; x.x.x.2; };
    file "...";
};

sc.v6int











route6 object

route:          81.20.192.0/23
descr:          RU-INTELECOM-NET
origin:         AS20866
mnt-by:         INTELECOM-MNT
created:        2013-05-13T11:05:51Z
last-modified:  2013-05-13T11:05:51Z
source:         RIPE


as-set:         AS-INTELECOM
descr:          Industiral Telecom
members:        AS20866
members:        AS49919
members:        AS60833
tech-c:         IBD-RIPE
tech-c:         PVR3-RIPE
admin-c:        IBD-RIPE
admin-c:        PVR3-RIPE
mnt-by:         INTELECOM-MNT
created:        2006-06-08T11:53:46Z
last-modified:  2016-08-31T08:15:43Z
source:         RIPE


organisation:    ORG-ITI1-RIPE
org-name:        LLC Promsvyaz-Invest
org-type:        LIR
address:         2A Dovatora st.
address:         398024
address:         Lipetsk
address:         RUSSIAN FEDERATION
phone:           +7 4742 517103
fax-no:          +7 4742 517109
admin-c:         PVR3-RIPE
admin-c:         LY10-RIPE
admin-c:         EVK10-RIPE
admin-c:         IBD-RIPE
abuse-c:         IA3269-RIPE
mnt-ref:         RIPE-NCC-HM-MNT
mnt-ref:         INTELECOM-MNT
mnt-by:          RIPE-NCC-HM-MNT
mnt-by:          INTELECOM-MNT
created:         2004-04-17T11:53:29Z
last-modified:   2017-10-30T14:48:39Z
source:          RIPE # Filtered



inetnum:         81.20.192.0 - 81.20.192.255
netname:         INTELECOM-2-NET
descr:           Industrial Telecom Inc., Moscow
country:         RU
admin-c:         IBD-RIPE
tech-c:          IBD-RIPE
tech-c:          PVR3-RIPE
status:          ASSIGNED PA
notify:          iptech@promsvyaz.ru
mnt-by:          INTELECOM-MNT
created:         2002-02-08T08:07:29Z
last-modified:   2016-08-30T08:07:37Z
source:          RIPE


route:           81.20.192.0/23
descr:           RU-INTELECOM-NET
origin:          AS20866
mnt-by:          INTELECOM-MNT
created:         2013-05-13T11:05:51Z
last-modified:   2013-05-13T11:05:51Z
source:          RIPE





aut-num:        AS20866
as-name:        INTELECOM-AS
org:            ORG-ITI1-RIPE
import:         from AS9002 action pref=100; accept ANY
import:         from AS31133 action pref=100; accept ANY
export:         to AS9002 announce AS-INTELECOM
export:         to AS9002 announce AS-INDESIT
export:         to AS9002 announce AS-NLMK
export:         to AS31133 announce AS-INTELECOM
export:         to AS31133 announce AS-INDESIT
export:         to AS31133 announce AS-NLMK
admin-c:        IBD-RIPE
admin-c:        PVR3-RIPE
tech-c:         IBD-RIPE
tech-c:         PVR3-RIPE
status:         ASSIGNED
mnt-by:         RIPE-NCC-END-MNT
mnt-by:         INTELECOM-MNT
mnt-routes:     INTELECOM-MNT
created:        2002-02-07T15:08:16Z
last-modified:  2017-11-15T09:19:08Z
source:         RIPE





Object in RIPE Database
Update object RIPEstat

    inet6num:        2a0c:4280::/29
    netname:         RU-INTELECOM-20180102
    country:         RU
    org:             ORG-ITI1-RIPE
    admin-c:         PVR3-RIPE
    tech-c:          PVR3-RIPE
    status:          ALLOCATED-BY-RIR
    mnt-by:          RIPE-NCC-HM-MNT
    mnt-by:          INTELECOM-MNT
    created:         2018-01-02T08:30:58Z
    last-modified:   2018-01-02T08:30:58Z
    source:          RIPE
    
    
    
    
    
role:           INTELECOM ABUSE
abuse-mailbox:  abuse@promsvyaz.ru
address:        6, st. Kraynaya, Lipetsk,Russia
nic-hdl:        IA3269-RIPE
mnt-by:         INTELECOM-MNT
created:        2013-04-29T14:08:23Z
last-modified:  2013-04-29T14:10:46Z
source:         RIPE # Filtered












----------------------------------------------------------- IPV6 PD -----------------------------

На C6 настраиваем dhcp-роутер с PD-delagation, вланом протаскиваем в офис, на akim.sc.int настраиваем 


# Enable IPv6 forwarding
net.ipv6.conf.all.forwarding = 1
 
# Obtain IPv6 address on wan interface by Stateless autoconfiguration (SLAAC)
net.ipv6.conf.eth0.accept_ra = 2
 
# I want to have one IPv6 address on my wan interface, based on my mac address. 
# Without this my router will also have temporary, random IPv6 addresses which will be changing over time.
net.ipv6.conf.all.use_tempaddr = 0
net.ipv6.conf.default.use_tempaddr = 0

Настраиваем wide-dhcpv6-client для PD и на LAN настраиваем dnsmasq или RADVD

Akim запрашивет префикс и раздаёт его потом в lan

2a0c:4280:0000:0003::x/126 - линк до доватора от CTD

2a0c:4280:0001:0300::/64   - адресация на линк до клиента
2a0c:4280:0103::/48   - адресация для Доваторов 2а
2a0c:4280:0103:0100::/56    -  адресация клиенту


1)Настройка сервера
ipv6 unciast-routing

ipv6 dhcp pool dovator-dhcpv6-pool
prefix-delegation pool dovatora-dhcpv6-pool lifetime 1800 600
ipv6 local pool dovatora-dhcpv6-pool 2a0c:4280:0103::/48 56
dns-server 2a0c:4280:0000:0013:0000:0000:0000:00bd/64
domain-name sc.int


interface Ethernet0/0
ipv6 address 2010:AB8:0:1::1/64 – назначаем адрес для интерфейса e0/0
ipv6 enable
ipv6 dhcp server dovator-dhcpv6-pool

ipv6 nd managed-config-flag
 ipv6 nd other-config-flag


In Interface Configuration Mode

    ipv6 address <specify IPv6 Address>
    ipv6 dhcp server <server name>rapid-commit

    
--------------------------------------------- ------------------------------- --------------------- --------------------------------------- ------------------------------------------
Настройка клиента.

На интерфейсе смотрящем в сторону сервера

ipv6 unicast-routing
!
interface Serial0/0
no ip address
ipv6 address autoconfig default
!--- The autoconfig default adds a static ipv6 
!--- default route pointing to upstream DHCP server.
!
ipv6 enable
ipv6 dhcp client pd prefix-from-provider
    
    
 На интерфейсах смотрящих в сторону LAN
interface FastEthernet0/0
no ip address
duplex auto
speed auto
ipv6 address prefix-from-provider ::1:0:0:0:1/64
    !--- The first 48 bits are imported from the delegated
!--- prefix (2001:db8:1200) and the ::/64 is the client
!--- identifier that gives the interface Fa0/1 the
!--- global IPv6 address 2001:DB8:1200:1::1/64.

//////////////////////////////// Настройка в LAN ///////////////////////////
    ipv6 address autoconfig  (на интерфейс в сторону)
    
    
--------------------------------------------- ------------------------------- --------------------- --------------------------------------- ------------------------------------------
Настройка клиента linux

# Enable IPv6 forwarding
net.ipv6.conf.all.forwarding = 1
 
# Obtain IPv6 address on wan interface by Stateless autoconfiguration (SLAAC)
net.ipv6.conf.eth0.accept_ra = 2
 
# I want to have one IPv6 address on my wan interface, based on my mac address. 
# Without this my router will also have temporary, random IPv6 addresses which will be changing over time.
net.ipv6.conf.all.use_tempaddr = 0
net.ipv6.conf.default.use_tempaddr = 0





-------------------- ------------------------------- ----------------------------- ----------------------------- ---------------------------- --------------------------- -------------------------
2) Настройка relay
Relay Agent Configuration

In Global Configuration Mode

    enable
    configure terminal
    ipv6 unicast-routing

 Также как и для IPv4 L3-коммутаторы и маршрутизаторы Cisco могут выполнять функции DHCP ретранслятора, для чего используется команда ipv6 dhcp relay destination ipv6-address, где ipv6-address – адрес сервера DHCPv6.
	ipv6 dhcp relay destination ipv6-address [interface-type interface-number] 
 
In Interface Configuration Mode

 

In DHCPv6 server Facing Interface:

    ipv6 address autoconfig
    ipv6 enable
    exit

In Clients Facing Interface

    ipv6 address <specify IPv6 address>
    ipv6 dhcp relay destination <specify destination IPv6 address><interface type>
    
-------------------------- ------------------------------- ------------------------ ------------------------- -------------------------------- ------------------------------------ --------------
interface FastEthernet0/0
mac-address 0000.2222.0000
no ip address
ipv6 address autoconfig default
ipv6 enable
ipv6 dhcp client pd PREFDEL rapid-commit



LAN кофигурация
Client Configuration

In Global Configuration Mode

    enable
    configure terminal
    ipv6 unicast-routing
    ipv6 nd route-owner

In Interface Configuration Mode

    ipv6 address dhcp rapid commit
    ipv6 enable
    ipv6 nd autoconfig prefix
    ipv6 nd autoconfig default-route
    exit


[https://supportforums.cisco.com/t5/network-infrastructure-documents/stateful-dhcpv6-relay-configuration-example/ta-p/3149338](https://supportforums.cisco.com/t5/network-infrastructure-documents/stateful-dhcpv6-relay-configuration-example/ta-p/3149338)
[https://www.cisco.com/c/en/us/support/docs/ip/ip-version-6-ipv6/113141-DHCPv6-00.html](https://www.cisco.com/c/en/us/support/docs/ip/ip-version-6-ipv6/113141-DHCPv6-00.html)

руля
ssh garry@81.20.197.40 -p 2233

The command ipv6 nd route-owner inserts Neighbor Discovery-learned routes into the routing table with "ND" status and enables ND autoconfiguration behavior.This command is configured in Global Configuration mode.
Enabling the command ipv6 nd autoconfig prefix in the interface configuration mode, uses Neighbor Discovery to install all valid on-link prefixes from RAs received on the interface.
To allow Neighbor Discovery to install a default route to the Neighbor Discovery-derived default router, use the command  ipv6 nd autoconfig default-route in the interface configuration mode


Disable RA at Router (Backbone)
[https://community.infoblox.com/t5/IPv6-CoE-Blog/Disabling-IPv6-Router-Advertisements-in-the-Data-Center/ba-p/7007](https://community.infoblox.com/t5/IPv6-CoE-Blog/Disabling-IPv6-Router-Advertisements-in-the-Data-Center/ba-p/7007)








Январь 9, 2014   Сети   Нет комметариев
IPv6 accept_ra и routing в Linux

Читайте доки, они рулят…
Потратил непозволительно много времени чтобы понять почему linux хост “вдруг” перестал принимать icmp6 router advertisement от рутера и удалил из таблицы маршрутизации default route. “Вдруг” – это после ковыряния туннелей. Как оказалось функции маршрутизации и router solicitation взаимоисключающие (ну почти).
Хост может быть или роутером и тогда сам рассылает RA или клиентом и тогда принимает объявы от роутеров. При активации sysctl переменной net.ipv6.conf.all.forwarding прием RA отвалился. Сие поведение описано в rfc2462. “Читайте доки, они рулят” – в который раз сказал я себе. А если линукс-хост это хомячковый рутер, который с одной стороны должен поймать адрес рутера от прова а с другой стороны самому быть рутером для домашней локалки? Как гласит ip-sysctl.txt это предусмотренно путем присвоения переменной accept_ra для интерфейса значения “2” (accept_ra=2). Т.е. если нельзя но очень хочется – то можно :)
BSD, кстати, тоже ведёт себя подобным образом, когда-то давно я уже об этом писал. Надо быть внимательнее…

     accept_ra – BOOLEAN

        Accept Router Advertisements; autoconfigure using them.

        Possible values are:

            0 Do not accept Router Advertisements.
            1 Accept Router Advertisements if forwarding is disabled.
            2 Overrule forwarding behaviour. Accept Router Advertisements even if forwarding is enabled.

        Functional default:

            enabled if local forwarding is disabled.
            disabled if local forwarding is enabled.

sysctl -w net.ipv6.conf.eth1/3291.accept_ra=2
            
[http://forum.ubuntu.ru/index.php?topic=186059.0](http://forum.ubuntu.ru/index.php?topic=186059.0)


ipv6 prefix list Junos, Cisco
[https://www.space.net/~gert/RIPE/ipv6-filters.html](https://www.space.net/~gert/RIPE/ipv6-filters.html)


Я не использую пока ipv6, поэтому сразу уберу соотв. правило из firewalld:

# firewall-cmd --permanent --zone=public --remove-service=dhcpv6-client




[https://blog.ipspace.net/2013/07/first-hop-ipv6-security-features-in.html](https://blog.ipspace.net/2013/07/first-hop-ipv6-security-features-in.html)
[https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/ipv6_fhsec/configuration/15-s/ip6f-15-s-book/ip6-ra-guard.html](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/ipv6_fhsec/configuration/15-s/ip6f-15-s-book/ip6-ra-guard.html)

IPv6 RA Guard
Настраивается на коммутаторе. Функция не пропускает RA не от роутеров.

Там где подключен комп
SW1(config)#ipv6 nd raguard policy RAGUARD
SW1(config-nd-raguard)#device-role host
SW1(config-nd-raguard)#exit
SW1(config)#int gig0/1
SW1(config-if)#ipv6 nd raguard attach-policy RAGUARD


Если подключаем роутер
SW1(config)#ipv6 access-list RAGUARD
SW1(config-ipv6-acl)#permit ipv6 host fe80::1 any
SW1(config-ipv6-acl)#exit
SW1(config)#ipv6 nd raguard policy RAGUARD
SW1(config-nd-raguard)#device-role router
SW1(config-nd-raguard)#match ipv6 access-list RAGUARD

fe80::1  - роутер, fe80::2 хост


[https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/ipaddr_dhcp/configuration/xe-3e/dhcp-xe-3e-book/DHCPv6-Guard.pdf](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/ipaddr_dhcp/configuration/xe-3e/dhcp-xe-3e-book/DHCPv6-Guard.pdf)
DHCPv6 Guard 
The DHCPv6 Guard feature blocks reply and advertisement messages that come from unauthorized DHCP servers and relay agents.
Также настраивается на коммутаторе. Принцип похожий.


IPV6 snooping
The IPv6 Neighbor Discovery Inspection, or IPv6 "snooping," feature bundles several Layer 2 IPv6 first-hop security features, including IPv6 Address Glean and IPv6 Device Tracking.
Обеспечивает защиту от подделки ip адресов








Я бы добавил про SLAAC следующее:
1. Описание механизма DAD. Штука очень важная.
2. Ну и rfc4941 (Privacy Extensions for Stateless Address Autoconfiguration in IPv6). Там как бы не совсем случайный набор цифр:)
3. Не упомянута возможность передачи RDNSS в RA, которая описана в rfc6106. Не все клиенты это умеют, но тем не менее.



ipv6 rfc
[https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/ipv6_fhsec/configuration/15-s/ip6f-15-s-book/ip6-rfcs.html](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/ipv6_fhsec/configuration/15-s/ip6f-15-s-book/ip6-rfcs.html)

Атаки на ipv6
attacks on duplicate address detection (DAD), address resolution, device discovery, and the neighbor cache



SIPCALC
[https://www.linux.com/learn/intro-to-linux/2017/10/calculating-ipv6-subnets-linux](https://www.linux.com/learn/intro-to-linux/2017/10/calculating-ipv6-subnets-linux)
