---
layout: post
title:  "radius-dlink"
date:   2012-05-12 20:12:16 +0400
categories: radius
tags: radius
---

# radius-dlink
[http://zyxel.ru/kb/2026](http://zyxel.ru/kb/2026)
[http://note.rajven.ru/?p=244](http://note.rajven.ru/?p=244)


Коммутаторы Zyxel:

radius-server host 1 [SERVER-IP] key [SECRET]
radius-accounting host 1  [SERVER-IP]  key  [SECRET]

aaa accounting system radius
aaa accounting exec start-stop radius
aaa accounting dot1x start-stop radius

aaa authentication login local radius
aaa authentication enable enable radius

(сделали без аккаунтинга)

Коммутаторы DLINK

create authen server_host [SERVER-IP] protocol radius port 1812 key [SECRET] timeout 15 retransmit 2
config authen server_group radius add server_host  [SERVER-IP] protocol radius
config authen_login default method local
create authen_login method_list_name rad_ext
config authen_login method_list_name rad_ext method radius
config authen_enable default method local_enable
create authen_enable method_list_name rad_ext_ena
config authen_enable method_list_name rad_ext_ena method radius
config authen application console login default
config authen application console enable default
config authen application telnet login method_list_name rad_ext
config authen application telnet enable method_list_name rad_ext_ena
config authen application ssh login method_list_name rad_ext
config authen application ssh enable method_list_name rad_ext_ena
config authen application http login method_list_name rad_ext
config authen application http enable method_list_name rad_ext_ena
config authen parameter response_timeout 0
config authen parameter attempt 3
config authen enable_admin all state enable
enable authen_policy

А в users указывать специфические опции для каждого вендора:

DEFAULT Huntgroup-Name == raisecom
User-Service-Type = 6,
Service-Type += Administrative-User,
Raisecom-Priority += 15

DEFAULT Huntgroup-Name == zyxel
Service-Type += Administrative-User,
User-Service-Type = 6,
Zyxel-Privilege-AVPair += «shell:priv-lvl=14″

DEFAULT Huntgroup-Name == cisco
User-Service-Type = 6,
Service-Type += Administrative-User,
Cisco-AVPair += «shell:priv-lvl=15″

DEFAULT Huntgroup-Name == qtech
User-Service-Type = 6,
Service-Type += Administrative-User,
Cisco-AVPair += «shell:priv-lvl=15″

DEFAULT Huntgroup-Name == dlink
dlink-Privelege-Level = 5,
Service-Type += Administrative-User,
Cisco-AVPair += «shell:priv-lvl=15″

DEFAULT Huntgroup-Name == maipu
User-Service-Type = 6,
Service-Type += Administrative-User,
Cisco-AVPair += «priv-lvl=15″




