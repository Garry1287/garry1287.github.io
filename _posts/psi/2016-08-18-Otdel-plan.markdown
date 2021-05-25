---
layout: post
title:  "Otdel-plan"
date:   2016-08-18 08:25:57 +0300
categories: PSI
tags: PSI
---

# Otdel-plan
1. Backup
Перейти на snmpv3 
[http://www.halfgaar.net/backing-up-unix](http://www.halfgaar.net/backing-up-unix)

Baracuda
Самописный скрипт
Bontmia
[http://rus-linux.net/MyLDP/BOOKS/sag-09/multi-level-backups.html](http://rus-linux.net/MyLDP/BOOKS/sag-09/multi-level-backups.html)
dar
rdiff-backup
fsbackup

dar — продвинутая версия tar, делает инкрементальные бэкапы, причём первую копию можно удалить, оставив от неё только метаинформацию. Сохраняет файлы с атрибутами в файлах заданного размера — например, чтобы на CD можно было записать. Пример использования — делаем первый бэкап, вытаскиваем метоинформацию, бэкап отправляем на FTP — много-много гигабайт, при следующих бэкапах используем метаинформацию как источник знаний о изменившихся файлах и отправляем на FTP инкрементальные копии. Достоинство — на локальной машине нет полной первой копии.

rdiff-backup — фактически система контроля версий. Недостаток — много файлов (сколько было плюс инкрементальные копии). 
Достоинство — иногда интересное — права на файлы хранит не только в виде идентификаторов пользователей, но и имён пользователей, при восстановлении в системе с другими идентификаторами права установятся на, например, www-data правильно. 
Ну и умеет работать с удалёнными архивами по ssh, что, правда, не очень полезно из-за возможных ошибок связи. 
Вариант использования — сделать первый бэкап на локальной машине, rsync'ом отправить на удалённую машину, стереть локальную копию и дальше работать только с удалённой.
Ошибки связи могут быть, но инкрементальные копии делаются быстро. И директорию, которую строит rdiff-backup, трудно записать на носители.


    2) лочим mysql, nginx и postfix останавливаем

Этот способ хорош если у Вас сервисы избыточные — т. е. после остановки nginx на первом сервере ваш сайт продолжит поддерживать в рабочем состоянии второй сервер. И наоборот при бэкапе второго сервера.

    dar — продвинутая версия tar, делает инкрементальные бэкапы, причём первую копию можно удалить, оставив от неё только метаинформацию.

tar это тоже умеет. Собственно, именно таким образом я его и использую. 

    good, reliable backups require forethought, effort and planning

И я о том же. Если бэкапить не особо вникая что и как — можно оказаться у разбитого (или, как минимум, серьёзно треснувшего) корыта после восстановления их таких бэкапов.

    A backup is more than data

IMHO необходимость поддержки разнообразных расширенных атрибутов и дырявых (sparse) файлов зависит от конкретных условий. Например, я использую расширенные атрибуты только для пометки самих бэкапов неизменяемыми (immutable), ACL вообще нет, а дырявые файлы делают только p2p-качалки — в таких условиях поддержка этих метаданных не нужна.

    I recommend you stay away from tar.

Я думаю, с этой рекомендацией он погорячился. Фактически его претензии к tar сводятся к необходимости указывать параметр -p при восстановлении бэкапа. Совет использовать --numeric-owner на самом деле корректен только при условии восстановления бэкапа полной системы, а для восстановления отдельных частей (база MySQL, например) да ещё и на другой системе это абсолютно некоррек

Не хотел углубляться в философию, но Вы мне не оставляете выбора. :) Автор статьи ещё не избавился от некоторых детских проблем. С одной стороны, он уже понял чем качественный подход отличается от среднего-общепринятого подхода и перестал слепо доверять софту. С другой, он ещё не понял, что качественно работать может только простой софт… и чем он проще, тем он меньше глючит. Поэтому ему очень хочется и чтобы качественно, и чтобы можно было одну программу запустить (желательно — без особых параметров), и чтобы она «сделала ему красиво». К сожалению, так не бывает. И даже если изредка встречается сложный комбайн, который не глючит — это исключение, подтверждающее правило.

Я не люблю комбайны. Меня вполне устраивает не только то, что tar не разбивает файлы, но и то, что он их не сжимает (точнее, не сжимал раньше, но и сейчас эта фича, к счастью, опциональна). Поэтому если нужно разбить по томам — я лучше вывод tar направлю в утилиту, которая умеет делать только это. Зашифровать — аналогично.

Кроме того, я в таких критических задачах как бэкап предпочитаю консервативные, проверенные десятилетиями решения, а не активно развивающийся софт. Это же не браузер!

P.S. Что касается возможности «проще» достать из архива отдельный файл — у меня необходимость в этом возникает раз в 3-4 года, поэтому необходимости упрощать эту операцию просто нет. А если кто-то это делает регулярно — возможно ему стоит начать использовать какую-нить систему контроля версий файлов. 





В своё время у нас было много копий поломано по этому поводу. Единственно, что DBMS была не MySQL, a ORACLE. Естественно не в фаликах, а «по-взрослому» :))), на raw-devices. Ну и бэкапили на плёнку. Чего и вам всем советую. На всякий случай оргньюанс: кассетки должно быть 3 штука: бабушка, мама и текущая. После бэкапа кассетки — в сейф, размещённый за пределами серверной, лучше за пределами здания. :)

После плясок с бубнами различного диаметра, цвета и звука, пришли к следующему:

— еженощно останавливать Оракл и сливать дидёй (dd) raw-девайсы в бэкап, на плёнку (кстати, восстанавливается на ура — быстно и весело)

— экспорт Ораклу делать раз в 2-3 дня (зависит от объёма предполагаемых работ ночером на сервере), это правильно с точки зрения контроля целостности того, чего сливается дидёй.

Кроме того (но это уже не совсем бэкап :)) ), все ФС и те же raw-девайсы rsync-ались на два зеркальных сервера, «боевой» Оракл выкладывал аркайвлоги по мере накопления транзакций, эти логи тоже rsync-ались каждые 5 минут.

По поводу утаптывания бэкапа gzip и иже. А надо? Подумайте о том, сколько лишнего драгоценного времени нужно будет потратить на раскрутку бэкапа в тот момент, когда времени просто не будет хватать. ИМХО дешевле купить пару быстрых стриммеров (скорости и объёмы растут, на вскидку: четветь тера в час на почти теровую кассету), десяток кассет, + построить зеркальный серверок, желательно в территориально удалённой серверной, нежели потерять данные. 




2. Monitoring
Cacti
  [http://habrahabr.ru/post/56345/](http://habrahabr.ru/post/56345/)
  [http://habrahabr.ru/post/105308/](http://habrahabr.ru/post/105308/)
  [http://www.debianhelp.co.uk/cactiplugins.htm](http://www.debianhelp.co.uk/cactiplugins.htm)
  [http://kamfjord.org/2009/04/19/automatic-network-graphing-with-cacti/](http://kamfjord.org/2009/04/19/automatic-network-graphing-with-cacti/)
  [http://docs.cacti.net/plugin:discovery](http://docs.cacti.net/plugin:discovery)
netramet
nagios
ntop
zabbix
Ganglia
Zenoss
  [http://habrahabr.ru/post/142974/](http://habrahabr.ru/post/142974/)
  [http://greendail.ru/node/80](http://greendail.ru/node/80)
  [http://greendail.ru/node/100](http://greendail.ru/node/100)
[http://www.samag.ru/archive/article/1216](http://www.samag.ru/archive/article/1216)


[http://www.network-weathermap.com/about](http://www.network-weathermap.com/about)

Аналог whats up
Munin
[http://www.netxms.org/](http://www.netxms.org/)
[http://kb.nocproject.org/display/SITE/NOC](http://kb.nocproject.org/display/SITE/NOC)
[http://habrahabr.ru/post/126051/](http://habrahabr.ru/post/126051/)
[http://habrahabr.ru/post/125034/](http://habrahabr.ru/post/125034/)



Общий обзор стандартных средств наблюдений за системой
[http://habrahabr.ru/post/49204/](http://habrahabr.ru/post/49204/)


Использовал и Nagios и Zabbix.
+ Nagios есть плагины практически под все задачи
+ Мало требует ресурсов
- Страшный интерфейс
- Муторно писать конфиги для каждого сервера.

Zabbix
+ Большая часть того что нужно идет в комплекте
+ Агенты могут передавать не только статус какого-то процесса (жив/мертв) но и вообще любую инфу. Можно мониторить например, количество активных соединений в nginx, количество запросов в секунду в mysql, загрузку диска и т.п.
+ Поддержка тимплейтов. Создаем тимплейт веб-сервер и подключаем мониторинг N парамеров. Затем для сервера1, сервера2, сервера3 устанавливаем, что нужно использовать это тимплейт. Очень сильно экономит время для настройки.
- При большом количестве параметров неплохо грузит систему. 
[http://habrahabr.ru/post/154723/](http://habrahabr.ru/post/154723/)
[http://www.zabbix.com/documentation/2.0/manual/discovery/low_level_discovery](http://www.zabbix.com/documentation/2.0/manual/discovery/low_level_discovery)
[http://habrahabr.ru/post/139165/](http://habrahabr.ru/post/139165/)
[http://habrahabr.ru/post/155333/](http://habrahabr.ru/post/155333/)

Яндекс карта
[http://www.zabbix.com/forum/showthread.php?t=37480](http://www.zabbix.com/forum/showthread.php?t=37480)

Смс уведомление
[http://habrahabr.ru/post/155321/](http://habrahabr.ru/post/155321/)
[http://habrahabr.ru/post/146509/](http://habrahabr.ru/post/146509/)
[http://habrahabr.ru/post/126963/](http://habrahabr.ru/post/126963/)


Нужна возможность для рисования сети, желательно привязать к Яндекс Карте
Важно наличие статей на русском
Приоритет - cacti познакомиться со всеми возможностями

Мониторинг железа и процессов
monit ([http://mmonit.com/monit/)](http://mmonit.com/monit/))
smart
самописные скрипты


Идеал
Мониторинг каналов (broadcast, multicast, unicast)
Мониторинг unix процессов
Мониторинг доступности устройств
Обратная связь (обработка трапов, письма, смс)
Карта устройств (на основе snmp построить карту устройств)
Функционал whatup
[http://www.manageengine.com/products/oputils/network-discovery-tools.html](http://www.manageengine.com/products/oputils/network-discovery-tools.html)

syslog-ng
rsyslog

Сделать главной в браузере страницу со ссылками на все системы

Rezerv
2 способа доступа в сеть из вне. (2 pptp сервера?) 2 типа vpn (openvpn или vtun)



[http://habrahabr.ru/company/alee/blog/137407/](http://habrahabr.ru/company/alee/blog/137407/)
[http://habrahabr.ru/post/92888/](http://habrahabr.ru/post/92888/)
[http://habrahabr.ru/post/112198/](http://habrahabr.ru/post/112198/)
[http://ru.wikipedia.org/wiki/Enterprise_content_management](http://ru.wikipedia.org/wiki/Enterprise_content_management)

Alfresco — Open Source ECM от Alfresco Software, Inc.
Nuxeo 5 — Open Source ECM от Nuxeo (Лицензия LGPL)
Jahia — Open Source ECM от Jahia Solutions Group


The Dude - небольшая, бесплатная программа, которая предназначена для сканирования сетей, мониторинга работы подключенных к ним
 устройств и предупреждения администратора в случае возникновения каких-либо проблем. 
Утилита работает в автоматическом режиме, самостоятельно определяет типы и виды обнаруженных устройств, проста в установке и работе,
 поддерживает пользовательские иконки и фоны, поддерживает работу с SNMP, ICMP, DNS и TCP, 
предоставляет прямой доступ к управлению удаленными устройствами и т.д. 




взять nocproject.org, оно умеет несколько вариантов построения топологий (хоть по мак-адресам с портов)
OpenNMS - [http://www.opennms.org/](http://www.opennms.org/) монстр на Яве.

[http://www.sergeysl.ru/freebsd-zabbix/](http://www.sergeysl.ru/freebsd-zabbix/)

weather-map (cacti)
[http://habrahabr.ru/post/143747/](http://habrahabr.ru/post/143747/)

Документация
[http://habrahabr.ru/post/119778/](http://habrahabr.ru/post/119778/)
racktables ([http://racktables.org/)](http://racktables.org/))
RackMonkey

ITDB
[http://www.sivann.gr/software/itdb/](http://www.sivann.gr/software/itdb/)








Поместить /etc в svn, чтобы она следила какие изменения мы сделали, чтобы была возможность откатиться
[http://habrahabr.ru/post/29440/](http://habrahabr.ru/post/29440/)


aide
tripwire
Делает хеши файлов и сравнивает, поиск злоумышленников


duplicity
[http://duplicity.nongnu.org/](http://duplicity.nongnu.org/)
[http://rascal.su/blog/2012/02/26/%D0%BF%D1%80%D0%B8%D0%BC%D0%B5%D1%80-%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F-duplicity-%D0%B4%D0%BB%D1%8F-%D0%B8%D0%BD%D0%BA%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D1%82/](http://rascal.su/blog/2012/02/26/%D0%BF%D1%80%D0%B8%D0%BC%D0%B5%D1%80-%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F-duplicity-%D0%B4%D0%BB%D1%8F-%D0%B8%D0%BD%D0%BA%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D1%82/)
[http://citkit.ru/articles/731/](http://citkit.ru/articles/731/)

Журналирование работы
[http://xgu.ru/l3/users/nt-ids-2008-09/syslog/root](http://xgu.ru/l3/users/nt-ids-2008-09/syslog/root)
[http://xgu.ru/wiki/LiLaLo](http://xgu.ru/wiki/LiLaLo)


Ленивый админ
[http://www.ibm.com/developerworks/ru/library/l-11sysadtips/index.html](http://www.ibm.com/developerworks/ru/library/l-11sysadtips/index.html)
[http://www.ibm.com/developerworks/ru/library/l-10sysadtips/index.html?S_TACT=105AGX99&S_CMP=CP](http://www.ibm.com/developerworks/ru/library/l-10sysadtips/index.html?S_TACT=105AGX99&S_CMP=CP)


[http://habrahabr.ru/post/81630/](http://habrahabr.ru/post/81630/)
[http://habrahabr.ru/post/225103/](http://habrahabr.ru/post/225103/)
[http://forums.cacti.net/about23089.html](http://forums.cacti.net/about23089.html)













Делать свои репозитории
в которые можно по своему собирать пакеты???




На kvm хосте собрать машину под zabbix
C помощью dude сделать карту и перенести под забикс






cpu cisco
[http://www.eric-a-hall.com/software/cacti-cisco-cpu/](http://www.eric-a-hall.com/software/cacti-cisco-cpu/)



ctd-c3  - 2 вентилятора (Fan 2 и Fan 4)
ctd-c0  - перегревается









Тулза для управления коммутаторами
[http://local.ucoz.org/publ/hard/svitchi_swithes/upravlenie_kommutatorami/60-1-0-170](http://local.ucoz.org/publ/hard/svitchi_swithes/upravlenie_kommutatorami/60-1-0-170)










smartools
Статиститка Yandex по жёстким дискам