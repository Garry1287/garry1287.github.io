---
layout: post
title:  "dhcp_opt82_catalyst"
date:   2009-08-25 19:59:59 +0400
categories: Networking
tags: Networking
---

# dhcp_opt82_catalyst
ip dhcp snooping information option
ip dhcp relay information trusted
ip dhcp snooping vlan 10 
ip dhcp snooping information option allow-untrusted


на порту в сторону нижестоящего коммутатора
interface fastethernet 1/0/24 ( пример )
ip dhcp relay information trusted
ip dhcp relay information policy-action keep
ip arp inspection trust ( доверяем всем )
ip dhcp snooping trust ( доверяем если глобально не включен ip dhcp snooping information option allow-untrusted )
ip arp inspection limit rate [number] ( ограничиваем количество пакетов в секунду )
ip dhcp snooping limit rate [number] ( ограничиваем количество пакетов в секунду )



no ip dhcp relay information check                                                                                                                           
ip dhcp snooping vlan 50-51                                                                                                                                  
ip dhcp snooping information option allow-untrusted                                                                                                          
ip dhcp snooping



ЭТО РАБОЧАЯ

ip dhcp snooping
ip dhcp snooping vlan 50
ip dhcp snooping information option
ip dhcp snooping information option allow-untrusted (для двойного релея)

На порту
Switch(config-if)# ip dhcp snooping 
trust




no ip dhcp relay information check #не проверять
ip dhcp relay information policy keep







Agent Circuit ID: 0004 0032 00 01
Agent Remote ID: 0006 ------ 1cbdb965fb60


Agent Circuit ID: 0004 0032 02 0c
Agent Remote ID: 0006 e05fb9524b40
e05f.b952.4b7f

sh ip dhcp snooping binding 







Что касаемо Selective Q-in-Q, то как пример можно использовать:

ena qinq
config qinq ports 1 role uni
config qinq ports all outer_tpid 0x9100
create vlan v7 tag 7
create vlan v8 tag 8
create vlan v9 tag 9
create vlan v13 tag 13
config vlan v7 add tagged 1
config vlan v8 add tagged 1
config vlan v9 add tagged 1
config vlan v13 add tagged 1, 13
create vlan_translation ports 1 cvid 7-9 add svid 13


При такой настройке в порту 1 живут VLAN 7-9, мы транслируем их в порт 13 с outertag 13.









Если вкратце то это выглядит так:

1) Включаете Q-in-Q на устройстве командой enable qinq.
2) Создаёте SP-VLAN-ы как обычные 802.1q VLAN-ы.
3) Командами config qinq ports ... назначаете порты как UNI (access) или NNI (uplink). Здесь же выставляете нужный TPID.
4) Порты UNI и NNI добавляете как tagged в SP-VLAN-ы. Естественно C-VLAN-ы не нужно создавать.
5) Создаёте таблицу VLAN Translation командами create vlan_translation. В них указываете какие C-VLAN-ы запихивать в какие SP-VLAN-ы. В этих же командах можно менять тег C-VLAN и не добавлять второй тег.

Это реализовано в аппаратной части. Но есть ограничение, размер VLAN Translation Table 768 записей. Но можно и обойти это ограничение запихнув все непоместившиеся в таблицу VLAN-ы по PVID access порта в соответствующий SP-VLAN. Чтобы это сделать нужно на UNI порту отключить missdrop и назначить PVID на порту.





Удалось победить QinQ на 3528 в нужном нам ключе.
итак...

Задача:
Встала острая необходимость пробросить свой транк (тегированые пакеты) через один VLAN сервис-провайдера.

Имелось на тот момент
Cisco3750 с возможносью организации dot1q-tunnel (QinQ по-русски)

Решение
Купили DLink3528 и взяли в руки бубен...(шаманский костёр не дала разжечь пожарная сигнализация)

на Cisco 3750 кросс-коннектом организовали QinQ
Код:
interface FastEthernet1/0/37
description ---- Tunel ----
switchport access vlan 67
switchport mode dot1q-tunnel
!
interface FastEthernet1/0/38
description ---- Trunk to Tunel ----
switchport trunk encapsulation dot1q
switchport trunk native vlan 3
switchport trunk allowed vlan 1,7,700
switchport mode trunk
!
interface FastEthernet1/0/39
description ---- Trunk to ServiceProvider ----
switchport trunk encapsulation dot1q
switchport trunk allowed vlan 67
switchport mode trunk


На 3528 тоже сделали кросс-коннект и провели следующие манипуляции (отмечу только важное):
Код:
# QINQ
enable qinq
config qinq ports 1-24,26 role nni missdrop disable outer_tpid 0x8100
config qinq ports 25 role uni missdrop disable outer_tpid 0x8100

# VLAN
config vlan default delete 1-28
config vlan default add tagged 24
create vlan 67 tag 67
config vlan 67 add tagged 26
config vlan 67 add untagged 25 advertisement disable
create vlan 7 tag 7
config vlan 7 add tagged 24
config vlan 7 add untagged 1 advertisement disable
create vlan 700 tag 700
config vlan 700 add tagged 24
config vlan 700 add untagged 2 advertisement disable


Пояснения:
- Схема: Cisco3750 порт 1/0/39 идёт транк с Сервис-Провайдером, от него в другом месте выходит транк на DLink3528 порт 26.
- На Cisco3750 порты 1/0/37 и 1/0/38 соединены кроссовером.
- На DLink3528 порты 24 и 25 соединены кроссовером.
- На Cisco3750, на порту 1/0/38 прописан левый нативный VLAN, чтоб получить тегированный VLAN 1
- У сервис-провайдера пришлось поднять MTU до 1524, и прописать порты в нашу сторону тегированным 67 VLANом


Получили:
- наши VLANы 1,7,700 бегают по одному VLANу 67 сервис-провайдера.
- есть удалённое управление DLink3528
- сразу на DLink3528 отдаются untaget пакеты

Неясности:
- STP между 3750 и 3528 :)









frame-tag tpid 0x88a8 












download firmware_fromTFTP 10.90.90.1 DES-3200R_1.33.B003.had image_id 1
download cfg_fromTFTP 10.90.90.1 /s-ring8/ushinskogo23-s1.sc.int