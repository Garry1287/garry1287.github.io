---
layout: post
title:  "show_error"
date:   2012-11-27 03:00:59 +0400
categories: dlink
tags: dlink
---

# show_error
CRC Error Counts otherwise valid packets that did not end on a byte (octet) boundary.

UnderSize The number of packets detected that are less than the minimum permitted packets size of 64 bytes and have a good CRC. Undersize packets usually indicate collision fragments, a nor-mal network occurrence.

OverSize Counts valid packets received that were longer than 1518 octets and less than the MAX_PKT_LEN. Internally, MAX_PKT_LEN is equal to 1536.

Fragment The number of packets less than 64 bytes with either bad framing or an invalid CRC. These are normally the result of collisions.

Jabber Counts invalid packets received that were longer than 1518 octets and less than the MAX_PKT_LEN. Internally, MAX_PKT_LEN is equal to 1536.

Drop The number of packets that are dropped by this port since the last Switch reboot.





ExDefer Counts the number of packets for which the first transmission attempt on a particular interface was delayed because the medium was busy.

CRC Error Counts otherwise valid packets that did not end on a byte (octet) boundary.

LateColl Counts the number of times that a collision is detected later than 512 bit-times into the transmission of a packet.

ExColl Excessive Collisions. The number of packets for which transmission failed due to excessive collisions.

SingColl Single Collision Frames. The number of successfully transmitted packets for which transmission is inhibited by more than one collision.

Collision An estimate of the total number of collisions on this network segment.



по той же ссылке - ищите

Таким образом, размер нормального кадра (включая адресную информацию и CRC-код) может быть в диапазоне 64—1518 байт(*) . Адаптер приемника способен распознавать следующие ошибки кадров (конец кадра определяется по пропаданию несущей):

* Длинный кадр (long, oversized) — более 1518 байт с правильным CRC-кодом. Может порождаться некорректным драйвером адаптера.
* Короткий кадр (runt, undersized) — менее 64 байт с правильным CRC-кодом. Может порождаться некорректным драйвером адаптера. _
* Болтливый» кадр (jabber) — более 1518 байт с неправильным CRC-кодом. Может порождаться неисправным трансивером (адаптером).
* Ошибка выравнивания (alignment error) — кадр, длина которого не кратна байту. Может порождаться неисправным адаптером, трансивером, кабелем.
* Ошибка контрольного кода (СRC error) — кадр правильной длины, но с неправильным CRC-кодом. Может порождаться помехами, слишком большой длиной кабеля.

----- мои камменты -----

64—1518 байт(*) - тут рассматривается фрейм без дополнений - например
vlan тег - добавит к фрейму 4 байта и будет максимальный 1522 байт
двойной влан (QinQ) - добавит к фрейму 8 байтов и будет максимальный 1526 байт

так каким набором протоколов добивается до 1536 не скажу - надо мануал курить



Блин , ну громадное спасибо.

И последняя напоминалка по паре RX , по

Drop The number of packets that are dropped by this port since the last Switch reboot.


Я так понимаю все пакеты на порту , которые были заблокированы по каким либо правилам свитча, от момента его сетевой активности на порту ?


Было бы еще неплохо разложить TX, пару.

ExDefer Counts the number of packets for which the first transmission attempt on a particular interface was delayed because the medium was busy.
LateColl Counts the number of times that a collision is detected later than 512 bit-times into the transmission of a packet.
ExColl Excessive Collisions. The number of packets for which transmission failed due to excessive collisions.
SingColl Single Collision Frames. The number of successfully transmitted packets for which transmission is inhibited by more than one collision.
Collision An estimate of the total number of collisions on this network segment.

Промт на это ответил .
"LateColl считает количество раз, что столкновение обнаружено позже чем 512 времен прохождения бита в передачу пакета.
ExColl Чрезмерные Столкновения. Число пакетов, для которых передача потерпела неудачу из-за чрезмерных столкновений.
SingColl Единственные Структуры Столкновения. Число успешно переданных пакетов, для которых передача запрещена больше чем одним столкновением.
Столкновение оценка общего количества столкновений на этом сегменте сети."


Вопрос по коллизиям, что это вообще такое, причины и следствия их появления ну и какие они бывают ?
Было бы еще неплохо тех. документацию на русском про коллизиям в сети.

Спасибо , Tsvetkovу , за широко раскрытую тему.




Tsvetkov, спасибо огромное , очень доходчиво.
У d-linka есть наглядный пример [http://www.dlink.ru/ru/faq/62/954.html](http://www.dlink.ru/ru/faq/62/954.html) Кадр (Фрейм) с тегом 802.1Q.

Следующие два значение в команде #show error ports - это

UnderSize The number of packets detected that are less than the minimum permitted packets size of 64 bytes and have a good CRC. Undersize packets usually indicate collision fragments, a nor-mal network occurrence.

и

OverSize Counts valid packets received that were longer than 1518 octets and less than the MAX_PKT_LEN. Internally, MAX_PKT_LEN is equal to 1536.

В переводе от promt.ru.

" UnderSize число пакетов обнаружил, что меньше чем минимальный разрешенный размер пакетов 64 байтов и имеют хороший CRC. Уменьшенные пакеты обычно указывают на фрагменты столкновения, нормальное возникновение сети.

OverSize рассчитывает, действительные пакеты получили, которые были более длинными чем 1518 октетов и меньше чем MAX_PKT_LEN. Внутренне, MAX_PKT_LEN равен 1536. "

Я знаю , что минимальный размер MTU 64 байта , максимальный 1500 байт.

Почему UnderSize 64 байта, что за ошибки тут имеются ввиду ?
Ну и соответственно OverSize почему от 1518 до 1536 , что это за ошибки ?


Помогите , кто чем может.










