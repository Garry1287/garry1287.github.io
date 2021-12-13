---
layout: post
title:  "Настройка console в kvm"
date:   2014-07-14 04:44:04 +0400
categories: kvm linux
tags: kvm
---

# Настройка console в kvm
add the red lines

```
[root@localhost ~]# cat /etc/default/grub
GRUB_CMDLINE_LINUX_DEFAULT="console=tty0 console=ttyS0,9600n8"
GRUB_TERMINAL=serial
GRUB_SERIAL_COMMAND="serial --speed=9600 --unit=0 --word=8 --parity=no --stop=1"

add the following line in /etc/inittab
[root@localhost ~]# tail -1 /etc/inittab
S0:12345:respawn:/sbin/agetty ttyS0 115200

add the following line in /etc/securetty file.
[root@localhost ~]# echo "ttyS0" >> /etc/securetty

update grub.cfg
[root@localhost ~]# grub2-mkconfig -o /boot/grub2/grub.cfg
Generating grub.cfg ...
Found linux image: /boot/vmlinuz-3.3.5-2.fc16.x86_64
Found initrd image: /boot/initramfs-3.3.5-2.fc16.x86_64.img
done
```


[http://lost-and-found-narihiro.blogspot.ru/2012/05/kvm-how-to-connect-to-fedora-vms-which.html](http://lost-and-found-narihiro.blogspot.ru/2012/05/kvm-how-to-connect-to-fedora-vms-which.html)



Типы подключения сети
NAT
```
garry:~ # ifconfig
eth0      Link encap:Ethernet  HWaddr 00:21:85:39:02:AD  
          inet addr:192.168.1.141  Bcast:192.168.1.255  Mask:255.255.255.0
          inet6 addr: fe80::221:85ff:fe39:2ad/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:8566573 errors:0 dropped:0 overruns:0 frame:0
          TX packets:2317417 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:3434760469 (3275.6 Mb)  TX bytes:300013361 (286.1 Mb)

eth0:0    Link encap:Ethernet  HWaddr 00:21:85:39:02:AD  
          inet addr:10.90.90.1  Bcast:10.90.90.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1

eth0:1    Link encap:Ethernet  HWaddr 00:21:85:39:02:AD  
          inet addr:192.168.1.36  Bcast:192.168.1.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:455970 errors:0 dropped:0 overruns:0 frame:0
          TX packets:455970 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:486439639 (463.9 Mb)  TX bytes:486439639 (463.9 Mb)

```


10.0.2.15
255.255.255.0
10.0.2.2

## Сетевой мост
```
bridge - eth0 
eth0      Link encap:Ethernet  HWaddr 00:21:85:39:02:AD  
          inet addr:192.168.1.141  Bcast:192.168.1.255  Mask:255.255.255.0
          inet6 addr: fe80::221:85ff:fe39:2ad/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:8581838 errors:0 dropped:0 overruns:0 frame:0
          TX packets:2327252 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:3436258910 (3277.0 Mb)  TX bytes:300845697 (286.9 Mb)

eth0:0    Link encap:Ethernet  HWaddr 00:21:85:39:02:AD  
          inet addr:10.90.90.1  Bcast:10.90.90.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1

eth0:1    Link encap:Ethernet  HWaddr 00:21:85:39:02:AD  
          inet addr:192.168.1.36  Bcast:192.168.1.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:456254 errors:0 dropped:0 overruns:0 frame:0
          TX packets:456254 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:486456702 (463.9 Mb)  TX bytes:486456702 (463.9 Mb)
```

И на хосте
192.168.1.206
255.255.255.0
192.168.1.11 


## Внутреняя сеть
для взаимодействия виртуальных машин

Виртуальный адаптер хоста
```
eth0      Link encap:Ethernet  HWaddr 00:21:85:39:02:AD  
          inet addr:192.168.1.141  Bcast:192.168.1.255  Mask:255.255.255.0
          inet6 addr: fe80::221:85ff:fe39:2ad/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:8614731 errors:0 dropped:0 overruns:0 frame:0
          TX packets:2343814 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:3450457524 (3290.6 Mb)  TX bytes:302242765 (288.2 Mb)

eth0:0    Link encap:Ethernet  HWaddr 00:21:85:39:02:AD  
          inet addr:10.90.90.1  Bcast:10.90.90.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1

eth0:1    Link encap:Ethernet  HWaddr 00:21:85:39:02:AD  
          inet addr:192.168.1.36  Bcast:192.168.1.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:456814 errors:0 dropped:0 overruns:0 frame:0
          TX packets:456814 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:486489382 (463.9 Mb)  TX bytes:486489382 (463.9 Mb)

vboxnet0  Link encap:Ethernet  HWaddr 0A:00:27:00:00:00  
          inet addr:192.168.56.1  Bcast:192.168.56.255  Mask:255.255.255.0
          inet6 addr: fe80::800:27ff:fe00:0/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:43 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:0 (0.0 b)  TX bytes:9840 (9.6 Kb)
```

192.168.56.101
255.255.255.0

Для взаимодействия хост машины и виртуальных, без доступа к инету
универсальный драйвер

NAT. В данном режиме адаптер использует сетевые настройки основной системы при взаимодействии с сетью физического узла и прочими внешними сетями. Сетевая подсистема VirtualBox транслирует IP-трафик с исходным IP-адресом виртуальной машины в трафик с исходным адресом сетевого адаптера хостовой системы (трансляция сетевых адресов, Network Address Translation). Реализация NAT в VirtualBox имеет определенные ограничения, связанные с поддержкой протокола ICMP, широковещательного UDP -трафика и технологий виртуальных частных сетей. Этот режим используется по умолчанию.
Сетевой мост. В данном режиме сетевой адаптер ВМ подключается к сетевому адаптеру хостовой системы и обрабатывает сетевые пакеты непосредственно в обход сетевого стека хостовой системы ( адаптер хостовой системы работает с адаптером ВМ в режиме моста ).
Внутренняя сеть. Сетевые адаптеры Виртуальных машин объединяются между собой в изолированный сегмент сети.
Виртуальный адаптер хоста. Сеть объединяющая в данный сегмент хостовую систему и виртуальные машины, включенные в данный сегмент. Для этого режима VirtualBox создает в хостовой системе программный сетевой интерфейс и устанавливает на нем IP-адрес.
Универсальный драйвер. Пользователь сам выбирает драйвер сетевого адаптера, который может быть входит в состав VirtualBox или загружается с пакетом дополнений к VirtualBox. На данный момент существует 2 драйвера реализующих 2 режима работы виртуального адаптера:

    UDP Туннель. Режим для связи виртуальных машин, запущенных на различных хостах. Работает над существующей сетевой инфраструктурой.
    VDE (Виртуальный Распределенный Ethernet). Этот режим может быть использован для подключения распределенных виртуальных машин к Виртуальному коммутатору Ethernet на Linux или FreeBSD хостах.



[http://integrator.adior.ru/index.php?option=com_content&view=article&id=92:virtualbox-nic-setup&catid=31:virtualbox-&Itemid=50](http://integrator.adior.ru/index.php?option=com_content&view=article&id=92:virtualbox-nic-setup&catid=31:virtualbox-&Itemid=50)

[http://lifeslider.blogspot.ru/2012/07/virtualbox.html](http://lifeslider.blogspot.ru/2012/07/virtualbox.html)




* NAT – наипростейший способ предоставить гостевой ОС доступ в интернет, при таком режиме осуществляется просто перенаправление 
(транзакции) пакетов;
* Bridge Adapter - сетевой адаптер виртуальной машины получает такой же доступ в сеть, 
как и сетевой адаптер host-машины, но нет доступа во внешний мир;
* Internal Network - внутренняя сеть для объединения виртуальных машин в локальную сеть, без наружу и к host-машине;
* Host-only adapter - Ваша виртуалка как живая, она имеет доступ к сети Интернет, 
находится в одной локальной сети с реальной и имеет к ней доступ.

```
  <interface type='bridge'>
      <mac address='52:54:00:85:e7:90'/>
      <source bridge='br0'/>
      <address type='pci' domain='0x0000' bus='0x00' slot='0x03' function='0x0'/>
    </interface>
```


По умолчанию KVM использует NAT через бридж с именем virbr0. 
Если необходимо, чтобы гостевая система была видна в той же самой сети как отдельный хост, можно использовать bridged interface. 


[http://hrafn.me/2010/01/kak-nastroit-bridzh-dlya-kvm-na-red-hat-enterprise-linux-5-4/](http://hrafn.me/2010/01/kak-nastroit-bridzh-dlya-kvm-na-red-hat-enterprise-linux-5-4/)


## Роутинг внутри kvm
[http://admoprog.blogspot.ru/2010/09/ipv4-ipv6-kvm-hetzner.html](http://admoprog.blogspot.ru/2010/09/ipv4-ipv6-kvm-hetzner.html)




Делаем настройки в iptables, чтобы трафик виртуалок «ходил» через соединение типа bridge
```
# iptables -I FORWARD -m physdev --physdev-is-bridged -j ACCEPT
```



Примечание 2:

Если на ВМ нужна «белая сеть», тогда ставим
--network=bridge:br0
Если на ВМ требуется «серая сеть», тогда ставим
--network=bridge:virbr0
В этом случае для ВМ будет присвоен серый IP по DHCP от хост-сервера.
--graphics vnc,listen=0.0.0.0,keymap=ru,password=some.password.here
Тут указываем пароль для подключения к ВМ по vnc

[http://habrahabr.ru/post/168791/](http://habrahabr.ru/post/168791/)



Перенаправляем вывод Grub для виртуального окружения в последовательный порт.
В /boot/grub/menu.lst добавляем:
```
   serial --speed=115200 --unit=0 --word=8 --parity=no --stop=1
   terminal --timeout=10 serial
```
Отключаем показ заставки  splash и перенаправляем вывод ядра в последовательный порт (в menu.lst):
```
   title CentOS (2.6.18-128.1.10.el5)
	root (hd0,0)
	kernel /boot/vmlinuz-2.6.18-128.1.10.el5 ro root=LABEL=/ console=ttyS0
	initrd /boot/initrd-2.6.18-128.1.10.el5.img
```

```
ln -s /usr/lib/systemd/systemd/serial-getty@.service /etc/systemd/system/getty.target.wants/serial-getty@ttyS0.service
```

Настраиваем запуск getty процесса для логина через ttyS0. В /etc/inittab прописываем:
```
   S0:12345:respawn:/sbin/agetty ttyS0 115200
```

```
ln -s /usr/lib/systemd/system/serial-getty\@.service /etc/systemd/system/getty.target.wants/serial-getty@ttyS0.service
```

```
[root@localhost ~]# cat /etc/default/grub
GRUB_CMDLINE_LINUX_DEFAULT="console=tty0 console=ttyS0,9600n8"
GRUB_TERMINAL=serial
GRUB_SERIAL_COMMAND="serial --speed=9600 --unit=0 --word=8 --parity=no --stop=1"

add the following line in /etc/inittab
[root@localhost ~]# tail -1 /etc/inittab
S0:12345:respawn:/sbin/agetty ttyS0 115200

add the following line in /etc/securetty file.
[root@localhost ~]# echo "ttyS0" >> /etc/securetty

update grub.cfg
[root@localhost ~]# grub2-mkconfig -o /boot/grub2/grub.cfg
Generating grub.cfg ...
Found linux image: /boot/vmlinuz-3.3.5-2.fc16.x86_64
Found initrd image: /boot/initramfs-3.3.5-2.fc16.x86_64.img
done
``






Если grub1, то вообще без проблем, дописываем console=ttyS0 и всё
[http://open-os.ru/probros-konsoli-virtualnoj-mashiny-v-xost-mashinu-na-baze-kvm/](http://open-os.ru/probros-konsoli-virtualnoj-mashiny-v-xost-mashinu-na-baze-kvm/)




Короче ничего не получилось, хотя я не уверен в кабеле. А на виртуальной всё ок
Либо надо включать в биосе, как на медиатеке. У себя я не нашёл

[http://klinkov.ya.ru/replies.xml?item_no=938](http://klinkov.ya.ru/replies.xml?item_no=938)

[http://www.linuxlib.ru/HowTo/Text-Terminal-HOWTO.html](http://www.linuxlib.ru/HowTo/Text-Terminal-HOWTO.html)

[http://www.lexpr.ru/node/514](http://www.lexpr.ru/node/514)
[http://vladimir-stupin.blogspot.ru/2009/09/ubuntu.html](http://vladimir-stupin.blogspot.ru/2009/09/ubuntu.html)

[http://www.altlinux.org/SerialLogin](http://www.altlinux.org/SerialLogin)
[http://0pointer.de/blog/projects/instances.html](http://0pointer.de/blog/projects/instances.html)

[http://blog.baturin.org/2009/08/linux.html](http://blog.baturin.org/2009/08/linux.html)
[http://www.dobromyslov.ru/sysadmin/connect-usb-to-com-rs232-cable/linux-connect-usb-to-com-rs232-cable](http://www.dobromyslov.ru/sysadmin/connect-usb-to-com-rs232-cable/linux-connect-usb-to-com-rs232-cable)

[http://ru.opensuse.org/SDB:Systemd](http://ru.opensuse.org/SDB:Systemd)

[http://www.opennet.ru/tips/info/2102.shtml](http://www.opennet.ru/tips/info/2102.shtml)

[http://open-os.ru/probros-konsoli-virtualnoj-mashiny-v-xost-mashinu-na-baze-kvm/](http://open-os.ru/probros-konsoli-virtualnoj-mashiny-v-xost-mashinu-na-baze-kvm/)

[http://rusdir.blogspot.ru/2010/12/linux.html](http://rusdir.blogspot.ru/2010/12/linux.html)

[http://www.opennet.ru/openforum/vsluhforumID1/37737.html](http://www.opennet.ru/openforum/vsluhforumID1/37737.html)


[http://lost-and-found-narihiro.blogspot.ru/2012/05/kvm-how-to-connect-to-fedora-vms-which.html](http://lost-and-found-narihiro.blogspot.ru/2012/05/kvm-how-to-connect-to-fedora-vms-which.html)

