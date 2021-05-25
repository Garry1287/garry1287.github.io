---
layout: post
title:  "ssh-agent(backup)"
date:   2014-09-30 08:38:50 +0400
categories: linux
tags: linux
---

# ssh-agent(backup)
Под oracle выполни (парольную фразу посложнее)
ssh-keygen -t dsa

Получиться

id_dsa
id_dsa.pub

id_dsa.pub  скопировать на postman и переименовать 
/home/oracle/.ssh/authorized_keys

chmod 700 на .ssh и на эти файлы сделать под oracle



[http://www.ibm.com/developerworks/ru/library/l-backup/index.html](http://www.ibm.com/developerworks/ru/library/l-backup/index.html)



~/.ssh/id_rsa.pub — открытый ключ. Его копируют на сервера, куда нужно получить доступ.
~/.ssh/id_rsa — закрытый ключ. Его нельзя никому показывать. Если вы в письмо/чат скопипастите его вместо pub, то нужно генерировать новый ключ.
 (Я не шучу, примерно 10% людей, которых просишь дать ssh-ключ постят id_rsa, причём из этих десяти процентов мужского пола 100%). 

centos_host - клиент, crystal - сервер. Бэкап сливается на crystal

приватный ключ расположен на клиентском, а публичный копируется на сервара
Ключи генерируются на клиентском, с которого мы хотим получить беспарольный доступ на сервер


backup@emerald-nat:/var/lib/named/master> history
    1  cd 
    2  l
    3  ssh-keygen -t rsa -b 4096
    4  ls
    5  cd .ssh
    6  ls
    7  scp id_rsa.pub backup@crystal.sc.int:.ssh/emerald.pub
    8  ssh crystal.sc.int
    9  exit
   10  ssh crystal.sc.int



1) Получается на клиенте сгенерили
2) Скопировали pub на сервер
3) Ходим с клиента на сервер без пароля

Или наоборот
1) На сервере сгенерили под нужного usera
2) Скопировали pub на клиентов
3) Ходим с сервера на клиентов без пароля

Для BackupPC наоборот - сервер хранения цепляется на клиентские компы и забирает оттуда бэкапы. Получается генериться всего одна пара ключей


Варианта два
Первый вариант при генерации ключей не указывать парольную фразу, что не секьюрно, так как, если приватный украдут, то у злоумышленника
будет доступ ко всем серверам, на которых расположен публичный

Второй вариант с парольной фразой, которая шифрует приватный ключ. Но для этого нужно запустить ssh-agent, который играет роль шлюза.
С его помощью программа ssh может использовать заранее расшифрованный ключ вместо того, 
чтобы запрашивать парольную фразу при каждой необходимости.  ssh-add - прога, добавляющая (отправляющая) парольную фразу программе ssh-agent.
После её запуска парольная фраза не будет запрашиваться. Проблема возникает только при ребуте, или при падение процесса ssh-agent
keychain - это скрипт, который запускается на клиенте.  keychain, представляющий собой интерфейс к программам ssh-agent и ssh-add,
 облегчающий процесс беспарольного доступа.
Когда вы зайдете на серверы в следующий раз, keychain запросит парольную фразу. 
При последующих входах, однако, ввод парольной фразы не будет запрашиваться до момента перезагрузки сервера.




[http://vds-admin.ru/ssh/ssh-autentifikatsiya-po-klyucham-ispolzovanie-programm-ssh-keygen-i-ssh-agent](http://vds-admin.ru/ssh/ssh-autentifikatsiya-po-klyucham-ispolzovanie-programm-ssh-keygen-i-ssh-agent)
[http://linux26.ru/articles/users/generacziya-klyuchej-dlya-besparolnogo-vxoda.html](http://linux26.ru/articles/users/generacziya-klyuchej-dlya-besparolnogo-vxoda.html)
[http://nix-sa.blogspot.ru/2011/06/ssh.html](http://nix-sa.blogspot.ru/2011/06/ssh.html)

useradd
[http://yapro.ru/web-master/unix/useradd.html](http://yapro.ru/web-master/unix/useradd.html)
[http://lostop.ru/page/42/](http://lostop.ru/page/42/)

