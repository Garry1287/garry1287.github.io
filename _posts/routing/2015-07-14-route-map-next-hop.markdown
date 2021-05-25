---
layout: post
title:  "route-map-next-hop"
date:   2015-07-14 12:26:38 +0300
categories: routing
tags: routing
---

# route-map-next-hop
This command sets the next-hop address for an incoming packet regardless of any explicit route for the packet. 

It is similar to the set ip default next-hop command except that a next-hop address specified with this command cannot be overridden by an explicit route.

 This command should be used in conjunction with the ip policy route-map command. 

The IP address does not have to be an address that is adjacent to the router.



The set ip default next-hop command verifies the existence of the destination IP address in the routing table, and…

    if the destination IP address exists, the command does not policy route the packet, but forwards the packet based on the routing table.
    if the destination IP address does not exist, the command policy routes the packet by sending it to the specified next hop.

The set ip next-hop command verifies the existence of the next hop specified, and…

    if the next hop exists in the routing table, then the command policy routes the packet to the next hop.
    if the next hop does not exist in the routing table, the command uses the normal routing table to forward the packet.



1. ip next-hop
2. ip default next-hop
3. default interface

Funtion:

1. ip next-hop: If next hop exist in the routing table then it will policy route the traffic to the next hop otherwise according to the default routing table.
2. ip default next-hop: If the destination exist in the routing table then it will not policy route the traffic and if destination does not exist in the routing table then it will policy route the same.
3. default interface: As same as default next-hop, i.e If the destination exist in the routing table then it will not policy route the traffic and if destination does not exist in the routing table then it will policy route the same over the specified interface.

 


В данной статье мы рассмотрим работу PBR с двумя командами set ip default next-hop и set ip next-hop. Команда set ip default next-hop проверяет существование адреса назначения в таблице маршрутизации и
 
    если адрес назначения существует, то команда не выполняет маршрутизацию пакета, вместо это пакет перенаправляется в соответствие таблице маршрутизации.
    если адрес назначения не существует, команда маршрутизирует пакет, посылая его на указанный next-hop.
     



Команда set ip next-hop проверяет существование указанного next-hop и
 
    если next-hop существует в таблице маршрутизации, тогда пакет направляется на этот next-hop.
    если next-hop не существует в таблице маршрутизации, пакет перенаправляется в соответствие с таблицей маршрутизации.
     




Не попадает в роут мап, вроде попадает


