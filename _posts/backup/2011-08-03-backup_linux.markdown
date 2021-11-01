---
layout: post
title:  "Backup linux сервера"
date:   2011-08-03 16:07:09 +0400
categories: backup linux
tags: backup linux tar mysqldump
---

# Backup_linux
```
/usr/bin/mysqldump -u root -p915xxx710 --opt zazhigai_ru > /var/backup/backup/zazhigai_ru.sql

/bin/tar -czf /var/backup/backup/etc_emerald.tar.gz /etc

/# tar cvpzf backup.tgz –-exclude=/proc –-exclude=/lost+found –-exclude=/backup.tgz –-exclude=/mnt –-exclude=/sys
```


opennet.ru/fsbackup
[http://www.opennet.ru/tips/info/1857.shtml](http://www.opennet.ru/tips/info/1857.shtml)
[http://www.opennet.ru/dev/fsbackup/](http://www.opennet.ru/dev/fsbackup/)
[http://www.opennet.ru/soft/Short_Doc_Bacula.pdf](http://www.opennet.ru/soft/Short_Doc_Bacula.pdf)
[http://www.halfgaar.net/backing-up-unix](http://www.halfgaar.net/backing-up-unix)
[http://habrahabr.ru/post/41492/](http://habrahabr.ru/post/41492/)
[http://www.ibm.com/developerworks/ru/library/l-backup/index.html](http://www.ibm.com/developerworks/ru/library/l-backup/index.html)
[http://www.ibm.com/developerworks/ru/library/l-Backup_4/](http://www.ibm.com/developerworks/ru/library/l-Backup_4/)
[http://ilab.me/howto/bash-tar-vps-backup/](http://ilab.me/howto/bash-tar-vps-backup/)

```
/usr/bin/mysqldump -u root -p915xxx710 --opt lipbalkon > /home/garry/backup/lipbalkon.sql
/bin/tar -czf /home/garry/backup/lipbalkon.tar.gz /home/lipbalkon/
/usr/bin/mysqldump -u root -p915xxx710 --opt um > /home/garry/backup/um.sql
/bin/tar -czf /home/garry/backup/um.tar.gz /var/home/umit-agro.sc.ru/
/bin/chown garry:users /home/garry/backup/*
```
На моем компе
```
scp  garry@hosting.sc.ru:/home/garry/backup/um.sql /home/garry/backup
```















```
export LC_CTYPE="ru_RU.UTF8"
```

Так как в системе нет собранной локали cp1251, для её сборки следует выполнить следующее:
```
gzip -d /usr/share/i18n/charmaps/CP1251.gz

localedef -c -f /usr/share/i18n/charmaps/CP1251 \
> -i /usr/share/i18n/locales/ru_RU \
> /usr/lib/locale/ru_RU.CP1251

ln -s /usr/lib/locale/ru_RU.CP1251 /usr/lib/locale/ru_RU.cp-1251
```
отредактировать следующие системные файлы:
```
/etc/sysconfig/language

RC_LANG="ru_RU.CP1251"

/etc/sysconfig/console

CONSOLE_ENCODING="CP1251"
```
















Rdiff-backup
[http://www.hilik.org.ua/rdiff-backup/](http://www.hilik.org.ua/rdiff-backup/)
[http://blog.sozinov.eu/2006/08/backup-with-rdiff-backup.html](http://blog.sozinov.eu/2006/08/backup-with-rdiff-backup.html)
[http://blog.sozinov.eu/2007/02/bacula.html](http://blog.sozinov.eu/2007/02/bacula.html)
[http://www.opennet.ru/openforum/vsluhforumID3/46139.html](http://www.opennet.ru/openforum/vsluhforumID3/46139.html)
[http://habrahabr.ru/post/18818/](http://habrahabr.ru/post/18818/)





LVM и Mysql

[http://www.samag.ru/archive/article/188](http://www.samag.ru/archive/article/188)
[http://www.cyberciti.biz/tips/consistent-backup-linux-logical-volume-manager-snapshots.html](http://www.cyberciti.biz/tips/consistent-backup-linux-logical-volume-manager-snapshots.html)
[http://www.opennet.ru/base/sys/linux_lvm2.txt.html](http://www.opennet.ru/base/sys/linux_lvm2.txt.html)
[http://xgu.ru/wiki/LVM](http://xgu.ru/wiki/LVM)
[http://habrahabr.ru/post/63394/](http://habrahabr.ru/post/63394/)
[http://habrahabr.ru/post/132123/](http://habrahabr.ru/post/132123/)

[http://www.sql.ru/forum/actualthread.aspx?tid=784890](http://www.sql.ru/forum/actualthread.aspx?tid=784890)
[http://gazette.linux.ru.net/rus/articles/taleLinuxLVM.html](http://gazette.linux.ru.net/rus/articles/taleLinuxLVM.html)
[http://ru.wikipedia.org/wiki/LVM](http://ru.wikipedia.org/wiki/LVM)
[http://guruadmin.ru/page/rezervnoe-kopirovanie-lvm-xen-domu](http://guruadmin.ru/page/rezervnoe-kopirovanie-lvm-xen-domu)
[http://www.linux.org.ru/forum/admin/4921132](http://www.linux.org.ru/forum/admin/4921132)
[http://lanit.su/index.php/LVM](http://lanit.su/index.php/LVM)
[http://john.5070.info/2009/06/%D0%BE%D1%80%D0%B3%D0%B0%D0%BD%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F-%D0%B1%D1%8D%D0%BA%D0%B0%D0%BF%D0%BE%D0%B2-%D1%81-%D0%BF%D0%BE%D0%BC%D0%BE%D1%89%D1%8C%D1%8E-lvm/](http://john.5070.info/2009/06/%D0%BE%D1%80%D0%B3%D0%B0%D0%BD%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F-%D0%B1%D1%8D%D0%BA%D0%B0%D0%BF%D0%BE%D0%B2-%D1%81-%D0%BF%D0%BE%D0%BC%D0%BE%D1%89%D1%8C%D1%8E-lvm/)