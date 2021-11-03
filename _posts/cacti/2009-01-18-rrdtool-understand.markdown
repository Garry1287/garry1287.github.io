---
layout: post
title:  "Понимание rrdtool"
date:   2009-01-18 11:52:35 +0300
categories: cacti
tags: cacti rrdtool
---

# Понимание rrdtool
[http://telematic00.blogspot.ru/2009/03/rrdtool-snmp.html](http://telematic00.blogspot.ru/2009/03/rrdtool-snmp.html)
[http://ruunix.ru/1038-rrdtool-stroim-grafiki-na-raz-dva-tri.html](http://ruunix.ru/1038-rrdtool-stroim-grafiki-na-raz-dva-tri.html)




[http://oss.oetiker.ch/rrdtool/](http://oss.oetiker.ch/rrdtool/)
[http://www.samag.ru/archive/article/275](http://www.samag.ru/archive/article/275)
[http://www.bog.pp.ru/work/rrdtool.html](http://www.bog.pp.ru/work/rrdtool.html)
[http://habrahabr.ru/post/30655/](http://habrahabr.ru/post/30655/)
[http://ru.wikibooks.org/wiki/RRDtool](http://ru.wikibooks.org/wiki/RRDtool)
[http://www.opennet.ru/base/net/netmond_rrdtool.txt.html](http://www.opennet.ru/base/net/netmond_rrdtool.txt.html)
[http://ruunix.ru/1038-rrdtool-stroim-grafiki-na-raz-dva-tri.html](http://ruunix.ru/1038-rrdtool-stroim-grafiki-na-raz-dva-tri.html)
[http://silverwraith.com/papers/freebsd-snmp.php](http://silverwraith.com/papers/freebsd-snmp.php)
[http://www.initialize.ru/cacti-grafiki-vidaut-nan](http://www.initialize.ru/cacti-grafiki-vidaut-nan)
[http://pbsplaza.nl/?p=163](http://pbsplaza.nl/?p=163)

```
04/03/2013 11:37:02 AM - WEBLOG: Poller[0] CACTI2RRD: /usr/bin/rrdtool graph - --imgformat=PNG --start=1364888221 --end=1364974621 --title='Localhost - Processes' --base=1000 --height=120 --width=500 --alt-autoscale-max --lower-limit='0' COMMENT:"From 2013/04/02 11:37:01 To 2013/04/03 11:37:01\c" COMMENT:" \n" --vertical-label='processes' DEF:a="/usr/opt/cacti/rra/localhost_proc_7.rrd":'proc':AVERAGE AREA:a#F51D30:"Running Processes" GPRINT:a:LAST:"Current\:%8.0lf" GPRINT:a:AVERAGE:"Average\:%8.0lf" GPRINT:a:MAX:"Maximum\:%8.0lf" 
```