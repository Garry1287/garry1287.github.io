---
layout: post
title:  "Bridge в cisco"
date:   2017-05-13 14:20:54 +0300
categories: cisco
tags: cisco
---

# Bridge в cisco

Путь: It.notes > Cisco > Настраивем бридж на роутерах cisco.

Настраивем бридж на портах роутера cisco. Сетевой мост, бридж (калька с англ. bridge) — сетевое устройство второго уровня модели OSI, предназначенное для объединения сегментов (подсети) компьютерной сети в единую сеть. (c)wiki

[http://ru.wikipedia.org/wiki/%D0%A1%D0%B5%D1%82%D0%B5%D0%B2%D0%BE%D0%B9_%D0%BC%D0%BE%D1%81%D1%82](http://ru.wikipedia.org/wiki/%D0%A1%D0%B5%D1%82%D0%B5%D0%B2%D0%BE%D0%B9_%D0%BC%D0%BE%D1%81%D1%82)

```
!

bridge irb

!
bridge 1 protocol ieee
bridge 1 route ip
```
назначаем интерфейсам вхождение в бридже (bridge-group 1)

```
!
interface Ethernet0/1
no ip address
full-duplex
no cdp enable
bridge-group 1
!
interface Ethernet0/2
no ip address
full-duplex
no cdp enable
bridge-group 1
!
```
Создаем новый интерфейс BVI и даем ему IP-адрес:
```
interface BVI1
ip address 192.168.1.3 255.255.255.0
```