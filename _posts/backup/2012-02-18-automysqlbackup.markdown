---
layout: post
title:  "automysqlbackup"
date:   2012-02-18 23:04:49 +0400
categories: automysqlbackup
tags: automysqlbackup
---

# automysqlbackup
[http://www.ekzorchik.ru/wordpress/2015/10/backup-all-databases/](http://www.ekzorchik.ru/wordpress/2015/10/backup-all-databases/)
[https://www.a2hosting.com/kb/developer-corner/mysql/mysql-database-backups-using-automysqlbackup](https://www.a2hosting.com/kb/developer-corner/mysql/mysql-database-backups-using-automysqlbackup)


Запускать  DumpPreUserCmd
$sshPath -q -x -l root $host /usr/local/bin/mysql_hostname_dump




Простой скрипт mysql
[http://www.sysadmin.in.ua/info/index/21/29/37](http://www.sysadmin.in.ua/info/index/21/29/37)


Скачать
[https://sourceforge.net/projects/automysqlbackup/files/](https://sourceforge.net/projects/automysqlbackup/files/)
Распокавать
Запусить ./install
Согласиться

Поправить
/etc/automysqlbackup/myserver.conf

создать /var/backup/db

Сделать скипт
[root@host cron.daily]# cat runmysqlbackup 
#!/bin/sh

/usr/local/bin/automysqlbackup /etc/automysqlbackup/myserver.conf

chown backup.backup /var/backup/db* -R
find /var/backup/db* -type f -exec chmod 400 {} \;
find /var/backup/db* -type d -exec chmod 700 {} \;


В исключения добавить
CONFIG_db_exclude=( 'information_schema' 'performance_schema' )
