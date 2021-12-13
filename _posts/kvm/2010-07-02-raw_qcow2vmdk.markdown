---
layout: post
title:  "Конвертация raw и qcow в vmdk"
date:   2010-07-02 09:36:29 +0400
categories: kvm linux
tags: kvm
---

# Конвертация raw и qcow в vmdk
I used the image converter tool qemu with the following command
```
qemu-img convert -f qcow2 myImage.qcow2 -O vmdk myNewImage.vmdk 
```
This command gives me a vmdk image which is only VMWare Workstation compatible. Therefore, in order to make it ESXi compatible I have to use the vmkfstools with the following command.
```
vmkfstools -i myImage.vmdk outputName.vmdk -d thin
```

```
qemu-img convert -p -O vmdk -f raw /dev/mapper/VG-lv_BEEMUSIC /mnt/convert/VG-lv_BEEMUSIC.vmdk
scp VG-lv_BEEMUSIC.vmdk root@192.168.37.20:/vmfs/volumes/200gb/

qemu-img convert -p -O vmdk -f raw /dev/vg_pool_storage/green_whatup /var/storvmdk/gwhatup.vmdk

qemu-img convert image.img -O vmdk image.vmdk

qemu-img convert /dev/vg_pool_storage/win_snap -O vmdk 

lvcreate -n storvmdk -L60G vg_pool_storage
mkfs.ext4 /dev/vg_pool_storage/storvmdk
mkdir /var/storvmdk
qemu-img convert /dev/vg_pool_storage/win_snap -O vmdk /var/storvmdk/whatup.vmdk
```


## Копируем на esxi
```
vmkfstools -i whatup.vmdk -d thin /vmfs/volumes/NAS_01/srv_gwhatup/gwhatup.vmdk
```

[https://stackoverflow.com/questions/37794846/convert-qcow2-to-vmdk-and-make-it-esxi-6-0-compatible](https://stackoverflow.com/questions/37794846/convert-qcow2-to-vmdk-and-make-it-esxi-6-0-compatible)

[https://iamsan.ru/virtualization/vmware-esxi/migrate-from-kvm-to-vmware-esxi](https://iamsan.ru/virtualization/vmware-esxi/migrate-from-kvm-to-vmware-esxi)

[http://everythingshouldbevirtual.com/migrating-vms-from-pf9-kvm-to-esxi](http://everythingshouldbevirtual.com/migrating-vms-from-pf9-kvm-to-esxi)
