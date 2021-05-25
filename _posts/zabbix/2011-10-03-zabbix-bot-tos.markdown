---
layout: post
title:  "zabbix-bot-tos"
date:   2011-10-03 22:31:07 +0400
categories: zabbix
tags: zabbix
---

# zabbix-bot-tos
SLACK+ZABBIX
[https://www.zabbix.com/integrations/slack](https://www.zabbix.com/integrations/slack)
[https://blog.amet13.name/2017/06/slack-redmine-zabbix-teamcity.html](https://blog.amet13.name/2017/06/slack-redmine-zabbix-teamcity.html)
[https://tradenark.com.ua/monitoring/zabbix/zabbix-send-notification-to-slack/](https://tradenark.com.ua/monitoring/zabbix/zabbix-send-notification-to-slack/)

TOS, COS
[https://www.zabbix.com/forum/zabbix-cookbook/52041-cisco-qos-cisco-class-based-qos-mib-monitoring](https://www.zabbix.com/forum/zabbix-cookbook/52041-cisco-qos-cisco-class-based-qos-mib-monitoring)
[https://github.com/sniffer80/Cisco.QOS.SNMP.For.Zabbix](https://github.com/sniffer80/Cisco.QOS.SNMP.For.Zabbix)
[https://github.com/sniffer80/Cisco.QOS.SNMP.For.Zabbix/blob/master/Cisco.QOS.SNMP.For.Zabbix.py](https://github.com/sniffer80/Cisco.QOS.SNMP.For.Zabbix/blob/master/Cisco.QOS.SNMP.For.Zabbix.py)
[https://github.com/peshovec/zabbix-cisco-classname](https://github.com/peshovec/zabbix-cisco-classname)
[https://www.zabbix.com/forum/in-russian/53041-zabbix-ping-tos](https://www.zabbix.com/forum/in-russian/53041-zabbix-ping-tos)



[https://www.zabbix.com/integrations/](https://www.zabbix.com/integrations/)
[https://www.zabbix.com/integrations/cisco](https://www.zabbix.com/integrations/cisco)



Создайте ТЕСТ элемент данных с типом SNMP трап:
Узел сети с IP адресом SNMP: 127.0.0.1
Ключ: snmptrap["General"]
Формат времени журнала: hh:mm:ss yyyy/MM/dd


Теперь создайте Item с такими параметрами:
Description: GetTraps,
Type: Zabbix trapper,
Key: snmptraps,
Type of information: Text,
Сохраните. 



Используйте 3 версию протокола везде где только можно, в режиме authPriv (шифрование и аутентификация
