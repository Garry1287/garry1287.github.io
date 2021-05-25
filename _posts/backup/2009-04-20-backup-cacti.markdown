---
layout: post
title:  "backup-cacti"
date:   2009-04-20 17:16:06 +0400
categories: backup-cacti
tags: backup-cacti
---

# backup-cacti
Backup Cacti
[http://www.k4route.ru/2010/01/cacti-backup-script.html](http://www.k4route.ru/2010/01/cacti-backup-script.html)
[http://www.vgnet.nl/knowledge/monitoring/cacti](http://www.vgnet.nl/knowledge/monitoring/cacti)



DB Mysql
/usr/local/cacti

/var/lib/cacti/cli
/var/lib/cacti/scripts

Отдельный скрипт на 
/var/lib/cacti/rra

/etc


Остановить поллер и запустить репликация /var/lib/cacti/rra


Stop the Poller

Now it’s time to stop the Cacti poller. Go to Console->Settings then hit the “Poller” tab and uncheck the “Enabled” box.

Copy RRD files

Now that the poller is stoped, we can copy the RRD files.

mv  /var/www/html/cacti/rra/* /var/www/html/cacti-0.8.8a/rra/





--_traffic_in_870.rrd