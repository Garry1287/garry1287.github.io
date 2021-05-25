---
layout: post
title:  "titova-vodop"
date:   2016-03-16 18:01:48 +0300
categories: PSI
tags: PSI
---

# titova-vodop

Ответы:

1. Резервирование и балансировка.

2. ТТК - L2

3. Локальные сети 

Компы
192.168.0.1 - 192.168.0.255
255.255.255.0

Компы
192.168.100.1 - 192.168.100.255
255.255.255.0


Адреса для игровых аппаратов
172.31.32.1 - 172.31.33.255
255.255.0.0



4. В данный момент мы пользуемся каналом ТТК, при проблемах в ручную переключаем на Промсвязь. Аналогично пункту 3.

5. 8 Мбит/с и 8 Мбит/с


ospf
ip ospf cost одинаковый выставите и будет балансировать
используйте sh ip route x.x.x.x для подбора метрик 
[http://www.alexr.me/index.php?option=com_content&view=article&id=115:quagga-ospf&catid=1:linux&Itemid=5](http://www.alexr.me/index.php?option=com_content&view=article&id=115:quagga-ospf&catid=1:linux&Itemid=5)

eigrp
[http://www.cisco.com/en/US/tech/tk365/technologies_tech_note09186a008009437d.shtml](http://www.cisco.com/en/US/tech/tk365/technologies_tech_note09186a008009437d.shtml)
[http://gh05ter.blogspot.ru/2012/01/eigrp.html](http://gh05ter.blogspot.ru/2012/01/eigrp.html)
[http://xgu.ru/wiki/EIGRP](http://xgu.ru/wiki/EIGRP)
[http://habrahabr.ru/post/139315/](http://habrahabr.ru/post/139315/)
[http://9va8.at.ua/forum/9-98-1](http://9va8.at.ua/forum/9-98-1)

ip sla
[http://xgu.ru/wiki/%D0%A0%D0%B5%D0%B7%D0%B5%D1%80%D0%B2%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5_%D0%98%D0%BD%D1%82%D0%B5%D1%80%D0%BD%D0%B5%D1%82-%D0%BA%D0%B0%D0%BD%D0%B0%D0%BB%D0%BE%D0%B2_%D0%B1%D0%B5%D0%B7_%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F_BGP](http://xgu.ru/wiki/%D0%A0%D0%B5%D0%B7%D0%B5%D1%80%D0%B2%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5_%D0%98%D0%BD%D1%82%D0%B5%D1%80%D0%BD%D0%B5%D1%82-%D0%BA%D0%B0%D0%BD%D0%B0%D0%BB%D0%BE%D0%B2_%D0%B1%D0%B5%D0%B7_%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F_BGP)
[http://sysadmins.ru/topic326834.html](http://sysadmins.ru/topic326834.html)
[http://www.opennet.ru/base/cisco/ip_sla.txt.html](http://www.opennet.ru/base/cisco/ip_sla.txt.html)
[http://forum.internetworkexpert.com/forums/p/16349/136384.aspx](http://forum.internetworkexpert.com/forums/p/16349/136384.aspx)
[http://www.anticisco.ru/pubs/DualISPRouter.pdf](http://www.anticisco.ru/pubs/DualISPRouter.pdf)
[http://blog.sokolov.me/2009/11/25/cisco-route-map-and-ip-sla-%D0%B1%D0%B0%D0%BB%D0%B0%D0%BD%D1%81%D0%B8%D1%80%D0%BE%D0%B2%D0%BA%D0%B0-%D0%BD%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D0%BA%D0%B8/](http://blog.sokolov.me/2009/11/25/cisco-route-map-and-ip-sla-%D0%B1%D0%B0%D0%BB%D0%B0%D0%BD%D1%81%D0%B8%D1%80%D0%BE%D0%B2%D0%BA%D0%B0-%D0%BD%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D0%BA%D0%B8/)