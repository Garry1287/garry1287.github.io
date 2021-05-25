---
layout: post
title:  "hosting_stat"
date:   2013-10-12 06:19:44 +0400
categories: linux
tags: linux
---

# hosting_stat
iotop
vmstat 1
iostat 1
[https://launchpad.net/mysql-tuning-primer](https://launchpad.net/mysql-tuning-primer)

MySQL пишет на диск, если не хватает tmp_table_size.
В основном это происходит когда не юзают индексы.


netwind, percona - не форк, как mariadb. По-этому они четко следуют за mysql -> добавляя лишь дополнительные патчи в сборку.

В percona обращаются с реальными проблемами. Там не синтетический "хайлоад", а вполне настоящий.

Например xtradb сделали для народа



О кино
Берете среднюю скорость чтения диска rnd и делите на битрейт фильма
Полученное число и будет максимальное число смотрителей фильмов