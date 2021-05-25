---
layout: post
title:  "fail2ban-new"
date:   2018-11-03 10:38:53 +0300
categories: linux
tags: linux
---

# fail2ban-new
free-nx
[http://dmitrykhn.homedns.org/dm/nx_svr.html](http://dmitrykhn.homedns.org/dm/nx_svr.html)



ssh via key
[http://www.opennet.ru/base/sec/ssh_intro.txt.html](http://www.opennet.ru/base/sec/ssh_intro.txt.html)





Основной конфигурационный файл Fail2Ban находится /etc/fail2ban/jail.conf. В самый низ данного файла добавим следующий блок:

nano /etc/fail2ban/jail.conf

[asterisk-iptables]
 
enabled  = true
filter   = asterisk
action   = iptables-allports[name=ASTERISK, protocol=all]
           sendmail-whois[name=ASTERISK, dest=root, sender=fail2ban@asterisk]
logpath  = /var/log/asterisk/fail2ban
maxretry = 3
bantime = 3600

Описание параметров:

enabled — значение true указывает что данный jail активен, false выключает действие изолятора.
filter — имя фильтра с регулярными выражениями, по которым идёт поиск.
logpath — путь к файлу логам FreeSWITCH, который программа Fail2ban будет обрабатывать с помощью заданного ранее фильтра.
action – операция, которая должна быть выполнена, если значение счётчика стало равным значению параметра maxretry.
maxretry  - количество неудачных запросов за которое банится хост.
bantime -  промежуток времени по умолчанию в секундах на которое банится провинившийся хост.
