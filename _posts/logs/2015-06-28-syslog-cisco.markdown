---
layout: post
title:  "syslog-cisco"
date:   2015-06-28 00:22:21 +0300
categories: logs
tags: logs
---

# syslog-cisco
от 2 до 0 на почту
от 3 до 7 в логи на сервере
от 5 до 0 отправлять с cisco (при необходиомости изменить на 7-0)
logging trap 5



service timestamps debug datetime msec localtime
service timestamps log datetime localtime 
logging on
logging buffered 32768
logging buffered informational
logging facility local2
logging 10.192.10.253
logging monitor debugging
logging trap notifications
logging origin-id hostname
logging history size 0



logging host outside 10.192.10.42
logging trap notifications
logging enable
logging timestamp
logging device-id hostname




facility local2  - cisco
facility local3	 - dlink
facility local4  - zyxel




service timestamps debug datetime msec localtime
service timestamps log datetime localtime 


Because there is a chance that more than one log message can have the same timestamp, you can display messages with sequence numbers so that you can unambiguously refer to a single message. 
By default, sequence numbers in log messages are not displayed. 

service sequence-numbers 

logging on

logging trap notifications
logging buffered 32768


Задание метки источника сообщения (facility), которым будут помечены сообщения, посылаемые на внешний syslog-сервер:(
logging facility local2

тогда на серевере делают
local2.* /var/log/cisco.log 

logging 10.192.10.42

Уровень серьезности, начиная с которого информация выводится на консоль:
logging console 2

Уровень серьезности, начиная с которого информация выводится на монитор (терминальная линия, на которой выдана команда: term monitor):
logging monitor debugging

Уровень серьезности, начиная с которого информация выводится на внешний syslog-сервер:
logging trap informational

добавили в качестве ID имя хоста cisco к каждому сообщению (полезно, если вы собираете логи с нескольких устройств cisco);
logging origin-id hostname

Используется с командой snmp-server enable trap для посылки на snmp сервер логов
logging history size 0

notify syslog

Ограничение количества лог сообщений.

logging rate-limit all 10 except error



Запрет прерывания во время ввода команд

Для того, что бы всплывающие сообщения не прерывали ввод команд в консольном режиме используется команда logging synchronous
Пример:

Router(config-line)#logging synchronous

(config)# login on-failure log
(config)# login on-success log 






Access-list для vty надо использовать 

           RouterOne(config)#access-list 117 permit tcp host 130.218.5.6 any established
           RouterOne(config)#access-list 117 permit tcp host 130.218.5.6 any log-input
           RouterOne(config)#access-list 117 deny ip any any log-input

           RouterOne(config)#line vty 0 4
           RouterOne(config-line)#access-class 117 in

Кол-во пакетов, пропускаемых
ip access-list log-update threshold 10

Сообщения SNMP (SNMP Traps)

   Если на вашем маршрутизаторе запущен SNMP, вы можете использовать SNMP
   уведомления для сбора дополнительной информации с него. Traps
   (уведомления) это пакеты которые посылаются на SNMP сервер когда какое
   то определённое событие произошло на маршрутизаторе, этими событиями
   может быть повышенная температура, изменения в конфигурации, состояние
   интерфейсов итд. Если Вы желаете включить SNMP уведомления на вашем
   маршрутизаторе то следует:

    1. При помощи команды snmp-server host указать SNMP сервер который будет принимать Traps;
    2. Командой snmp-server enable traps включаем SNMP уведомления.

   В следующим примере настроим маршрутизатор отсылать уведомления на SNMP
   сервер с адресом 13.145.6.5:

           RouterOne#config terminal
           Enter configuration commands, one per line. End with CNTL/Z.

           RouterOne(config)#snmp-server host 13.145.6.5 public
           RouterOne(config)#snmp-server enable traps


   В данном примере мы указали маршрутизатору отсылать все возможные
   уведомления (Traps) на SNMP сервер. При помощи дополнительных
   аргументов к команде snmp-server enable traps Вы можете ограничить виды
   посылаемых уведомлений. Обратитесь к документации Cisco по SNMP Traps
   за более детальной информацией.







Логирование попыток доступа через VTY терминалы.

   Контроль попыток подключения к маршрутизатору через vty терминалы очень
   важен. Это может заранее предупредить Вас о попытках злоумышленника
   получить доступ к вашему маршрутизатору. Например Вы хотите чтобы через
   виртуальную консоль к вашему маршрутизатору имел доступ только IP
   130.18.5.6, для этого напишем ACL:

           RouterOne#config terminal
           Enter configuration commands, one per line. End with CNTL/Z.

           RouterOne(config)#access-list 117 permit ip host 130.18.5.6 any
           RouterOne(config)#access-list 117 deny ip any any log-input


   Далее установим этот список доступа на VTY терминалы от 0 до 4:

           RouterOne#config terminal
           Enter configuration commands, one per line.

           RouterOne(config)#line vty 0 4
           RouterOne(config-line)#access-class 117 in


   Теперь при попытках неавторезированого доступа к VTY будет
   сгенирировано лог сообщение подобного вида:

           Oct 13 21:10:44.185 EDT: %SEC-6-IPACCESSLOGP: list 120 denied tcp
           19.8.59.41(63104) - > 0.0.0.0(23), 1 packet


   Многие администраторы хотят иметь полную информацию о всех сеансах на
   VTY терминалах маршрутизатора, как успешных так и заблокированных. Если
   есть необходимость учитывать все сеансы на виртуальных терминалах, то
   хорошей идеей будет использовать параметр established при логировании
   успешных попыток доступа на терминалы, без лишней перегрузки syslog
   сервера. Нужно пропускать без логирования все пакеты уже установленного
   TCP соединения, пропускать и логировать все первые пакеты TCP сессий с
   разрешеных IP и блокировать и логировать остальные пакеты.

   В следующем примере будим логировать все попытки доступа к виртуальным
   терминалам как успешные так и нет:

[http://www.opennet.ru/base/cisco/cisco_logging.txt.html](http://www.opennet.ru/base/cisco/cisco_logging.txt.html)
[http://www.cisco.com/en/US/docs/switches/lan/catalyst2950/software/release/12.1_9_ea1/configuration/guide/swlog.html](http://www.cisco.com/en/US/docs/switches/lan/catalyst2950/software/release/12.1_9_ea1/configuration/guide/swlog.html)


ntp server 10.192.10.42
ntp authenticate
ntp authentication-key 5555 md5 Jk7b3n4Adv 7
ntp trusted-key 5555



ASA



logging host outside 10.192.10.42
logging trap informational
logging enable
logging timestamp
logging device-id hostname







clock timezone MSK +4
clock set 20:03:20 JAN 16 2013


NTP
ntp authentication-key 5555 md5 Jk7b3n4Adv
ntp trusted-key 5555
ntp server 10.192.10.190 key 5555 source outside prefer
ntp authenticate












На rock.sc.ru

local2.* @quartz.sc.ru


на quartz

#Writing into Mysql
$ModLoad ommysql

#write in mysql
if      ($fromhost-ip == '81.20.192.59')
then    ommysql:127.0.0.1,rsyslogdb,username,password


local2.* : ommysql:127.0.0.1,rsyslogdb,username,password






iptech должны получить доступ





Модули
#$ModLoad imudp
#$UDPServerRun 514
# обеспечивает получение по TCP
#$ModLoad imtcp
#$InputTCPServerRun 514


Конфигурационные директивы
$FileOwner root
$FileGroup adm
$FileCreateMode 0640
$DirCreateMode 0755
$Umask 0022







logging message-counter syslog
logging buffered 4096 informational
logging rate-limit all 100 except errors









[http://www.volgablob.ru/wiki/%D0%9E%D0%B1%D0%B7%D0%BE%D1%80_%D0%B2%D0%BE%D0%B7%D0%BC%D0%BE%D0%B6%D0%BD%D0%BE%D1%81%D1%82%D0%B5%D0%B9_RSyslog-%D1%81%D0%B5%D1%80%D0%B2%D0%B5%D1%80%D0%B0](http://www.volgablob.ru/wiki/%D0%9E%D0%B1%D0%B7%D0%BE%D1%80_%D0%B2%D0%BE%D0%B7%D0%BC%D0%BE%D0%B6%D0%BD%D0%BE%D1%81%D1%82%D0%B5%D0%B9_RSyslog-%D1%81%D0%B5%D1%80%D0%B2%D0%B5%D1%80%D0%B0)
[http://habrahabr.ru/post/136537/](http://habrahabr.ru/post/136537/)
[http://www.rsyslog.com/doc/rsyslog_mysql.html](http://www.rsyslog.com/doc/rsyslog_mysql.html)
[http://www.lissyara.su/articles/freebsd/programms/rsyslog+loganalyzer+mysql/](http://www.lissyara.su/articles/freebsd/programms/rsyslog+loganalyzer+mysql/)
[http://www.k-max.name/linux/rsyslog-na-debian-nastrojka-servera/](http://www.k-max.name/linux/rsyslog-na-debian-nastrojka-servera/)
[http://wiki.rsyslog.com/index.php/FailoverSyslogServer](http://wiki.rsyslog.com/index.php/FailoverSyslogServer)
[http://www.rsyslog.com/doc/rsyslog_reliable_forwarding.html](http://www.rsyslog.com/doc/rsyslog_reliable_forwarding.html)
[http://www.cisco.com/en/US/docs/security/asa/asa82/configuration/guide/monitor_syslog.html](http://www.cisco.com/en/US/docs/security/asa/asa82/configuration/guide/monitor_syslog.html)
[http://yakim.org.ua/articles/servers/113-rsyslog-loganalizer.html](http://yakim.org.ua/articles/servers/113-rsyslog-loganalizer.html)
[http://www.dkws.org.ua/phpbb2/viewtopic.php?p=36965](http://www.dkws.org.ua/phpbb2/viewtopic.php?p=36965)
[http://www.cisco.com/web/about/security/intelligence/acl-logging.html](http://www.cisco.com/web/about/security/intelligence/acl-logging.html)
[http://wiki.rsyslog.com/index.php/Configuration_Samples](http://wiki.rsyslog.com/index.php/Configuration_Samples)
[http://doc.12th.ru/doku.php?id=start:syslog](http://doc.12th.ru/doku.php?id=start:syslog)
[http://kobzarcheg.blogspot.ru/2012/10/rsyslog.html](http://kobzarcheg.blogspot.ru/2012/10/rsyslog.html)

отправка по e-mail
[http://mazday.wordpress.com/2009/05/14/email-%D0%BD%D0%BE%D1%82%D0%B8%D1%84%D0%B8%D0%BA%D0%B0%D1%86%D0%B8%D1%8F-rsyslog-%D1%81-%D1%84%D0%B8%D0%BB%D1%8C%D1%82%D1%80%D0%B0%D1%86%D0%B8%D0%B5%D0%B9-%D1%81%D0%BE%D0%BE%D0%B1%D1%89%D0%B5%D0%BD/](http://mazday.wordpress.com/2009/05/14/email-%D0%BD%D0%BE%D1%82%D0%B8%D1%84%D0%B8%D0%BA%D0%B0%D1%86%D0%B8%D1%8F-rsyslog-%D1%81-%D1%84%D0%B8%D0%BB%D1%8C%D1%82%D1%80%D0%B0%D1%86%D0%B8%D0%B5%D0%B9-%D1%81%D0%BE%D0%BE%D0%B1%D1%89%D0%B5%D0%BD/)




В большинстве случаев в файл конфигурации нужно добавить всего одну строку:
*.info;mail.none;authpriv.none;cron.none @@IP_центрального_сервера:514
Две "собачки" перед строкой означают, что сообщения протокола будут переданы удаленному серверу rsyslog, 514 - это порт, который используется удаленным сервером.
Если вы какие-то сообщения желаете отправлять в файл, а не на сервер (для уменьшения размера БД сервера), то просто укажите имя файла, например:
mail.* -/var/log/maillog
Если есть желание выводить сообщения на консоль всех подключенных к системе пользователей, то используйте звездочку вместо действия:
*.emerg *








Шаблоны
$template mailSubject,"ServerLog: Warning on %hostname%"

$template mailBody,"SERVERLOG\r\nError on  %hostname%\r\nError  =  '%msg%'"
#2
$template mailBodyPing,"SERVERLOG\r\nThe %hostname% is DOWN"


Фильтры
1.Традиционные - traditional" severity and facility based selectors
local2.* @quartz.sc.ru

2.RainerScript-based filters (фильтрация на основе языка RainerScript - фактически обычный if - then - else)


3.property-based filters (фильтрация на основе свойств сообщения (как в template))












Тильда обнуляет всё что подпадает под её фильтр. Уберите или перенесите ниже строку:

:hostname, contains, "SERVER" ~

Тильда обозначает, что она обнуляет (дропает) все сообщения от предыдущего фильтра
Например, получатся что тильда дропает все сообщения, содержащие informational
*.* /var/log/allmsgs-incl-informational.log
:msg, contains, "informational"  ~ 
*.* /var/log/allmsgs-no-informational.log


Существует так же, специальный символ &, который повторяет выполнение прошлого фильтра и запускает действие, указанное после данного символа.
*.=crit /var/log/somefile
& root
& /var/log/criticalmessages

Отправляет все критичные в файл somefile и root и criticalmessages



The "-" means don't sync after each write
# & ~ means drop messages that the last filter found (avoid duplication)
& ~ получается дропает все сообщения прошлого фильтра (используется для избежания дублирования)

Пример - отправляет сообщения от ядра в консоль, потом в файл /var/log/kernel, а потом дропает их, чтобы в другом месте не вылезали
kern.*                                          /dev/console
&                                               /var/log/kernel
& ~





$template TDraytek,"/var/log/draytek/%HOSTNAME%-%SYSLOGFACILITY-TEXT%-%SYSLOGSEVERITY-TEXT%.log"
if $source contains 'draytek' then ?TDraytek
& ~








$ModLoad imrelp
$RelpServerRun 514

На сервер логов

*.* :omrelp:remotehost:port









Название таблицы в базе
SystemEvents, а не systemevents

Без пробела
local2.* :ommysql:127.0.0.1,rsyslog,rsyslog,Gu9evwP




Тест
logger -p local2.warning "test log message"


logger -n 81.20.192.11 -p local2.warning "test log message from rock"




logger -p local3.warning "test log message"



Использовать RELP
Буфферизировать пересылаемые данные на клиенте
Можно ли буфферизировать на циске? длинке?

[http://wiki.rsyslog.com/index.php/FailoverSyslogServer](http://wiki.rsyslog.com/index.php/FailoverSyslogServer)
Прописываем 2 лог сервера на девайсе, а потом на каждом из прописанных делаем, чтобы отправлялся на один из серверов хранения логов или на другой
Если первый не доступен, то он пишет во второй

*.* @@primary-syslog.example.com
$ActionExecOnlyWhenPreviousIsSuspended on
& @@secondary-1-syslog.example.com
& @@secondary-2-syslog.example.com
& /var/log/localbuffer
$ActionExecOnlyWhenPreviousIsSuspended off




$ModLoad imuxsock             # local message reception

$WorkDirectory /rsyslog/work  # default location for work (spool) files

$ActionQueueType LinkedList   # use asynchronous processing
$ActionQueueFileName srvrfwd  # set file name, also enables disk mode
$ActionResumeRetryCount -1    # infinite retries on insert failure
$ActionQueueSaveOnShutdown on # save in-memory data if rsyslog shuts down
*.*       @@server:port




1.Поднять monit для mysql, rsyslog, apache(не важно)








 Можно указать дополнительные syslog сервера, для дублирования лог
   записей при помощи дополнительных команд logging <ip-address>.


Надо  буфферизировать на клиенте логи, пока сервер не поднимиться после падения
Но надо исппользовать Tcp или RELP





Наша сеть
vpn-nlmk
backbone
others



Делаем ucarp или heartbeat (что лучше, так как я не умею) между sapphire и rock, с него пересылаем логи
на quartz или на другой сервер (Xen), как написано здесь [http://wiki.rsyslog.com/index.php/FailoverSyslogServer](http://wiki.rsyslog.com/index.php/FailoverSyslogServer), но буфферизацией, где надо запустить 3 loganalizera (vpn nlmk, backbone, остальное),
 с quartz бекапим базы с логами


С vpn-nlmk отсылаем логи на rock и sapphire, c rock пересылаем логи сразу же на quartz или при его недоступности на другой сервер
между адресами поднять ucarp?

C backbone шлём на quartz и на другой сервер

С others отсылается на sapphire, а с него либо на quartz или при его недоступности на другой сервер 

Quartz считаем главным, а второй резервным


sapphire

lo:2      Link encap:Local Loopback  
          inet addr:81.20.196.53  Mask:255.255.255.255
          UP LOOPBACK RUNNING  MTU:16436  Metric:1

lo:3      Link encap:Local Loopback  
          inet addr:10.192.10.252  Mask:255.255.255.255
          UP LOOPBACK RUNNING  MTU:16436  Metric:1






rock

eth1:0    Link encap:Ethernet  HWaddr 00:0C:29:D7:5D:9A  
          inet addr:81.20.196.54  Bcast:0.0.0.0  Mask:255.255.255.255
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1

eth2      Link encap:Ethernet  HWaddr 00:0C:29:D7:5D:A4  
          inet addr:10.192.10.42  Bcast:10.192.10.43  Mask:255.255.255.252
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:1295727 errors:0 dropped:0 overruns:0 frame:0
          TX packets:1248067 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:130872225 (124.8 Mb)  TX bytes:99114295 (94.5 Mb)

eth2:0    Link encap:Ethernet  HWaddr 00:0C:29:D7:5D:A4  
          inet addr:10.192.10.254  Bcast:0.0.0.0  Mask:255.255.255.255
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1

eth2:1    Link encap:Ethernet  HWaddr 00:0C:29:D7:5D:A4  
          inet addr:10.192.10.253  Bcast:0.0.0.0  Mask:255.255.255.255
          UP BROADCAST RUNNING MULTICAST  MTU:1500  





С бекбона отправлять логи на quartz и на sapphire
Сделать конфиг для бекбона на cisco и dlink

service timestamps debug datetime msec localtime
service timestamps log datetime localtime 
clock timezone MSK +4
clock calendar-valid
ntp update-calendar
access-list 61 remark NTP: access-group peer
access-list 61 permit 81.20.196.53
access-list 61 permit 81.20.196.54
access-list 61 deny any
access-list 62 remark NTP: access-group serve-only
access-list 62 permit 192.168.0.0 0.0.255.255
access-list 62 permit 172.20.0.0 0.0.255.255
access-list 62 permit 81.20.192.0 0.0.15.255
access-list 62 deny any
ntp logging
ntp access-group peer 61
ntp access-group serve-only 62
ntp server 81.20.196.53 prefer
ntp server 81.20.196.54

service timestamps debug datetime msec localtime
service timestamps log datetime localtime 
logging on
logging buffered informational
logging buffered 32768
logging facility local3
logging 81.20.196.53
logging 192.168.121.17
logging monitor debugging
logging trap notifications
logging origin-id hostname
logging history size 0


access-list 23 permit 81.20.192.0 0.0.0.127
access-list 23 permit 192.168.113.0 0.0.0.255


enable sntp                                                                    
config time_zone operator + hour 4 min 0
config sntp primary 192.168.113.1 secondary 81.20.196.54 poll-interval 720

enable syslog                                                                  
create syslog host 1 ipaddress 192.168.113.1 severity all facility local3 udp_port 514  state enable 
config log_save_timing log_trigger



Сделать конфиг для узлов для cisco и dlink
+ установка времени на dlink

Перенастроить sapphire
Володю по snmp заставить поменять настройки на всех коммутаторах,
установить ntp и log сервер (sapphire)








Логирование linux сервера
1. Определиться с набором демонов и самой ОС, которые строго надо логировать
2. Определиться какие из них надо отправлять на выделенный лог сервер
3. logrotate
4. logwatch







CREATE DATABASE logbackbone;
GRANT ALL ON logbackbone.* TO logbackbone@localhost IDENTIFIED BY 'Gu9evwP';
flush privileges;

Database changed
mysql> show tables;
+-----------------------+
| Tables_in_logbackbone |
+-----------------------+
| charts                |
| config                |
| dbmappings            |
| fields                |
| groupmembers          |
| groups                |
| savedreports          |
| searches              |
| sources               |
| users                 |
| views   


Добавил руками таблицу


DROP TABLE IF EXISTS `SystemEvents`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `SystemEvents` (
  `ID` int(10) unsigned NOT NULL AUTO_INCREMENT,
  `CustomerID` bigint(20) DEFAULT NULL,
  `ReceivedAt` datetime DEFAULT NULL,
  `DeviceReportedTime` datetime DEFAULT NULL,
  `Facility` smallint(6) DEFAULT NULL,
  `Priority` smallint(6) DEFAULT NULL,
  `FromHost` varchar(60) DEFAULT NULL,
  `Message` text,
  `NTSeverity` int(11) DEFAULT NULL,
  `Importance` int(11) DEFAULT NULL,
  `EventSource` varchar(60) DEFAULT NULL,
  `EventUser` varchar(60) DEFAULT NULL,
  `EventCategory` int(11) DEFAULT NULL,
  `EventID` int(11) DEFAULT NULL,
  `EventBinaryData` text,
  `MaxAvailable` int(11) DEFAULT NULL,
  `CurrUsage` int(11) DEFAULT NULL,
  `MinUsage` int(11) DEFAULT NULL,
  `MaxUsage` int(11) DEFAULT NULL,
  `InfoUnitID` int(11) DEFAULT NULL,
  `SysLogTag` varchar(60) DEFAULT NULL,
  `EventLogType` varchar(60) DEFAULT NULL,
  `GenericFileName` varchar(60) DEFAULT NULL,
  `SystemID` int(11) DEFAULT NULL,
  `processid` varchar(60) NOT NULL DEFAULT '',
  `checksum` int(11) unsigned NOT NULL DEFAULT '0',
  PRIMARY KEY (`ID`)
) ENGINE=InnoDB AUTO_INCREMENT=7631 DEFAULT CHARSET=utf8;







Перевод часов

clock summer-time MSD recurring last Sun Mar 2:00 last Sun Oct 2:00


Apr  3 14:12:49: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.19 on GigabitEthernet0/2.10 from FULL to DOWN, Neighbor Down: Too many retransmissions
Apr  3 14:13:49: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.19 on GigabitEthernet0/2.10 from DOWN to DOWN, Neighbor Down: Ignore timer expired
Apr  3 14:14:08: %OSPF-5-ADJCHG: Process 110, Nbr 81.20.192.19 on GigabitEthernet0/2.10 from LOADING to FULL, Loading Done







access-list 7 permit 81.20.192.0 0.0.0.127
access-list 7 permit 81.20.192.64 0.0.0.3
access-list 7 permit 192.168.113.0 0.0.0.255
access-list 7 permit 192.168.121.0 0.0.0.255
access-list 7 permit 192.168.1.0 0.0.0.255








