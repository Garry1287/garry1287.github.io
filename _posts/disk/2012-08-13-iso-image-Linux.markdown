---
layout: post
title:  "Монтируем iso-образ в Linux"
date:   2012-08-13 10:59:21 +0400
categories: disk
tags: disk
---

# Монтируем iso-образ в Linux
Монтируем iso-образ в Linux
Saturday, December 8th, 2007

В этом нам поможет losetup:
```
# losetup /dev/loop0 file.iso
# mount /dev/loop0 /mnt
```
Обратная процедура:
```
# umount /mnt
# losetup -d /dev/loop0
```



## losetup
Данная утилита позволяет представить файл, как блочное устройство, 
что позволяет нам насоздавать кучу виртуальных жестких дисков, к примеру, и ставить эксперименты с их объединением в RAID. 

losetup -a показать файлы, привязанные к блочным устройствам

losetup -d /dev/loop0 удалить блочное устройство /dev/loop0 

dd if=/dev/zero of=./file-01.img bs=200M count=1 создаем файл размером 200Мб

losetup -f --show ./file-01.img создается блочное устройство на основе файла file-01.img, -f - находит свободное имя для устройства,  --show - показывает имя найденного устройства