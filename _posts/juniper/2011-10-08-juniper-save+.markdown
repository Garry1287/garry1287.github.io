---
layout: post
title:  "juniper-save+"
date:   2011-10-08 20:42:52 +0400
categories: juniper
tags: juniper
---

# juniper-save+
---
layout: post
title:  "Juniper EX4200 - восстановление после ошибки  error: could not copy to juniper.save+"
date:   2018-12-20 17:31:15 +0300
categories: networking
---


##Juniper EX4200 - восстановление после ошибки  error: could not copy to juniper.save+ 


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

*[[http://juniper.ucoz.ru/index/file_from_server/0-43](http://juniper.ucoz.ru/index/file_from_server/0-43)]([http://juniper.ucoz.ru/index/file_from_server/0-43)](http://juniper.ucoz.ru/index/file_from_server/0-43))
*[[http://prostoblog-unit.blogspot.com/2016/06/junos.html](http://prostoblog-unit.blogspot.com/2016/06/junos.html)]([http://prostoblog-unit.blogspot.com/2016/06/junos.html)](http://prostoblog-unit.blogspot.com/2016/06/junos.html))


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





configuration mode # 	commit confirmed <время_в_минутах>

Применяет кандидатскую конфигурацию на указанное количество минут (по умолчанию (если не указывать количество минут) на 10). По истечению времени происходит откат на предыдущую конфигурацию. Для применения конфигурации (перевода ее из временной в постоянную) необходимо ввести команду «commit» или «commit check»
ВНИМАНИЕ! Повторный ввод команды «commit confirmed» не приведет к сбросу времени. Вместо этого, временная конфигурация будет подтверждена (как при подтверждении временной конфигурации командой «commit» или «commit check»), а временной конфигурацией станет кандидатская (на момент повторного ввода «commit confirmed») конфигурация, даже если никаких изменений не проводилось (в таком случае временной станет «нулевая» конфигурация).


% ls -al
total 156052
drwxrwxrwt   5 root  config         512 Feb 14 16:25 .
drwxr-xr-x  31 root  wheel          512 Jan 21  2013 ..
-rw-r-----   1 root  config           0 Sep  3  2017 .db_lock
drwxrwxr-x   2 root  operator       512 Sep  3  2017 .snap
-rw-r--r--   1 root  config     1048576 Dec 20 13:01 chassisd.dynamic.db
-rw-r-----   1 root  config    22544384 Dec 20 13:01 juniper.data
-rw-r-----   1 root  config    24641536 Feb 14 16:26 juniper.db
-rw-r-----   1 root  config     2621440 Sep  3  2017 juniper.dyn
-rw-r-----   1 root  config    22544384 Dec 20 13:01 juniper.save
drwxr-xr-x   2 root  config         512 Sep  3  2017 private
-rw-r-----   1 root  config    16777216 Sep  3  2017 schema.db
drwxr-xr-x   3 root  config         512 Sep  3  2017 sdb



aviva@router1# commit confirmed
commit confirmed will be automatically rolled back in 10 minutes unless confirmed
commit complete

Чтобы сделать временную активацию постоянной, запустите следующую команду:

[edit]
aviva@router1# commit

[http://juniper.ucoz.ru/index/temp_commit/0-41](http://juniper.ucoz.ru/index/temp_commit/0-41)


Перегрузка оборудования
root@juniper> request system reboot

Удаление ненужных файлов
root@juniper> request system storage cleanup

Откат конфигураций
root@juniper# rollback {откат на последнюю конфигурацию}

[http://juniper.ucoz.ru/index/reserv_copy/0-45](http://juniper.ucoz.ru/index/reserv_copy/0-45)
[http://juniper-rus.blogspot.com/2012/10/2.html](http://juniper-rus.blogspot.com/2012/10/2.html)

1.По схеме

root@ctd-s2:RE:0% ls -al
total 248
drwxr-xr-x   6 root  wheel   1024 Feb 14 16:25 .
drwxr-xr-x  25 root  wheel    512 Jan 21  2013 ..
drwxrwxr-x   2 root  wheel    512 Aug 26  2012 .snap
drwxr-xr-x   4 root  wheel    512 Dec 20 13:01 db
-rw-r-----   1 root  wheel  14716 Feb 14 16:25 juniper.conf+.gz
-rw-r-----   1 root  wheel  14772 Nov 20 11:39 juniper.conf.1.gz
-rw-r-----   1 root  wheel  14768 Nov 20 10:53 juniper.conf.2.gz
-rw-r-----   1 root  wheel  14720 Nov  8 09:56 juniper.conf.3.gz
-rw-r-----   1 root  wheel  14762 Dec 20 13:01 juniper.conf.gz
---x--x---   1 root  wheel     32 Dec  8  2016 juniper.conf.md5
drwx------   3 root  wheel   2048 Nov 21  2014 lost+found
-rw-r-----   1 root  wheel  11447 Mar 23  2017 rescue.conf.gz
-rw-------   1 root  wheel    668 Jan 25  2013 ssh_host_dsa_key
-rw-r--r--   1 root  wheel    612 Jan 25  2013 ssh_host_dsa_key.pub
-rw-------   1 root  wheel    227 Jan 25  2013 ssh_host_ecdsa_key
-rw-r--r--   1 root  wheel    184 Jan 25  2013 ssh_host_ecdsa_key.pub
-rw-------   1 root  wheel    987 Jan 25  2013 ssh_host_key
-rw-r--r--   1 root  wheel    652 Jan 25  2013 ssh_host_key.pub
-rw-------   1 root  wheel   1675 Jan 25  2013 ssh_host_rsa_key
-rw-r--r--   1 root  wheel    404 Jan 25  2013 ssh_host_rsa_key.pub
-rw-r--r--   1 root  wheel   1512 Jan 21  2013 usage.db
drwxr-xr-x   2 root  wheel    512 Nov 21  2014 vchassis

2.Rollback
3.

