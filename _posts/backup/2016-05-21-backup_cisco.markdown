---
layout: post
title:  "backup_cisco"
date:   2016-05-21 09:03:18 +0300
categories: backup cisco
tags: backup cisco
---

# backup_cisco
[https://habrahabr.ru/post/171681/](https://habrahabr.ru/post/171681/)

Router(config)#kron policy-list Backup         
Router(config-kron-policy)#cli show run | redirect 	 tftp://10.1.1.1/test.cfg        
Router(config-kron-policy)#exit         !       
Router(config)#kron occurrence Backup at 23:00 Sun recurring         
Router(config-kron-occurrence)#policy-list Backup




на Cisco ASA нет таких механизмов резервирования конфигурации, как на коммутаторах и маршрутизаторах, но есть call-home.
Можно использовать snapshot и команду copy, как показано в примере ниже.
В качестве Mail сервера можно использовать любой почтовый сервер (SMTP без авторизации).

service call-home
no call-home reporting anonymous
call-home
 alert-group-config snapshot
  add-command "copy /noconfirm running-config tftp://10.0.0.33/ASA;int=inside"
 contact-email-addr asa@network.loc
 mail-server 10.0.0.44 priority 1

 profile COPYCONFIG
  destination address email monitoring@network.loc
  destination transport-method email
  subscribe-to-alert-group snapshot periodic daily
