---
layout: post
title:  "access-list-gryazi"
date:   2016-03-26 19:24:43 +0300
categories: PSI
tags: PSI
---

# access-list-gryazi
access-list 31 deny   172.28.16.1
access-list 31 permit 172.28.16.0 0.0.3.255
access-list 31 permit 10.0.16.0 0.0.3.255
access-list 31 deny   any


access-list 131 deny udp 172.28.16.0 0.0.3.255 any eq 67
access-list 131 deny udp 10.0.16.0 0.0.3.255 any eq 67
access-list 131 permit ip 172.28.16.0 0.0.3.255 any
access-list 131 permit ip 10.0.16.0 0.0.3.255 any
access-list 131 deny   any any






1.Снять роут мап
Если заработает хорошо, то попробовать 131 роут мап


interface Vlan2010
 description Derkach I.U.ul.Chelyskiana.1.10
 ip unnumbered Loopback2
 ip helper-address 172.28.0.4
 ip policy route-map pptp-nat2
 service-policy input VLAN_POLICY_5120

vlan 2010
  name Derkach I.U.ul.Chelyskiana.1.10

int Gi1/0/1
  switchport trunk allowed vlan add 2010

create vlan Derkach.I.U.ul.Chelyskiana.1.10 tag 2010
config vlan Derkach.I.U.ul.Chelyskiana.1.10 add tagged 25-26


create vlan Derkach.I.U.ul.Chelyskiana.1.10 tag 2010
config vlan Derkach.I.U.ul.Chelyskiana.1.10 add tagged 25
config vlan Derkach.I.U.ul.Chelyskiana.1.10 add untagged 1
config ports 1 description "Derkach.I.U.ul.Chelyskiana.1.10" state enable


interface Vlan2011
 description Loshkarev.R.A.ul.Pravda15.70
 ip unnumbered Loopback2
 ip helper-address 172.28.0.4
 ip policy route-map pptp-nat2
 service-policy input VLAN_POLICY_5120

vlan 2011
  name Loshkarev.R.A.ul.Pravda15.70

int Gi1/0/1
  switchport trunk allowed vlan add 2011

create vlan Loshkarev.R.A.ul.Pravda15.70 tag 2011
config vlan Loshkarev.R.A.ul.Pravda15.70 add tagged 25-26


create vlan Loshkarev.R.A.ul.Pravda15.70 tag 2011
config vlan Loshkarev.R.A.ul.Pravda15.70 add tagged 25
config vlan Loshkarev.R.A.ul.Pravda15.70 add untagged 5
config ports 5 description "Loshkarev.R.A.ul.Pravda15.70" state enable








interface Vlan2012
 description Peksheev.S.I.ul.Pravda15.41
 ip unnumbered Loopback2
 ip helper-address 172.28.0.4
 ip policy route-map pptp-nat2
 service-policy input VLAN_POLICY_5120

vlan 2012
  name Peksheev.S.I.ul.Pravda15.41

int Gi1/0/1
  switchport trunk allowed vlan add 2012

create vlan Peksheev.S.I.ul.Pravda15.41 tag 2012
config vlan Peksheev.S.I.ul.Pravda15.41 add tagged 25-26


create vlan Peksheev.S.I.ul.Pravda15.41 tag 2012
config vlan Peksheev.S.I.ul.Pravda15.41 add tagged 25
config vlan Peksheev.S.I.ul.Pravda15.41 add untagged 6
config ports 6 description "Peksheev.S.I.ul.Pravda15.41" state enable












interface Vlan2013
 description Hlebushkin.A.E.ul.Cheluskina1.18
 ip unnumbered Loopback2
 ip helper-address 172.28.0.4
 ip policy route-map pptp-nat2
 service-policy input VLAN_POLICY_4096

vlan 2013
name Hlebushkin.A.E.ul.Cheluskina1.18

int Gi1/0/1
  switchport trunk allowed vlan add 2013

create vlan Hlebushkin.A.E.ul.Cheluskina1.18 tag 2013
config vlan Hlebushkin.A.E.ul.Cheluskina1.18 add tagged 25-26


create vlan Hlebushkin.A.E.ul.Cheluskina1.18 tag 2013
config vlan Hlebushkin.A.E.ul.Cheluskina1.18 add tagged 25
config vlan Hlebushkin.A.E.ul.Cheluskina1.18 add untagged 2
config ports 2 description "Hlebushkin.A.E.ul.Cheluskina1.18" state enable








interface Vlan2015
 description Gubanov.I.V.ul.Pravda64.23
 ip unnumbered Loopback2
 ip helper-address 172.28.0.4
 ip policy route-map pptp-nat2
 service-policy input VLAN_POLICY_10240

vlan 2015
name Gubanov.I.V.ul.Pravda64.23

int Gi1/0/6
  switchport trunk allowed vlan add 2015

create vlan Gubanov.I.V.ul.Pravda64.23 tag 2015
config vlan Gubanov.I.V.ul.Pravda64.23 add tagged 25-26


create vlan Gubanov.I.V.ul.Pravda64.23 tag 2015
config vlan Gubanov.I.V.ul.Pravda64.23 add tagged 25
config vlan Gubanov.I.V.ul.Pravda64.23 add untagged 1
config ports 1 description "Gubanov.I.V.ul.Pravda64.23" state enable





interface Vlan2016
 description Korotaev.D.R.ul.Cheluskina2.47
 ip unnumbered Loopback2
 ip helper-address 172.28.0.4
 ip policy route-map pptp-nat2
 service-policy input VLAN_POLICY_10240

vlan 2016
name Korotaev.D.R.ul.Cheluskina2.47

int Gi1/0/1
  switchport trunk allowed vlan add 2016

create vlan Korotaev.D.R.ul.Cheluskina2.47 tag 2016
config vlan Korotaev.D.R.ul.Cheluskina2.47 add tagged 25-26


create vlan Korotaev.D.R.ul.Cheluskina2.47 tag 2016
config vlan Korotaev.D.R.ul.Cheluskina2.47 add tagged 25
config vlan Korotaev.D.R.ul.Cheluskina2.47 add untagged 1
config ports 1 description "Korotaev.D.R.ul.Cheluskina2.47" state enable











interface Vlan2017
 description Batischeva.M.V.ul.Komsomolskaya2.44
 ip unnumbered Loopback2
 ip helper-address 172.28.0.4
 ip policy route-map pptp-nat2
 service-policy input VLAN_POLICY_2048

vlan 2017
name Batischeva.M.V.ul.Komsomolskaya2.44

int Gi1/0/1
  switchport trunk allowed vlan add 2017

create vlan Batischeva.M.V.ul.Komsomol2.44 tag 2017
config vlan Batischeva.M.V.ul.Komsomol2.44 add tagged 25-26


create vlan Batischeva.M.V.ul.Komsomol2.44 tag 2017
config vlan Batischeva.M.V.ul.Komsomol2.44 add tagged 25
config vlan Batischeva.M.V.ul.Komsomol2.44 add untagged 1
config ports 1 description "Batischeva.M.V.ul.Komsomol2.44" state enable






config bandwidth_control 2 rx_rate 2048 tx_rate 2048


username bill privilege 15 secret 5 $1$JDo2$GWBWo5AYHxIQNtAjqOguu.


















