---
layout: post
title:  "VMware-plan"
date:   2013-05-17 10:35:43 +0400
categories: linux
tags: linux
---

# VMware-plan
(edit settings - интерфейс - network label -> там выбираешь нужный готовый VM Network, для 27 влан мы уже делали)

ну тогда хорошо... VT-d не обязательно, но VT-x - нужны. Иначе 64-битные виртуалки не взлетят
с VT-d- в виртуалки можно PCI-ные платы пробрасывать, но это специфичный случай.

собственно, вот и весь "хитрый план" (tm) про вмвари...
Два сервака, двумя каналами в каждый в СХД (в разные контроллеры). Что дает 2Gbit/s и отказоустойчивость при пропадении одного канала.
один датастор два сервака могут использовать совместно.

Но - не успел я это сделать. Т.к. не просто ушел, а еще и в разные здания разъехались...




а этот NAS сделал по следующим причинам:
- вмварь не работает с программными рейдами, а на борту купленных серверов были именно такие.
- купленные контроллеры - вмварь понимает, но это контроллеры начального уровня, в них нет батарейки - а потому нет кэша на запись.
А без кеша на запись всю тормозит как падла при числе ВМ больше 4...