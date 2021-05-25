---
layout: post
title:  "bridge_linux"
date:   2010-02-02 08:15:17 +0300
categories: linux
tags: linux
---

# bridge_linux
[http://blog.davidvassallo.me/2012/05/05/kvm-brctl-in-linux-bringing-vlans-to-the-guests/](http://blog.davidvassallo.me/2012/05/05/kvm-brctl-in-linux-bringing-vlans-to-the-guests/)

1.Добавляем в бридж eth0 и 2 vnic интерфейса (они же tap). Теперь имеем бридж через который нетегированный трафик может летать как угодно
2.Создаем на основе eth0 2 влана, 5 и 7. Объединяем их в 2 бриджа с двумя vnic интерфейсами (они же tap). Имеем 2 бриджа br5, br7 через которые трафик untagged попадает на вируталки
3.Добавляем в бридж eth0 и 2 vnic интерфейса (они же tap), Создаем на брижде 2 влана - br0.5, br0.7. Теперь на обе виртуалки может попадать тэгированный трафик из 5 и 7 влана

Появилась новая фича - vlan-filter
[https://developers.redhat.com/blog/2017/09/14/vlan-filter-support-on-bridge/](https://developers.redhat.com/blog/2017/09/14/vlan-filter-support-on-bridge/)

Означает, что мы можем настраивать бридж, как нормальный свитч, каждый из портов (реальный, виртуальный tap) можем прописывать вланы тэгом или untagged.
По умолчанию иммеем ненастроенный свитч, который пропускает все

 bridge vlan show
port	vlan ids

enp4s0f0	 1 PVID Egress Untagged

br1	 1 PVID Egress Untagged

vnet0	 1 PVID Egress Untagged

vnet1	 1 PVID Egress Untagged

vnet2	 1 PVID Egress Untagged

Имеем br1, в нем физический и 3 tap интерфейса, все они пропускают всё.
---------------------------

Можно на нём сделать vlan-filter и всё будет по серьёзному как в статье
# bridge vlan show
port    vlan ids
bond0    1 PVID Egress Untagged
         2
         3

br0      1 PVID Egress Untagged

guest_1_tap_0    1 Egress Untagged
         2 PVID Egress Untagged

guest_2_tap_0    1 Egress Untagged
         2 PVID Egress Untagged

guest_2_tap_1    1 Egress Untagged
         3 PVID Egress Untagged

guest_3_tap_0    1 Egress Untagged
         3 PVID Egress Untagged



2 физических порта собраны в bond, bond и 4 tap интерфейса собраны в br0, нужные вланы прописаны на портах
2 и 3 вланы tagged на bond, на виртуалках untagged.









Create a bond device, the same as above.

# ip link add bond0 type bond
# ip link set bond0 type bond miimon 100 mode balance-alb
# ip link set eth0 down
# ip link set eth0 master bond0
# ip link set eth1 down
# ip link set eth1 master bond0
# ip link set bond0 up

Create the bridge interface, enable VLAN filter and attach the bond interface to the bridge directly.

# ip link add br0 type bridge
# ip link set br0 up
# ip link set br0 type bridge vlan_filtering 1

# ip link set bond0 master br0

Attach the tap device to the bridge.

# ip link set guest_1_tap_0 master br0
# ip link set guest_2_tap_0 master br0

# ip link set guest_2_tap_1 master br0
# ip link set guest_3_tap_0 master br0

Set the tap interface with the VLAN filter.

# bridge vlan add dev guest_1_tap_0 vid 2 pvid untagged master
# bridge vlan add dev guest_2_tap_0 vid 2 pvid untagged master

# bridge vlan add dev guest_2_tap_1 vid 3 pvid untagged master
# bridge vlan add dev guest_3_tap_0 vid 3 pvid untagged master

# bridge vlan add dev bond0 vid 2 master
# bridge vlan add dev bond0 vid 3 master



Так как mikrotik - это linux, то там тоже самое
[https://wiki.mikrotik.com/wiki/Manual%3AInterface/Bridge#Bridge_VLAN_Filtering](https://wiki.mikrotik.com/wiki/Manual%3AInterface/Bridge#Bridge_VLAN_Filtering)
