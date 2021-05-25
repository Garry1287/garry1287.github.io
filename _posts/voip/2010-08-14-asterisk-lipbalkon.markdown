---
layout: post
title:  "asterisk-lipbalkon"
date:   2010-08-14 17:48:56 +0400
categories: voip
tags: voip
---

# asterisk-lipbalkon
    
Добрый день!


пароль su "ImThBe IsIn05" конфиг менять и перегружать под su надо 


/etc/asterisk/inc/ext-local/town.inc.conf - тут можно поменять номер

"/etc/init.d/asterisk162 reload" - команда перегрузить конфиг астериска


/var/log/asterisk/cdr-csv - путь к записям вызовов



54-03-13


#!/bin/sh
/usr/bin/bzcat /var/log/asterisk/cdr-csv/rotated/Master.csv-`date +%Y%m%d`.bz2 | grep 540313 > /home/garry/ringlog/Master_$(date +%Y%m%d).cvs
echo 'This is yesterday rings' | mail -s "Rings to 540313 from yesterday - `date --date="1 days ago" +%Y%m%d`" -a /home/garry/ringlog/Master_$(date +%Y%m%d).cvs  igordzu@yandex.ru
/usr/bin/bzcat /var/log/asterisk/cdr-csv/rotated/Master.csv-`date +%Y%m%d`.bz2 | grep 540313 | awk -F"," '{ print $2,$11}'  | mail -s "Rings to 540313 from yesterday - `date --date="1 days ago" +%Y%m%d`" balkon6140@mail.ru