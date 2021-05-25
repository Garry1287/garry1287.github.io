---
layout: post
title:  "lvm_kvm_snapshot"
date:   2014-02-18 13:54:55 +0400
categories: kvm
tags: kvm
---

# lvm_kvm_snapshot
/dev/vg_kvmhost1/lv_centos7_py


kvmhost1:/etc/libvirt/qemu # lvcreate -L10G -s -n snap_centos7_py /dev/vg_kvmhost1/lv_centos7_py

kvmhost2# virsh vol-create-as vg_pool_storage lv_centos7_py 40G 

dd if=/dev/vg_kvmhost1/snap_centos7_py  bs=1M | gzip -c | ssh root@192.168.121.44 "gunzip -c |  dd of=/dev/vg_pool_storage/lv_centos7_py"


systemctl start nginx
systemctl start uwsgi


lvconvert --merge /dev/vg_kvmhost1/snap_centos7_py

либо
lvremove /dev/vg_kvmhost1/snap_centos7_py




KVM миграция
[http://www.pivpav.ru/post/86](http://www.pivpav.ru/post/86)
[http://www.itkitchen.net/kvm-vm-migration/](http://www.itkitchen.net/kvm-vm-migration/)

[http://adminunix.ru/tar-chasto-ispol-zuemy-e-klyuchi/](http://adminunix.ru/tar-chasto-ispol-zuemy-e-klyuchi/)

Настройка kvm
[https://www.poseti.net/articles/centos-7-nastrojka-kvm](https://www.poseti.net/articles/centos-7-nastrojka-kvm)
[https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Virtualization_Administration_Guide/create-lvm-storage-pool-virsh.html](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Virtualization_Administration_Guide/create-lvm-storage-pool-virsh.html)
[http://www.linuxtopia.org/online_books/rhel6/rhel_6_virtualization/rhel_6_virtualization_chap-Virtualization-Storage_Pools-Storage_Pools.html](http://www.linuxtopia.org/online_books/rhel6/rhel_6_virtualization/rhel_6_virtualization_chap-Virtualization-Storage_Pools-Storage_Pools.html)
[https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Virtualization_Deployment_and_Administration_Guide/chap-KVM_live_migration.html](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Virtualization_Deployment_and_Administration_Guide/chap-KVM_live_migration.html)

----------

[root@kvmhost1 ~]# lvcreate -L10G -s -n snap_host_centos /dev/vg_pool_storage/lv_host_centos
  Using default stripesize 64,00 KiB.
  Logical volume "snap_host_centos" created.
[root@kvmhost1 ~]# 
Обновил joomla и удалил снапшот


[root@kvmhost1 ~]# lvremove /dev/vg_pool_storage/snap_host_centos
Do you really want to remove active logical volume vg_pool_storage/snap_host_centos? [y/n]: y
  Logical volume "snap_host_centos" successfully removed


