---
layout: post
title:  "Juniper EX4200 - восстановление после ошибки  error: could not copy to juniper.save+"
date:   2018-12-20 17:31:15 +0300
categories: networking
---


## Juniper EX4200 - восстановление после ошибки  error: could not copy to juniper.save+ 


```
run file list /var/rundb/ detail 

/var/rundb/:
total blocks: 199412
-rw-r-----  1 root  config         0 Sep 3   2017 .db_lock
drwxrwxr-x  2 root  operator       512 Sep 3   2017 .snap/
-rw-r--r--  1 root  config   1048576 Dec 20 13:01 chassisd.dynamic.db
-rw-r-----  1 root  config  22544384 Dec 20 13:01 juniper.data
-rw-r-----  1 root  config  24641536 Dec 20 16:11 juniper.data+
-rw-r-----  1 root  config  24641536 Dec 20 16:52 juniper.db
-rw-r-----  1 root  config   2621440 Sep 3   2017 juniper.dyn
-rw-r-----  1 root  config  22544384 Dec 20 13:01 juniper.save
drwxr-xr-x  2 root  config       512 Sep 3   2017 private/
-rw-r-----  1 root  config  16777216 Sep 3   2017 schema.db
drwxr-xr-x  3 root  config       512 Sep 3   2017 sdb/
total files: 8
```

Попробую удалить juniper.data+ и по инструкции.
Думаю делать ночью или когда кто-то будет на ЦТД

* [http://juniper.ucoz.ru/index/file_from_server/0-43](http://juniper.ucoz.ru/index/file_from_server/0-43)
* [http://prostoblog-unit.blogspot.com/2016/06/junos.html](http://prostoblog-unit.blogspot.com/2016/06/junos.html)


```
 Here's what I would do (while connected via console!)

 

1. show configuration | no-more | save current-config
(I'd also recommend to take a local backup to your workstation as well, just in case)

 

2. start shell user root
<enter password>

 

3. cd /config
 

4. rm -f juniper.conf+
 

5. exit from shell
 

6. enter configuration mode and do a 'load override current-config' & commit
```
