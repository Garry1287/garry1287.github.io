---
layout: post
title:  "ospf-about"
date:   2010-10-28 15:28:47 +0400
categories: routing
tags: routing
---

# ospf-about
DR и BDR

Для уменьшения сетевого траффика в каждой зоне выбираются выделенный (designated router (DR)) 
и резервный (backup designated router (BDR)) роутеры, с которыми и общаются все остальные роутеры зоны.

Не только в зоне, а в отдельной подсети. Ведь процесс обмена идёт путём multicast
Поэтому хотя по факту все вроде в одной area 0, но фактически получается несколько area (каждай подсеть)












OSPF Subnets


It is used when pulling routes into OSPF.  So lets imagine you are redistributing routes from EIGRP into OSPF.  
Imagine if we had the following routes in the routing table that were learned from EIGRP process 1.

 

172.16.0.0/16

172.17.1.0/24

172.17.2.0/24

172.17.3.0/24

 

Now if I want to redistribute into OSPF that might look like the following.

 

router ospf 1

redistribute eigrp 1 subnets

 

--or--

 

router ospf 1

redistribute eigrp 1

 

Without the "subnets" keyword, only the first route (172.16.0.0/16) would be redistributed. 
Whose other routes are not classful routes, they're subnets. Therefore they would not be redistributed without the "subnets" keyword. 
Now keep in mind that if we leave auto-summarization enabled, 
eigrp will automatically install a classful null route as a summary for anything that it has as an eigrp route.
