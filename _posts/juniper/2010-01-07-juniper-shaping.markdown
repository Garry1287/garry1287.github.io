---
layout: post
title:  "Shaping на juniper"
date:   2010-01-07 19:22:16 +0300
categories: juniper Networking
tags: juniper
---

# Shaping на juniper

[http://www.juniper.net/documentation/en_US/junos10.4/topics/example/firewall-filter-ex-series-configuring.html](http://www.juniper.net/documentation/en_US/junos10.4/topics/example/firewall-filter-ex-series-configuring.html)

[https://kb.juniper.net/InfoCenter/index?page=content&id=KB14250](https://kb.juniper.net/InfoCenter/index?page=content&id=KB14250)



Re: Traffic Shaping and Bandwidth limitation
Options

‎01-24-2014 11:33 PM

```
set interfaces ge-0/0/1 per-unit-scheduler

set interfaces ge-0/0/1 vlan-tagging

set interfaces ge-0/0/1 unit 0 vlan-id 90

set interfaces ge-0/0/1 unit 0 family inet address 10.10.90.1/24

set class-of-service interfaces ge-0/0/1 unit 0 shaping-rate 10k
```
 

 ****Policer portion is optional but it will over ensure that user on this subnet can send and receive traffic above the specified parameters****
```
set interfaces ge-0/0/1 unit 0 family inet policer input LB-policer

set interfaces ge-0/0/1 unit 0 family inet policer output LB-policer

set firewall policer LB-policer logical-bandwidth-policer

set firewall policer LB-policer if-exceeding bandwidth-percent  100

set firewall policer LB-policer if-exceeding burst-size-limit 125k

set firewall policer LB-policer then discard
```
&deg;
Please mark this as accepted solution if it works for you

A kudos is a good way of appreciation


[https://www.juniper.net/documentation/en_US/junos/topics/concept/policer-mx-m120-m320-burstsize-determining.html](https://www.juniper.net/documentation/en_US/junos/topics/concept/policer-mx-m120-m320-burstsize-determining.html)

[https://www.juniper.net/documentation/en_US/junos13.2/topics/example/firewall-filter-ex-series-configuring.html](https://www.juniper.net/documentation/en_US/junos13.2/topics/example/firewall-filter-ex-series-configuring.html)

[http://www.juniper.net/documentation/en_US/junos12.1/topics/example/firewall-filter-stateless-example-rate-limits-based-on-destination-class.html](http://www.juniper.net/documentation/en_US/junos12.1/topics/example/firewall-filter-stateless-example-rate-limits-based-on-destination-class.html)

[http://www.juniper.net/documentation/en_US/junos12.1/topics/example/firewall-filter-stateless-example-rate-limits-based-on-destination-class.html](http://www.juniper.net/documentation/en_US/junos12.1/topics/example/firewall-filter-stateless-example-rate-limits-based-on-destination-class.html)
