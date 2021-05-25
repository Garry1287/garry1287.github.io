---
layout: post
title:  "zcash_monero"
date:   2012-02-08 19:48:20 +0400
categories: mining
tags: mining
---

# zcash_monero
Monero
[https://ru.wikipedia.org/wiki/Monero](https://ru.wikipedia.org/wiki/Monero)
[https://moneropools.com/](https://moneropools.com/)
[https://getmonero.org/resources/user-guides/mine-to-pool.html](https://getmonero.org/resources/user-guides/mine-to-pool.html)
[https://getmonero.org/downloads/#linux](https://getmonero.org/downloads/#linux)
[http://miningclub.info/threads/nastrojka-xmr-monero-majnera-dlja-processora.5676/page-2](http://miningclub.info/threads/nastrojka-xmr-monero-majnera-dlja-processora.5676/page-2)
[http://bitcoinminingsite.ru/majning-monero-solo-ili-v-pule-na-processore-ili-videokarte/](http://bitcoinminingsite.ru/majning-monero-solo-ili-v-pule-na-processore-ili-videokarte/)
[https://moneropool.com/](https://moneropool.com/)
[http://monero.org/services/mining-pools/](http://monero.org/services/mining-pools/)
[https://bitmakler.com/mining_Monero-XMR__pools](https://bitmakler.com/mining_Monero-XMR__pools)
[http://miningclub.info/threads/kakoj-pul-luchshe-dlja-majninga-monero.1811/page-3](http://miningclub.info/threads/kakoj-pul-luchshe-dlja-majninga-monero.1811/page-3)
[http://forum.bitcoinfo.ru/viewtopic.php?f=20&t=30505](http://forum.bitcoinfo.ru/viewtopic.php?f=20&t=30505)

Zcash
[https://z.cash/download.html](https://z.cash/download.html)
[http://miningclub.info/threads/kak-zapustit-majning-zcash-na-linux-nicehash.485/](http://miningclub.info/threads/kak-zapustit-majning-zcash-na-linux-nicehash.485/)


Калькулятор
[http://www.mycryptobuddy.com/ZCashMiningCalculator](http://www.mycryptobuddy.com/ZCashMiningCalculator)
[http://whattomine.com/](http://whattomine.com/)


wallmonpsi
passvika

muzzle musical october knee depth strained puck rigid update fabrics aggravate february wife amnesty usher owls together azure cucumber acoustic utility else moisture nestle puck

Переводил Monero на биржу и не указал Payment ID, деньги на счёт так и не поступили. Что делать в таком случае?


46kYok9K6Go6Qdi4kCoNkQfGrCagnQYfbH4Wd8b4PBLBidoHiwSHEv2H5ZncfYoYxNJWJaGWqVgByQT2dSX5YGKSHGXyS8n

Процессор i7 2670 8 ядер, хочу вообще запустить посмотреть сколько выдает, майнить монеро xmr, пул minergate xmr.pool.minergate.com:45560. Как запустить не совсем понимаю.

Кошелёк
bizfyn.ru/kak-sozdat-koshelek-monero/




 *      { "low_power_mode" : false, "no_prefetch" : true, "affine_to_cpu" : 0 },
 *      { "low_power_mode" : false, "no_prefetch" : true, "affine_to_cpu" : 1 },


"cpu_threads_conf" :
[
   { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 0 },
   { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 1 },
   { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 2 },
   { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 3 },
   { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 4 },
   { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 5 },
   { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 6 },
   { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 7 },
],

"use_slow_memory" : "warn",

"nicehash_nonce" : false,

"use_tls" : false,
"tls_secure_algo" : true,
"tls_fingerprint" : "",

"pool_address" : "moscow.minemonero.pro:7777",
"wallet_address" : "СЮДА НАДО ВСТАВИТЬ СТРОКУ КОШЕЛЬКА",
"pool_password" : "worker001",

"call_timeout" : 10,
"retry_time" : 10,
"giveup_limit" : 0,

"verbose_level" : 4,

"h_print_time" : 60,

"output_file" : "",

"httpd_port" : 0,

"prefer_ipv4" : true,




xmr-stak-cpu действительно быстрее cpuminer-opt и minerd.

По результатам тестов получил прирост от 5 до 20%, в зависимости от среды.


В конфигах настраиваем:
1. "no_prefetch" : true
2. Affinity mask по количеству физических ядер. Под Windows ядра и потоки чередуются, под Linux - физические ядра лидируют.

Пример для Windows:
"cpu_thread_num" : 4,
"cpu_threads_conf" : [
{ "low_power_mode" : false, "no_prefetch" : true, "affine_to_cpu" : 0 },
{ "low_power_mode" : false, "no_prefetch" : true, "affine_to_cpu" : 2 },
{ "low_power_mode" : false, "no_prefetch" : true, "affine_to_cpu" : 4 },
{ "low_power_mode" : false, "no_prefetch" : true, "affine_to_cpu" : 6 },
],

Пример для Linux:
"cpu_thread_num" : 4,
"cpu_threads_conf" : [
{ "low_power_mode" : false, "no_prefetch" : true, "affine_to_cpu" : 0 },
{ "low_power_mode" : false, "no_prefetch" : true, "affine_to_cpu" : 1 },
{ "low_power_mode" : false, "no_prefetch" : true, "affine_to_cpu" : 2 },
{ "low_power_mode" : false, "no_prefetch" : true, "affine_to_cpu" : 3 },
],


Многие нарываются на ошибку "MEMORY ALLOC FAILED". Майнер при этом работает, но процентов на 20 медленнее. Решение простейшее:

Linux:
sudo sysctl -w vm.nr_hugepages=128
sudo echo "vm.nr_hugepages=128" >> /etc/sysctl.conf

Windows (перезагрузка обязательна; ntrights - утилита из resource pack):
ntrights -u %USERNAME% +r SeLockMemoryPrivilege
shutdown -r -f -t 00


Сравнение 3 разных майнеров:
cpuminer-opt - 1660-1665H\s
minerd - 1660-1665H\s
xmr-stak-cpu - 1792-1798H\s 

[https://forum.bits.media/index.php?/topic/22218-chto-seichas-mainit-na-protcessorakh/page-63](https://forum.bits.media/index.php?/topic/22218-chto-seichas-mainit-na-protcessorakh/page-63)
[https://github.com/fireice-uk/xmr-stak-cpu](https://github.com/fireice-uk/xmr-stak-cpu)
[https://pachinvadim.ru/all/mayning-na-cpu/](https://pachinvadim.ru/all/mayning-na-cpu/)
[https://silentmonero.com/downloads/xmr-stak-cpu/](https://silentmonero.com/downloads/xmr-stak-cpu/)
[http://bittogether.com/index.php?topic=377.60](http://bittogether.com/index.php?topic=377.60)
[http://miningclub.info/threads/xmr-stak-cpu-nastrojka.4119/page-4](http://miningclub.info/threads/xmr-stak-cpu-nastrojka.4119/page-4)

Попробовать
[https://minemonero.pro/en/#](https://minemonero.pro/en/#)!/help/getting_started

sudo boblightd > /dev/null 2>&1 &


"cpu_threads_conf" :
[
   { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 0 },
   { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 1 },
   { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 2 },
   { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 3 },
   { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 4 },
   { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 5 },
   { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 6 },
   { "low_power_mode" : true, "no_prefetch" : true, "affine_to_cpu" : 7 },
],


"pool_address" : "pool.miners.pro:3333",
"wallet_address" : "46kYok9K6Go6Qdi4kCoNkQfGrCagnQYfbH4Wd8b4PBLBidoHiwSHEv2H5ZncfYoYxNJWJaGWqVgByQT2dSX5YGKSHGXyS8n",
"pool_password" : "",
