---
layout: post
title:  "upgrade-openwrt"
date:   2009-10-27 12:46:02 +0300
categories: linux
tags: linux
---

# upgrade-openwrt
root@Dz-router:/# /bin/ash /tmp/listuserpackages.sh
User-installed packages are the following:
libc
opkg
kmod-usb-core
busybox
odhcpd
swconfig
kmod-ledtrig-usbdev
kmod-nf-nathelper
base-files
netifd
uboot-envtools
dnsmasq
kmod-usb2
firewall
odhcp6c
fstools
kmod-ath9k
uci
wpad-mini
dropbear
mtd
libgcc
ppp
kmod-gpio-button-hotplug
luci-proto-ipv6
iptables
openvpn-openssl
igmpproxy
ip6tables
luci
kernel
ppp-mod-pppoe



base-files
dnsmasq
dropbear
firewall
igmpproxy
kmod-tun
liblzo
libopenssl
luci-base
luci-theme-bootstrap
odhcpd
openvpn-openssl
opkg
rpcd
uboot-envtools
uhttpd
uhttpd-mod-ubus
zlib



[https://openwrt.org/ru/doc/howto/generic.sysupgrade](https://openwrt.org/ru/doc/howto/generic.sysupgrade)




overlayfs:/overlay 100Мбит
32 мбит swap


Флешку как хранилище сдеалть
Установить minidlna
настроить torren



нет wan interface


[   12.372253]  sda: sda1 sda2 sda3
[   12.383324] sd 0:0:0:0: [sda] Attached SCSI removable disk

sda1 - overlay
swap
sda3 - nas


config 'mount'
        option  target  '/mnt/sda1'
        option  uuid    '6bfa397d-e7fa-498b-b821-6d1c5423e2a8'
        option  enabled '0'

config 'swap'
        option  uuid    '2f9c8bae-4f0f-4a68-b9d1-b50f8f1493b2'
        option  enabled '0'

config 'mount'
        option  target  '/mnt/sda3'
        option  uuid    '84a0a32f-009c-4385-b9e5-5e6ca13809f6'
        option  enabled '0'

        
        
        
tar -C /overlay -cvf - . | tar -C /mnt/sda1 -xf -

Флешка
[http://openwrtblog.blogspot.com/2015/03/openwrt-usb-usb.html](http://openwrtblog.blogspot.com/2015/03/openwrt-usb-usb.html)
[https://openwrt.org/ru/doc/howto/usb.storage](https://openwrt.org/ru/doc/howto/usb.storage)
[https://autohome.org.ua/12-openwrt/10-ustanovka-openwrt-na-vneshnij-nositel-na-routere-wr703n](https://autohome.org.ua/12-openwrt/10-ustanovka-openwrt-na-vneshnij-nositel-na-routere-wr703n)
[https://openwrt.org/docs/guide-user/storage/usb-drives-quickstart](https://openwrt.org/docs/guide-user/storage/usb-drives-quickstart)
Samba
[https://openwrt.org/docs/guide-user/services/nas/usb-storage-samba-webinterface](https://openwrt.org/docs/guide-user/services/nas/usb-storage-samba-webinterface)

root@Dzwrt:~# uci set transmission.@transmission[0].enabled="1"
root@Dzwrt:~# uci commit transmission                                                                                                                                              
root@Dzwrt:~# service transmission restart                                                                                                                                         
root@Dzwrt:~# opkg install minidlna



torrent

[https://openwrt.org/docs/guide-user/services/downloading_and_filesharing/transmission](https://openwrt.org/docs/guide-user/services/downloading_and_filesharing/transmission)
[https://autohome.org.ua/12-openwrt/30-install-transmission-openwrt-wr703n](https://autohome.org.ua/12-openwrt/30-install-transmission-openwrt-wr703n)


[https://habr.com/ru/post/128451/](https://habr.com/ru/post/128451/)







media_dir="PVA,/backup | V,/home/garry/cinema"

media_dir=V,/mnt/sda1/video



config minidlna config
        option 'enabled' '0'
        option user 'minidlna'
        option port '8200'
        option interface 'wlan0' 
        option friendly_name 'OpenWrt DLNA Server'
        option db_dir '/var/run/minidlna'
        option log_dir '/var/log/minidlna'
        option inotify '1'
        option enable_tivo '0'
        option wide_links '0'
        option strict_dlna '0'
        option presentation_url '[http://192.168.1.100:8200](http://192.168.1.100:8200)'
        option notify_interval '900'
        option serial '12345678'
        option model_number '1'
        option root_container '.'
        list media_dir 'V,/mnt/usb/'    
        option album_art_names 'Cover.jpg/cover.jpg/AlbumArtSmall.jpg/albumartsmall.jpg/AlbumArt.jpg/albumart.jpg/Album.jpg/album.jpg/Folder.jpg/folder.jpg/Thumb.jpg/thumb.jpg'

        
        
        list media_dir 'V,/mnt/nas/share/Cinema' 
        
[https://andidoso.blogspot.com/2014/10/openwrt-hdd-samba-nas-server_12.html](https://andidoso.blogspot.com/2014/10/openwrt-hdd-samba-nas-server_12.html)
[https://webaport.com/blog/setup-router-openwrt-usb-hdd-swap-sftp-samba-minidlna/](https://webaport.com/blog/setup-router-openwrt-usb-hdd-swap-sftp-samba-minidlna/)
Не заработал mkv и png









Проблема решена
Дело на самом деле было в Недостатке прав на файлы

Описываю свои действия может кому пригодится.

В Линуксовой ФС Задаём права на папки и файлы командой:

sudo chmod -R 755 папка

Проверяем командой:

sudo -u minidlna ls -l папка

Должно быть для папок - drwxr-xr-x и rwxr-xr-x для файлов.

Важно! Указанные выше права должны быть предоставлены всем папкам по пути к нужной папке. Команду chmod на промежуточные папки можно использовать без аргумента -R.

Если медиаконтент собираем с помощью ссылок, то в конфиге раскомментируем строку:

wide_links=no и пишем wide_links=yes

Для ФС ntfs или fat команда sudo chmod -R 755 папка не прокатит

Я сделал:

В приложении disk для диска с ntfs или fat - расширенные параметры раздела/изменить параметры монтирования, отключаем параметры автоматического подключения и далее выставляем нужные нам параметры. Диск монтируется в /mnt и права доступа становятся как указано выше (по крайней мере у меня так стало).

Спасибо большое всем кто помог мне разобраться!!!!!
Записан
