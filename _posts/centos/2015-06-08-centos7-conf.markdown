---
layout: post
title:  "centos7-conf"
date:   2015-06-08 18:43:11 +0300
categories: centos7-conf
tags: centos
---

# centos7-conf
[https://access.redhat.com/documentation/ru-RU/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/index.html](https://access.redhat.com/documentation/ru-RU/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/index.html)
[http://blog.acmenet.ru/2016/01/01/centos-7-2-install/](http://blog.acmenet.ru/2016/01/01/centos-7-2-install/)
[https://exz.su/2015/01/27/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-centos-7/](https://exz.su/2015/01/27/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-centos-7/)
[https://www.centos.org/forums/viewtopic.php?t=53972](https://www.centos.org/forums/viewtopic.php?t=53972)

Сразу же выключаем Network Manager.

systemctl stop NetworkManager && systemctl disable NetworkManager && systemctl restart network

Настройка сети


vi /etc/sysconfig/selinux
 
SELINUX=disabled


yum -y install epel-release
[https://wiki.centos.org/AdditionalResources/Repositories](https://wiki.centos.org/AdditionalResources/Repositories)


systemctl stop firewalld && systemctl disable firewalld


 yum -y install yum-cron yum-utils


 yum install iptables-services
 iptables -P INPUT DROP
 
service iptables save







/etc/fail2ban/jail.d/iptables.conf 

[ssh-iptables]
enabled = true
filter = sshd
action = iptables[name=SSH, port=2222, protocol=tcp]
logpath = %(sshd_log)s
maxretry = 5
bantime = 86400

По умолчанию делает action в firewalld

[https://sys-adm.in/os/nix/497-fail2ban-on-centos.html](https://sys-adm.in/os/nix/497-fail2ban-on-centos.html)
[https://bozza.ru/art-232.html](https://bozza.ru/art-232.html)
[https://sys-adm.in/os/nix/497-v-on-centos.html](https://sys-adm.in/os/nix/497-v-on-centos.html)
[https://www.centos.org/forums/viewtopic.php?t=47284](https://www.centos.org/forums/viewtopic.php?t=47284)
[https://vps.ua/wiki/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_Fail2ban](https://vps.ua/wiki/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_Fail2ban)
[http://vam.in.ua/index.php/it/15-other-posix/243-linux-fail2ban-configuring.html](http://vam.in.ua/index.php/it/15-other-posix/243-linux-fail2ban-configuring.html)

Хорошая статья
[https://www.digitalocean.com/community/tutorials/how-to-protect-ssh-with-fail2ban-on-centos-7](https://www.digitalocean.com/community/tutorials/how-to-protect-ssh-with-fail2ban-on-centos-7)


Например, удалим из Fail2Ban IP адрес 192.168.1.101, который был забанен в соответствии с правилами из секции [ssh-iptables] :

$ sudo fail2ban-client set ssh-iptables unbanip 192.168.1.101














3) Настройка yum-cron для своевременного оповещения об обновлениях

# yum install yum-cron
# vim /etc/yum/yum-cron.conf

[commands]
update_messages = yes
download_updates = no
apply_updates = no
random_sleep = 360

[emitters]
system_name = test.localnet
emit_via = stdio
ouput_width = 80

[email]
email_from = root@localhost
email_to = root
email_host = localhost

[groups]
group_list = None
group_package_types = mandatory, default

[base]
debuglevel = -2
mdpolicy = group:main

#активируем проверку обновлений и запустим yum-cron
# systemctl enable yum-cron
# systemctl start yum-cron




SUDO
#Sudo access for wheel group users
%wheel  ALL=(ALL)       NOPASSWD: ALL























[https://kamaok.org.ua/?p=1735](https://kamaok.org.ua/?p=1735)
1.Настройка/проверка сети, DNS-серверов, имени хоста,отключение IPv6

 
# vi /etc/sysconfig/network-scripts/ifcfg-ens33
1
	
# vi /etc/sysconfig/network-scripts/ifcfg-ens33

TYPE=Ethernet
BOOTPROTO=none
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=no
IPV6_AUTOCONF=no
IPV6_DEFROUTE=no
IPV6_PEERDNS=no
IPV6_PEERROUTES=no
IPV6_FAILURE_FATAL=no
NAME=ens33
UUID=811c6d24-2c55-48e8-9948-c28bffafb63d
DEVICE=ens33
ONBOOT=yes
IPADDR=192.168.1.86
PREFIX=24
GATEWAY=192.168.1.1
DNS1=8.8.8.8
DNS2=8.8.4.4
DOMAIN=domain.com
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
	
TYPE=Ethernet
BOOTPROTO=none
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=no
IPV6_AUTOCONF=no
IPV6_DEFROUTE=no
IPV6_PEERDNS=no
IPV6_PEERROUTES=no
IPV6_FAILURE_FATAL=no
NAME=ens33
UUID=811c6d24-2c55-48e8-9948-c28bffafb63d
DEVICE=ens33
ONBOOT=yes
IPADDR=192.168.1.86
PREFIX=24
GATEWAY=192.168.1.1
DNS1=8.8.8.8
DNS2=8.8.4.4
DOMAIN=domain.com

# service network restart
1
	
# service network restart

# vi /etc/resolv.conf
1
	
# vi /etc/resolv.conf

search domain.com 
nameserver 8.8.8.8
nameserver 8.8.4.4
1
2
3
	
search domain.com 
nameserver 8.8.8.8
nameserver 8.8.4.4

# vi /etc/hostname
1
	
# vi /etc/hostname

centos71.domain.com
1
	
centos71.domain.com

# hostname
1
	
# hostname

centos71.domain.com
1
	
centos71.domain.com

Второй способ установки имени хоста
# hostnamectl set-hostname centos71.domain.com
1
	
# hostnamectl set-hostname centos71.domain.com

# systemctl restart systemd-hostnamed
1
	
# systemctl restart systemd-hostnamed

Настройка файла /etc/hosts
# vi /etc/hosts
1
	
# vi /etc/hosts

192.168.1.86 centos71.domain.com centos71
1
	
192.168.1.86 centos71.domain.com centos71

# systemctl restart systemd-hostnamed
1
	
# systemctl restart systemd-hostnamed

 

2.Подключение Epel-репозитария
# yum install epel-release
1
	
# yum install epel-release

Либо
# rpm -Uvh [http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-8.noarch.rpm](http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-8.noarch.rpm)
1
	
# rpm -Uvh [http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-8.noarch.rpm](http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-8.noarch.rpm)

 

3.Установка базовых пакетов

yum install nano traceroute mtr curl wget screen mc tcpdump ntsysv bind-utils rsync unzip zip jwhois pwgen mailx net-tools

 

4.Отключение Selinux (при необходимости)

	
# sed -i 's/SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config

# setenforce 0
1
	
# setenforce 0

Проверяем
# getenforce
1
	
# getenforce

Permissive
1
	
Permissive

 

5.Остановка и отключение firewalld. Установка iptables в качестве файерволла(при необходимости)
# systemctl stop firewalld
1
	
# systemctl stop firewalld

# systemctl disable firewalld
1
	
# systemctl disable firewalld

# yum install iptables-services iptables
1
	
# yum install iptables-services iptables

# systemctl enable iptables
1
	
# systemctl enable iptables

# nano /etc/sysconfig/iptables-config
1
	
# nano /etc/sysconfig/iptables-config

IPTABLES_SAVE_ON_STOP="yes"
IPTABLES_SAVE_ON_RESTART="yes"
IPTABLES_SAVE_COUNTER="yes"
1
2
3
	
IPTABLES_SAVE_ON_STOP="yes"
IPTABLES_SAVE_ON_RESTART="yes"
IPTABLES_SAVE_COUNTER="yes"

Копируем init-скрипт для того, чтобы можно было сохранять правила командой /etc/init.d/iptables save
# cp /usr/libexec/iptables/iptables.init /etc/init.d/iptables
1
	
# cp /usr/libexec/iptables/iptables.init /etc/init.d/iptables

# systemctl start iptables
1
	
# systemctl start iptables

# iptables -F
1
	
# iptables -F

# /etc/init.d/iptables save
1
	
# /etc/init.d/iptables save

# systemctl restart iptables
1
	
# systemctl restart iptables

 

6.Настройка SSH-сервера

Создание SSH-ключей
# ssh-keygen -t rsa -b 2048
1
	
# ssh-keygen -t rsa -b 2048

# nano /etc/ssh/sshd_config
1
	
# nano /etc/ssh/sshd_config

Port 2220
Protocol 2
PermitRootLogin without-password
AuthorizedKeysFile      .ssh/authorized_keys
PermitEmptyPasswords no
PasswordAuthentication yes
1
2
3
4
5
6
	
Port 2220
Protocol 2
PermitRootLogin without-password
AuthorizedKeysFile      .ssh/authorized_keys
PermitEmptyPasswords no
PasswordAuthentication yes

# sshd -t && systemctl restart sshd
1
	
# sshd -t && systemctl restart sshd

Для корректной работы sshd-агента(если нужно пробрасывать ssh-ключ на другие сервера при подключении через этот сервер)
# nano /etc/ssh/sshd_config
1
	
# nano /etc/ssh/sshd_config

AllowAgentForwarding yes
1
	
AllowAgentForwarding yes

# nano /etc/ssh/ssh_config
1
	
# nano /etc/ssh/ssh_config

Host *
   ForwardAgent yes
1
2
	
Host *
   ForwardAgent yes

# sshd -t && systemctl restart sshd
1
	
# sshd -t && systemctl restart sshd

 

7.Настройка редактора по умолчанию(при необходимости)
Например. Установим редактор по умолчанию nano
Только для пользователя root
# nano /root/.bashrc
1
	
# nano /root/.bashrc

export EDITOR="nano"
1
	
export EDITOR="nano"

# cd ~root && source .bashrc
1
	
# cd ~root && source .bashrc

(или перелогиниваемся)
Если необходимо для всех пользователей установить редактор по умолчанию,то
# nano /etc/bashrc
1
	
# nano /etc/bashrc

export EDITOR="nano"
1
	
export EDITOR="nano"

# cd ~<username> && source .bashrc
1
	
# cd ~<username> && source .bashrc

(или перелогиниваемся)

 

8.Настройка/проверка часового пояса. Настройка синхронизации времени
Просмотр существующих поясов
# timedatectl list-timezones
1
	
# timedatectl list-timezones

Установка нужного часового пояса
# timedatectl set-timezone Europe/Kiev
1
	
# timedatectl set-timezone Europe/Kiev

Просмотр текущих значений
# timedatectl
1
	
# timedatectl

Настройка синхронизации времени
Ручная
# yum install ntpdate
1
	
# yum install ntpdate

# ntpdate  0.ua.pool.ntp.org
1
	
# ntpdate  0.ua.pool.ntp.org

(для Украины)
Синхронизация BIOS-времени с системным временем
# hwclock --systohc
1
	
# hwclock --systohc

Автоматическая
# yum install ntp
1
	
# yum install ntp

# systemctl enable ntpd
1
	
# systemctl enable ntpd

# systemctl start ntpd
1
	
# systemctl start ntpd

 

9. Отключение ненужных служб
Просмотр активных/запущенных служб
# systemctl list-units --type service
1
	
 systemctl list-units --type service

Отключение ненужных служб
Например
# systemctl disable NetworkManager.service
1
	
# systemctl disable NetworkManager.service

 

10.Отключение IPv6(при необходимости)
# nano /etc/sysctl.conf
1
	
# nano /etc/sysctl.conf

net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
1
2
	
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1

# sysctl -p
1
	
# sysctl -p

 

11.Установка порога использования swap(при необходимости)
Уменьшение процента свободной оперативной памяти, по достижению которой системы будет использовать файл подкачи(по умолчанию установлено 60)
# nano /etc/sysctl.conf
1
	
# nano /etc/sysctl.conf

vm.swappiness = 10
1
	
vm.swappiness = 10

# sysctl -p
1
	
# sysctl -p

 

12.Настройка Postfix
# nano /etc/postfix/main.cf
1
	
# nano /etc/postfix/main.cf

myhostname = centos71.domain.com
mydomain = domain.com
myorigin = $mydomain
inet_interfaces = localhost
inet_protocols = ipv4
mydestination = $myhostname, localhost.$mydomain, localhost
1
2
3
4
5
6
	
myhostname = centos71.domain.com
mydomain = domain.com
myorigin = $mydomain
inet_interfaces = localhost
inet_protocols = ipv4
mydestination = $myhostname, localhost.$mydomain, localhost

# postfix check && systemctl restart postfix
1
	
# postfix check && systemctl restart postfix

# systemctl enable postfix
1
	
# systemctl enable postfix

 

13.Установка почтового алиаса(при необходимости)
Если нужно почту root-пользователя пересылать на свой почтовый ящик
# nano /etc/aliases
1
	
# nano /etc/aliases

root:   myuser@domain.com
1
	
root:   myuser@domain.com

# newaliases
1
	
# newaliases

 

14.Создание привилегированного пользователя с правом выполнения всех команд с помощью SUDO без пароля(при необходимости)
# useradd -m -d /home/myuser -s /bin/bash myuser
1
	
# useradd -m -d /home/myuser -s /bin/bash myuser

# passwd myuser
1
	
# passwd myuser

# visudo
1
	
# visudo

myuser       ALL=(ALL)       NOPASSWD: ALL
1
	
myuser       ALL=(ALL)       NOPASSWD: ALL

Если необходимо дать привилегированный доступ группе wheel без пароля(предварительно включим в эту группу нашего пользователя)
# usermod -a -G wheel  myuser
1
	
# usermod -a -G wheel  myuser

# visudo
1
	
# visudo

%wheel        ALL=(ALL)       NOPASSWD: ALL
1
	
%wheel        ALL=(ALL)       NOPASSWD: ALL

 

15.Настройка максимального количества установленных ядер в системе(старые ядра будут автоматически удаляться при установки новых ядер)
# nano /etc/yum.conf
1
	
# nano /etc/yum.conf

installonly_limit=3
1
	
installonly_limit=3

 

16.Перегружаем систему и проверяем корректность ее работы после перезагрузки


