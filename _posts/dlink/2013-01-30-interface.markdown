---
layout: post
title:  "interface"
date:   2013-01-30 08:10:10 +0400
categories: dlink
tags: dlink
---

# interface
 no ip redirects
 no ip unreachables
 no ip proxy-arp
 
 
 
 
 
  spanning-tree portfast
 spanning-tree portfast trunk
Функция обеспечивающая то, что на данном порту подлкючено оконечное обородование без настройки stp, соответственно транком и аксеесом

 spanning-tree bpdufilter enable
Команда bpdufilter запрещает прохождение BPDU фреймов на порту.

 spanning-tree bpduguard enable
При попадинии BPDU stp на порт, сработает errdisable
Команда bpduguard слушает начилие любых BPDU фреймов и блокирует порт.


switchport nonegotiate
nonegotiate — Порт готов перейти в режим trunk, но при этом не передает DTP-кадры порту на другом конце. Этот режим используется для предотвращения конфликтов с другим "не-cisco" оборудованием. В этом случае коммутатор на другом конце должен быть вручную настроен на использование trunk'а. 


show errdisable recovery

LINK-3-UPDOWN - нет несущей, из-за помех, отсутствия синхонизации и пр. (L1 проблема)
LINEPROTO-5-UPDOWN - соответственно, нет канального протокола (L2 проблема)



 Это: выключить спаннинг; на траковом порту включить switchport nonegotiate; посмотреть ошибки физического уровня в выводе интерфейса (если есть, то менять кабель), поиграться со скоростью и дуплексом.


[http://www.cisco.com/cisco/web/support/RU/10/105/105416_errdisable_recovery.html](http://www.cisco.com/cisco/web/support/RU/10/105/105416_errdisable_recovery.html)
[http://www.firewall.cx/cisco-technical-knowledgebase/cisco-switches/883-cisco-switches-errdisable-autorecovery](http://www.firewall.cx/cisco-technical-knowledgebase/cisco-switches/883-cisco-switches-errdisable-autorecovery)
[http://vetriks.ru/tech-library/57-cisco-003-04.html](http://vetriks.ru/tech-library/57-cisco-003-04.html)





interface FastEthernet0/2
 description IPoE abonents
 switchport access vlan 1011
 switchport mode access
 switchport port-security
 switchport port-security maximum 3
 switchport port-security violation restrict
 ip access-group dhcp_control in
 storm-control broadcast level pps 200 150
 storm-control multicast level 60.00 30.00
 storm-control action shutdown
 storm-control action trap
 spanning-tree portfast
 spanning-tree bpdufilter enable


 
 Но access port - это:
- port-security (лимит количества MAC) + sticky если нужно;
- portfast;
- bpduguard;
- storm-control broadcast/multicast = 5.0%
- storm-contrl unicast 20-70K pps (зависит от роли порта);
- dhcp snooping (защита от левого DHCP);
- swi unicast block (в отдельных случаях);
- protected (или private-vlan);
- mls qos cos override



На клиентских
storm-control broadcast level 0.50 0.40

storm-control multicast level 0.50 0.40

 storm-control action ?????

на портах между коммутаторами

storm-control broadcast level 5 3

storm-control multicast level 5 3

 
 The number limits the total percentage of that traffic type on the interface. So, storm-control broadcast level 10 limits that interface to only transmit at most 10% of its interface bandwidth worth of broadcast packets. 10% is a good normal number. However if you are running any broadcast applications it could cause problems. It is also dangerous to set the port to automatically go into shutdown. Now as a bad guy, all I need to do is send a flood of broadcast traffic at that interface that hits the 10% threshold and I can shutdown the switchport and easily DoS the switch.
 
 We use 7% broadcast and 10% multicast
 
 Switch(config-if)#storm-control broadcast level ?
<0.00 – 100.00>  Enter rising threshold
bps              Enter suppression level in bits per second
pps              Enter suppression level in packets per second




interface GigabitEthernetX/Y
 description ** Standard End-User Port **
 switchport access vlan 10
 switchport mode access
 switchport voice vlan 25
 switchport port-security maximum 5
 switchport port-security
 switchport port-security aging time 5
 switchport port-security violation restrict
 switchport port-security aging type inactivity
 no logging event link-status
 load-interval 30
 srr-queue bandwidth share 1 30 40 30
 priority-queue out 
 no snmp trap link-status
 storm-control broadcast level pps 1k 500
 storm-control action shutdown
 storm-control action trap
 spanning-tree portfast
 service-policy input END-USER-INPUT-POLICY
 ip dhcp snooping limit rate 100
 
 rising threshold 
 Восходящий порог 
 
 Whenever broadcast traffic exceeds 30% of the interface bandwidth, we will take action. I didn’t configure any action yet but the default action will drop exceeding traffic.

 
 
 Drop - дропает пакеты
 Shutdown ложит порт и поднимает через CountDown время. Если это время не указано 5 минут поднимает, либо сам администратор должен поднять

  The threshold value is measured in Kbit/sec when the action isto drop mode; it is measured in pps(packets/sec) when the action is set to shutdown mode. 

  Time interval
  Это поле позволяет задать временной интервал, через который микросхема
коммутатора будет предоставлять данные по количеству многоадресных и
широковещательных пакетов для надлежащей работы функции управления
трафиком. Эти данные будут опеределяющим фактором при принятии
решения о том, что число входящих пакетов превысило пороговую
величину. Этот интервал может принимать значения от 5 до 30 с (по
умолчанию 5 с).

Count Down
Таймер Count Down позволяет определить время в минутах, в течение
которого Коммутатор не будет закрывать порт, на котором обнаружен
пакетный шторм. Этот параметр имеет значение только для портов,
настроенных со значением Shutdown в поле Action, т.е. при использовании
программной функции управления трафика. Допустимые значения в данном
поле 0, 5-30 с. По умолчанию задано 0, что означет, что порт никогда не
будет переходить в состояние shutdown.

 
 [http://xcme.blogspot.ru/2015/11/traffic-control.html](http://xcme.blogspot.ru/2015/11/traffic-control.html)
  Работа Traffic Control на разных ревизиях
Проверили на стенде работу Traffic Control в коммутаторах DES-3028 и DES-3200-28 всех ревизий. Исходили мы из этого:

Режим Shutdown:
При обнаружении шторма на порту, когда превышено значение Threshold, свич блокирует на этом порту весь входящий трафик на период Count Down (кроме STP-трафика). Через каждый интервал Time Interval производится проверка на наличие шторма, превышающего Threshold. Если по истечении времени Count Down трафик еще присутствует, тогда порт переводится в режим Shutdown Rest. Через 5 минут порт автоматически вернется в нормальное состояние. Если же при следующей проверке до истечения Count Down шторм не обнаруживается, тогда свич переводит порт в нормальный режим, разрешая входящий трафик на нем.

В режиме Shutdown значение Threshold представлено в пакетах в секунду.

Такой режим мы использовали долгое время, пока не перешли к использованию режима drop. В этом режиме трафик, превышающий threshold, должен просто отбрасываться без лишних премудростей. Но еще ранее было замечено, что в режиме shutdown коммутатор сообщает об обнаружении шторма, а в режиме drop сообщения иногда есть, а иногда нет. Вот с этим и захотелось разобраться.

При тестах было замечено, что DES-3200-28/C1 при работе в режиме drop сообщает в лог о шторме, а остальные коммутаторы из списка выше - нет. Причем фильтрация в этом режиме у /C1 работает намного качественнее, в то время как при использовании /B1 второй хост получает часть пакетов от "флудящего" хоста. В режиме shutdown коммутаторы работают, вроде бы, одинаково.

Пришлось снова открывать инструкции. Судя по ним, для модели DES-3028 значение параметра threshold представлено в килобитах в секунду (не указано для обоих режимов или для одного); на DES-3200-28/A1/B1 — в килобитах в секунду в режиме drop и пакетах в секунду в режиме shutdown; на DES-3200-28/C1 — в пакетах в секунду в обоих режимах.

Вот здесь то, судя по всему, и порылась наша собака!

Ограничение по PPS намного точнее, чем по Kbit/sec. При этом режим drop удобнее тем, что трафик обрабатывается аппаратно, а порт клиента не блокируется.

Итоговые результаты такие:

    DES-3200-28/C1 - лучше всего справляется со штормом в сети. В режиме drop он будет ограничивать шторм аппаратными средствами, сообщая в лог о начале и окончании шторма. Порт при этом отключаться не будет, а клиент будет получать услугу.
    DES-3200-28/A1/B1 - для этой модели предстоит выбирать между: а) ограничивать лишний трафик по максимуму, блокируя порт и сообщая об этом в логе; б) не блокировать порт, пропускать больше лишнего трафика и ничего не сообщать в лог.
    DES-3028 - аналогично как в предыдущем случае. Про режим shutdown пояснений в инструкции не нашлось, но, скорее всего, дело обстоит точно так же, как у DES-3200-* первых ревизий.

p.s. Помню как несколько лет в все плевались от ревизии C1, выгребая со складов остатки B1. И это было оправдано, т.к. софт был очень сырым. Между тем, все больше убеждаюсь, что ревизия C1 на порядок лучше старых моделей. Это совершенно другой коммутатор.



Автор: xcme на 17:36 Отправить по электронной почтеНаписать об этом в блогеОпубликовать в TwitterОпубликовать в FacebookПоделиться в Pinterest




config traffic control auto_recover_time 0
config traffic trap none
config traffic control  1-27 broadcast disable multicast disable unicast disable action drop threshold 255000 countdown 0 time_interval 5
                                                                                























 remember, Multicast levels (which includes more things) must be higher, or at least equal, to the Broadcast levels when configuring Storm-Control!
Multicast level должен быть эквивалентен или больше, чем броадкаст


All Layer 2 Broadcasts are Multicasts.
All Layer 2 Multicasts are not Broadcasts.
you should set Multicast limit HIGHER than the Broadcast limit
[http://cauew.blogspot.ru/2008/09/storm-control-everything-you-need-to.html](http://cauew.blogspot.ru/2008/09/storm-control-everything-you-need-to.html)

[http://www.netcraftsmen.com/understanding-cisco-traffic-storm-control/](http://www.netcraftsmen.com/understanding-cisco-traffic-storm-control/)

Use the following commands to accomplish flood-blocking at the interface level;
Switch(config-if)#switchport block {unicast | multicast}


Броадкас и мультикаст по 10% на всех кроме STP портов
[http://www.juniper.net/techpubs/en_US/junos11.4/topics/concept/rate-limiting-storm-control-understanding.html](http://www.juniper.net/techpubs/en_US/junos11.4/topics/concept/rate-limiting-storm-control-understanding.html)
[https://www.juniper.net/techpubs/en_US/junos/topics/example/rate-limiting-storm-control-configuring.html](https://www.juniper.net/techpubs/en_US/junos/topics/example/rate-limiting-storm-control-configuring.html)

xe-0/0/0        up    up   Link to Cat4900 ctd-s6
    Total packets                 125904131016     152870088174
    Unicast packets               124619818611     151859849501
    Broadcast packets                715952600        728970289
    Multicast packets                568359805        281268384



xe-0/0/1        up    up   SORM 10G port
    Total packets                            5    1159105585336
    Unicast packets                          0    1155281112040
    Broadcast packets                        0       2263622589
    Multicast packets                        5       1560850707


    Total packets                  42725160612      55581052078
    Unicast packets                42468168033      54902695184
    Broadcast packets                102339937        502556418
    Multicast packets                154652642        175800476



xe-0/0/2        up    up   K9-S9-10G
    Total packets                  42727727271      55584520125
    Unicast packets                42470727674      54906125959
    Broadcast packets                102344144        502583385
    Multicast packets                154655453        175810781


xe-0/0/3        up    up   CTD-S8 (DGS-3627G)
    Total packets                 119987627981     160920625008
    Unicast packets               119643263428     159268328122
    Broadcast packets                187822875       1023238601
    Multicast packets                156541678        629058285


xe-0/0/4        up    up   REDBACK 6/2 INET
    Total packets                 324713774251     464772097121
    Unicast packets               324713149291     464766631599
    Broadcast packets                     9571           627528
    Multicast packets                   615389          4837994



xe-0/0/5        up    up   Matyra-S0_Te1:25
    Total packets                  60054589605      86375680194
    Unicast packets                59899074719      86314405150
    Broadcast packets                 76412232         59867309
    Multicast packets                 79102654          1407735

xe-0/0/6        up    up   CTD-C5 Backbone
xe-0/0/7        up    up   RB 6/1 USERS
xe-0/0/8        up    up   RB 5/1 USERS
ge-0/0/10       up    up   Trunk for NLMK-CE0
ge-0/0/11       up    up   To BGW CTD-C6 Gi0/0/0 ae0
ge-0/0/12       up    up   RSPAN for SORM from CTD-S1
ge-0/0/13       up    up   CTD-S1 Gi0/10 ae1
ge-0/0/14       up    up   CTD-C5 Gi0/0/3 ae3
ge-0/0/15       up    up   Mirror to k9 for VM HyperVisors
ge-0/0/16       up    down CTD-C5 Gi0/0/4 ae3
ge-0/0/17       up    up   To BGW CTD-C6 Gi0/0/1 ae2
ge-0/0/18       up    up   CTD-C6 Gi0/0/3 trunk 802.1q
ge-0/0/19       up    up   CTD-C5 Gi0/0/1 ae3
ge-0/0/20       up    up   CTD-S1 Gi0/5 ae1
ge-0/0/21       up    up   Vodopyanova 21a
ge-0/0/22       up    up   Link-VPN-RETN
ge-0/0/23       up    up   To BGW CTD-C6 Gi0/0/2 ae0
xe-0/0/30                  Test second link to K9
xe-0/0/31                  Second Link to Cat4900
ae0             up    up   BGW CTD-C6
ae1             up    up   CTD-S1
ae3             up    up   It was etherchanel to CTD-C5 Backbone


1.Сделать везде 10%, потом поставить на мониторинг и оценить в пакетах
