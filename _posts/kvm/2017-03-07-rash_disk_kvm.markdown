---
layout: post
title:  "rash_disk_kvm"
date:   2017-03-07 17:48:01 +0300
categories: kvm
tags: kvm
---

# rash_disk_kvm

[http://andreykl.blogspot.ru/2011/12/kvm-centos-62-lvm.html](http://andreykl.blogspot.ru/2011/12/kvm-centos-62-lvm.html)


dd if=/dev/mapper/vg_kvmhost1-lv_win2003 of=/dev/mapper/vg_kvmhost1-lv_win2003_copy



 attach-disk suse_monit /dev/mapper/vg_kvmhost1-lv_win2003_copy vdb --sourcetype block --persistent
detach-disk suse_monit /dev/mapper/vg_kvmhost1-lv_win2003_copy


На машинке suse_monit
echo 1 > /sys/bus/pci/rescan

Но диск появился как vda

Сделал через yast, потом винда chdisk сделала и всё ок








    <disk type='file' device='cdrom'>
      <driver name='qemu' type='raw'/>
      <source file='/var/lib/libvirt/images/en_win_srv_2003_r2_enterprise_kn_with_sp2_cd1_x13-13664.iso'/>
      <target dev='hdc' bus='ide'/>
      <readonly/>
      <alias name='ide0-1-0'/>
      <address type='drive' controller='0' bus='1' target='0' unit='0'/>
    </disk>



Добавить CDROM в виртуальную машину

Чтобы в виртуальной машине появилось CDROM устройство, добавьте в конфигурацию такой раздел внутри <devices>:

<disk type='file' device='cdrom'> 
<target dev='hdc' bus='ide'/> 
<readonly/> </disk>

Теперь можно будет в созданное устройство вставить ISO диск или подключить его к другому устройству на гипервизоре.
Вставить или сменить CDROM

virsh attach-disk guest01 /root/disc2.iso hdc --type cdrom
--mode readonly

Убрать CDROM

virsh attach-disk guest01 " " hdc --type cdrom
 --mode readonly




attach-disk win2003 /var/lib/libvirt/images/SQL2005_Standart_rus_CD1.iso hdc --type cdrom --mode readonly 





virsh # attach-disk win2003 /var/lib/libvirt/images/SS2005_CD1.iso hdc --type cdrom --mode readonly
Disk attached successfully

virsh # attach-disk win2003 '' hdc --type cdrom --mode readonly
Disk attached successfully


