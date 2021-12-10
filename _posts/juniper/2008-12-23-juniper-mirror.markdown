---
layout: post
title:  "Мирроринг на juniper"
date:   2008-12-23 12:48:46 +0300
categories: juniper Networking
tags: juniper
---

# Мирроринг на juniper

[https://www.juniper.net/documentation/en_US/junos11.1/topics/concept/port-mirroring-ex-series.html](https://www.juniper.net/documentation/en_US/junos11.1/topics/concept/port-mirroring-ex-series.html)

[https://show-route.blogspot.com/2015/12/juniper-ex-port-mirroring-to-vlan.html](https://show-route.blogspot.com/2015/12/juniper-ex-port-mirroring-to-vlan.html)

[https://juniper.io.ua/s749338/nastroyka_junos_ex_4200_switching._nastroyka_vlan_na_junos_ex_4200](https://juniper.io.ua/s749338/nastroyka_junos_ex_4200_switching._nastroyka_vlan_na_junos_ex_4200)

[https://kb.juniper.net/InfoCenter/index?page=content&id=KB21200](https://kb.juniper.net/InfoCenter/index?page=content&id=KB21200)

[https://kb.juniper.net/InfoCenter/index?page=content&id=KB23027](https://kb.juniper.net/InfoCenter/index?page=content&id=KB23027)

[https://www.juniper.net/documentation/en_US/junos/topics/example/port-mirroring-local-qfx-series.html](https://www.juniper.net/documentation/en_US/junos/topics/example/port-mirroring-local-qfx-series.html)

[https://www.juniper.net/documentation/en_US/junos/topics/concept/port-mirroring-ex-series.html#port-mirror-terminology](https://www.juniper.net/documentation/en_US/junos/topics/concept/port-mirroring-ex-series.html#port-mirror-terminology)

[https://www.juniper.net/documentation/en_US/junos/topics/concept/port-mirroring-ex-series.html](https://www.juniper.net/documentation/en_US/junos/topics/concept/port-mirroring-ex-series.html)

```
 set ethernet-switching-options analyzer employee-monitor input ingress interface ge-0/0/0.0
set ethernet-switching-options analyzer employee-monitor input ingress interface ge-0/0/1.0
set ethernet-switching-options analyzer employee-monitor output interface ge-0/0/10.0
```


```
p access-list e voice-record

permit udp any range any range

monitor session 1 filter ip access-group voice-record
```


1. На in льем всем
```
 set ethernet-switching-options analyzer employee-monitor input ingress interface ge-0/0/0.0
set ethernet-switching-options analyzer employee-monitor input ingress interface ge-0/0/1.0

set interfaces ge-0/0/31 unit 0 family ethernet-switching filter ouput 
```

```
set firewall family ethernet-switching filter forRKN term cust2web from destination-port 80, 443, 53
set firewall family ethernet-switching filter forRKN term cust2web  then accept
```


```
set interfaces ge-0/0/0 unit 0 family ethernet-switching filter input watch-employee
set interfaces ge-0/0/1 unit 0 family ethernet-switching filter input watch-employee
```
```
analyzer sorm-monitor {
    input {
        ingress {
            interface xe-0/0/6.0;
            interface ge-0/0/12.0;
            interface ge-0/0/15.0;
        }
        egress {
            interface xe-0/0/6.0;
            interface ge-0/0/12.0;
            interface ge-0/0/15.0;
        }
    }
    output {
        interface {
            xe-0/0/1.0;
        }
    }
}
```

## analyzer sorm-rkn

```
set ethernet-switching-options analyzer sorm-monitor input ingress interface xe-0/0/6.0
set ethernet-switching-options analyzer sorm-monitor input ingress interface ge-0/0/12.0
set ethernet-switching-options analyzer sorm-monitor input ingress interface ge-0/0/15.0
set ethernet-switching-options analyzer sorm-monitor input egress interface xe-0/0/6.0
set ethernet-switching-options analyzer sorm-monitor input egress interface ge-0/0/12.0
set ethernet-switching-options analyzer sorm-monitor input egress interface ge-0/0/15.0
set ethernet-switching-options analyzer sorm-monitor output vl92
```



```
enable rspan
create vlan vlanid 100 
config mirror port 50 add source ports 1 both
enable miror
config vlan vlanid 100 name RSPAN_VLAN  
create rspan vlan vlan_name RSPAN_VLAN 
config rspan vlan vlan_name RSPAN_VLAN source add ports 1 both
```

```
create mirror group_id 1
config mirror group_id 1 target_port 5 
config mirror group_id 1 state enable
config mirror group_id 1 add source ports 9,21-22 rx 
config mirror group_id 1 add source ports 9,21-22 tx 
enable mirror
```

```
create vlan rspanvlan tag 4094
config vlan rspanvlan add tagged 21,22
create rspan vlan vlan_name rspanvlan
config rspan vlan vlan_name rspanvlan redirect add port 22
enable rspan
```
```
enable rspan
create vlan rspanvlan tag 93
create rspan vlan vlan_name rspanvlan
config rspan vlan vlan_name rspanvlan source add ports 9,21-22 both
config mirror port 5
enable mirror
```

```
config vlan rspanvlan add 
```


```
garry@ctd-s2# run show interfaces xe-0/0/1    
Physical interface: xe-0/0/1, Enabled, Physical link is Up
  Interface index: 135, SNMP ifIndex: 623
  Description: SORM 10G port
  Link-level type: Ethernet, MTU: 9216, Speed: 10Gbps, Duplex: Full-Duplex, BPDU Error: None, MAC-REWRITE Error: None, Loopback: Disabled, Source filtering: Disabled,
  Flow control: Enabled
  Device flags   : Present Running
  Interface flags: SNMP-Traps Internal: 0x0
  Link flags     : None
  CoS queues     : 8 supported, 8 maximum usable queues
  Current address: 3c:8a:b0:1f:1a:84, Hardware address: 3c:8a:b0:1f:1a:84
  Last flapped   : 2018-07-19 13:19:30 GMT-3 (5w6d 21:14 ago)
  Input rate     : 0 bps (0 pps)
  Output rate    : 910322048 bps (180873 pps)
```


```
  ip access-list extended ACL_RADIUS
 permit udp any range 1645 1646 any
 permit udp any range 1812 1813 any
!
monitor session 1 source interface Gi1/0/1
monitor session 1 destination remote vlan 190
monitor session 1 filter ip access-group ACL_RADIUS
no mac address-table learning vlan 190
```

```
ip access-list standard Capture_ACL
  permit ip any host 10.1.1.1
  permit ip host 10.1.1.1 any
!
monitor session 1 source vlan 11, 12 rx
monitor session 1 destination GigabitEthernet 0/40 ingress
monitor session 1 filter ip access-group Capture_ACL
```



```
    monitor session 2 type erspan-destination
     description dest
     destination interface GigabitEthernet0/0/5
     source
      erspan-id 102
      ip address x.x.x.x

    monitor session 3 type erspan-source
     description src
     source interface GigabitEthernet0/0/7
     destination
      erspan-id 102
      ip address x.x.x.x
      origin ip address x.x.x.x


 permit udp any range 1645 1646 any
 permit udp any range 1812 1813 any
 ```
 
 [http://ciscooc.blogspot.com/2014/08/ips-deployment.html](http://ciscooc.blogspot.com/2014/08/ips-deployment.html)
 
 [http://admindoc.ru/788/spanrspan/](http://admindoc.ru/788/spanrspan/)
 
 [https://begemot-31.livejournal.com/1081.html](https://begemot-31.livejournal.com/1081.html)
 
 
 Необходимо создать ACL с описанием трафика который надо перехватить (вешать эту ACL ни на какой интерфейс НЕ НАДО)

```
7606#conf t
7606(config)#ip access-list extended test1
7606(config-ext-nacl)#permit icmp 1.1.1.0 0.0.0.255 host 2.2.2.2
7606(config-ext-nacl)#permit icmp host 2.2.2.2 1.1.1.0 0.0.0.255

7606#sh access-list test1
Extended IP access list test1
10 permit icmp 1.1.1.0 0.0.0.255 host 2.2.2.2
    20 permit icmp host 2.2.2.2 1.1.1.0 0.0.0.255
```

При необходимости, можно уточнить  нужные протоколы и порты. В данном случае пример для мониторинга результатов команды ‘ping’ между устройством с адресом 2.2.2.2 и любым устройством находящемся в сети 1.1.1.0/24 (1.1.1.0 255.255.255.0), обращаю внимание что на 7606 везде кроме адреса на инте используется так называемый ‘Wildcard mask’ который на самом деле значительно удобнее обычной маски подсети, таблица для сравнения доступна тут.

Необходимо создать ‘monitor session’ (вобщем-то сам перехватчик)

```
7606#conf t
7606(config)#monitor session 1 type capture
7606(config-mon-capture)#filter access-group test1
7606(config-mon-capture)#source interface Po1
```

Впринципе тут можно уточнить размер буфера и т.п., но данных настроек достаточно т.к. остальное циска проставит сама (размер буфера будет максимальный).
```
7606#sh run interface Po1
!
interface Port-channel1
no ip address
end
```

```
7606#sh monitor session all
Session 1
---------
Type                   : Capture Session
Capture filters        :
     acl               : test1

Egress SPAN Replication State:
Operational mode       : Distributed
Configured mode        : Distributed
```

Теперь осталось запустить это всё:

`7606#monitor capture start`

Остановить можно командой:

`7606#monitor capture stop`

Очистить содержимое перехватчика:

`7606#monitor capture clear`

Скопировать на tftp (и не только) можно командой:
```
7606#monitor capture export buffer tftp://3.3.3.3/test-ping1.pcap
Copying capture buffer of session [1] to location tftp://3.3.3.3/test-ping1.pcap
!!
7606#
```
Для удаление перехватчика:
```
7606#conf t
7606(config)#no monitor session 1
7606(config)#end

7606#sh monitor session all
 No SPAN configuration is present in the system.
```