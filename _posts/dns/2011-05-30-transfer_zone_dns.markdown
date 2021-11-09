---
layout: post
title:  "Transfer zone dns"
date:   2011-05-30 06:29:01 +0400
categories: dns
tags: dns
---

# Transfer zone dns
Всем привет.

Трансфер DNS зоны из-за NAT отваливается по тамауту.
Экспериментально выяснил что если зона совсем маленькая
(из вывода dig ;; XFR size: 23 records (messages 1, bytes 542))
то трансфер проходит. Если "bytes > приблизительно 2500", то не проходит.
Пока подозрение именно на NAT (на inside интерфейсе есть еще inspect),
но куда конкретно копать что-то не соображу.

Трансфер делаю так
```
dig @server axfr zone.test.com
dig @81.20.192.16 axfr 113.168.192.in-addr.arpa
```

```
allow-transfer { 192.168.0.2; }; на мастер
chmod 775 /var/named/chroot/var/named на мастере
```



























