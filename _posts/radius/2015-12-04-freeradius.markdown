---
layout: post
title:  "freeradius"
date:   2015-12-04 13:39:16 +0300
categories: radius
tags: radius
---

# freeradius
Freeradius + MySQL на CentOS

1. Установка mysql
yum install mysql mysql-devel mysql-server (далее везде говорим Y)
2. Устанавливаем пароль для юзера root на mysql
mysqladmin –u root password 123456
3. Устанваливаем freeradius
yum install freeradius freeradius-mysql (далее везде говорим Y)
Я как-то привык к текстовому редактору vi. Поэтому и редактирую конифурационные файлы в нем.
4. Редактируем файл /etc/raddb/users
Создаем тестового пользователя
vi /etc/raddb/users
Добавляем следующее:
test Auth-Type := Local, User-Password == "test"
Service-Type = Framed-User,
Framed-IP-Address = 192.168.13.1,
Framed-IP-Netmask = 255.255.255.0,

5. Правим /etc/raddb/client.conf
в этом файле содержаться данные о радиус-клиентах, т.е. NAS. Добавляем следующую запись:
Client 127.0.0.1 {
secret = 123
shortname=localhost
}
6. Проверяем работоспособность радиуса утилитой radtest:
на одной консоли запускаем radiusd –X (в режиме дебаггинга)
на второй консоли запускаем radtest test test localhost 1812 123
Если на эту команду приходит Access-Accept, то все ок. Двигаемся дальше

7. Начинаем прикручивать mysql .
mysql -u root –p
mysql> create database radius; // создаем БД radius
mysql> grant all on radius.* to radius@localhost identified by test; // открываем доступ к таблицам
mysql> \q
mysql –u root –p radius </usr/share/doc/freeradius-1.1.3/examples/mysql.sql //подгружаем нужные таблицы, далле это проверяем
mysql –u root –p
mysql> use radius;
mysql>show tables;
mysql> \q

8. Правим /etc/raddb/sql.conf
раскомментируем строчку
readclients = yes
9. Правим /etc/raddb/radius.conf
В модулях authtorize {}, accounting {}, post-auth {}, раскомментируем sql. Важно чтобы строчка $INCLUDE ${confdir}/sql.conf тоже присутствовала в файле.

Далее остается заполнить таблицы MySQL нужными записями.







[http://www.opennet.ru/base/cisco/radius.txt.html](http://www.opennet.ru/base/cisco/radius.txt.html)
























 Разберемся более детально с настройкой фрирадиуса+mysql.
Для начала терминология.
AV пара - пара атрибут=значение

авторизация - процесс проверки AV пар пользователя. В ходе
авторизации могут также устанавливаться определённые AV пары(для сервера
freeradius), смысл авторизации заключается в проверке достаточности
информации, предоставленной пользователем, для того, чтобы пользователь мог
пройти аутентификацию.

аутентификация - процесс опроса внешних источников данных radius сервером
для сравнения AV пар, предоставленных пользователем, и пар, хранящихся во
внешнем источнике; выбор метода аутентификации определяется AV парой Auth-Type.

аккаунтинг(или учёт) - процесс посылки NAS пакетов на radius-сервер,
которые содержат информацию о текущем соединении(время, количество
переданного трафика и.т.д.), на основании этой информации скрипты
счетчиков или биллинговой системы могут выполнять различные действия по
ограничению доступа пользователей на NAS.

Итак, переходим в режим mysql пользователем root
mysql -u -root –p
mysql> use radius;
mysql> show tables;
и на выходе получаем список подгруженных ранее таблиц:
+------------------+
| Tables_in_radius |
+------------------+
| nas |
| radacct |
| radcheck |
| radgroupcheck |
| radgroupreply |
| radpostauth |
| radreply |
| usergroup |
+------------------+
8 rows in set (0.00 sec)

Разберемся необходимые нам таблицы.

Usergroup - данные о группах пользователей, например
mysql> select * from usergroup;
+----+---------------+-----------+
| id | UserName | GroupName |
+----+---------------+-----------+
| 1 | d_startov | kzn |
| 2 | r_krasnov | nch |
+----+---------------+-----------+
2 rows in set (0.00 sec)
Radcheck - AV пары для проверки пользователя(обычно пароль), например

+----+----------------+----------------+--+--------------------+
| id | UserName | Attribute |op| Value |
+----+----------------+----------------+--+--------------------+
| 1 | d_startov | User-Password |==| testing123 |
| 2 | r_krasnov | Auth-Type |:=| Accept |
+----+----------------+----------------+--+--------------------+
2 rows in set (0.02 sec)
Radgroupcheck - проверка атрибутов для группы(не знаю, зачем это нужно)

Radreply - таблица, содержащая AV пары, передающиеся клиенту сервером при
прохождении аутентификации, например

mysql> select * from radreply;

+----+------------+-------------------+--+---------------------------------+
| id | UserName | Attribute |op| Value |
+----+------------+-------------------+--+---------------------------------+
| 1 | d_startov | Framed-IP-Address | =| 1.2.3.4 |
| 2 | d_startov | Framed-IP-Address | =| 2.3.4.1 |
| 3 | d_startov | Framed-IP-Netmask | =| 255.255.255.255 |
| 4 | r_krasnov| Framed-Routing | =| Broadcast-Listen |
| 5 | r_krasnov | Framed-Route | =| 2.3.4.0 255.255.255.248 |
| 6 | r_krasnov | Idle-Timeout | =| 900 |
+----+------------+-------------------+--+---------------------------------+
6 rows in set (0.01 sec)
Radgroupreply - AV пары, содержащиеся в ответе сервера для данной группы,
например:

mysql> select * from radgroupreply;
+----+-----------+--------------------+--+---------------------+
| id | GroupName | Attribute |op| Value |
+----+-----------+--------------------+--+---------------------+
| 34 | kzn | Framed-Compression | =| Van-Jacobsen-TCP-IP |
| 33 | kzn | Framed-Protocol | =| PPP |
| 32 | kzn | Service-Type | =| Framed-User |
| 31 | kzn | Auth-Type | =| Local |
| 35 | kzn | Framed-MTU | =| 1500 |
| 36 | nch | Auth-Type | =| Local |
| 37 | nch | Framed-Protocol | =| PPP |
| 38 | nch | Service-Type | =| Framed-User |
| 39 | nch | Framed-Compression | =| Van-Jacobsen-TCP-IP |
| 40 | kzn | Auth-Type | =| Local |
| 41 | kzn | Service-Type | =| Framed-User |
| 42 | kzn | Framed-Protocol | =| PPP |
+----+-----------+--------------------+--+---------------------+
12 rows in set (0.01 sec)
Крайне необходимыми могут быть циско-проприетарные ав-пары. Их значения можно найти на циско.ком. Например, вот метод присвоения циско policy-map’ов. Для этого используется атрибут cisco-avpair.
cisco-avpair = "ip:sub-qos-policy-in=<in policy name>"
cisco-avpair = "ip:sub-qos-policy-out=<out policy name>"

Учтите тот факт, что mysql используется для авторизации пользователя,
парольная аутентификация осуществляется модулем, который определён в AV
паре Auth-Type(в таблице radcheck можно присвоить пользователю это поле по
умолчанию с помощью оператора ':='). Существует много типов
аутентификации(см. соответствующие значения атрибутов в словаре
dictionary), большинство из них определяют пароль из mysql. В данном
примере для простоты приведён пример типа аутентификации Accept, который
сразу же возвращает пакет разрешения доступа, применять этот тип следует
лишь в тестирующих целях. Другие распространённые методы аутентификации:

System - системная аутентификация(для pap протокола), обычно нужна запись в
/etc/passwd для проверки пароля, друго вариант - использование файла users.

Chap - аутентификация протокола chap(пароль передаётся в открытом виде)

Reject - отклонение доступа пользователя.

Ms-Chap

Ldap - проверка пароля через службу каталогов ldap(необходимо поправить
подсекцию ldap в секции modules файла radiusd.conf)

Важно знать, что для некоторых типов аутентификации(system) можно использовать
зашифрованные пароли - Crypt-Password в формате Unix crypt. Для Ms-Chap
необходимо использовать параметры LM-Password и NT-Password. Для изучения других
параметров полезно почитать файл словаря dictionary.

И ещё один хинт: иногда очень полезно использовать пользователя по
умолчанию DEFAULT для сообщения некоторых AV пар, общих для всех пользователей.

Для настройки radiusd необходимо проверить следующие пункты radiusd.conf:
секция modules, дабы убедиться, что файл конфигурации mysql включен:

modules {
# Включение файла для работы с mysql, для работы с другими СУБД
# используются файлы
# Postgresql: ${confdir}/postgresql.conf
# MS-SQL: ${confdir}/mssql.conf
$INCLUDE ${confdir}/sql.conf
}


секция авторизации, настроенная для использования ldap и mysql:

authorize {
preprocess
chap
mschap
suffix
files
sql
ldap
}


Настройка данных методов проводится в соответствующих подсекциях секции
modules. В разделе аутентификации можно также объявлять собственные методы,
например:

authenticate {
authtype my_dialup {
pap
chap
ldap
}
}


и использовать их в поле Auth-Type.

В файле sql.conf также делаются некоторые изменения для указания сереверу radius
информации о поиске данных в mysql:

sql {

# Тип базы данных
driver = "rlm_sql_mysql"

# Параметры соединения
server = "localhost"
login = "root"
password = "mysql_passwd"

# База данных, используемая радиусом
radius_db = "radius"

# Первая таблица хранит записи начала соединения(start), 2-я -
# записи окончания соединения(stop). Если они совпадают, то эти записи
# хранятся в одной таблице.
acct_table1 = "radacct"
acct_table2 = "radacct"
# Таблица авторизации и установки типа аутентификации
authcheck_table = "radcheck"
authreply_table = "radreply"
# Групповые таблицы
groupcheck_table = "radgroupcheck"
groupreply_table = "radgroupreply"
# Соответствие пользователей группам
usergroup_table = "usergroup"

# Remove stale session if checkrad does not see a double login
deletestalesessions = yes

# Все sql запросы выводятся в режиме отладки radiusd -x
sqltrace = yes
sqltracefile = /usr/local/var/log/radius/sqltrace.sql

# Количество соединений с сервером. При большой загрузке
# рекоммендуется увеличить.
num_sql_socks = 5

# Число секунд, перед тем как сервер предпринимает повторную
# попытку соединения, если произошёл сбой соединения с mysql.
connect_failure_retry_delay = 60

Настройка клиентов производится в файле clients.conf:
clients.conf

# В данном файле описываются клиенты aka NAS. Формат файла напоминает файл
# настройки tacacs+. Вначале идёт определение клиента: client
# имя_или_ip_адрес, затем идёт список AV пар для данного клиента,
# заключённый в фигурные скобки. Приведу несколько примеров:
client 127.0.0.1 {
# Пароль для идентификации клиента и обмена с ним данными. Данным
# ключом также осуществляется проверка неизменности передаваемых
# пакетов(подпись).
secret = some_strange_secret

# Краткое имя для клиента.
shortname = localhost

# Следующие три поля необязательны, но они полезны для работы
# скрипта checkrad.pl(проверка работы процессов
# сервера)

# Поле типа NAS, может принимать следующие значения:
# Хотя, за каким эта дурь нужна я так и не понял :)
# cisco
# computone
# livingston
# max40xx
# multitech
# netserver
# pathras
# patton
# portslave
# tc
# usrhiper
# other
nastype = other # localhost обычно не является NAS

# Две следующие строчки зарезервированы на будущее. Вообще-то они
# использоваться должны для проверки имени пользователя и пароля
# для данного NAS
# login = !root
# password = someadminpas
}
client some.test.ru {
secret = some_host_secret
shortname = somenas
}
# Также можно определять пароль для всех клиентов для некоторой подсети(чем
# меньше подсеть, тем лучше, а вообще IMHO это не есть хорошо из
# соображений безопасности)
client 192.168.0.0/24 {
secret = a_very_long_passwd
shortname = private-network
}





[http://bgp-4.ru/wrapper.php?p=51](http://bgp-4.ru/wrapper.php?p=51)
[http://forum.nag.ru/forum/index.php?showtopic=52856](http://forum.nag.ru/forum/index.php?showtopic=52856)
[http://www.samag.ru/archive/article/105](http://www.samag.ru/archive/article/105)
[http://www.deltann.ru/10/d-092007/p-152](http://www.deltann.ru/10/d-092007/p-152)
[http://books.google.ru/books?id=cReeiIWc_Q0C&pg=PT319&lpg=PT319&dq=sradutmp&source=bl&ots=LXc_tIP4HT&sig=JBGuazBGxmcdzLXJZzRWJP5m9sQ&hl=en&sa=X&ei=_fhSUf3sDcjQ4QTjzoDACA&redir_esc=y#v=onepage&q&f=false](http://books.google.ru/books?id=cReeiIWc_Q0C&pg=PT319&lpg=PT319&dq=sradutmp&source=bl&ots=LXc_tIP4HT&sig=JBGuazBGxmcdzLXJZzRWJP5m9sQ&hl=en&sa=X&ei=_fhSUf3sDcjQ4QTjzoDACA&redir_esc=y#v=onepage&q&f=false)
