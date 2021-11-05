---
layout: post
title:  "Mdadm raid (программный рейд)"
date:   2011-09-20 09:41:20 +0400
categories: disk
tags: disk
---

# Mdadm raid
[https://mnorin.com/chto-takoe-mdadm-i-kak-im-pol-zovat-sya.html](https://mnorin.com/chto-takoe-mdadm-i-kak-im-pol-zovat-sya.html)

[https://habrahabr.ru/post/200194/](https://habrahabr.ru/post/200194/)

Первый sector (316674048-976773167, по умолчанию 316674048): 


```
[root@kvmhost2 autostart]# fdisk /dev/sdd
Welcome to fdisk (util-linux 2.23.2).

Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Device does not contain a recognized partition table
Building a new DOS disklabel with disk identifier 0x264f216c.

Команда (m для справки): n
Partition type:
   p   primary (0 primary, 0 extended, 4 free)
   e   extended
Select (default p): p
Номер раздела (1-4, default 1): 3
Первый sector (2048-976773167, по умолчанию 2048): 316674048
Last sector, +sectors or +size{K,M,G} (316674048-976773167, по умолчанию 976773167): 
Используется значение по умолчанию 976773167
Partition 3 of type Linux and of size 314,8 GiB is set

Команда (m для справки): t
Selected partition 3
Hex code (type L to list all codes): fd
Changed type of partition 'Linux' to 'Linux raid autodetect'

Команда (m для справки): w
Таблица разделов была изменена!
```

```
mdadm --create /dev/md128 --level=10 --raid-devices=4 /dev/sda3 /dev/sdb3 /dev/sdc3 /dev/sdd3


mdadm --create /dev/md3 --level=10 --raid-devices=4 /dev/sda6 /dev/sdb6 /dev/sdc6 missing
mke2fs -j /dev/md3
mdadm --examine --scan >> /etc/mdadm/mdadm.conf
```

Имеет 4 диска: /dev/sd[abcd], на каждом из которых создано по одному разделу.
Хотим получить RAID10, как комбинацию из двух raid1, объединенных в raid0 (striping).

Создаем два RAID1, /dev/md0 и /dev/md1
```
   mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sda1 /dev/sdb1
   mdadm --create /dev/md1 --level=1 --raid-devices=2 /dev/sdc1 /dev/sdd1
```

Объединяем их в RAID10 (1+0):
```
   mdadm --create /dev/md2 --chunk=64 --level=0 --raid-devices=2 /dev/md0 /dev/md1
```

Тоже самое можно проделать одной командой
```
   mdadm --create /dev/md0 --level=10 --raid-devices=4 /dev/sda1 /dev/sdb1 /dev/sdc1 /dev/sdd1
```

Смотрим, что получилось в итоге:
```
   mdadm --detail /dev/md2 
   cat /proc/mdstat
```
   
   
   
