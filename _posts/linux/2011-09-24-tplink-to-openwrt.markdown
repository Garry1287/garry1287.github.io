---
layout: post
title:  "tplink-to-openwrt"
date:   2011-09-24 20:03:18 +0400
categories: linux
tags: linux
---

# tplink-to-openwrt
### 1. ПРОШИВКА TLWR1043

[http://www.youtube.com/watch?v=2mlFc2IK3yE](http://www.youtube.com/watch?v=2mlFc2IK3yE)

# TLWR1043
# Качаем ImageBuilder под нашу архитектуру
[http://downloads.openwrt.org/attitude_adjustment/12.09/ar71xx/generic/OpenWrt-ImageBuilder-ar71xx_generic-for-linux-i486.tar.bz2](http://downloads.openwrt.org/attitude_adjustment/12.09/ar71xx/generic/OpenWrt-ImageBuilder-ar71xx_generic-for-linux-i486.tar.bz2)

# Распаковываем его, переходим в директорию OpenWrt-ImageBuilder-ar71xx_generic-for-linux-i486.
# Смотрим какие профили есть (какие девайсы)

make info

# Запускаем сборку образа с минимумом необходимого

make image PROFILE=TLWR1043 PACKAGES="uhttpd luci kmod-usb-core kmod-usb2 kmod-ledtrig-usbdev kmod-usb-ohci kmod-usb-storage kmod-fs-ext4"

# Готовый образ в ./bin/ar71xx/

# Для перепрошивки с заводской на openWRT.
# openwrt-ar71xx-generic-tl-wr1043nd-v1-squashfs-factory.bin
# Обновление через стандартный web-interface.

# При первом входе через web [http://192.168.1.1](http://192.168.1.1) нужно задать пароль root. После этого можно подключаться по ssh.

/*****
[http://wiki.openwrt.org/doc/howto/generic.sysupgrade](http://wiki.openwrt.org/doc/howto/generic.sysupgrade)

# Для обновления из openwrt
# openwrt-ar71xx-generic-tl-wr1043nd-v1-squashfs-sysupgrade.bin

# Передаём прошивку на роутер 
scp {openwrt-ar71xx-generic-tl-wr1043nd-v1-squashfs-sysupgrade.bin,md5sums} root@192.168.1.1:/tmp/

# Подключаемся к роутеру.
# Проверяем, что все норм
cd /tmp
md5sum -c md5sums 2> /dev/null | grep OK

# use the following command to upgrade:
sysupgrade -v /tmp/openwrt-ar71xx-generic-tl-wr1043nd-v1-squashfs-sysupgrade.bin

*****/

# Получаем Linux на SOHO железячке
root@OpenWrt:~# uname -a
Linux OpenWrt 3.3.8 #1 Sat Mar 23 16:49:30 UTC 2013 mips GNU/Linux


### 2. Монтирование usbflash в качестве root
[http://wiki.openwrt.org/doc/howto/extroot](http://wiki.openwrt.org/doc/howto/extroot)

# Что мы имеем:

root@OpenWrt:~# df -h
Filesystem                Size      Used Available Use% Mounted on
rootfs                    4.9M    444.0K      4.4M   9% /
/dev/root                 2.0M      2.0M         0 100% /rom
tmpfs                    14.3M    872.0K     13.4M   6% /tmp
tmpfs                   512.0K         0    512.0K   0% /dev
/dev/mtdblock3            4.9M    444.0K      4.4M   9% /overlay
overlayfs:/overlay        4.9M    444.0K      4.4M   9% /

root@OpenWrt:/tmp# free
             total         used         free       shared      buffers
Mem:         29212        24824         4388            0         1920
-/+ buffers:              22904         6308


# 32MB RAM и 8MB flash. Не сильно разгуляешься. 
# Поэтому добавим swap 128MB, root 512MB, home все остальное.

# Подготовим flash на компе.
sudo cfdisk /dev/sdb
# Создадим три раздела:
/dev/sdb1 512M type83 for root booting
/dev/sdb2 128M type82 for swap
/dev/sdb3 ~3G  type83 for home

# Форматируем 
mkfs.ext4 /dev/sdb1
mkfs.ext4 /dev/sdb3

# Вставляем флешку в роутер.

# Устанавливаем пакеты:
opkg update
opkg install block-extroot block-hotplug block-mount 

# Мигрируем на новый корень

mkdir -p /tmp/{cproot,sda1}
mount /dev/sda1 /tmp/sda1
mount --bind / /tmp/cproot
tar -C /tmp/cproot -cvf - . | tar -C /tmp/sda1 -xf -
umount /tmp/cproot
umount /tmp/sda1

# Нужно настроить fstab (можно через web)

config global 'automount'
        option from_fstab '1'
        option anon_mount '1'

config global 'autoswap'
        option from_fstab '1'
        option anon_swap '0'

config swap
        option device '/dev/sda2'
        option enabled '1'

config mount
        option device '/dev/sda3'
        option options 'rw,sync,noatime,nodiratime'
        option enabled_fsck '0'
        option enabled '1'
        option fstype 'ext4'
        option target '/home'

config mount
        option enabled '1'
        option device '/dev/sda1'
        option target '/'
        option fstype 'ext4'
        option options 'rw,sync,noatime,nodiratime'
        option is_rootfs '1'


# Далее редактируем /etc/init.d/fstab
Нужно закоментировать следующие строчки:
#        [ -e /tmp/fstab ] || {                                                                                          
#                echo '# WARNING: this is an auto generated file, please use uci to set defined filesystems' > /tmp/fstab
#        } 

reboot

# После перезагрузки:
root@OpenWrt:~# df -h
Filesystem                Size      Used Available Use% Mounted on
rootfs                  488.6M     32.0M    431.9M   7% /
/dev/root                 2.0M      2.0M         0 100% /rom
tmpfs                    14.3M    916.0K     13.4M   6% /tmp
tmpfs                   512.0K         0    512.0K   0% /dev
/dev/sda1               488.6M     32.0M    431.9M   7% /overlay
overlayfs:/overlay      488.6M     32.0M    431.9M   7% /
/dev/sda3                 3.1G    111.4M      2.9G   4% /home
root@OpenWrt:~# 
root@OpenWrt:~# 
root@OpenWrt:~# free
             total         used         free       shared      buffers
Mem:         29212        24216         4996            0         3964
-/+ buffers:              20252         8960
Swap:       130692           56       130636

# Теперь можем устанавливать много полезного. Я установил первым делом ip и openvpn
opkg update
opkg install ip openvpn







