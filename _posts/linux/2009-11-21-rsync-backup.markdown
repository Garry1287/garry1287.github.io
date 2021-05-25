---
layout: post
title:  "rsync-backup"
date:   2009-11-21 05:52:24 +0300
categories: linux
tags: linux
---

# rsync-backup
sudo rsync -avWr --delete --progress --exclude=/home/garry/cinema --bwlimit=1000 --ignore-errors /home /mnt/vg_dz



mkdir /mnt/3disk-home
mount /dev/mapper/vg--3disk-lv_home /mnt/3disk-home
sudo rsync -avWr --delete --progress --exclude=/home/garry/cinema --exclude=/home/garry/ios --exclude=/home/garry/books --exclude=/home/garry/ccna --exclude=/home/garry/Загрузки --exclude=/home/garry/Хакер --bwlimit=1000 --ignore-errors /home /mnt/3disk-home


############ Бэкап на яндекс диск
mkdir /mnt/yandex.disk

mount -t davfs [https://webdav.yandex.ru](https://webdav.yandex.ru) /mnt/yandex.disk/
sudo rsync -avWr --delete --progress --bwlimit=1000 --ignore-errors /home/garry/ios /home/garry/books /home/garry/ccna /home/garry/Хакер /mnt/yandex.disk/home-garry


Сообщим утилите davfs2 свой логин и пароль от webdav удалённого диска.
В файл /etc/davfs2/secrets или ~/.davfs2/secrets (не заработало!) добавляем строку:

/root/yandex.disk	yandex_username	yandex_password

rsync -azVP /home/garry/books user@192.168.0.1:/backup
rsync -azVP /home/garry/ccna user@192.168.0.1:/backup
rsync -azVP /home/garry/ios user@192.168.0.1:/backup


##################
ip firewall address-list export file=ip.rsc

