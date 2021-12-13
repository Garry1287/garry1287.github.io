---
layout: post
title:  "Создание и определение пула в kvm"
date:   2013-05-09 03:47:07 +0400
categories: kvm linux
tags: kvm
---

# Создание и определение пула в kvm (kvm-pool-define)

1)Через fdisk - сделать для md128 тип 8e (lvm)
2) создать pvcreate
3) cоздать vgcreate
vg_images   
4) lv создаем c помощью virsh уже
```
   vgcreate guest_images_lvm /dev/sdb1
   virsh pool-define-as vg_pool_storage logical
```
    
Достаточно команды
```
virsh pool-define-as guest_images_lvm logical
```

```
vg_pool_storage   1   0   0 wz--n- 629,27g 629,27g
[root@kvmhost2 dev]# virsh pool-build vg_pool_storage
ошибка: Не удалось собрать пул vg_pool_storage
ошибка: internal error: Child process (/usr/sbin/vgcreate vg_pool_storage) unexpected exit status 5:   A volume group called vg_pool_storage already exists.


[root@kvmhost2 dev]# virsh pool-start vg_pool_storage
Пул vg_pool_storage запущен

[root@kvmhost2 dev]# virsh pool-list
 Имя               Статус Автозапуск
-------------------------------------------
 vg_pool_storage      активен no        

[root@kvmhost2 dev]#  virsh pool-autostart vg_pool_storage
Добавлена метка автоматического запуска пула vg_pool_storage

[root@kvmhost2 dev]# virsh pool-list
 Имя               Статус Автозапуск
-------------------------------------------
 vg_pool_storage      активен yes       
```



Кратко
```
pvcreate /dev/md128
vgcreate vg_pool_storage /dev/md128
virsh pool-define-as vg_pool_storage logical
``` 
 
 
## Переезд машины
```
lvcreate --size 10G --snapshot --name centos7_snap /dev/vg_pool_storage/lv_centos7_py

dd if=/dev/vg_pool_storage/centos7_snap | ssh root@kvmhost1.sc.int 'dd of=/dev/vg_pool_storage/lv_centos7_py'

lvremove /dev/vg_pool_storage/centos7_snap
```