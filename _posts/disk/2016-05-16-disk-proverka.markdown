---
layout: post
title:  "Проверка раздела диска в linux"
date:   2016-05-16 19:07:40 +0300
categories: disk
tags: disk
---

# Проверка раздела диска в linux
```
 Filesystem                             1K-blocks      Used Available Use% Mounted on
devtmpfs                                 1847180         0   1847180   0% /dev
tmpfs                                    1858788       620   1858168   1% /dev/shm
tmpfs                                    1858788      9816   1848972   1% /run
tmpfs                                    1858788         0   1858788   0% /sys/fs/cgroup
/dev/mapper/vg_garry-lv_root            10255636   5737948   3977016  60% /
/dev/mapper/vg_garry-lv_usr             25671908   9369816  14974988  39% /usr
/dev/mapper/ST3250318AS_9VY23ZY4-part1 240232960 214141812  25097976  90% /backup/backup_home
/dev/mapper/vg_garry-lv_var             15416264   1048052  13565396   8% /var
/dev/mapper/cr_home                    315252228 305028980   9245632  98% /home
tmpfs                                     371756        20    371736   1% /run/user/1000
```

## Разделы
```
sudo badblocks -v /dev/sda1 > badsectors.txt
sudo e2fsck -l badsectors.txt /dev/sda1
```

## Диск
```
umount /dev/hda1
fsck /dev/hda1
```
## Исправление ошибок
```
sudo fsck -f -c -y /dev/sda
sudo smartctl -H /dev/sda1
sudo smartctl -H /dev/sda1
smartctl -s on -a /dev/sde
```

После этого смотрим информацию под READ SMART DATA. Результат может принимать два значения: PASSED или FAILED. Если выпало последнее, можно начинать делать резервные копии и искать замену винчестеру.

```
rescue:~# lvm pvscan
rescue:~# lvm vgscan
rescue:~# lvm lvchange -ay /dev/VolGroup00/LogVol00
rescue:~# lvm lvscan
ACTIVE '/dev/VolGroup00/LogVol00' [133.85 GB] inherit
inactive '/dev/VolGroup00/LogVol01' [8.45 GB] inherit
rescue:~# fsck -yfv /dev/VolGroup00/LogVol00
```

## Подключаем любой линуксовый лайв образ:
```
rescue:~# lvm pvscan
rescue:~# lvm vgscan
rescue:~# lvm lvchange -ay /dev/VolGroup0/LogVo0
rescue:~# lvm lvscan
ACTIVE ‘/dev/VolGroup0/LogVol0’ [100.0 GB]
inactive ‘/dev/VolGroup0/LogVol0’ [10.0 GB]
rescue:~# fsck -yfv /dev/VolGroup0/LogVol0
```

## После завершения проверки перезагружаем сервер.

```
/usr/bin/rsync -arvz --progress --stats --delete-after /home/garry/.wine /home/garry/.thumbnails /home/garry/.hplip /home/garry/FEBE /home/garry/books /home/garry/.VirtualBox /home/garry/.thunderbird /home/garry/.mozilla /home/garry/.firefox /home/garry/shared  /home/garry/asa-asdm /home/garry/vks-nlmk /home/garry/voip /home/garry/sh /home/garry/nerabochee /home/garry/rabochee /home/garry/py /home/garry/bin /home/garry/Documents /home/garry/junos_rus /home/garry/MyBlog /home/garry/mikrotik /home/garry/old_good_project /home/garry/mans /home/garry/Docs.txt /home/garry/3Gfile /home/garry/12 /backup/backup_home/localhost | /usr/bin/mail -s "home backup report" ibd@sc.ru
```


```badblocks -v /dev/sdb3 > /home/garry/sdb3-badblock.txt```

 
 
 
