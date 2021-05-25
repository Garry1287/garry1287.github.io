---
layout: post
title:  "mstp-change"
date:   2010-09-18 19:43:23 +0400
categories: mstp
tags: mstp
---

# mstp-change
      Изменения конфигурации производим с sapphire.
     
      1.Размыкаем оба кольца
      CTD-S1
      int Gi0/25
      sh
      int Gi0/27
      sh

      
       
      2. Т.к. между CTD-S1 и CTD-S6 etherchannel, то добавляем
      конфигурацию на S6, затем на S1.
      conf t
      
      spanning-tree mst configuration
      instance 4 vlan 1816
      instance 4 vlan 1817
      instance 4 vlan 1818
      
      vlan 1816
       name TRRB1816
      vlan 1817
       name TRRB1817
      vlan 1818
       name TRRB1818
      
      3. Далее добавляем конфигурацию на коммутаторы начиная с "дальнего
      конца".
          3.1. ATS45-S0
          3.2. CDE-S0
          3.3. K9-S9
          config stp instance_id 4 add_vlan 1816-1818
          create vlan TRRB1816 tag 1816
          config vlan TRRB1816 a t 8,25,26
      
          create vlan TRRB1817 tag 1817
          config vlan TRRB1817 a t 8,25,26
      
          create vlan TRRB1818 tag 1818
          config vlan TRRB1818 a t 8,25,26
      
      4. Замыкаем кольца на CTD-S1.
      
   
      P.S. Возможно, что пункт 2 можно исключить и в пункте 3 добавлять
      конфигурацию в последовательности
          3.1. ATS45-S0
          3.2. CDE-S0
          3.3. K9-S9
          3.4. CTD-S6
          3.5. CTD-S1























#ctd-s6

conf t
vlan 219
 name stk-psi-voip

spanning-tree mst configuration
instance 1 vlan 219




#ctd-s1

conf t
vlan 219
 name stk-psi-voip

spanning-tree mst configuration
instance 1 vlan 219


int Gi0/25
switchport trunk allowed vlan add 219

int Gi0/27
switchport trunk allowed vlan add 219




#ats45-s0

conf t
vlan 219
 name stk-psi-voip


spanning-tree mst configuration
instance 1 vlan 219


int Gi0/52
switchport trunk allowed vlan add 219


int Gi0/51
switchport trunk allowed vlan add 219



#cde-s0

conf t
vlan 219
name stk-psi-voip


spanning-tree mst configuration
instance 1 vlan 219


int Gi0/52
switchport trunk allowed vlan add 219

int Gi0/49
switchport trunk allowed vlan add 219

int Gi0/50
switchport trunk allowed vlan add 219












#k9-s9

create vlan stk-psi-voip tag 219

config stp instance_id 1 add_vlan 219 


config vlan stk-psi-voip a t 1,8,25,26





config stp instance_id 1 add_vlan 10

