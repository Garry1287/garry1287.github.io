---
layout: post
title:  "virtual-reassembly"
date:   2010-01-16 11:20:55 +0300
categories: virtual-reassembly
tags: cisco
---

# virtual-reassembly
Feb 19 08:59:18: %IP_VFR-4-FRAG_TABLE_OVERFLOW: GigabitEthernet0/0: the fragment table has reached its maximum threshold 16
Feb 19 09:11:07: %IP_VFR-4-FRAG_TABLE_OVERFLOW: GigabitEthernet0/0: the fragment table has reached its maximum threshold 16


Насколько я понимаю, идея этих ограничений - не дать злоумышленнику забить всю память фрагментами пакетов. Так что я бы исходила из того, сколько под это не жалко памяти. Дефолтные значения 16 и 32 дают нам оценку сверху (допустим, что фрагменты будут большие, поскольку это выгодно атакующему) 16*32*1500 / 1024 = 750KB.
С предложенными значениям мы получаем величину в 128 раз больше дефолтной (т.е. примерно 94MB). Сколько у Вас там свободной памяти? 



[http://sergeyn.blogspot.ru/2009/03/ipvfr-4-fragtableoverflow.html](http://sergeyn.blogspot.ru/2009/03/ipvfr-4-fragtableoverflow.html)
[http://www.cisco.com/en/US/docs/ios/12_3t/12_3t8/feature/guide/gt_vfrag.html](http://www.cisco.com/en/US/docs/ios/12_3t/12_3t8/feature/guide/gt_vfrag.html)

debug ip virtual-reassembly

no debug ip virtual-reassembly 



ip virtual-reassembly [max-reassemblies number] [max-fragments number] [timeout seconds] [drop-fragments] 



 max-reassemblies 
	
Число ip пакетов которые могут быть собраны в заданное времы
(Optional) Maximum number of IP datagrams that can be reassembled at any given time. Default value: 64.
If the maximum value is reached, all fragments within the following fragment set will be dropped and an alert message will be logged to the syslog server.

max-fragments 
Число фрагметов которые разрешено для одного пакета
(Optional) Maximum number of fragments that are allowed per IP datagram (fragment set). Default value: 16.
If an IP datagram that is being reassembled receives more than the maximum allowed fragments, the IP datagram will be dropped and an alert message will be logged to the syslog server.

timeout seconds
(Optional) Timeout value, in seconds, for an IP datagram that is being reassembled. Default value: 3 seconds.
If an IP datagram does not receive all of the fragments within the specified time, the IP datagram (and all of its fragments) will be dropped.

drop-fragments
(Optional) Enables the VFR to drop all fragments that arrive on the configured interface. By default, this function is disabled. 








initial fragment— First fragment within a fragment set. This fragment should have a Layer 4 header and should have an offset of zero. 
