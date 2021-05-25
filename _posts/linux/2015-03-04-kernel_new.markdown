---
layout: post
title:  "kernel_new"
date:   2015-03-04 22:02:49 +0300
categories: linux
tags: linux
---

# kernel_new
[http://blog.vpsville.ru/blog/howto/140.html](http://blog.vpsville.ru/blog/howto/140.html)
[https://linuxinsider.ru/kak-obnovit-versiyu-yadra-v-centos-7/](https://linuxinsider.ru/kak-obnovit-versiyu-yadra-v-centos-7/)


# rpm --import [https://www.elrepo.org/RPM-GPG-KEY-elrepo.org](https://www.elrepo.org/RPM-GPG-KEY-elrepo.org)
# rpm -Uvh [http://www.elrepo.org/elrepo-release-7.0-2.el7.elrepo.noarch.rpm](http://www.elrepo.org/elrepo-release-7.0-2.el7.elrepo.noarch.rpm)
Yum — найти доступные версии ядра

Затем установите последнее стабильное ядро ​​магистрали:

 

    # yum --enablerepo=elrepo-kernel install kernel-ml

[https://kamaok.org.ua/?p=372](https://kamaok.org.ua/?p=372)
[http://blog.stolbunsky.com/2016/01/upgrade-centos7-kernel.html](http://blog.stolbunsky.com/2016/01/upgrade-centos7-kernel.html)


1.Просмотр установленных ядер:

# rpm -q kernel
1
	
# rpm -q kernel

 

2.Устанавливаем пакет yum-utils:

# yum install yum-utils
1
	
# yum install yum-utils

 

3.Используем утилиту package-cleanup, который входит в состав пакета yum-utils для удаления всех старых  ядер , оставляя при этом два самых свежих ядра

# package-cleanup --oldkernels --count=2
1
	
# package-cleanup --oldkernels --count=2

 

4.Просмотр оставшихся установленных ядер:

# rpm -q kernel
1
	
# rpm -q kernel

 

5. При необходимости определяем кол-во установленных в системе ядер

# nano /etc/yum.conf
1
	
# nano /etc/yum.conf

installonly_limit=3
1
	
installonly_limit=3
