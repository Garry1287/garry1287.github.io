---
layout: post
title:  "Логирование в juniper"
date:   2017-01-03 06:16:37 +0300
categories: juniper Networking
tags: juniper
---

# Логирование в juniper
```
8     0000-00-00 00:34:40 Configuration saved to flash (Username: Anonymous, IP:
                           10.90.90.92)                                        
7     0000-00-00 00:24:50 Port 24 link up, 100Mbps  FULL duplex                
6     0000-00-00 00:24:47 Port 19 link down                                    
5     0000-00-00 00:23:58 Successful login through Web (Username: Anonymous, IP:
                           10.90.90.92)                                        
4     0000-00-00 00:18:47 Web session timed out (Username: Anonymous, IP: 10.90.
                          90.92)                                               
3     0000-00-00 00:08:37 Successful login through Web (Username: Anonymous, IP:
                           10.90.90.92)        
```

```
syslog {file cli-commands {interactive-commands info;authorization info;}user * {interactive-commands info;authorization info;}}


garry@ctd-s2# show system syslog   
host 192.168.121.1 {
    any any;
    source-address 192.168.121.13;
}
file security {
    authorization info;
    interactive-commands info;
    archive size 10m files 3;
}
file messages {
    any warning;
    authorization notice;
    archive size 10m files 3;
}

{master:0}[edit]


garry@ctd-s2# show system syslog file messages ?                
Possible completions:
  <[Enter]>            Execute this command
  allow-duplicates     Do not suppress the repeated message
  any                  All facilities
+ apply-groups         Groups from which to inherit configuration data
+ apply-groups-except  Don't inherit configuration data from these groups
> archive              Archive file information
  authorization        Authorization system
  change-log           Configuration change log
  conflict-log         Configuration conflict log
  daemon               Various system processes
  dfc                  Dynamic flow capture
  explicit-priority    Include priority and facility in messages
  external             Local external applications
  firewall             Firewall filtering system
  ftp                  FTP process
  interactive-commands  Commands executed by the UI
  kernel               Kernel
  match                Regular expression for lines to be logged
  ntp                  NTP process
  pfe                  Packet Forwarding Engine
  security             Security related
> structured-data      Log system message in structured format
  user                 User processes
  |                    Pipe through a command
{master:0}[edit]
garry@ctd-s2# show system syslog file messages any ?
Possible completions:
  <[Enter]>            Execute this command
  alert                Conditions that should be corrected immediately
  any                  All levels
  critical             Critical conditions
  emergency            Panic conditions
  error                Error conditions
  info                 Informational messages
  none                 No messages
  notice               Conditions that should be handled specially
  warning              Warning messages
  |                    Pipe through a command
```


```
set system syslog archive size 100k
set system syslog archive files 3
set system syslog user * any emergency
set system syslog host 172.30.5.100 any any
set system syslog host 172.30.5.100 authorization warning
set system syslog host 172.30.5.100 daemon any
set system syslog host 172.30.5.100 security any
set system syslog host 172.30.5.100 change-log none
set system syslog host 172.30.5.100 interactive-commands none
set system syslog host 172.30.5.100 facility-override local1
set system syslog host 172.30.5.100 source-address 172.30.2.241
set system syslog host other-routing-engine any any
set system syslog host other-routing-engine source-address 172.30.2.241
set system syslog file messages any alert
set system syslog file interactive-commands interactive-commands error
set system syslog file kmd-logs daemon info
set system syslog file kmd-logs match KMD
set system syslog time-format year
set system syslog time-format millisecond
set system syslog source-address 172.30.2.241
```


```
set security log cache limit 256
set security log mode stream
set security log format sd-syslog
set security log rate-cap 2000
set security log source-address 172.30.2.241
set security log stream NOC severity warning
set security log stream NOC format sd-syslog
set security log stream NOC category all
set security log stream NOC host 172.30.5.100
```

```
syslog {
/* write all security-related messages to file /var/log/security */
file security {
authorization info;
interactive-commands info;
}
/* write messages about potential problems to file /var/log/messages: */
/* messages from "authorization" facility at level "notice" and above, */
/* messages from all other facilities at level "warning" and above */
file messages {
authorization notice;
any warning;
}
/* write all messages at level "critical" and above to terminal of user "alex" if */
/* that user is logged in */
user alex {
any critical;
}
/* write all messages from the "daemon" facility at level "info" and above, and */
/* messages from all other facilities at level "warning" and above, to the */
/* machine monitor.mycompany.com */
host monitor.mycompany.com {
daemon info;
any warning;
}
/* write all messages at level "error" and above to the system console */
console {
any error;
}
}
```


```
show configuration system syslog


user * {
    any emergency;
}
host 10.9.0.33 {
    any any;
    change-log none;
    interactive-commands none;
    explicit-priority;
}
host 10.9.8.52 {
    any any;
    source-address 10.9.8.20;
}
file messages {
    any critical;
    authorization info;
    explicit-priority;
}
file interactive-commands {
    interactive-commands error;
}
}

set system syslog file  messages any info
```

[https://www.51sec.org/2015/12/juniper-srx-logging-methods-and-configuration-stream-mode-vs-event-mode/](https://www.51sec.org/2015/12/juniper-srx-logging-methods-and-configuration-stream-mode-vs-event-mode/)

[https://www.juniper.net/documentation/en_US/junos/topics/example/firewall-filter-option-logging-example.html](https://www.juniper.net/documentation/en_US/junos/topics/example/firewall-filter-option-logging-example.html)


```
1 syslog {/* write all security-related messages to file /var/log/security */file security {authorization info;interactive-commands info;}

file messages {authorization notice;any warning;}


host monitor.mycompany.com {daemon info;any warning;}

set system syslog file  messages  any info
```


messages - сохранять ряд
121.1 сохранять больше
security - autor

``
syslog {
/* write all security-related messages to file /var/log/security */
file security {
authorization info;
interactive-commands info;
}
/* write messages about potential problems to file /var/log/messages: */
/* messages from "authorization" facility at level "notice" and above, */
/* messages from all other facilities at level "warning" and above */
file messages {
authorization notice;
any warning;
}
```


```
set system syslog file security interactive-commands info;authorization info
archive size 750k files 2;
set system syslog file qflogs archive size 1g

set system syslog file messages any any; authorization info
```

[http://www.sourcecodebd.net/2018/01/14/juniper-turning-on-logging/](http://www.sourcecodebd.net/2018/01/14/juniper-turning-on-logging/)

[http://tech4u.pro/info-networks/97-juniper-junos-logging-vvedenie](http://tech4u.pro/info-networks/97-juniper-junos-logging-vvedenie)

`set system syslog file interactive-commands interactive-commands error`
