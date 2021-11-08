---
layout: post
title:  "upload_download_cfg_snmp_des3526"
date:   2017-02-28 07:52:41 +0300
categories: dlink
tags: dlink
---

# upload_download_cfg_snmp_des3526
`create iproute default 192.168.117.1 1`


Скачать
```
snmpset -v 2c -c HKeGeUfo 192.168.117.142 1.3.6.1.4.1.171.12.1.2.1.1.3.3 a 192.168.117.1
snmpset -v 2c -c HKeGeUfo 192.168.117.142 1.3.6.1.4.1.171.12.1.2.1.1.4.3 i 2 
snmpset  -v 2c -c HKeGeUfo 192.168.117.142 1.3.6.1.4.1.171.12.1.2.1.1.5.3 s bel4
snmpset  -v 2c -c HKeGeUfo 192.168.117.142 1.3.6.1.4.1.171.12.1.2.1.1.7.3 i 2
snmpset  -v 2c -c HKeGeUfo 192.168.117.142 1.3.6.1.4.1.171.12.1.2.1.1.8.3 i 3
```

Закачать
```
snmpset -v 2c -c HKeGeUfo 192.168.117.142 1.3.6.1.4.1.171.12.1.2.1.1.3.3 a 192.168.117.1
snmpset -v 2c -c HKeGeUfo 192.168.117.142 1.3.6.1.4.1.171.12.1.2.1.1.4.3 i 2 
snmpset  -v 2c -c HKeGeUfo 192.168.117.142 1.3.6.1.4.1.171.12.1.2.1.1.5.3 s bel4
snmpset  -v 2c -c HKeGeUfo 192.168.117.142 1.3.6.1.4.1.171.12.1.2.1.1.7.3 i 3
snmpset  -v 2c -c HKeGeUfo 192.168.117.142 1.3.6.1.4.1.171.12.1.2.1.1.8.3 i 3
```