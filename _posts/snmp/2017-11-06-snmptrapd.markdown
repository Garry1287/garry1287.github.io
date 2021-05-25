---
layout: post
title:  "snmptrapd"
date:   2017-11-06 12:06:53 +0300
categories: snmp
tags: snmp
---

# snmptrapd
#snmptrapd.conf

Код: Выделить всё
    traphandle 1.3.6.1.4.1.171.11.64.1.2.15.2.0.2 /root/snmp/trap.sh
    traphandle 1.3.6.1.4.1.171.11.69.1.2.15.2.0.2 /root/snmp/trap.sh
    disableAuthorization yes

/root/snmp/trap.sh - это путь до скрипта который должен срабатывать и прихождении trap



есть еще snmptt скрипт и такой же плагин для кактуса






>create snmp group trap_community v3 noauth_nopriv notify_view CommunityView
>create snmp user trap_community trap_community
>create snmp host 10.79.128.70 v3  noauth_nopriv trap_community
>
>dlink трапы отсылает (я их вижу tcpdump'ом), но snmptrapd из snmp-utils их
>ловить не хочет, если включить авторизацию - ловит, но тогда для
>каждого коммутатора нужно snmpengineid в конфиг заносить
>
>как уговорить snmptrapd ловить snmp trap v3 без авторизации?
>

уже не нужно, всё просто:
# cat snmptrapd.conf
logoption s 7
logoption f /var/log/snmptrapd-direct.log

createUser -e 8000000000000000000000 trap_community MD5 "authpassphrase"
authUser log,execute,net trap_community noauth