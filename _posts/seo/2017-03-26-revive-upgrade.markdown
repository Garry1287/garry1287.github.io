---
layout: post
title:  "revive-upgrade"
date:   2017-03-26 02:27:43 +0300
categories: seo
tags: seo
---

# revive-upgrade
Создаём копию БД (вообще копия базы есть, сделанная backupPC)

create database adbd_3_2_3;
GRANT ALL PRIVILEGES ON adbd_3_2_3.* TO reklama6xbd@localhost
FLUSH PRIVILEGES;

mysqldump -u reklama6xbd -pb2dbe51 adbd –skip-lock-tables > /home/garry/adbd.sql
mysql -u reklama6xbd -pb2dbe51 adbd_3_2_3 < /home/garry/adbd.sql

Скачиваем и распоковываем в папку
unzip -d /srv/www/ad/public_html_3_2_3  revive-adserver-3.2.3.zip 

Копируем файл настроек
cp /srv/www/ad/public_html/var/ad.iptech48.ru.conf.php /srv/www/ad/public_html_3_2_3/var/

Изменяем в нем имя БД

Создаем файлик, чтобы при обновление не происходил бэкап БД, так как бекап делали сначала
touch /srv/www/ad/public_html_3_2_3/var/NOBACKUPS

Меняем местами папки
mv public_html public_html_3_2_1
mv public_html_3_2_3 public_html

Правим права
chown -R reklama6x:reklama6x /srv/www/ad/public_html

Заходим 
[http://ad.iptech48.ru](http://ad.iptech48.ru) 
и проводим обновление

Если не успешно, то откатываемся



[https://www.revive-adserver.com/support/upgrading/](https://www.revive-adserver.com/support/upgrading/)

