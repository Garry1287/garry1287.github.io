---
layout: post
title:  "cryptosetup+loop"
date:   2013-07-21 10:14:59 +0400
categories: crypt backup
tags: backup
---

# cryptosetup+loop
[https://cryptopunks.org/article/awesome%2Btruecrypt%2Balternative%2Bfor%2Blinux/](https://cryptopunks.org/article/awesome%2Btruecrypt%2Balternative%2Bfor%2Blinux/)

Два слова о петлевом устройстве (Loop-device)
Loopback Device (loop) это механизм ядра Linux, используемый для интерпретации файлов как реальных блочных устройств. 
Главное, что все инструменты, используемые для работы с реальными дисками (например mount), могут быть использованы и для петлевых устройств.


Образ привязывается к loop-устройству, после этого система может работать с этим устройством, как с обычным блочным. 
  losetup - set up and control loop devices
cryptsetup - manage plain dm-crypt and LUKS encrypted volumes

[http://mydebianblog.blogspot.ru/2012/05/linux-loop-device-aes.html](http://mydebianblog.blogspot.ru/2012/05/linux-loop-device-aes.html)




Создаем файл 12
dd if=/dev/urandom of=12 bs=512K count=40
cryptsetup luksFormat 12
Вводи YES и пароль 2 раза

Представляем файл 12 в виде блочного устройства
losetup /dev/loop0 /home/garry/12

Открываем контейнер
cryptsetup luksOpen /dev/loop0 12_dev

Создаем файловую систему
mkfs.ext4 /dev/mapper/12_dev

Создаём папку для монтирования
mkdir /home/garry/12dir

Монтируем
mount /dev/mapper/12_dev /home/garry/12dir/

chown garry:users 12dir
Заводим файл, в этой папке и т д, например файл с паролями 11 или 12

Отмонтируем
umount /dev/mapper/12_dev

Извлекаем контейнер
cryptsetup luksClose /dev/mapper/12_dev

Чтобы пользоваться - необходимо открыть контейнер, монтировать, записывать, отмонтировать, закрывать контейнер

[http://huh-muh.blogspot.ru/2014/06/linux.html](http://huh-muh.blogspot.ru/2014/06/linux.html)
[https://habrahabr.ru/post/59247/](https://habrahabr.ru/post/59247/)
[http://help.ubuntu.ru/wiki/luks_cloud](http://help.ubuntu.ru/wiki/luks_cloud)
[http://rus-linux.net/MyLDP/sec/Hard-drive-encryption-in-Linux.html](http://rus-linux.net/MyLDP/sec/Hard-drive-encryption-in-Linux.html)
[https://losst.ru/shifrovanie-diskov-v-linux](https://losst.ru/shifrovanie-diskov-v-linux)









Представляем файл 12 в виде блочного устройства
losetup /dev/loop0 /home/garry/12

Открываем контейнер
cryptsetup luksOpen /dev/loop0 12_dev


Монтируем
mount /dev/mapper/12_dev /home/garry/12dir/

Отмонтируем
umount /dev/mapper/12_dev

Извлекаем контейнер
cryptsetup luksClose /dev/mapper/12_dev





Работа с LVM аналогична
[http://usefree.com.ua/lvm-and-cryptsetup/](http://usefree.com.ua/lvm-and-cryptsetup/)
[https://debian-administration.org/article/469/How_to_set_up_an_encrypted_filesystem_in_several_easy_steps](https://debian-administration.org/article/469/How_to_set_up_an_encrypted_filesystem_in_several_easy_steps)




[https://wiki.archlinux.org/index.php/Dm-crypt/Device_encryption#Adding_LUKS_keys](https://wiki.archlinux.org/index.php/Dm-crypt/Device_encryption#Adding_LUKS_keys)
[https://askubuntu.com/questions/653866/cryptsetup-luksaddkey-throwing-maximum-keyfile-size-exceeded-error-fix-14-0](https://askubuntu.com/questions/653866/cryptsetup-luksaddkey-throwing-maximum-keyfile-size-exceeded-error-fix-14-0)
[https://habrahabr.ru/post/329648/](https://habrahabr.ru/post/329648/)
[https://cryptopunks.org/article/awesome%2Btruecrypt%2Balternative%2Bfor%2Blinux/](https://cryptopunks.org/article/awesome%2Btruecrypt%2Balternative%2Bfor%2Blinux/)
[https://pastebin.com/QJdPCqbU](https://pastebin.com/QJdPCqbU)


cr_virt         /dev/disk/by-id/ata-WDC_WD2500AAJS-22VTA0_WD-WMART2037954-part2 none       none

openvpn --config /home/garry/MyDocs/mngt-garry.ovpn


udo mkfs.ext4 /dev/mapper/3Gdev
mke2fs 1.43.8 (1-Jan-2018)
Creating filesystem with 767488 4k blocks and 192000 inodes
Filesystem UUID: ebfa7a82-3931-4579-bf25-2a7a4113d2ab
Superblock backups stored on blocks: 
        32768, 98304, 163840, 229376, 294912
