---
layout: post
title:  "firewall-vienna"
date:   2017-03-09 10:05:45 +0300
categories: zavod
tags: zavod
---

# firewall-vienna
access-list outside_access_in extended permit ip any any 
access-list outside_access_in extended permit tcp any any 
access-list outside_access_in extended permit udp any any 
access-list outside_access_in extended permit icmp any any 
access-list inside_access_in extended permit ip any any 
access-list inside_access_in extended permit tcp any any 
access-list inside_access_in extended permit udp any any 
access-list inside_access_in extended permit icmp any any 


access-list outside_access_in extended permit ip 172.19.5.101 10.170.0.37
access-list outside_access_in extended permit ip 10.186.4.51 10.186.4.51
access-list outside_access_in extended deny ip any 10.170.0.37
access-list outside_access_in extended deny ip any 10.170.0.55
access-list outside_access_in extended deny ip any 10.170.0.56
access-list outside_access_in extended deny ip any 10.170.0.57
access-list outside_access_in extended deny ip any 10.170.0.61
access-list outside_access_in extended deny ip any 10.170.0.62
access-list outside_access_in extended deny ip any 10.170.0.85
access-list outside_access_in extended deny ip any 10.170.0.109
access-list outside_access_in extended permit ip any any 

access-list inside_access_in extended permit ip 10.170.0.37 172.19.5.101
access-list inside_access_in extended permit ip 10.170.0.109 10.186.4.51
access-list inside_access_in extended deny ip 10.170.0.37 any
access-list inside_access_in extended deny ip 10.170.0.55 any
access-list inside_access_in extended deny ip 10.170.0.56 any
access-list inside_access_in extended deny ip 10.170.0.57 any
access-list inside_access_in extended deny ip 10.170.0.61 any
access-list inside_access_in extended deny ip 10.170.0.62 any
access-list inside_access_in extended deny ip 10.170.0.85 any
access-list inside_access_in extended deny ip 10.170.0.109 any
access-list inside_access_in extended permit ip any any



outside - смотрит в интернет
inside - в локалку
( У нас наоборот)

[http://deltaconfig.ru/cisco-asa-internet-access/](http://deltaconfig.ru/cisco-asa-internet-access/)

Действие 1, отменяем старые правила
no access-group inside_access_in in interface inside
no access-group outside_access_in in interface outside

2. Создаем object-group
object-group network VIENNA_GROUP_HOSTS
network-object host 10.170.0.37
network-object host 10.170.0.55
network-object host 10.170.0.56
network-object host 10.170.0.57
network-object host 10.170.0.61
network-object host 10.170.0.62
network-object host 10.170.0.85
network-object host 10.170.0.109

3.Создаем новый access-list
no access-list inside_access_in 

access-list inside_access_in extended permit ip host 172.19.5.101 host 10.170.0.37
access-list inside_access_in extended permit ip host 10.186.4.51 host 10.170.0.109
access-list inside_access_in extended deny ip any object-group VIENNA_GROUP_HOSTS
access-list inside_access_in extended permit ip any any 


no access-list outside_access_in extended permit ip any any
no access-list outside_access_in extended permit tcp any any
no access-list outside_access_in extended permit udp any any
no access-list outside_access_in extended permit icmp any any

access-list outside_access_in extended permit ip host 10.170.0.37 host 172.19.5.101
access-list outside_access_in extended permit ip host 10.170.0.109 host 10.186.4.51
access-list outside_access_in extended deny ip object-group VIENNA_GROUP_HOSTS any
access-list outside_access_in extended permit ip any any

4.
access-group inside_access_in in interface inside
access-group outside_access_in in interface outside
