---
layout: post
title:  "rsyslog-debian"
date:   2018-02-06 09:36:23 +0300
categories: logs
tags: logs
---

# rsyslog-debian
Как настроить сеть (Лучше всего нормальный адрес)
    logs
    backup

На rock повесить адрес из 121 подсети


Установка, репозитории
Автозапуск

Запуск программ при старте Debian:

Добавление скрипта в автозагрузку:

Shell
# update-rc.d имя_в_initd defaults
1
	
# update-rc.d имя_в_initd defaults

Удаление скрипта из автозагрузки:

Shell
# update-rc.d -f имя_в_initd remove
1
	
# update-rc.d -f имя_в_initd remove





        # chmod +x /etc/init.d/nginx
# /usr/sbin/update-rc.d -f nginx defaults      




Логи отправлять на sapphire и на rock (проверить одновременно отправляют или нет)
Оттуда переправлять на debian (аналогично верхней строке)
