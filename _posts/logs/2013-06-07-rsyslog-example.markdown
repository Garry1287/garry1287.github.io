---
layout: post
title:  "rsyslog-example"
date:   2013-06-07 17:45:57 +0400
categories: logs
tags: logs
---

# rsyslog-example


    16 = 00010000 = local0

    17 = 00010001 = local1

    18 = 00010010 = local2

    19 = 00010011 = local3

    20 = 00010100 = local4

    21 = 00010101 = local5

    22 = 00010110 = local6

    23 = 00010111 = local7


logging enable
logging timestamp
logging buffer-size 8192
logging console debugging
logging buffered informational
logging trap informational
logging asdm informational
logging device-id hostname
logging host outside 10.192.10.253
logging host outside 10.192.10.252


logging history size 0
logging trap notifications
logging origin-id hostname
logging facility local2
logging host 10.192.10.253
logging host 10.192.10.252









По ip фильтровать входящие сообщения



Разделить типы оборудования по facility по важности.
НЛМК - local2
Backbone - local3
Коммутаторы - по ip
cisco роутеры - local4
Специальных лог для критических, со всех девайсов
local7 - дом. коммутаторы


Cde-c3.sc.ru ok
Cde-c2.sc.ru ok
Ctd-c6.sc.int (Sap no)
Ctd-c0.sc.ru ok
Ctd-c2.sc.ru ok
Ctd-c3.sc.ru (Sap no)
ctd-c4(k9-c0) ok
Ctd-c5.sc.int (Sap no)
Ctd-c7.sc.ru (Sap no)
ats45-c0.sc.ru ok
Cde-s0.sc.int ok
Ctd-s6.sc.int (Sap no)
Ctd-s1.sc.int  (Sap no)
ats45-s0.sc.int ok

k9-s9.sc.int
V21a-s0.sc.int
bras01.sc.int



local 5

logging history size 0
logging trap notifications
logging origin-id hostname
logging facility local5
logging 192.168.113.1
logging 192.168.121.26



p8-s0.sc.int
p8-s1.sc.int
p8-s2.sc.int
Rtm-s0.sc.int
Europort-s0.sc.int
Europort-s1.sc.int
Ctd-s0
Ctd-s8
Ctd-s4
Cde-s1.sc.int
Altai-s0.sc.int
s66-agg.sc.int
s66-s0.sc.int
s66-s1.sc.int
Ppr-s0.sc.int
P2k-s0.sc.int
Fsb-s0.sc.int
fsb-s0.sc.int
ats45-s0.sc.int
p8-s0.sc.int
altai-s0.sc.int 
ppr-s0.sc.int
europort-s1.sc.int















НЛМК
Логи отпарваляем на sapphire и rock, а с rock на vz1

Баскбоне
Логи отпарваляем на sapphire и vz1

Коммутаторы
Логи отпарваляем на sapphire





Затем расладывать полученную информацию по папкам и датам
Если facility не присваивал, то soure ip определять


1)IPVPN-NLNK
local2  под vpn-nlmk сделать
и по ip разбирать



На rock.sc.ru

local2.* @quartz.sc.ru

на quartz

$template RemoteFromHost, "/var/log/VPN-NLMK/%FROMHOST%.log"
$template DailyPerHostLogs,"/var/log/VPN-NLMK/%$YEAR%/%$MONTH%/%$DAY%/%HOSTNAME%.log"

local2.* : ?DailyPerHostLogs


(Как быть где 2 канала? По hostname. Надо только проверить как это работает) 








2)Backbone
Можно обычную схему замутить, по source ip или hostname. Hostname лучше
$template RemoteFromHost, "/var/log/VPN-NLMK/%FROMHOST%.log
:fromhost, isequal,"192.168.5.1" ?RemoteFromHost

Агрегаторы
Nodes
Районы
Servers
Others







на quartz

#Writing into Mysql
$ModLoad ommysql

#write in mysql
if      ($fromhost-ip == '81.20.192.59')
then    ommysql:127.0.0.1,rsyslogdb,username,password


local2.* : ommysql:127.0.0.1,rsyslogdb,username,password



















Отделный файл для дебаг сообщений
ЧТобы при включении term mon, не сыпались 1






rsync -avz --stats  /home/garry /disk


# Cisco ASA5510 FW01 Logging
:fromhost-ip,isequal, 172.28.28.194                  /var/log/cisco/cisco-asa5510.log


Включаем ротацию логов, с помощью logrotate:
/etc/logrotate.d/cisco-log

/var/log/cisco/*.log
{
daily
rotate 10
missingok
notifempty
sharedscripts
postrotate
/bin/kill -HUP `cat /var/run/syslogd.pid 2> /dev/null` 2> /dev/null || true
endscript
}





sh run logging

	
logging enable
logging timestamp
logging trap warnings
logging asdm informational
logging facility 23
logging host inside-mngmt 10.0.128.26



if $programname == 'programname' and $msg contains 'a text string' and $syslogseverity <= '6' then /var/log/custom/bind.log

if $programname == 'programname' then @remote.syslog.server
& ~

# Example: Log mail server control messages to mail-queue.log
if $hostname == 'titus'\
and $programname == 'smtp.queue.'\
and $syslogseverity <= '6' then /var/log/titus/mail-queue.log
& ~


Usefull filters:

$hostname
$programname
$msg
$syslogseverity

Operators:

== (equals)
contains
and
or





#
# Cisco's log part
#
$template RemoteFromHost, "/var/log/remote/%FROMHOST%.log"

:fromhost, isequal,"192.168.5.1" ?RemoteFromHost
:fromhost, isequal,"192.168.5.1" ~
:fromhost, isequal,"192.168.224.65" ?RemoteFromHost
:fromhost, isequal,"192.168.224.65" ~
# 







# template
$template RemoteHost,"/var/log/HOSTS/%HOSTNAME%/%$YEAR%/%$MONTH%/%$DAY%/%syslogfacility-text%.log"
# used for Cisco, vanilla syslog when we can't parse host name
$template RemoteFromHost,"/var/log/HOSTS/%FROMHOST%/%$YEAR%/%$MONTH%/%$DAY%/%syslogfacility-text%.log"

# NOTE - we can't bind UDP to a ruleset, so it enters the local RuleSet
#   and has to be dealt with here

$RuleSet local

# for cisco, vyatta - doesn't send hostname, need to use IP manually
:fromhost, isequal, "192.168.0.99" ?RemoteFromHost
:fromhost, isequal, "192.168.0.99" ~
:fromhost, isequal, "192.168.0.103" ?RemoteFromHost
:fromhost, isequal, "192.168.0.103" ~
:fromhost, isequal, "192.168.0.97" ?RemoteFromHost
:fromhost, isequal, "192.168.0.97" ~
:fromhost, isequal, "192.168.0.111" ?RemoteFromHost
:fromhost, isequal, "192.168.0.111" ~
# anything from a remote host gets logged as such
:source, isequal, "" ?RemoteHost
:source, isequal, "" ~









файла стоит "минус" (–), то после каждой записи в журнал демон не будет выполнять синхронизацию файла, то есть осуществлять системный вызов fsync(). 
Это повышает производительность системы, поскольку сообщений обычно много, и если после каждого выполнять синхронизацию журнала, система будет работать медленно. 

~ (тильда) - после данного символа сообщение будет удалено и дальнейшая обработка не продолжится

Существует так же, специальный символ &, который повторяет выполнение прошлого фильтра и запускает действие, 
указанное после данного символа. Это очень удобно для фильтрации  или экономии системных ресурсов, например:












Фильтрация на основе свойств позволяет построить обработку, опираясь на свойства сообщений,
 такие как: HOSTNAME, syslogtag и msg (полный список свойств сообщения можно найти по ссылке ниже, в разделе Available Properties).
 Фильтр на основе свойств должен начинаться с двоеточия, это говорит rsyslog, что используется новый тип фильтра. После двоеточия следует имя свойства сообщения,
 запятая, имя выполняемой операции сравнения, запятая и последнее — значение для сравнения. Значение должно быть заключено в кавычки. 
Между запятыми могут присутствовать пробелы или табуляции. Имена свойств и операций сравнения чувствительны к регистру. Примерный шаблон фильтра выглядит так:

:property, [!]compare-operation, "value"

Поддерживаются следующие операции сравнения:

contains — проверка, содержит ли свойство указанное значение.

isequal — сравнивает строку value с содержимым свойства, они должны быть полностью одинаковы.

startswith — проверяет что свойство начинается со строки value.

regex — сравнивает свойство с заданным регулярным выражением.

Дополнительную информацию о конфигурационном файле и свойствах сообщений можно найти тут: rsyslog.conf — Linux man page.

Пример:

:fromhost, regex, "sto$"
:ommysql:localhost,deustolog,Ursyslog,superf4rs1t4009
& ~

Пример2:
:syslogtag,contains,"named" > ip,db_mail,login,pass
:syslogtag,contains,"named" ~

Фильтрация на основе выражений использует другой синтаксис.

Пример:

if $FROMHOST startswith 'deusto' then :ommysql:localhost,deustolog,Ursyslog,superf4rs1t4009
& ~

Пример2:
if $msg contains 'GUI_set' and not $msg contains 'VALIDATOR' then @@192.1.100.1

Пример3:

if $fromhost-ip contains '192.168.0.50' /var/log/192.168.0.50.message





#(Фильтрация по слову в сообщении $msg)
if $msg contains 'Alarm' then {
:ommail:;mailBodyPing :ommysql:localhost,LogDB,user,123
}  )






if $programname == 'popa3d' and $syslogseverity <= '6' then /var/log/popa3d.log
if $programname == 'popa3d' and $syslogseverity <= '6' then ~






A solution to rotate logs on a daily basis is to use dynamic files and after a while rotate the log files away. Quick sample:

/etc/rsyslog.conf:

#####################################################
# Log everything to a per host daily logfile        #
#####################################################
$template DailyPerHostLogs,"/var/log/syslog/%$YEAR%/%$MONTH%/%$DAY%/%HOSTNAME%/messages.log"
*.* -?DailyPerHostLogs

/etc/cron.hourly/syslog-bzip2:

# Compress *.log-files not changed in more than 24 hours:
find /var/log/syslog/2008 -type f -mtime +1  -name "*.log" -exec bzip2 '{}' \;








==Code: Select all==
if $syslogfacility-text == 'local6' and $programname == 'httpd' then /var/log/httpd-access.log
if $syslogfacility-text == 'local6' and $programname == 'httpd' then ~
if $syslogfacility-text == 'local7' and $programname == 'httpd' then /var/log/httpd-error.log
if $syslogfacility-text == 'local7' and $programname == 'httpd' then ~









#from cisco nlmk
local2.*                                @81.20.192.11
local2.*                                -/var/log/nlmk.log
&       ~

#
# the rest in one file
#
*.*;mail.none;news.none                 -/var/log/messages


#
# enable this, if you want to keep all messages
# in one file
#*.*                                    -/var/log/allmessages


#
# Some foreign boot scripts require local7
local0,local1.*                         -/var/log/localmessages
local3.*                                -/var/log/localmessages
local4,local5.*                         -/var/log/localmessages
local6,local7.*                         -/var/log/localmessages






Если
Syslogtag начинается со MSWinEventLog#011, то оправлять в /var/log/messages в формате, описанном в шаблоне fixsnareFormat
а также отправлять на сервер 192.168.1.8 в формате fixsnareForwardFormat
никуда больше эти логи не лить

:syslogtag, startswith, "MSWinEventLog#011" /var/log/messages;fixsnareFormat
& @192.168.1.8;fixsnareForwardFormat
& ~


$template fixsnareFormat2,"%timereported% %fromhost-ip% broken-MSWinEventLog %HOSTNAME% %syslogtag%%msg:::drop-last-lf%\n"