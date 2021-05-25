---
layout: post
title:  "logrotate"
date:   2018-03-12 00:49:55 +0300
categories: logs
tags: logs
---

# logrotate
nginx_access.log
nginx_error.log

apache_access.log
apache_error.log


/srv/www/*/log/nginx*log {                                                                                                                                        
    daily                                                                                                                                                    
    rotate 10                                                                                                                                                
    missingok                                                                                                                                                
    notifempty                                                                                                                                               
    compress                                                                                                                                                 
    sharedscripts                                                                                                                                            
    postrotate                                                                                                                                               
        [ ! -f /var/run/nginx.pid ] || kill -USR1 `cat /var/run/nginx.pid`                                                                                   
    endscript                                                                                                                                                
}  



/srv/www/*/log/apache*log {
    missingok
    notifempty
    sharedscripts
    delaycompress
    postrotate
        /sbin/service httpd reload > /dev/null 2>/dev/null || true
    endscript
}


apache раз в неделю
nginx каждый день


[http://mdex-nn.ru/page/slow-query-log-mysql.html](http://mdex-nn.ru/page/slow-query-log-mysql.html)

/var/log/mysqld.log {
        # create 600 mysql mysql
        notifempty
        daily
        rotate 3
        missingok
        compress
    postrotate
        # just if mysqld is really running
        if test -x /usr/bin/mysqladmin && \
           /usr/bin/mysqladmin ping &>/dev/null
        then
           /usr/bin/mysqladmin flush-logs
           ret=$?
           if test $ret -ne 0
           then
              echo "/logrotate.d/mysql failed, probably because" >&2
              echo "the root acount is protected by password." >&2
              echo "See comments in /logrotate.d/mysql on how to fix this" >&2
              exit $ret
           fi
        fi
    endscript
}





/var/log/mysql.log /var/log/mysql/mysql.log /var/log/mysql/mysql-slow.log {
        daily
        rotate 7
        missingok
        create 640 mysql adm
        compress
        sharedscripts
        postrotate
                test -x /usr/bin/mysqladmin || exit 0
                MYADMIN="/usr/bin/mysqladmin --defaults-file=/etc/mysql/logrotate.cnf"
                if [ -z "`$MYADMIN ping 2>/dev/null`" ]; then
                  if killall -q -s0 -umysql mysqld; then
                    exit 1
                  fi 
                else
                  $MYADMIN flush-logs
                fi
        endscript
}


/var/log/mysqld.log {
        create 640 mysql mysql
        notifempty
        missingok
        postrotate
                # just if mysqld is really running
                if test -x /usr/bin/mysqladmin && \
                   /usr/bin/mysqladmin --defaults-extra-file=/root/mysql/logrotate.cnf ping &>/dev/null
                then
                   /usr/bin/mysqladmin --defaults-extra-file=/root/mysql/logrotate.cnf flush-logs
                fi
                /usr/bin/chcon -u system_u -r object_r -t mysqld_log_t /var/log/mysqld.log
        endscript
}














if      ($syslogfacility-text == 'kern') and \
        ($msg contains 'IN=' and $msg contains 'OUT=') \
then    -/var/log/firewall
&       ~



/var/log/firewall
{
        rotate 4
        daily
        missingok
        notifempty
        compress
        delaycompress
        sharedscripts
        postrotate
                /sbin/service rsyslog reload > /dev/null # for RHEL
        endscript
}

