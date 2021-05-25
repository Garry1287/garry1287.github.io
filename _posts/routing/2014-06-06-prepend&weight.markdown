---
layout: post
title:  "prepend&weight"
date:   2014-06-06 22:23:12 +0400
categories: routing
tags: routing
---

# prepend&weight
Изменение weight с помощью route-map:

route-map <name> permit <sequence>
 match <condition>
 set weight <weight>

Применение route-map:

router bgp 65000
 neighbor <ip-address> route-map <name> in







router bgp 1

neighbor 1.2.3.4 remote-as 1

neighbor 1.2.3.4 next-nop-self

neighbor 1.2.3.4 route-map WEIGHT in


route-map WEIGHT permit 10

match community 1:1

set weight 10000


ip prefix-list video_nets seq 10 permit 10.186.0.0/24 le 32
ip prefix-list video_nets seq 20 permit 192.168.253.0/24 le 32
ip prefix-list video_nets seq 30 permit 10.29.18.0/24 le 32
ip prefix-list video_nets seq 40 permit 10.29.19.0/24 le 32
ip prefix-list video_nets seq 100 deny 0.0.0.0/0 le 32


access-list 1 permit 170.10.0.0 0.0.255.255

ip access-list extended VIDEO_NETS
 permit ip  any
 permit ip host 172.19.7.146 any
 permit ip host 172.19.7.154 any
 permit ip host 172.19.7.148 any
 permit ip host 172.19.7.149 any


 ----------------------------------------------------------------------------------------------------------
   neighbor 10.192.10.157 route-map SETWEIGHT in
 neighbor 10.192.10.157 route-map ADDPREPEND_VIDEO out

 ip access-list extended OUR_VIDEO_NET
 permit ip 10.222.255.0 0.0.0.255 any
ip access-list extended VIDEO_NETS
 permit ip 10.186.0.0 0.0.0.255 any
 permit ip 192.168.253.0 0.0.0.255 any
 permit ip 10.29.18.0 0.0.0.255 any
 permit ip 10.29.19.0 0.0.0.255 any

    
route-map SETWEIGHT permit 10
 match ip address VIDEO_NETS
 set weight 100
!         
route-map SETWEIGHT permit 20
 set weight 0

 
route-map ADDPREPEND_VIDEO permit 10
 match ip address OUR_VIDEO_NET
 set as-path prepend 65062 65062
!         
route-map ADDPREPEND_VIDEO permit 20

  
  
  
  
  
  
  
  
  
 neighbor 10.192.10.157 route-map SETWEIGHT in

 
 ip access-list extended VIDEO_NETS
 permit ip 10.186.0.0 0.0.0.255 any
 permit ip 192.168.253.0 0.0.0.255 any
 permit ip 10.29.18.0 0.0.0.255 any
 permit ip 10.29.19.0 0.0.0.255 any

 
 route-map SETWEIGHT permit 10
 match ip address VIDEO_NETS
 set weight 100
!
route-map SETWEIGHT permit 20
 set weight 0

 
 
 
  ip access-list extended OUR_VIDEO_NET
 permit ip 10.98.1.0 0.0.0.255 any
 
 
 
 
   ip access-list extended OUR_VIDEO_NET
 permit ip  10.222.255.0 0.0.0.255 any

  route-map ADDPREPEND_VIDEO permit 10
 match ip address OUR_VIDEO_NET
 set as-path prepend 65062 65062
!
route-map ADDPREPEND_VIDEO permit 20
 
 
 
