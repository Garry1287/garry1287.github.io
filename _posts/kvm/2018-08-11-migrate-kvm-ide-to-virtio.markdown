---
layout: post
title:  "Миграция в kvm с ide  на virtio"
date:   2018-08-11 03:29:08 +0300
categories: kvm
tags: kvm
---

# Миграция в kvm с ide  на virtioo

[https://www.virtualmin.com/node/25526](https://www.virtualmin.com/node/25526)
[http://linux.ioerror.us/2015/05/how-to-migrate-from-ide-to-virtio-in-rhel-6-5-kvm-guest-with-lvms/](http://linux.ioerror.us/2015/05/how-to-migrate-from-ide-to-virtio-in-rhel-6-5-kvm-guest-with-lvms/)

[http://www.grosseosterhues.com/2011/03/migrate-kvm-ide-to-virtio/](http://www.grosseosterhues.com/2011/03/migrate-kvm-ide-to-virtio/)

[http://habrahabr.ru/post/176823/](http://habrahabr.ru/post/176823/)

[http://forum.proxmox.com/threads/9694-Change-disk-device-from-ide-to-virtio](http://forum.proxmox.com/threads/9694-Change-disk-device-from-ide-to-virtio)

[http://serverfault.com/questions/690014/how-to-migrate-from-ide-to-virtio-in-rhel-6-5-kvm-guest-with-lvms](http://serverfault.com/questions/690014/how-to-migrate-from-ide-to-virtio-in-rhel-6-5-kvm-guest-with-lvms)

## Клонирование виртуальной машины
[http://fedorenko.ucoz.org/publ/linux/virtualizacija/klonirovanie_virtualnykh_mashin_qemu_kvm/11-1-0-48](http://fedorenko.ucoz.org/publ/linux/virtualizacija/klonirovanie_virtualnykh_mashin_qemu_kvm/11-1-0-48)

## Virtio - kvm оптимизация
[http://vasilisc.com/optimization-virtual-server](http://vasilisc.com/optimization-virtual-server)

[http://vasilisc.com/optimization-guest-os-kvm](http://vasilisc.com/optimization-guest-os-kvm)

[http://furalol.blogspot.ru/2012/08/kvm-kvm.html](http://furalol.blogspot.ru/2012/08/kvm-kvm.html)

[http://www.ibm.com/developerworks/ru/library/l-overcommit-kvm-resources/index.](http://www.ibm.com/developerworks/ru/library/l-overcommit-kvm-resources/index.)


```
  <memory_device>
    <entry name='size'>4096 MB</entry>
    <entry name='form_factor'>DIMM</entry>
    <entry name='locator'>DIMM_B1</entry>
    <entry name='bank_locator'>NODE 0 CHANNEL 1 DIMM 0</entry>
    <entry name='type'>Other</entry>
    <entry name='type_detail'>Synchronous</entry>
    <entry name='speed'>1067 MHz</entry>
    <entry name='manufacturer'>0x0198</entry>
    <entry name='serial_number'>0xB81047D6</entry>
    <entry name='part_number'>9965426-045.A00LF</entry>
  </memory_device>
</sysinfo>
```

```
vg_pool_storage

   pool-create-as name type [--source-host hostname] [--source-path path] [--source-dev path] [--source-name name] [--target path] [--source-format format] [--auth-type
       authtype --auth-username username --secret-usage usage] [[--adapter-name name] | [--adapter-wwnn --adapter-wwpn] [--adapter-parent parent]] [--build] [[--overwrite] |
       [--no-overwrite]] [--print-xml]
```

```
# virsh pool-define-as guest_images_fs fs - - /dev/sdc1 - "/guest_images"
virsh pool-define-as guest_images_lvm logical - - /dev/sdc libvirt_lvm /dev/libvirt_lvm   (vg libvirt_lvm)
virsh pool-define-as guest_images dir - - - - "/guest_images"
```

## Pool guest_images_fs defined

```
virsh pool-define-as vg_pool_storage logical - - - vg_pool_storage /dev/vg_pool_storage

 pool-define-as name type [--source-host hostname] [--source-path path] [--source-dev path] [--source-name name] [--target path] 

/dev/vg_pool_storage 777


    [--source-host hostname] provides the source hostname for pools backed by storage from a remote server (pool types netfs, iscsi, rbd, sheepdog, gluster).

           [--source-path path] provides the source directory path for pools backed by directories (pool type dir).

           [--source-dev path] provides the source path for pools backed by physical devices (pool types fs, logical, disk, iscsi, zfs).

           [--source-name name] provides the source name for pools backed by storage from a named element (pool types logical, rbd, sheepdog, gluster).

           [--target path] is the path for the mapping of the storage pool into the host file system.
```

```
virsh pool-start vg_pool_storage
ошибка: Не удалось запустить пул vg_pool_storage
ошибка: unsupported configuration: cannot find logical volume group name 'vg_pool_storage'
```




```
lvcreate --size 10G --snapshot --name centos7_snap /dev/vg_pool_storage/lv_centos7_py

dd if=/dev/vg_pool_storage/centos7_snap | ssh root@kvmhost1.sc.int 'dd of=/dev/vg_pool_storage/lv_centos7_py'

lvremove /dev/vg_pool_storage/centos7_snap
```