---
layout: post
title:  "bgp-indesit"
date:   2014-04-05 20:03:04 +0400
categories: routing
tags: routing
---

# bgp-indesit
interface GigabitEthernet0/0.700
 description #Indesit-BGP NET #pheonix 19.11.2009 
 bandwidth 2048
 encapsulation dot1Q 700
 ip address 81.20.192.141 255.255.255.252
 ip access-group 130 in
 ip flow ingress
 rate-limit input 10240000 1960000 3920000 conform-action transmit exceed-action drop
 rate-limit output 10240000 1960000 3920000 conform-action transmit exceed-action drop
 no cdp enable
end



  neighbor 81.20.192.142 activate
  neighbor 81.20.192.142 send-community both
  neighbor 81.20.192.142 prefix-list permit_indesit in
  neighbor 81.20.192.142 prefix-list grey_net out

Запрещаем серые, разрешаем все остальные
ip prefix-list grey_net seq 5 deny 10.0.0.0/8
ip prefix-list grey_net seq 10 deny 172.16.0.0/12
ip prefix-list grey_net seq 20 deny 192.168.0.0/16
ip prefix-list grey_net seq 100 permit 0.0.0.0/0 le 32

Разрешаем аннонсировать нам только свою сеть
ip prefix-list permit_indesit seq 5 permit 193.104.11.0/24 le 32
ip prefix-list permit_indesit seq 50 deny 0.0.0.0/0 le 32






*> 0.0.0.0          81.16.117.9                          700 8744 i
Gateway of last resort is 81.16.117.9 to network 0.0.0.0

BGP routing table entry for 0.0.0.0/0, version 2
Paths: (1 available, best #1, table Default-IP-Routing-Table)
Multipath: eBGP iBGP
  Not advertised to any peer
  8744
    81.16.117.9 from 81.16.117.9 (81.16.117.9)
      Origin IGP, localpref 100, weight 700, valid, external, best
      Extended Community: RT:8744:777


B*   0.0.0.0/0 [20/0] via 81.16.117.9, 7w0d








Объявить default в BGP
neighbor X.X.X.X default originate





Например со стороны ЦО:  (В сторону комбината)

Код:
ISP1(config)#ip prefix-list default seq 5 permit 0.0.0.0/0
ISP1(config)#router bgp 31
ISP1(config-router)#neighbor x.x.x.x prefix-list default out
ISP1(config-router)#neighbor x.x.x.x default-originate






Бранчи:

Код:
CE(config)#access-list 1 permit 0.0.0.0
CE(config)#route-map localonly
CE(config-route-map)#match ip address 1
CE(config)#ip prefix-list local seq 5 permit 0.0.0.0/0
CE(config)#router bgp 62211
CE(config-router)#neighbor 2.2.2.2 prefix-list local in
CE(config-router)#neighbor 9.9.9.9 route-map localonly in


А теперь уже можно играться с запрещением дефолта по BGP. Создаем префикс-лист с названием DENY-DEFAULT-IN:

router(config)# ip prefix-list DENY-DEFAULT-IN seq 5 deny 0.0.0.0/0 le 1
router(config)# ip prefix-list DENY-DEFAULT-IN seq 10 permit 0.0.0.0/0 ge 2

















Конфиг для k9-c0
1. Одна ebgp с комбинатом, и 2 ibgp с cde-c3 и ctd-c6
2. От них ничего принимать не надо, так как всё что надо есть по ospf. К ним анонсировать 194 сеть комбината и то на первоначальном этапе не надо
3. от комбината нужно разрешить 194 сеть и всё, к ним послать default. Получаем Bgp сессию - это конец первого этапа
4. Второй этап  - поменять route object 194 сети и разрешить объявлять сеть 194 по ibgp нашим bgw, которые объявят её во внешний мир, удаляем статик
5



AS60833

ctd-c6

int Lo0
 desc # Interface for Tunnel endpoint, IP/MPLS and BGP exchanges
 ip address 81.20.192.75 255.255.255.255 

router bgp 20866
 no synchronization
 bgp log-neighbor-changes
 neighbor 81.20.192.79 remote-as 20866
 neighbor 81.20.192.79 update-source Loopback0






neighbor 81.20.192.79 shutdown





k9-c0
int Lo0
 desc # Interface for Tunnel endpoint, IP/MPLS and BGP exchanges
 ip address 81.20.192.79 255.255.255.255



router bgp 20866
 no synchronization
 bgp log-neighbor-changes
 neighbor 81.20.192.75 remote-as 20866
 neighbor 81.20.192.75 update-source Loopback0
 neighbor 81.20.192.75 prefix-list ibgp-neigb-in in
 neighbor 81.20.192.75 prefix-list ibgp-neigb-out out
 neighbor 81.20.192.78 remote-as 20866
 neighbor 81.20.192.78 update-source Loopback0
 neighbor 81.20.192.78 prefix-list ibgp-neigb-in in
 neighbor 81.20.192.78 prefix-list ibgp-neigb-out out
 neighbor 81.20.192.130 remote-as 60833
 neighbor 81.20.192.130 default-originate
 neighbor 81.20.192.130 prefix-list default out
 neighbor 81.20.192.130 prefix-list nlmk-194-in in
 






Prefix-list на out для комбината (только default)
ip prefix-list default seq 10 permit 0.0.0.0/0
ip prefix-list default seq 20 deny 0.0.0.0/0 ge 1 le 32

Prefix-list на in от комбината (одна 194)
ip prefix-list nlmk-194-in seq 5 permit 81.20.194.0/24 le 32
ip prefix-list nlmk-194-in seq 20 deny 0.0.0.0/0 le 32

Prefix-list на in от ibgp соседей (Ничего нах не надо, может только нашу для теста)
ip prefix-list ibgp-neigb-in seq 20 deny 0.0.0.0/0 le 32

Prefix-list на out для ibgp соседей - объявлять только 194, а в начале нихера не объявлять
###########ip prefix-list ibgp-neigb-out seq 5 permit 81.20.194.0/24 le 32
ip prefix-list ibgp-neigb-out seq 20 deny 0.0.0.0/0 le 32



ip prefix-list DEFAULT-IN-PERMIT seq 5 permit 0.0.0.0/0
ip prefix-list DEFAULT-IN-DENY seq 5 deny 0.0.0.0/0
ip prefix-list DEFAULT-IN-DENY seq 10 permit any







Команды для проверки с их стороны
show  ip bgp 



sh ip bgp neighbors 81.20.192.129 routes
sh ip bgp neighbors 81.20.192.129 advertised-routes



Команды для проверки с нашей стороны

show ip bgp 
show ip bgp 





 neighbor 81.16.117.9 update-source GigabitEthernet0/1
 neighbor 81.20.192.71 remote-as 20866
 neighbor 81.20.192.71 update-source Loopback0
 neighbor 81.20.192.71 timers 15 45 45
 neighbor 81.20.192.72 remote-as 20866
 neighbor 81.20.192.72 update-source Loopback0
 neighbor 81.20.192.73 remote-as 20866
 neighbor 81.20.192.73 update-source Loopback0
 neighbor 81.20.192.74 remote-as 20866
 neighbor 81.20.192.74 update-source Loopback0
 neighbor 81.20.192.75 remote-as 20866
 neighbor 81.20.192.75 update-source Loopback0
 neighbor 81.20.192.76 remote-as 20866
 neighbor 81.20.192.76 update-source Loopback0
 neighbor 81.20.192.77 remote-as 20866
 neighbor 81.20.192.77 ebgp-multihop 2
 neighbor 81.20.192.77 update-source Loopback0
 neighbor 81.20.192.79 remote-as 20866
 neighbor 81.20.192.79 shutdown






router bgp 20866
 no synchronization
 bgp log-neighbor-changes
 network 192.168.12.0
 neighbor 81.20.192.71 remote-as 20866
 neighbor 81.20.192.71 update-source Loopback0
 neighbor 81.20.192.72 remote-as 20866
 neighbor 81.20.192.72 update-source Loopback0
 neighbor 81.20.192.76 remote-as 20866
 neighbor 81.20.192.76 update-source Loopback0
 neighbor 81.20.192.77 remote-as 20866
 neighbor 81.20.192.77 update-source Loopback0
 neighbor 81.20.192.78 remote-as 20866
 neighbor 81.20.192.78 update-source Loopback0
 neighbor 81.20.193.122 remote-as 20866
 neighbor 81.20.193.122 update-source Loopback0
 neighbor 192.168.90.1 remote-as 20866
 neighbor 192.168.90.1 update-source GigabitEthernet0/0.457
 neighbor 192.168.91.3 remote-as 20866
 neighbor 192.168.91.3 update-source Loopback2
 no auto-summary
 !
 address-family vpnv4
 neighbor 81.20.192.71 activate
 neighbor 81.20.192.71 send-community extended
 neighbor 81.20.192.72 activate
 neighbor 81.20.192.72 send-community extended
 neighbor 81.20.192.76 activate
 neighbor 81.20.192.76 send-community extended
 neighbor 81.20.192.77 activate
 neighbor 81.20.192.77 send-community extended
 neighbor 81.20.192.78 activate
 neighbor 81.20.192.78 send-community extended
 neighbor 81.20.193.122 activate
 neighbor 81.20.193.122 send-community extended
 neighbor 192.168.90.1 activate
 neighbor 192.168.90.1 send-community both
 neighbor 192.168.90.1 route-reflector-client
 neighbor 192.168.91.3 activate
 neighbor 192.168.91.3 send-community both
 exit-address-family











 neighbor 192.168.90.1 remote-as 20866
 neighbor 192.168.90.1 update-source GigabitEthernet0/0.457
 neighbor 192.168.91.3 remote-as 20866
 neighbor 192.168.91.3 update-source Loopback2




At a basic level, it does exactly what it says!  :)
 
When you have an e-bgp peer, the next hop is always changed to your peering IP address (next-hop-self, or setting the IP to its own).  This is because ebgp peers don't have any need to know about all the details inside another ASN.  Next hops are measured by an AS Path.
 
In i-bgp peers, information is not changed.  The theory is that everyone know about everything inside the same AS!  Now, this is nice as long as that's true!
 
What happens when the link between two e-bgp peers (obviously known to the edge router because it's connected) is NOT exchanged via any IGP?  Suddenly other internal routers learn i-bgp routes that appear to be unreachable.  They show an unknown IP as the next hop.
 
Ascii digram:
 
(AS 100) -- 10.100.1.1----------10.100.1.2 (AS200-R1)10.200.1.1-------10.200.1.2(AS200-R2)
 
AS 200 routers are i-bgp peers (who could be multiple hops away from each other but this is a short example!).  AS100-200 exchange routes over 10.100.1.0 network.
 
R1 shows all routes with 10.100.1.1 as the next hop.  This is simple and per spec, and is reachable because it's connected.
 
UNLESS R2 is aware of the 10.100.1.0 network, it will learn all of AS100's routes and will view them all as unreachable.
 
If R1 sets "next-hop-self" when pointing to R2s neighbor statement, all of the routes will be changed to reflect 10.200.1.1 as the next hop which is reachable.
 
HTH,




Next-hop

Изменение атрибута next-hop зависит от того какому соседу анонсируется маршрут — iBGP или eBGP:

    по умолчанию, когда маршрут анонсируется eBGP-соседу, атрибут next-hop меняется на IP-адрес маршрутизатора, который анонсирует маршрут;
    по умолчанию, когда маршрут анонсируется iBGP-соседу, атрибут next-hop не изменяется. 

Изменение поведения по умолчанию атрибута next-hop для iBGP-соседа — все обновления для соседа отправлять с указанием в качестве next-hop локального маршрутизатора:

dyn3(config-router)# neighbor <ip-address | peer-group-name>  next-hop-self 

Изменение поведения по умолчанию атрибута next-hop для eBGP-соседа — все обновления для соседа отправлять без изменения атрибута next-hop:

dyn3(config-router)# neighbor <ip-address | peer-group-name>  next-hop-unchanged




1) You don't have a route to it.

2) You need ebgp-multihop but haven't configured it. (If it's not on a
directly connected network or you're using update-source loopback, you need
ebgp-multihop)




 neighbor 81.20.192.75 remote-as 20866
 neighbor 81.20.192.75 update-source Loopback0





Jun  6 12:14:05.564: BGP: aggregate timer expired
Jun  6 12:14:12.908: BGP: Neighbor validation failed. Flags: 0x0, Neighbor-topo check: failed, Router ID: 192.168.121.28
Jun  6 12:14:13.756: BGP: aggregate timer expired
Jun  6 12:14:22.124: BGP: Neighbor validation failed. Flags: 0x0, Neighbor-topo check: failed, Router ID: 192.168.121.28




Neighbor validation failed. Flags: 0x0, Neighbor-topo check: failed, Router ID: 192.168.121.28






 Address tracking is enabled, the RIB does have a route to 81.20.192.122

Is this host reachable for you?
Is this host directly connected to your router or this host is multihop?








no bgp default ipv4-unicast
Команда требует прописывания 
neighbor x.x.x.x activate в  address-family ipv4, чтобы активировать сессию. По умолчанию наоборот
У нас эта команда на ctd-c6
[http://blog.networkrise.com/2013/02/06/bgp-default-ipv4-unicast/](http://blog.networkrise.com/2013/02/06/bgp-default-ipv4-unicast/)
[http://www.cisco.com/en/US/docs/ios/iproute_bgp/command/reference/irg_bgp1.html#wp1113664](http://www.cisco.com/en/US/docs/ios/iproute_bgp/command/reference/irg_bgp1.html#wp1113664)









ip prefix-list ibgp-neigb-in seq 10 permit 2.94.156.0/24 le 32





no neighbor 81.20.192.79 shutdown
 address-family ipv4
neighbor 81.20.192.79 active










bgp troubleshooting
[http://www.cisco.com/en/US/tech/tk365/technologies_tech_note09186a008009478a.shtml#bgp_trouble_neighbor](http://www.cisco.com/en/US/tech/tk365/technologies_tech_note09186a008009478a.shtml#bgp_trouble_neighbor)






K9-C0#show ip bgp rib-failure
Network            Next Hop                      RIB-failure   RIB-NH Matches
81.20.194.0/24     81.20.192.130       Higher admin distance 


K9-C0#show ip bgp
BGP table version is 5, local router ID is 81.20.204.97
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale
Origin codes: i - IGP, e - EGP, ? - incomplete

   Network          Next Hop            Metric LocPrf Weight Path
r> 81.20.194.0/24   81.20.192.130            0             0 60833 i



[http://blog.ioshints.info/2007/12/what-is-bgp-rib-failure.html](http://blog.ioshints.info/2007/12/what-is-bgp-rib-failure.html)
[http://www.cisco.com/en/US/tech/tk365/technologies_q_and_a_item09186a00800949e8.shtml#twenty-three](http://www.cisco.com/en/US/tech/tk365/technologies_q_and_a_item09186a00800949e8.shtml#twenty-three)




Мультихоп
[http://sh-run.com.ua/ebgp-multihop.html](http://sh-run.com.ua/ebgp-multihop.html)






bgp prepend для входящего
bgp weight для исходящего