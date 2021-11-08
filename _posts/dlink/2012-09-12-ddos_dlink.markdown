---
layout: post
title:  "Настройка защиты от ddos и других атак на dlink"
date:   2012-09-12 19:45:53 +0400
categories: dlink
tags: dlink
---

# Настройка защиты от ddos и других атак на dlink
```
config dos_prevention dos_type land_attack action drop state disable
config dos_prevention dos_type blat_attack action drop state disable
config dos_prevention dos_type smurf_attack action drop state disable 
config dos_prevention dos_type tcp_null_scan action drop state disable 
config dos_prevention dos_type tcp_xmascan action drop state disable
config dos_prevention dos_type tcp_synfin action drop state disable
```


* Land Attacks – These attacks result from sending a specially crafted packet to a machine 
where the source host IP address is the same as the destination host IP address. T
he system attempts to reply to itself, resulting in system lookup

* Blat Attack – These switch result from sending a specially crafted packet to a machine 
where the source host port is the same as the destination host port. The system attempts to reply to itself, resulting in system lockup

* Smurf Attacks – This attack uses Internet Control Message Protocol (ICMP) echo requests packets (pings) to cause network congestion

* NULL scan – TCP sequence number is zero and all control bits are zeros

* Xmascan – TCP sequence number is zero and the FIN, URG and PSH bits are set

* Scan SYNFIN –SYN and FIN bits are set in the packet

* SYN with port 1024 – SYN packets with source port less than 1024


---


Как-то составлял описание атак, которые блокируют коммутаторы D'Link. Поправьте если есть ошибки.
Описание атак:
*  Ping of death — тип сетевой атаки, при которой компьютер-жертва получает особым образом подделанный эхо-запрос (ping), 
после которого он перестает отвечать на запросы вообще. 
В данный момент этот тип атак практически не наблюдается, т.к. уязвимость была исправлена в конце 90х годов.

* tcp_synfin. Одна из разновидностей стелс сканирования. В данном пакете одновременно установлены флаги SYN 
(используется для установления соединения) и 
* FIN (Final - посылается при завершении соединения ). 
Расчет делается на то, что на такой пакет разные TCP/IP стеки реагигуют по разному. На основании этого делается вывод о том какая ОС на хосте.

* Blat attack. Разновидность DOS атаки в котором порт источника равен порту назначения.

* Land attack. Метод атаки заключается в отправке поддельного пакета TCP SYN (инициация соединения) 
с одинаковыми IP-адресами и номерами портов источника и назначения. Может приводить к зависанию сервера.

* tcp_xmasscan. Дос атака в которой порядковый номер пакета равен нулю, а FIN, URG и PSH биты установлены.

* tcp_null_scan. Тип атаки в которой порядковый номер пакета равен нулю и все управляющие биты установлены в ноль.
 Используется для получения информации об открытых портов портах клиента, версии ОС и тп.

* tcp_tiny_frag_attack (атака малыми фрагментами). Детектируется в случае, если размер любого из фрагментов 
за исключением последнего меньше 400 байт, это означает, что фрагмент, по-видимому, преднамеренно сформирован.
 Малые фрагменты могут использоваться в атаках типа «отказ в обслуживании» или при попытках обойти защитные механизмы.

* tcp_syn_srcport_less_1024. Тип атаки в котором при установлении соединения указывается порт источника меньше 1024. 
Обычно данные порты зарезервированны службы и не выдаются при создании TCP подлючения.
















