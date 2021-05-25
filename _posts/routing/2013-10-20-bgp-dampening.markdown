---
layout: post
title:  "bgp-dampening"
date:   2013-10-20 05:49:43 +0400
categories: routing
tags: routing
---

# bgp-dampening


в таблицу маршрутизации когда значение пенальти будет меньше reuse или по прошествии max-suppress limit времени.

 Важно обратить внимание на то, что если suppress-limit равен 2000 и маршрут флапнулся 2 раза за 10 секунд, 

то он останется в таблице маршрутизации, так как пенальти через 5 секунд будет меньше 1000, а значит и суммарное меньше 2000.


bgp dampening half-life reuse suppress-limit max-suppress [route-map map-name]

half-life
reuse
suppress-limit
max-suppress


route-map DAMP permit 10
set dampening 20 950 2500 80



Half-lie-time — время, которое должно пройти с момента поднятия линка и ведущее к снятию пенальти.(по умолчанию 15 минут)
Supress-Limit — Если значение пенальти становится больше значения Supress-Limit то такой маршрут считается недостижимым и отбрасывается.
Reuse Limit — Если Пенальти становится меньше Reuse Limit и линк в состоянии UP, то с него снимается Supressed и он снова распростроняется. (по умолчанию 750)

Значение пенальти уменьшается каждые 5 секунд на значение 
(penalty / half-life(в секундах) )*5.

Пример




Penalty — количество очков, которое плюсуется когда роутер начинает флапать. (по умолчанию прибавляется по 1000)
Suppressed — маршрут, который не анонсируется, даже если линк в состоянии UP.



[http://admindoc.ru/1254/bgp-route-dampening/](http://admindoc.ru/1254/bgp-route-dampening/)
[https://dharmaroute.wordpress.com/2010/09/07/bgp-optimization-on-the-edge-dam/](https://dharmaroute.wordpress.com/2010/09/07/bgp-optimization-on-the-edge-dam/)











STAGDOK-CE0#sh ip bgp 10.222.1.1
BGP routing table entry for 10.222.1.1/32, version 310
Paths: (1 available, no best path)
Flag: 0x820
  Not advertised to any peer
  20866 65062 (history entry)
    10.192.10.157 from 10.192.10.157 (81.20.204.97)
      Origin IGP, localpref 100, external
      Dampinfo: penalty 2953, flapped 3 times in 00:01:05


STAGDOK-CE0#sh ip bgp dampening flap-statistics 
BGP table version is 312, local router ID is 10.192.10.158
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale
Origin codes: i - IGP, e - EGP, ? - incomplete

   Network          From            Flaps Duration Reuse    Path
 h 10.222.1.1/32    10.192.10.157   4     00:02:11          20866 65062 




STAGDOK-CE0#sh ip bgp dampening flap-statistics 
BGP table version is 312, local router ID is 10.192.10.158
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale
Origin codes: i - IGP, e - EGP, ? - incomplete

   Network          From            Flaps Duration Reuse    Path
*d 10.222.1.1/32    10.192.10.157   4     00:04:41 00:06:19 20866 65062 
STAGDOK-CE0#sh ip bgp dampening flap-statistics 
BGP table version is 312, local router ID is 10.192.10.158
Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
              r RIB-failure, S Stale
Origin codes: i - IGP, e - EGP, ? - incomplete

   Network          From            Flaps Duration Reuse    Path
*d 10.222.1.1/32    10.192.10.157   4     00:04:48 00:06:09 20866 65062 
STAGDOK-CE0#sh ip route  10.222.1.1             
% Subnet not in table
STAGDOK-CE0#sh ip route  10.222.1.1
% Subnet not in table
STAGDOK-CE0#sh ip bgp 10.222.1.1                
BGP routing table entry for 10.222.1.1/32, version 312
Paths: (1 available, no best path)
  Not advertised to any peer
  20866 65062, (suppressed due to dampening)
    10.192.10.157 from 10.192.10.157 (81.20.204.97)
      Origin IGP, localpref 100, valid, external
      Dampinfo: penalty 3445, flapped 4 times in 00:05:00, reuse in 00:05:59
