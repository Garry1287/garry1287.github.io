---
layout: post
title:  "Access-list на коммутаторе dlink"
date:   2016-09-14 06:47:37 +0300
categories: dlink
tags: dlink
---

# dlink-access-list
Количество пакетов в секунду (PPS)


```
create access_profile  ip  source_ip 255.255.255.255 tcp dst_port_mask 0xFFFF    profile_id 30
config access_profile profile_id 30  add access_id 1  ip  source_ip 192.168.1.35 tcp dst_port 135  port 1-28 deny
config access_profile profile_id 30  add access_id 3  ip  source_ip 192.168.1.35 tcp dst_port 138  port 1-28 deny
config access_profile profile_id 30  add access_id 4  ip  source_ip 192.168.1.35 tcp dst_port 139  port 1-28 deny
config access_profile profile_id 30  add access_id 5  ip  source_ip 192.168.1.35 tcp dst_port 445  port 1-28 deny
config access_profile profile_id 30  add access_id 6  ip  source_ip 192.168.1.35 tcp dst_port 22  port 1-28 deny
config access_profile profile_id 30  add access_id 7  ip  source_ip 192.168.1.35 tcp dst_port 21  port 1-28 deny
config access_profile profile_id 30  add access_id 8  ip  source_ip 192.168.1.35 tcp dst_port 20  port 1-28 deny
config access_profile profile_id 30  add access_id 9  ip  source_ip 192.168.1.35 tcp dst_port 25  port 1-28 deny
config access_profile profile_id 30  add access_id 10  ip  source_ip 192.168.1.35 tcp dst_port 143  port 1-28 deny
config access_profile profile_id 30  add access_id 11  ip  source_ip 192.168.1.35 tcp dst_port 110  port 1-28 deny
create access_profile  ip  source_ip 255.255.255.255 udp dst_port_mask 0xFFFF    profile_id 40
config access_profile profile_id 40  add access_id 1  ip  source_ip 192.168.1.35 udp dst_port 135  port 1-28 deny
config access_profile profile_id 40  add access_id 3  ip  source_ip 192.168.1.35 udp dst_port 138  port 1-28 deny
config access_profile profile_id 40  add access_id 4  ip  source_ip 192.168.1.35 udp dst_port 139  port 1-28 deny
config access_profile profile_id 40  add access_id 5  ip  source_ip 192.168.1.35 udp dst_port 445  port 1-28 deny
disable cpu_interface_filtering
```
