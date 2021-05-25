---
layout: post
title:  "BIGtelecom"
date:   2018-01-23 06:32:01 +0300
categories: routing
tags: routing
---

# BIGtelecom
interface TenGigabitEthernet0/3/0.1042
 bandwidth 307200
 description #Bigtelecom
 encapsulation dot1Q 1042
 ip address 81.20.192.149 255.255.255.252
 ip flow ingress
 ip flow egress
 service-policy input BIGTELECOM-Policy-300  
 service-policy output BIGTELECOM-Policy-300                                                                                                                                                                                                                                                                             
end         


          


policy-map BIGTELECOM-Policy-300
 class RETN-Policy
  police cir 307200000 bc 57600000 be 115200000

    

AS196770
AS-SET AS-BIGTELECOM-LIPETSK
194.0.68.0/22


% Information related to '194.0.68.0/22AS196770'

route:          194.0.68.0/22
descr:          JSC "BIG Telecom Lipetsk"
origin:         AS196770
mnt-by:         MNT-BIGTELECOM-LIPETSK
source:         RIPE # Filtered


as-set:         AS-BIGTELECOM-LIPETSK
descr:          BIG Telecom Lipetsk ASes
members:        AS196770, AS15672
tech-c:         DF1791-RIPE
admin-c:        DF1791-RIPE
mnt-by:         MNT-BIGTELECOM-LIPETSK
source:         RIPE # Filtered



Отправлять всё кроме LES
ip prefix-list deny_lesnets_from_uplinks seq 10 deny 195.34.224.0/19 ge 20
ip prefix-list deny_lesnets_from_uplinks seq 12 deny 95.179.0.0/17 le 21
ip prefix-list deny_lesnets_from_uplinks seq 13 deny 178.234.0.0/16 le 21
ip prefix-list deny_lesnets_from_uplinks seq 50 permit 0.0.0.0/0 le 32










ip prefix-list bigtelecom_net seq 10 permit 194.0.68.0/22 le 32
ip prefix-list bigtelecom_net seq 50 deny 0.0.0.0/0 le 32


neighbor 81.20.192.150 shutdown
neighbor 81.20.192.150 remote-as 196770

address-family ipv4
neighbor 81.20.192.150 activate
neighbor 81.20.192.150 prefix-list deny_lesnets_from_uplinks out
neighbor 81.20.192.150 prefix-list bigtelecom_net in
neighbor 81.20.192.150 default-originate


 
ip prefix-list default seq 10 permit 0.0.0.0/0
ip prefix-list default seq 20 deny 0.0.0.0/0 ge 1



ip prefix-list adv-to-megafon seq 20 permit 194.0.68.0/22 le 32






Добавить в AS-SET AS-INTELECOM как members AS196770

И в aut-num:AS20866 добавить 
import:         from AS196770 action pref=100; accept AS196770
export:         to AS31133 announce AS-BIGTELECOM-LIPETSK
(Хотя там нет комбината и индезита), скорее всего фильтры по AS-SET работают
