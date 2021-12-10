---
layout: post
title:  "Pim в juniper"
date:   2011-03-27 16:51:43 +0400
categories: juniper Networking
tags: juniper
---

# Pim в juniper вместе с ospf

## Pim
[https://forum.nag.ru/index.php?/topic/136208-juniper-mx80-prodakshn-konfig-igmppim/](https://forum.nag.ru/index.php?/topic/136208-juniper-mx80-prodakshn-konfig-igmppim/)

[http://juniper-exam.ru/wiki/%D0%93%D0%BB%D0%B0%D0%B2%D0%B0_3._Routing_protocols_(DVMRP](http://juniper-exam.ru/wiki/%D0%93%D0%BB%D0%B0%D0%B2%D0%B0_3._Routing_protocols_(DVMRP),_PIM-DM,_PIM-SM)

[https://3-4-5-6.blogspot.com/2012/02/configuring-multicasting-with-juniper.html](https://3-4-5-6.blogspot.com/2012/02/configuring-multicasting-with-juniper.html)


## Juniper OSPF proccess

[https://habr.com/ru/post/275119/](https://habr.com/ru/post/275119/)

[http://subnets.ru/blog/?p=1642](http://subnets.ru/blog/?p=1642)

[https://forums.juniper.net/t5/Routing/Multiple-OSPF-processes/m-p/4156#M142](https://forums.juniper.net/t5/Routing/Multiple-OSPF-processes/m-p/4156#M142)


----

 Re: Multiple OSPF processes
‎06-30-2008 06:28 AM

Hi Tiziano,

 

routing-instances are definitely the way to go.  You can create a routing-instance for each of the OSPF "processes" you want.  Each of those routing-instances will have associated interfaces.  You can then configure OSPF within the routing-instance and associate the interfaces with the OSPF area.  Then you should be able to see the neighbours with...

 
```
show ospf neighbor instance $your-instance-name$
```
 

...and the routing table for your instance with... 

 
```
show route table $your-instance-name$.inet.0
```
 

You may want to exchange routing information with the main routing-instance by using rib-groups.  You can do the following...

 
```
routing-options {

    rib-groups {

        my-rib {

            import-ribs [ my-instance.inet.0 inet.0 ];

        }

    }

}

routing-instances {

    my-instance {

        interface so-0/0/0.0;

        interface ge-1/0/0.0; 

        rib-group my-rib;

        protocols {

            ospf {

                area 0.0.0.0 {

                    interface so-0/0/0.0;

                    interface ge-1/0/0.0;

                }

            }

        }

    }

}
```
 

I hope that gives you some pointers. 
