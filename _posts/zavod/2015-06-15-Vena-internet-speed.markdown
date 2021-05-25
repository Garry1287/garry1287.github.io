---
layout: post
title:  "Vena-internet-speed"
date:   2015-06-15 14:31:12 +0300
categories: zavod
tags: zavod
---

# Vena-internet-speed
Скорость интернет соединения
Formula to Calculate TCP throughput

bps — бит в секунду, единица измерения скорости обработки информации.
Bps — байт в секунду, единица измерения скорости обработки информации.



Пропускная способность = размер буфера / задержка

TCP-Window-Size-in-bits / Latency-in-seconds = Bits-per-second-throughput


RCV buffer size / RTT = Max TCP throughput = ? bps
** Buffer size is normally 65Kbps

ex) (64Kbyte x 8bit) / 0.17 = 3011764 bps = 3Mbps, (RTT=170ms) 

Размер окна по умолчанию 64KB = 65536 Bytes
Поэтому скорость tcp соединения (пропусканая способность канала) зависит от пинга (длины канала)
Если пинг постоянен, то увеличить пропускную способность можно только увеличивая размер окна





[http://bradhedlund.com/2008/12/19/how-to-calculate-tcp-throughput-for-long-distance-links/](http://bradhedlund.com/2008/12/19/how-to-calculate-tcp-throughput-for-long-distance-links/)



Optimal TCP window size

Bandwidth-in-bits-per-second * Round-trip-latency-in-seconds = TCP window size in bits / 8 = TCP window size in bytes

Размер буфера = RTT * полоса пропускания

RTT - это пинг
RTT=2 x Delay Product
 - Optimal RCV buffer size is considered to be 2 x BDP, where BDP is the Bandwidth*Delay Product


ex) RTT is 20 ms, and connection speed is 10 Mbps.
  2 x (10Mbps/8 * .020s) = 50Kbytes 



Наш случай 
100Мбит/с канал
RTT - 50 милисекунд

Стандартный размер tcp окна TCP window size
64KB = 65536 Bytes.   65536 * 8 = 524288 bits


524288 / 0.05 = 10 485 760
524288 / 0.04 = 13 107 200


Размер окна

512 kbytes
