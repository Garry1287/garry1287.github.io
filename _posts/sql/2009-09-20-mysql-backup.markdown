---
layout: post
title:  "mysql-backup"
date:   2009-09-20 15:08:37 +0400
categories: sql
tags: sql
---

# mysql-backup
Бэкап mysql
1. Копирование файлов
/var/lib/mysql/db/

  Остановка базы
  Блокировка таблиц
  Сброс кеша
  создание snapshot
  запуск базы
  копирование со снапшота
  уничтожение снапшота

Для баз MyISAM существует официальная бесплатная утилита mysqlhotcopy, которая «правильно» копирует файлы баз MyISAM без остановки сервера. 
Существует аналогичная утилита для InnoDB, но она платная, хотя и возможностей в ней больше.

innodb hot backup и mysqlhotcopy это ни в коем случае не «через текстовые файлы».
innodb hot backup — практически то же самое, что и percona xtrabackup.
mysqlhotcopy — просто копирует MYD/MYI файлы 




2.  Копирование через текстовые файлы (mysqldump, Dumper)
    /usr/bin/mysqldump -u root -p915Nyg710 --opt lipbalkon > /home/garry/backup/lipbalkon.sql

3. Инкрементные бэкапы
    Percona XtraBackup
4. Репликация
    


[http://habrahabr.ru/post/137380/](http://habrahabr.ru/post/137380/)
[http://habrahabr.ru/post/63394/](http://habrahabr.ru/post/63394/)
[http://wikiadmin.net/MySQL_%D0%91%D1%8D%D0%BA%D0%B0%D0%BF_%D0%B8_%D0%B2%D0%BE%D1%81%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5_%D0%B1%D0%B0%D0%B7_%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D1%85/](http://wikiadmin.net/MySQL_%D0%91%D1%8D%D0%BA%D0%B0%D0%BF_%D0%B8_%D0%B2%D0%BE%D1%81%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5_%D0%B1%D0%B0%D0%B7_%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D1%85/)