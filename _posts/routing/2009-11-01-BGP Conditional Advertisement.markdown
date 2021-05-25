---
layout: post
title:  "BGP Conditional Advertisement"
date:   2009-11-01 05:35:19 +0300
categories: routing
tags: routing
---

# BGP Conditional Advertisement
[https://sites.google.com/site/amitsciscozone/home/bgp/bgp-conditional-advertisement](https://sites.google.com/site/amitsciscozone/home/bgp/bgp-conditional-advertisement)
[http://hackingcisco.blogspot.ru/2011/05/lab-118-bgp-conditional-route.html](http://hackingcisco.blogspot.ru/2011/05/lab-118-bgp-conditional-route.html)
[http://lostintransit.se/2011/04/05/conditional-bgp-advertisement-with-advertise-map/](http://lostintransit.se/2011/04/05/conditional-bgp-advertisement-with-advertise-map/)


neighbor <neighbor-ip-address> advertise-map <map1> non-exist-map <map2>
1)map2 - если находится совпадение, то статус "withdraw", если не находит, то статус Advertise
2)map1 -  префикс(ы) объявляются, если в первом пункте Adversite

neighbor <neighbor-ip-address> advertise-map <map1> exist-map <map2>
1)map2 - если находится совпадение, то статус  Advertise , если не находит, то статус "withdraw"
2)map1 -  префикс(ы) объявляются, если в первом пункте Adversite



В нашем случае следовало бы использовать non-exist-map 
non-exist-map должен содержать префиксы известный сайтов, сетей (яндекс, вк и т. д.)
Если мы их прекращаем видеть со стороны Мегафона - основной канал (то есть канал упал)
То начинаем объявлять в сторону РЕТН наши сети.

neighbor RETN_BGPPEER_IP advertise-map OUR_NETS non-exist-map VK_YA_MEGAFON
