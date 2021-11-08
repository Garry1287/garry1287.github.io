---
layout: post
title:  "Фильтрация мультикаст на dlink"
date:   2014-03-28 08:04:40 +0400
categories: dlink
tags: dlink
---

# multicast_filter_dlink
Здравствуйте, где можно почерпнуть информацию или вообще как запретить мультикаст на портах свичей
DES3200, DGS3200,DES3010g,DGS3100
Очень интересует подобная информация, т.к. есть пользователи за радиоканалами.

Этот профиль запрещает вещание мультикаста с абонентских портов (3028, 3200):
Код:
```
create access_profile ip destination_ip_mask 240.0.0.0 profile_id 7
config access_profile profile_id 7 add access_id auto_assign ip destination_ip 224.0.0.0 port 1-24 deny
```

А следующий запрещает подписки:
Код:
```
create cpu access_profile profile_id 2 ip destination_ip_mask 240.0.0.0
config cpu access_profile profile_id 2 add access_id 1 ip destination_ip 224.0.0.0 port 1-24 deny
```

Теперь клиент не может ни запросить группу ни организовать свое вещание. Если в сети предоставляется услуга иптв можно разрешить клиенту запрашивать определенные потоки:
Код:
```
create cpu access_profile profile_id 1 ip destination_ip_mask 255.255.248.0
config cpu access_profile profile_id 1 add access_id 1 ip destination_ip 239.1.8.0 port 1-24 permit
```

Чтобы работали CPU ACL надо выполнить команду:
Код:
enable cpu_interface_filtering

[http://forum.dlink.ru/viewtopic.php?f=2&t=147368](http://forum.dlink.ru/viewtopic.php?f=2&t=147368)




брать можно, и то и то.
в 3200 c1 есть нюанс по части limited multicast addr - либо выставляем порты/вланы в deny,

 либо создаем mcast_filter_profile и прицепляем к портам/вланам и делаем permit, иначе мультик не идет (хотя в ранних ревизиях работало и без этого).

с des1210-28/me/b2 тоже нюанс - сначала enable igmp_snooping multicast_vlan, и только потом настройки (в других железках эту команду всегда можно было ставить хоть в конец конфига), иначе не съедает блок конфига ism. 
