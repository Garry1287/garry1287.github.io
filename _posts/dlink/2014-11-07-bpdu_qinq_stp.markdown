---
layout: post
title:  "Настройка bpdu для qinq"
date:   2014-11-07 06:53:44 +0300
categories: dlink
tags: dlink
---

# Настройка bpdu для qinq

```
# bpdu_qinq_stp
 config bpdu_tunnel ports 22 type uplink                                                                                                                     
disable bpdu_tunnel



config address_binding ip_mac ports 1-24 state disable allow_zeroip disable forward_dhcppkt enable
config address_binding ip_mac ports 1-24 mode arp stop_learning_threshold 500 
config address_binding dhcp_snoop max_entry ports 1-24 limit 5

```

Мониторинг порта показал, что после включения QinQ на DES-3200-26, коммутатор начинает передавать и принимать BPDU на адрес 01:80:C2:00:00:08, вместо 01:80:C2:00:00:00. В то время как DGS продолжает использовать адрес 01:80:C2:00:00:00 в своих BPDU пакетах. В итоге два коммутатора просто не видят друг друга по STP.

Уважаемые сотрудники D-Link, хотелось бы получить хоть какой-нибудь комментарий по данному вопросу, а то все как в пустоту...



DGS-3100 и DES-3200 не получится объединить в STP кольцо при включенном Q-in-Q на DES-3200.
По стандарту при включении Q-in-Q bpdu пакеты провайдерских портов будут отсылаться на mac 01-80-c2-00-00-08 во избежании путаницы клиентских и провайдерских копий stp, т.к. bpdu пакеты не тегируются.
А так как на DGS-3100 Q-in-Q нет (и не будет), то решить вашу задачу, к сожалению, не представляется возможным.


В случае использования Q-in-Q будет разница в том, на какой Destination MAC будет отправляться BPDU пакет. На UNI и NNI портах это значение будет отличаться.
Рекомендую Вам сниффером посмотреть Destination MAC-адрес у BPDU пакетов и Вы увидите отличие.



При включенном mstp & qinq dgs3620-28sc (firmware 2.00b023) посылает bpdu:
в uni порт - на адрес 01:80:c2:00:00:00
в nni порт - на адрес 01:80:c2:00:00:08

Такой вопрос: можно ли сделать так, чтобы для nni порта использовался mac адрес 01:80:c2:00:00:00?
Это нужно, чтобы подружить catalyst 4900m и dgs3620-28sc.


Нельзя.
В nni порт коммутаторы отсылают bpdu на мак 01:80:c2:00:00:08


Как выяснилось - если очень хочется, то можно:
`config stp nni_bpdu_addr dot1d`

В этом случае будьте аккуратным с stp, чтобы у вас не перепутались клиентские и операторские деревья.



 NNI BPDU Address   : dot1d  

 NNI BPDU Address   : dot1ad  


Для каталиста наивысший BID
Для корневого DGS ниже (он никогда не может стать рутом)
Для длинков - стандартный (они никогда рутом не могут стать)


Это когда приоритет для DGS выше
```
k9-s6#sh spanning-tree mst

##### MST0    vlans mapped:   1-21,23-25,27-1998,2000-4094
Bridge        address 0013.1afa.6280  priority      32768 (32768 sysid 0)
Root          address 5cd9.983e.9d00  priority      24576 (24576 sysid 0)
              port    Fa0/3           path cost     200000   
Regional Root this switch
Operational   hello time 2 , forward delay 15, max age 20, txholdcount 6 
Configured    hello time 2 , forward delay 15, max age 20, max hops    20

Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/1            Desg FWD 200000    128.1    P2p Edge 
Fa0/3            Root FWD 200000    128.3    P2p Bound(RSTP) 
Fa0/4            Altn BLK 200000    128.4    P2p Bound(RSTP) 
Fa0/24           Desg FWD 200000    128.24   P2p Edge 

##### MST1    vlans mapped:   22,26
Bridge        address 0013.1afa.6280  priority      32769 (32768 sysid 1)
Root          this switch for MST1

Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/3            Mstr FWD 200000    128.3    P2p Bound(RSTP) 
Fa0/4            Altn BLK 200000    128.4    P2p Bound(RSTP) 
Fa0/24           Desg FWD 200000    128.24   P2p Edge 

##### MST2    vlans mapped:   1999
Bridge        address 0013.1afa.6280  priority      32770 (32768 sysid 2)
Root          this switch for MST2

Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/3            Mstr FWD 200000    128.3    P2p Bound(RSTP) 
Fa0/4            Altn BLK 200000    128.4    P2p Bound(RSTP) 
Fa0/24           Desg FWD 200000    128.24   P2p Edge 
```


Cisco так не работает. В статье написано
master port - это линк к корневому (CIST), который находится во вне региона


Приоритет для CIST устанавливается в 0 instanse
`spanning-tree mst 0 priority 16384`

Конфиги в mst-rstp 

```
(3200-28)========(3627G)==========(K9-S6)
52 влан		23,24 UNI		mstp
53 влан		1999 transp		0 инстанс все	
25,26 uplink	22 mng			1 (22,26)
26 mng		21,22 NNI		2 (1999)
		Vlan_tra для 26		3,4 порты транк
		на 23,24 порту		
```

1. Новые рутовые приоритеты 
2. Остальные приоритеты (поменять приоритет для 0 инстанса с ctd-s1 на ctd-s6)
3. Включить config stp nni_bpdu_addr dot1d
4. Настроить порты на DGS v21a-s0
```
config stp ports 1:24 fbpdu enable
config stp ports 1:24 externalCost auto  edge false p2p auto state enable restricted_role false restricted_tcn false lbd disable

config stp ports 1:25 fbpdu enable
config stp ports 1:25 externalCost auto  edge false p2p auto state enable restricted_role false restricted_tcn false lbd disable
config stp ports 2:25 fbpdu enable
config stp ports 1:25 externalCost auto  edge false p2p auto state enable restricted_role false restricted_tcn false lbd disable
```
На ctd-s6
```
conf t
interface GigabitEthernet2/20
no spanning-tree portfast trunk
no spanning-tree bpdufilter enable
```

На k9
```
  config stp ports 25 externalCost auto  edge false p2p auto state enable restricted_role false restricted_tcn false lbd disable
 config stp ports 25 fbpdu enable

config ports 25 state enable
```

  



