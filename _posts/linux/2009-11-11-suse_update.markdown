---
layout: post
title:  "suse_update"
date:   2009-11-11 19:30:46 +0300
categories: linux
tags: linux
---

# suse_update
Удалить старые репозитории.
Отключить старые


Обновить OSS репозиторий
Просто исправив версию в старом на новую


Установить rpm
rpm -Uhv '[http://download.opensuse.org/distribution/11.0/repo/oss/suse/i586/rpm-4.4.2-199.1.i586.rpm](http://download.opensuse.org/distribution/11.0/repo/oss/suse/i586/rpm-4.4.2-199.1.i586.rpm)' 

Обновить zypper
zypper in zypper

Добавить репозитории
Включить, которые отключал и изменение версии
Updates и Non-oss

Теперь об обещанном подводном камне. В процессе обновления, при изменении файлов в /etc/sysconfig , zypper вызывает SuSEconfig, 
для генерации разных системных файлов в /etc . 
В то же время в процессе обновления в системе меняются некоторые утилиты, которые вызываются из SuSEconfig'a, 
что иногда вызывает его временную неработоспособность. Эта "неработоспособность" приводит к тому, что процесс обновлений прерывается и не факт, 
что его затем можно будет продолжить корректно.
 Возможно, что к релизу этот баг подправят. Но пока работает именно так, как я описал. К счастью, SuSEconfig можно отключить. 
Делается это редактированием файла /etc/sysconfig/suseconfig.
 Достаточно в этом файле изменить значение переменной ENABLE_SUSECONFIG="yes" на ENABLE_SUSECONFIG="no" . 
После этого SuSEconfig работать больше не будет. На обновленной системе его затем будет необходимо включить обратно.

Затем, рекомендуется изменить в файле /etc/zypp/zypp.conf (если не сделали этого раньше) параметр commit.download.mode в значение DownloadInAdvance. 
Это заставит zypper выполнить обновление после предварительного выкачивания всех пакетов.
После завершения обновления включаем обратно SuSEconfig и запускаем его из командной строки: SuSEconfig (обратите внимание, что буква 'u' маленькая). 
После того, как он отработал, я решил перестраховаться и запустил еще раз 

Выполнить скрипт
#!/bin/sh
zypper ref
zypper lu
zypper -n dup -l
mkinitrd
reboot


mkinitrd - это скрипт, выполняющий пересборку initrd (образа, критичного для загрузки системы).
 Также желательно запустить zypper ve для дополнительной проверки системы на целостность зависимостей.

[http://download.opensuse.org/distribution/12.1/repo/oss/suse/i586/rpm-4.9.1.2-1.5.i586.rpm](http://download.opensuse.org/distribution/12.1/repo/oss/suse/i586/rpm-4.9.1.2-1.5.i586.rpm)