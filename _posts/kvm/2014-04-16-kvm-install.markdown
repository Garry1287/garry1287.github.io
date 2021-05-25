---
layout: post
title:  "kvm-install"
date:   2014-04-16 14:43:36 +0400
categories: kvm
tags: kvm
---

# kvm-install
[http://doc.opensuse.org/documentation/html/openSUSE/opensuse-kvm/cha.kvm.requires.html](http://doc.opensuse.org/documentation/html/openSUSE/opensuse-kvm/cha.kvm.requires.html)
[http://docs.fedoraproject.org/ru-RU/Fedora/12/html-single/Virtualization_Guide/index.html#chap-Virtualization_Guide-Network_Configuration](http://docs.fedoraproject.org/ru-RU/Fedora/12/html-single/Virtualization_Guide/index.html#chap-Virtualization_Guide-Network_Configuration)
[http://habrahabr.ru/post/71709/](http://habrahabr.ru/post/71709/)
[http://andrey.org/kvm-on-centos/](http://andrey.org/kvm-on-centos/)
[http://zauris.ru/kvm.html](http://zauris.ru/kvm.html)
[http://open-os.ru/instrumenty-dlya-raboty-s-kvm/](http://open-os.ru/instrumenty-dlya-raboty-s-kvm/)
[http://fgh151.blog.ru/97484995.html](http://fgh151.blog.ru/97484995.html)
[http://linuxforum.ru/viewtopic.php?id=27073](http://linuxforum.ru/viewtopic.php?id=27073)
[http://linuxru.org/linux/165](http://linuxru.org/linux/165)

[http://vmind.ru/2011/03/31/vnedryaem-virtualizaciyu-kvm-chast-1/](http://vmind.ru/2011/03/31/vnedryaem-virtualizaciyu-kvm-chast-1/)

О libvirt
[http://wiki.dvo.ru/wiki/%D0%9E%D1%80%D0%B3%D0%B0%D0%BD%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F_%D0%B8%D0%BD%D1%84%D1%80%D0%B0%D1%81%D1%82%D1%80%D1%83%D0%BA%D1%82%D1%83%D1%80%D1%8B_%D0%B2%D0%B8%D1%80%D1%82%D1%83%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D1%85_%D0%BC%D0%B0%D1%88%D0%B8%D0%BD_%D0%BD%D0%B0_%D0%B1%D0%B0%D0%B7%D0%B5_libvirt](http://wiki.dvo.ru/wiki/%D0%9E%D1%80%D0%B3%D0%B0%D0%BD%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F_%D0%B8%D0%BD%D1%84%D1%80%D0%B0%D1%81%D1%82%D1%80%D1%83%D0%BA%D1%82%D1%83%D1%80%D1%8B_%D0%B2%D0%B8%D1%80%D1%82%D1%83%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D1%85_%D0%BC%D0%B0%D1%88%D0%B8%D0%BD_%D0%BD%D0%B0_%D0%B1%D0%B0%D0%B7%D0%B5_libvirt)
[http://help.ubuntu.ru/wiki/%D1%80%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE_%D0%BF%D0%BE_ubuntu_server/%D0%B2%D0%B8%D1%80%D1%82%D1%83%D0%B0%D0%BB%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F/libvirt](http://help.ubuntu.ru/wiki/%D1%80%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE_%D0%BF%D0%BE_ubuntu_server/%D0%B2%D0%B8%D1%80%D1%82%D1%83%D0%B0%D0%BB%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F/libvirt)

Vm install (не получилось)
[http://www.server-world.info/en/note?os=SUSE_Linux_Enterprise_Server_11&p=xen&f=3](http://www.server-world.info/en/note?os=SUSE_Linux_Enterprise_Server_11&p=xen&f=3)

Монтирование виртуальной машины к основной
[http://koder-ua.blogspot.ru/2012/01/libvirt-co-3.html](http://koder-ua.blogspot.ru/2012/01/libvirt-co-3.html)
[http://www.hub.ru/wiki/Libvirt](http://www.hub.ru/wiki/Libvirt)



Информация о железе
[http://ubuntovod.ru/instructions/ubuntu-system-information.html](http://ubuntovod.ru/instructions/ubuntu-system-information.html)
[http://www.unixpin.com/wordpress/2008/08/14/cpu-number/](http://www.unixpin.com/wordpress/2008/08/14/cpu-number/)

1. Сколько памяти и процессор на этой машине 8 процессоров и 8 гигов памяти
2. Планирую запустить 4 машины (opensuse-monit и centos-hosting), 2 в резерве для будущего (debian для поучиться)
3. Куда ставить в файл или lvm (lvm)
4. Как устанавливать 
5. IP адреса для неё и mngt(ssh,vnc)
6.






[    0.056197] smpboot: CPU0: Intel(R) Xeon(R) CPU           E5620  @ 2.40GHz (fam: 06, model: 2c, stepping: 02)
cpu MHz         : 1596.000
cache size      : 12288 KB



Можно на машину по один проц и один гиг памяти

8 процессоров по 2,4 GHz
Память
8128820 получается по 1024 или 2048 на каждую машинку оперативки




Сначала создаем хранилище
qemu-img create -f host_device /dev/vm_images/img1 10G

а потом
ставим машинку
# virt-install --accelerate --hvm --connect qemu:///system \
	--network network:default \
	--name rhel3support --ram=756\
	--file=/var/lib/libvirt/images/rhel3support.img \
	--file-size=6 --vnc --cdrom=/dev/sr0



qemu-img create -f host_device /dev/vg_kvmhost1/lv_suse_monit 20G

  328  2013-08-14 16:29:53 virt-install --name=suse_monit --name=linux --os-type=linux --vcpus=2 --hvm --network network=default --disk path=/dev/vg_kvmhost1/lv_suse_monit -r 1024  --cdrom=/var/lib/libvirt/images/openSUSE-12.3-DVD-x86_64.iso --vnc -w bridge:br0
  329  2013-08-14 16:30:07 virt-install --name=suse_monit --name=linux --os-type=linux --vcpus=2 --hvm --disk path=/dev/vg_kvmhost1/lv_suse_monit -r 1024  --cdrom=/var/lib/libvirt/images/openSUSE-12.3-DVD-x86_64.iso --vnc -w bridge:br0
  330  2013-08-14 16:30:28 virt-install --name=suse_monit --name=linux --os-type=linux --vcpus=2 --hvm --disk path=/dev/vg_kvmhost1/lv_suse_monit -r 1024  --cdrom=/var/lib/libvirt/images/openSUSE-12.3-DVD-x86_64.iso --vnc -w bridge:br0 --noautoconsole
  331  2013-08-14 16:30:44 virt-install --name=suse_monit  --os-type=linux --vcpus=2 --hvm --disk path=/dev/vg_kvmhost1/lv_suse_monit -r 1024  --cdrom=/var/lib/libvirt/images/openSUSE-12.3-DVD-x86_64.iso --vnc -w bridge:br0 --noautoconsole




virt-install --name=suse_monit  --os-type=linux --vcpus=2 --hvm --disk path=/dev/vg_kvmhost1/lv_suse_monit -r 1024  -c /var/lib/libvirt/images/openSUSE-12.3-DVD-x86_64.iso --vnc -w bridge:br0 --noautoconsole
virt-install --name=suse_monit  --os-type=linux --vcpus=2 --hvm --disk path=/dev/vg_kvmhost1/lv_suse_monit -r 1024  -c /var/lib/libvirt/images/openSUSE-12.3-DVD-x86_64.iso --vnc -w bridge:br0 --noautoconsole


/var/lib/libvirt/images/openSUSE-12.3-DVD-x86_64.iso
/dev/vg_kvmhost1/lv_suse_monit






ssh -C -L5900:127.0.0.1:5900 root@192.168.121.34
vncviewer localhost





Установка CentOS

ssh -C -L5900:127.0.0.1:5901 root@192.168.121.34


virt-install --name=host-centos  --os-type=linux --vcpus=2 --hvm --disk path=/dev/vg_kvmhost1/lv_host_centos -r 2048 -c /var/lib/libvirt/images/CentOS-6.4-x86_64-minimal.iso --vnc -w bridge:br0 --noautoconsole












Сеть для КVM

Чтобы отдать tagged ничего делать не надо, он и так отдаётся через бридж
В бридж объединяется eth0 интерфейс материнской машины и интрефейс виртуальной машины через настройку в xml файле

Чтобы на разные машины отдать untagged, то необходимо в бридж объединять интерфейс vlan11 (или другой), которые заведён на 
eth0 интерфейсе материнской машины и интрефейс виртуальной машины через настройку в xml файле

[http://blog.davidvassallo.me/2012/05/05/kvm-brctl-in-linux-bringing-vlans-to-the-guests/](http://blog.davidvassallo.me/2012/05/05/kvm-brctl-in-linux-bringing-vlans-to-the-guests/)
[http://www.linux-kvm.org/page/Networking](http://www.linux-kvm.org/page/Networking)
[http://forum.ubuntu.ru/index.php?topic=81091.0](http://forum.ubuntu.ru/index.php?topic=81091.0)
[http://doc.opensuse.org/documentation/htmlsingle/openSUSE/opensuse-kvm.html](http://doc.opensuse.org/documentation/htmlsingle/openSUSE/opensuse-kvm.html)
[http://www.linux-kvm.org/page/Virtio](http://www.linux-kvm.org/page/Virtio)
[http://www.pixelchaos.net/2008/07/16/vlan-bridging-in-xen/](http://www.pixelchaos.net/2008/07/16/vlan-bridging-in-xen/)
[http://blogoless.blogspot.ru/2012/10/centos-6-bridge-vlan-and-bond.html](http://blogoless.blogspot.ru/2012/10/centos-6-bridge-vlan-and-bond.html)
[https://mthode.org/posts/2012/Oct/vlan-trunking-to-kvm-vms/](https://mthode.org/posts/2012/Oct/vlan-trunking-to-kvm-vms/)
[http://wiki.libvirt.org/page/Networking](http://wiki.libvirt.org/page/Networking)
[http://kmaiti.blogspot.ru/2011/06/how-to-configure-network-bridge-vlan-on.html](http://kmaiti.blogspot.ru/2011/06/how-to-configure-network-bridge-vlan-on.html)





Импорт машины
qemu-img convert zenoss.sc.int-flat.vmdk -O qcow2 zenoss.img
virt-install --name=host-zenoss  --os-type=linux --vcpus=1 --hvm --import --disk path=/vmware/zenoss.img,format=qcow2 -r 512 --vnc -w bridge:br0 --noautoconsole

[http://manuel.kiessling.net/2013/03/19/converting-a-running-physical-machine-to-a-kvm-virtual-machine/](http://manuel.kiessling.net/2013/03/19/converting-a-running-physical-machine-to-a-kvm-virtual-machine/)

Это миграция в LVM раздел
Migrating virtual machines from ESXi 4.1 to a KVM host was easiert than I thought. It was nothing more than copy the .vmdk file from the ESXi to the KVM host, create a virtual machine and add the .vmdk as a disk.

A command line say more than a thousand words. ;-)

scp -r root@esxi:/vmfs/volumes/datastore1/vm1 /tmp # Copy VM to KVM host
lvcreate -n /dev/VolGroup/vm1 -L 12g VolGroup # Create partition for VM
dd if=/tmp/vm1/vm1-flat.vmdk of=/dev/VolGroup/vm1 # Transfer raw image to partition

After that create a virtual machine and use the partition as disk. You could also use the .vmdk file directly w/o transferring it to a partition.

Bonus round:

dd if=/tmp/vm1/vm1-flat.vmdk | pv | of=/dev/VolGroup/vm1 # Show progress while transferring




[http://gnu.su/plugins/forum/forum_viewtopic.php?633](http://gnu.su/plugins/forum/forum_viewtopic.php?633)
[https://wiki.xkyle.com/ESX_to_KVM_Migration](https://wiki.xkyle.com/ESX_to_KVM_Migration)
[http://backdrift.org/converting-windows-guests-from-vmware-esx-to-kvm-with-virtio-drivers](http://backdrift.org/converting-windows-guests-from-vmware-esx-to-kvm-with-virtio-drivers)
[http://www.linux-kvm.org/page/How_To_Migrate_From_Vmware_To_KVM](http://www.linux-kvm.org/page/How_To_Migrate_From_Vmware_To_KVM)
[http://wiki.smartos.org/display/DOC/Migrating+from+ESXi+4.x](http://wiki.smartos.org/display/DOC/Migrating+from+ESXi+4.x)
[http://opennodecloud.com/documentation/howtos/kvm-guests-virt-install-examples/](http://opennodecloud.com/documentation/howtos/kvm-guests-virt-install-examples/)
[https://www.sharktooth.de/doku.php/linux:virtualization:migrating_from_esxi_to_kvm_qemu](https://www.sharktooth.de/doku.php/linux:virtualization:migrating_from_esxi_to_kvm_qemu)



'/vmware/win2003/image.qcow2',device='disk',size=500,sparse=false,cache='writeback',bus='ide'


Устанока windows 2003 на qcow2  (нужно было format='qcow2')
ssh -C -L5900:127.0.0.1:5902 root@192.168.121.34
vncviewer localhost
virt-install --name=win2003  --os-type=windows --vcpus=1 --hvm --disk path='/vmware/win2003/image.qcow2',device='disk',size=21474836480,sparse=false,cache='writeback',bus='ide',format='qcow2' -r 1024 -c /var/lib/libvirt/images/en_win_srv_2003_r2_enterprise_kn_with_sp2_cd1_x13-13664.iso --vnc -w bridge:br0 --noautoconsole


[http://itman.in/kvm-windows-2003/](http://itman.in/kvm-windows-2003/)



 
Changing the Network Card Model

kvm and qemu currently default to using the rtl8139 NIC. Supported NICs in Ubuntu 8.04 LTS are i82551, i82557b, i82559er, ne2k_pci, pcnet, rtl8139, e1000, and virtio. To use an alternate NIC, dump the xml as above, then edit your xml to have:

<domain type='kvm'>
  ...
    <interface type='network'>
      ...
      <model type='e1000'/>
    </interface>
  ...
</domain>
[http://www.libvirt.org/formatdomain.html](http://www.libvirt.org/formatdomain.html)
[https://access.redhat.com/site/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Virtualization_Administration_Guide/sect-Virtualization-Troubleshooting-KVM_networking_performance.htmlsingle](https://access.redhat.com/site/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Virtualization_Administration_Guide/sect-Virtualization-Troubleshooting-KVM_networking_performance.htmlsingle)














proxmox

proxmox меня устраивает более чем полность. openvz работает, kvm работает. Поддержка если надо покупается.
Не хватает некоторых вещей, но идеального ничего нет.

Можно конечно сразу посмотреть на решение от сосисочной компании (parallels), но там уже деньги :) 
Тесты делали, могу сказать, что HDD с virtio намного шустрее пишет/читает, нежели без него, не говоря уже о VBox, 
но сейчас уже точной инфы не осталось :( 


в случае ВинХР и BSOD с кодом IRQL_NOT_LESS_OR_EQUAL пробуйте загружать модуль КВМ под тип процессора так: kvm-intel flexpriority=0.
 Это помогает реально! И — ВНИМАНИЕ — об этом можно прочитать только на закрытом багтрекере КрасноШляпы!!! 
То есть по такому распространенному глюку ИНФЫ НЕТ!!! Поэтому…


5)… если у вас есть непонятные проблемы с виртуалками — пишите разрабам КВМ!!! Лучше и быстрее их вам никто не поможет!!!

6) Вин Сервер 2003 32бит работает под КВМ с дровами Виртио без проблем.



Добавить

[http://www.ossportal.ru/technologies/kvm/blogs/160](http://www.ossportal.ru/technologies/kvm/blogs/160)




virsh edit win2003
<memory unit='KiB'>2097152</memory>
<currentMemory unit='KiB'>2097152</currentMemory>

1048576

<memballoon model='virtio'>
      <address type='pci' domain='0x0000' bus='0x00' slot='0x04' function='0x0'/>
    </memballoon>


    managedsave                    managed save of a domain state
    managedsave-remove             Remove managed save of a domain
    maxvcpus                       connection vcpu maximum
    memtune                        Get or set memory parameters
    migrate                        migrate domain to another host
    migrate-setmaxdowntime         set maximum tolerable downtime
    migrate-setspeed               Set the maximum migration bandwidth
    migrate-getspeed               Get the maximum migration bandwidth



    cpu-baseline                   compute baseline CPU
    cpu-compare                    compare host CPU with a CPU described by an XML file
    cpu-stats                      show domain cpu statistics



    setmaxmem                      change maximum memory limit
    setmem                         change memory allocation
    setvcpus                       change number of virtual CPUs


setvcpus suse_monit --count 1
error: Requested operation is not valid: domain is not running



setmaxmem win2003 --size 4194304
error: Unable to change MaxMemorySize
error: Requested operation is not valid: cannot resize the maximum memory on an active domain







 Networking (help keyword 'network'):
    net-autostart                  autostart a network
    net-create                     create a network from an XML file
    net-define                     define (but don't start) a network from an XML file
    net-destroy                    destroy (stop) a network
    net-dumpxml                    network information in XML
    net-edit                       edit XML configuration for a network
    net-info                       network information
    net-list                       list networks
    net-name                       convert a network UUID to network name
    net-start                      start a (previously defined) inactive network
    net-undefine                   undefine an inactive network
    net-update                     update parts of an existing network's configuration
    net-uuid                       convert a network name to network UUID

































Динамическое выделение памяти для виртуальных машин
[http://www.ossportal.ru/technologies/kvm/blogs/160](http://www.ossportal.ru/technologies/kvm/blogs/160)


itman.in/kvm-otklyuchenie-i-podklyuchenie-ustrojstv/
itman.in/virsh-commands/
itman.in/kvm-windows-network-optimization/
[http://itman.in/kvm-disk-optimization/](http://itman.in/kvm-disk-optimization/)
[http://itman.in/kvm-debug/](http://itman.in/kvm-debug/)
[http://itman.in/kvm-virt-install/](http://itman.in/kvm-virt-install/)
[http://www.linux-kvm.org/page/Networking](http://www.linux-kvm.org/page/Networking)
[http://www.linux-kvm.com/content/windows-balloon-driver#comment-1495](http://www.linux-kvm.com/content/windows-balloon-driver#comment-1495)
[http://www.linux-kvm.org/page/Using_VirtIO_NIC](http://www.linux-kvm.org/page/Using_VirtIO_NIC)
[http://linuxforum.ru/viewtopic.php?id=28380](http://linuxforum.ru/viewtopic.php?id=28380)

Запуск Windows под Linux KVM
[http://habrahabr.ru/post/176823/](http://habrahabr.ru/post/176823/)

Миграция с одного физического сервера на другой
[http://habrahabr.ru/post/119972/](http://habrahabr.ru/post/119972/)






#!/bin/bash 
 
NAME=ubuntu1204
CDROM='/home/user/Distributives/precise-alternate-amd64.iso'
 
virt-install --connect qemu:///system \
-n "$NAME" \
-r 1024 \
--arch=x86_64 \
--vcpus=1 \
--os-type=linux \
--os-variant=virtio26 \
--cdrom "$CDROM" \
--disk "/var/lib/libvirt/images/$NAME.img",bus=virtio,size=6,format=raw,cache=writeback \
--network network=default \
--hvm \
--accelerate \
--graphics vnc,password=password,listen=0.0.0.0,port=5903 &

[https://ru.wikibooks.org/wiki/%D0%A3%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5_%D0%B2%D0%B8%D1%80%D1%82%D1%83%D0%B0%D0%BB%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D0%B5%D0%B9_%D0%BD%D0%B0_%D0%BE%D1%81%D0%BD%D0%BE%D0%B2%D0%B5_libvirt](https://ru.wikibooks.org/wiki/%D0%A3%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5_%D0%B2%D0%B8%D1%80%D1%82%D1%83%D0%B0%D0%BB%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D0%B5%D0%B9_%D0%BD%D0%B0_%D0%BE%D1%81%D0%BD%D0%BE%D0%B2%D0%B5_libvirt)






Actually, I was able to make it work by changing only a couple of things.... One was the /etc/webmin/servers/*.serv file to say virtio instead of IDE.

Second, was to change /etc/fstab on the virtual machine to use vdb1 instead of sdb1.

Third was to change /boot/grub/grub.conf to use vdb1.


dumpxml


Полезные фишки
[http://www.hub.ru/wiki/Libvirt](http://www.hub.ru/wiki/Libvirt)





virt-install --name=srv1 --ram=2000 --boot=cdrom,hd --disk=path=srv1hd,size=50,bus=virtio --cdrom=/data/admin/ISO/Windows_Server_2012_Standard_Ru.IMG --os-type=windows --os-variant=win2k8 --graphics=vnc,password=09876 -w bridge:br0 --autostart

virt-install \
-n gwhatup \
-r 2048 \
--vcpus=2 \
--os-type=win2003 \
--boot hd \
--disk "/dev/vg_pool_storage/green_whatup",bus=virtio,format=raw,cache=writeback \
--graphics vnc,listen=0.0.0.0
-w bridge:br0 --autostart

-c /home/goodigy/dists/CentOs-7.0-1406-x86_64-Minimal.iso \
--disk pool=storage,size=20,bus=virtio,format=qcow2,cache=writeback \
--graphics vnc,listen=0.0.0.0



 <disk type='block' device='disk'>
      <driver name='qemu' type='raw'/>
      <source dev='/dev/vg_pool_storage/green_whatup'/>
      <target dev='hda' bus='ide'/>
      <address type='drive' controller='0' bus='0' target='0' unit='0'/>

    <disk type='file' device='disk'>
      <driver name='qemu' type='qcow2'/>
      <source file='/home/images/suse_monit.qcow2'/>
      <target dev='hda' bus='ide'/>
      <address type='drive' controller='0' bus='0' target='0' unit='0'/>
    </disk>



virt-install \
-n bitrix \
-r 512\
--vcpus=1 \
--os-type=linux \
--os-variant=virtio26 \
--boot hd \
--disk "/home/igy/kvm/bitrix2.img",bus=virtio,format=qcow2,cache=writeback\
--graphics vnc,listen=0.0.0.0






KVM кластер
[https://yvision.kz/post/368995](https://yvision.kz/post/368995)
    Выделим два сервера под хранилище данных (СХД). На каждом таком сервере должны быть установлены по два жестких диска для рейд массива уровня 1 - зеркалирования. Далее через DRBD  или GlusterFS надо связать эти два сервера СХД чтобы они реплицировали данные зеркального массива между собой. Для обеспечения высокой доступности на эти сервера необходимо установить HeartBeat, чтобы он автоматически выбирал master или slave СХД в случае не доступности одного или другого. На таких серверах нужно создать LVM тома под каждую виртуальную машину - гостя.
    Выделим два сервера под виртуализацию для гипервизоров KVM. Это уже получается 4 сервера, для настройки отказоустойчивости за место HeartBeat здесь можно применить Pacemaker, чтобы он автоматически активировал нужный сервер виртуализации KVM при недоступности одного из двух.

Чтобы не настраивать в ручную такие сервисы как DRBD, HeatBeat и Pacemaker, существует готовая система виртуализации по имени oVirt. Рекомендую ознакомиться с данной системой.
