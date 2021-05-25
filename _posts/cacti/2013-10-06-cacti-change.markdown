---
layout: post
title:  "cacti-change"
date:   2013-10-06 20:39:08 +0400
categories: cacti-change
tags: cacti
---

# cacti-change
INSERT INTO poller

INSERT INTO `snmpagent_cache`



Count: 1  Time=3.83s (3s)  Lock=0.00s (0s)  Rows_sent=0.0 (0), Rows_examined=0.0 (0), root[root]@localhost
  CREATE TABLE `poller_time` (
  `id` mediumint(N) unsigned NOT NULL AUTO_INCREMENT,
  `pid` int(N) unsigned NOT NULL DEFAULT 'S',
  `poller_id` smallint(N) unsigned NOT NULL DEFAULT 'S',
  `start_time` datetime NOT NULL DEFAULT 'S',
  `end_time` datetime NOT NULL DEFAULT 'S',
  PRIMARY KEY (`id`)
  ) ENGINE=MyISAM AUTO_INCREMENT=N DEFAULT CHARSET=utf8

Count: 31  Time=2.95s (91s)  Lock=0.00s (0s)  Rows_sent=0.0 (0), Rows_examined=1.0 (31), cacti[cacti]@localhost
  DELETE FROM `snmpagent_cache` WHERE `oid` = 'S'

Count: 31  Time=2.95s (91s)  Lock=0.00s (0s)  Rows_sent=0.0 (0), Rows_examined=0.0 (0), cacti[cacti]@localhost
  INSERT IGNORE INTO `snmpagent_cache`      (`oid`, `name`, `mib`, `type`, `otype`, `kind`, `max-access`, `value`)      VALUES ('S', 'S', 'S', 'S', 'S', 'S', 'S', 'S')

Count: 74  Time=2.69s (199s)  Lock=0.00s (0s)  Rows_sent=0.0 (0), Rows_examined=1.0 (74), cacti[cacti]@localhost
  UPDATE `snmpagent_cache`   SET `value` = 'S'   WHERE `mib` = 'S'   AND `name` = 'S'

Count: 177  Time=2.39s (422s)  Lock=0.00s (0s)  Rows_sent=0.0 (0), Rows_examined=0.0 (0), cacti[cacti]@localhost
  INSERT INTO poller (id, total_time, last_update, last_status, status)  VALUES ('S', 'S', NOW(), NOW(), N)  ON DUPLICATE KEY UPDATE total_time=VALUES(total_time), last_update=VALUES(last_update),  last_status=VALUES(last_status), status=VALUES(status)

Count: 91  Time=2.26s (205s)  Lock=0.00s (0s)  Rows_sent=0.0 (0), Rows_examined=0.0 (0), cacti[cacti]@localhost
  INSERT INTO `snmpagent_cache`      (name, value, oid)      VALUES ('S', 'S', 'S'), ('S', 'S', 'S'), ('S', 'S', 'S'), ('S', 'S', 'S'), ('S', 'S', 'S')      ON DUPLICATE KEY UPDATE value=VALUES(value)

Count: 7  Time=2.16s (15s)  Lock=0.00s (0s)  Rows_sent=0.0 (0), Rows_examined=0.0 (0), cacti[cacti]@localhost
  INSERT INTO poller (id, snmp, script, server, last_status, status)  VALUES ('S', 'S', 'S', 'S', NOW(), N)  ON DUPLICATE KEY UPDATE snmp=VALUES(snmp), script=VALUES(script),  server=VALUES(server), last_status=VALUES(last_status), status=VALUES(status)

Count: 110  Time=2.05s (225s)  Lock=0.00s (0s)  Rows_sent=0.0 (0), Rows_examined=0.0 (0), cacti[cacti]@localhost
  INSERT INTO `snmpagent_cache`      (name, value, oid)      VALUES ('S', 'S', 'S'), ('S', 'S', 'S'), ('S', 'S', 'S'), ('S', 'S', 'S'), ('S', 'S', 'S'), ('S', 'S', 'S'), ('S', 'S', 'S')      ON DUPLICATE KEY UPDATE value=VALUES(value)

Count: 1  Time=1.40s (1s)  Lock=0.00s (0s)  Rows_sent=1.0 (1), Rows_examined=1.0 (1), cacti[cacti]@localhost
  SHOW COLUMNS FROM host LIKE 'S'

Count: 1  Time=1.20s (1s)  Lock=0.00s (0s)  Rows_sent=0.0 (0), Rows_examined=0.0 (0), cacti[cacti]@localhost
  SELECT sm.*   FROM snmpagent_managers_notifications AS smn   INNER JOIN snmpagent_managers AS sm   ON sm.id = smn.manager_id   WHERE smn.notification = 'S'   AND smn.mib = 'S'   ORDER BY sm.snmp_message_type



 Договор №LPK00988 от 20.08.2015г. 


CMDPHP SQL Backtrace: (/poller.php: 540 process_poller_output)(/lib/poller.php: 384 db_fetch_assoc)(/lib/database.php: 361 db_fetch_assoc_prepared)(/lib/database.php: 402 cacti_debug_backtrace) 
2018/07/10 16:19:43 - DBCALL ERROR: SQL Assoc Failed!, Error: MySQL server has gone away
2018/07/10 16:19:43 - DBCALL ERROR: SQL Assoc Failed!, Error:2006, SQL:'SELECT po.output, po.time, UNIX_TIMESTAMP(po.time) as unix_time, po.local_data_id, dl.data_template_id, pi.rrd_path, pi.rrd_name, pi.rrd_num FROM poller_output AS po INNER JOIN poller_item AS pi ON po.local_data_id=pi.local_data_id AND po.rrd_name=pi.rrd_name INNER JOIN data_local AS dl ON dl.id=po.local_data_id ORDER BY po.local_data_id LIMIT 40000' 




    innodb_log_file_size
    innodb_buffer_pool_size
    innodb_flush_log_at_trx_commit
    innodb_flush_method
    log_bin and sync_binlog
    innodb_buffer_pool_instances
    innodb_write_io_threads


 Сообщение от maximus200 Посмотреть сообщение
Прописал строку
Код:
innodb_file_per_table=1
в файле my.cnf
перезапустил mysqldx



может пригодится

#дамп всех баз
mysqdump -pРУТОВЫЙ_ПАРОЛЬ_КБАЗАМ -A --opt > /путь/куда/кладем/дамп/all_bases.sql

#останавливаем mysql
/etc/init.d/mysqld stop

#удаляем файды
rm /путь/к/файлу/bdata1
rm /путь/к/файлу/ib_logfile0
rm /путь/к/файлу/ib_logfile0

#запускаем mysql
/etc/init.d/mysqld start

#заливаем дамп
mysql < /путь/куда/кладем/дамп/all_bases.sql


если всё это записать в файл, и запускать его, то будет более-менее автоматизировано

перед использованием скрипт, обязательно, проверить все команды руками, по одной

top - 16:39:32 up 9 days,  1:18,  1 user,  load average: 0,66, 0,79, 0,57
httpd
xfsaild/dm-3
xfsaild/dm-3



General recommendations:
    Control warning line(s) into /var/log/mariadb/mariadb.log file
    Control error line(s) into /var/log/mariadb/mariadb.log file
    Set up a Password for user with the following SQL statement ( SET PASSWORD FOR 'user'@'SpecificDNSorIp' = PASSWORD('secure_password'); )
    Set up a Secure Password for user@host ( SET PASSWORD FOR 'user'@'SpecificDNSorIp' = PASSWORD('secure_password'); )
    Reduce your overall MySQL memory footprint for system stability
    Dedicate this server to your database for highest performance.
    Enable the slow query log to troubleshoot bad queries
    Configure your accounts with ip or subnets only, then update your configuration with skip-name-resolve=1
    Set thread_cache_size to 4 as a starting value
    Consider installing Sys schema from [https://github.com/mysql/mysql-sys](https://github.com/mysql/mysql-sys)
    Before changing innodb_log_file_size and/or innodb_log_files_in_group read this: [http://bit.ly/2wgkDvS](http://bit.ly/2wgkDvS)
Variables to adjust:
  *** MySQL's maximum memory usage is dangerously high ***
  *** Add RAM before increasing MySQL buffer variables ***
    query_cache_size (=0)
    query_cache_type (=0)
    query_cache_limit (> 1M, or use smaller result sets)
    thread_cache_size (start at 4)
    innodb_log_file_size should be (=119M) if possible, so InnoDB total log files size equals to 25% of buffer pool size.

