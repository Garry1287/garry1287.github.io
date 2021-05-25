---
layout: post
title:  "bgp-nlmk-change"
date:   2018-03-04 19:55:52 +0300
categories: routing
tags: routing
---

# bgp-nlmk-change
1.В поиске вбиваем 81.20.194.0
[https://apps.db.ripe.net/search/query.htm](https://apps.db.ripe.net/search/query.htm)

videint0

меняем 
descr:          RU-INTELECOM-NET-194             на RU-NLMK-NET
origin:         AS20866				на 60833


2. Ломается инет у комбината, когда обновляются фильтры, которые создаются из route object
Узнаем по крикам и по анонсированию этой сети. Она не должна анонсироваться во внешний мир
Например на rviews или на lg.retn.net lg.starttelecom.ru

3. Разрешаем на k9-c0 в prefix list 194 сеть анонсировать по ibgp на ctd-c6 

ip prefix-list ibgp-neigb-out seq 5 permit 81.20.194.0/24 le 32

4. На ctd-c6 видим, что префикс пришел от нейбора

sh ip bgp neighbors 81.20.192.79 routes

должна быть 194 сеть 

5. Убираем 
router bgp 20866
  no network 81.20.194.0 mask 255.255.255.0

6.Смотрим на lg.retn.net чтобы aspath был таким
20866 60833 I 

Если так, то всё ок

7. Можно наверно по rviews увидеть тоже самое
8. Повторить всё тоже самое со Старттелекомом
9. Убить статик
10. Сделать редистрибьюцию из bgp в ospf
(нужна информация о 81.20.194.0 для нашей внутренний сети)


redistribute bgp 20866 metric 1 metric-type 1 subnets prefix-list nlmk-194-in


В принципе этого достаточно, так как других сетей нет, но думаю 
надо префикс листом отфильтровать, разрешая только 194 сеть

nlmk-194-in


ip prefix-list nlmk-194-in seq 5 permit 81.20.194.0/24 le 32
ip prefix-list nlmk-194-in seq 20 deny 0.0.0.0/0 le 32



router ospf 110
 redistribute connected metric 1 metric-type 1 subnets
 redistribute static metric 1 metric-type 1 subnets
 redistribute bgp 65022 metric 1 metric-type 1 subnets
 passive-interface default
 no passive-interface GigabitEthernet0/1
 network 10.98.98.0 0.0.0.255 area 0


