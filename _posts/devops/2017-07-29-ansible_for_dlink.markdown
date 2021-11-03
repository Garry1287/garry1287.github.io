---
layout: post
title:  "Ansible и dlink"
date:   2017-07-29 21:06:44 +0400
categories: devops 
tags: devops ansible dlink
---

# ansible_for_dlink
No need to use regex for pattern searching. You can use search like this:
```
when: name_prefix | search("stage-dbs")

ansible_sysdescr == "D-Link DES-3200-28 Fast Ethernet Switch" or ansible_sysdescr =="
```

```
192.168.117.117	d8:fe:e3:ed:4a:40	DES-3200-28	C1	4.36.B016	"R3DZ1DA003613"          DES-3200-28/C1 Fast Ethernet Switch                 OK v
192.168.117.122	1c:bd:b9:5a:8e:40	DES-3200-28	A1	1.83.B009	"PVI41A6002833"             D-Link DES-3200-28 Fast Ethernet Switch              OK v
192.168.117.134	c0:a0:bb:db:37:45	DES-1210-28	B2	6.07.B011	OID                                   DES-1210-28/ME                                                        OK
192.168.117.25	1c:7e:e5:6d:45:c0	DES-3200-28	B1	1.83.B009	"PVZ82B7000552"       D-Link DES-3200-28 Fast Ethernet Switch             OK v
192.168.117.27	00:21:91:97:35:73	DES-3028		2.92.B04	""                                      D-Link DES-3028 Fast Ethernet Switch                    OK v
192.168.118.2	00:1b:11:b5:b6:cc	DES-3526	0A3G	6.20.B18	OID                                  DES-3526 Fast-Ethernet Switch                                   OK  v (timeout=55)
192.168.118.18	00:1e:58:a3:61:9c	DES-3526	A4G	6.20.B18	OID                                       DES-3526 Fast-Ethernet Switch                              OK v
192.168.118.122	1c:7e:e5:6d:40:20	DES-3200-28	B1	1.83.B009	"PVZ82B7000626"          D-Link DES-3200-28 Fast Ethernet Switch             OK v
```
```
192.168.113.9	00:0f:3d:ca:e9:82	DES-3226S	2C1		OID                                                          DES-3226S Fast-Ethernet Switch                              OK
192.168.113.59	34:08:04:65:67:2c	DES-3200-10	A1	1.83.B008	"PVI31BC001883"        D-Link DES-3200-10 Fast Ethernet Switch                OK v
192.168.113.17	00:13:46:26:95:ba	DES-2108	                                                                          DES-2108                                V2.00.17                        Исключать эти свитчи
192.168.113.76	00:1c:f0:0c:1b:8e	DES-3026	Such		OID                                                   Dlink DES-3026 Fast Ethernet Switch                       OK v
192.168.113.234	5c:d9:98:3e:9a:00	DGS-3627G	A1	2.52.B45	""                                      DGS-3627G Gigabit Ethernet Switch                           OK  v                         
192.168.115.12	90:94:e4:43:0f:d0	DES-3200-10	C1	4.36.B009	"R3J11C8001957"               DES-3200-10/C1 Fast Ethernet Switch                         OK v
192.168.113.243	00:1c:f0:9d:71:67	DES-3526	A4	6.20.B20	OID                                          DES-3526 Fast-Ethernet Switch                                     OK v
```



Zyxel
```
snmpwalk -v 2c -c QffPDLvvz 192.168.118.202 SNMPv2-MIB::sysDescr.0
SNMPv2-MIB::sysDescr.0 = STRING: MES-3528
```
```
snmpwalk -v 2c -c SFgJZAc2 10.148.2.111 SNMPv2-MIB::sysDescr.0
SNMPv2-MIB::sysDescr.0 = STRING: MES3500-24
```
```
snmpwalk -v 2c -c QffPDLvvz 10.148.0.35 SNMPv2-MIB::sysDescr.0
SNMPv2-MIB::sysDescr.0 = STRING: XGS-4728F
```

```
    - name: Configure DES-1210
      script: ansible_tel/dlink-telnet-ansible.py {{ inventory_hostname }} ansible_tel/template.txt
      delegate_to: 127.0.0.1
      when: ansible_sysdescr == "DES-1210-28/ME/B2"

      
        tasks:

    - name: Get snmp facts
      snmp_facts:
        host: '{{ inventory_hostname }}'
        version: v2c
        community: SFgJZAc2
      register: snmp_facts_result

    - name: Configure DES-3200-28
      script: ansible_tel/dlink-telnet-ansible.py {{ inventory_hostname }} ansible_tel/template.txt
      delegate_to: 127.0.0.1
      when: "'DES-3200-28' in ansible_sysdescr"
      
    - name: Configure DES-3200-10
      script: ansible_tel/dlink-telnet-ansible.py {{ inventory_hostname }} ansible_tel/template.txt
      delegate_to: 127.0.0.1
      when: "'DES-3200-10' in ansible_sysdescr"
      
    - name: Configure DES-3526
      script: ansible_tel/dlink-telnet-ansible.py {{ inventory_hostname }} ansible_tel/template.txt
      delegate_to: 127.0.0.1
      when: "'DES-3526' in ansible_sysdescr"
      
    - name: Configure DES-3028
      script: ansible_tel/dlink-telnet-ansible.py {{ inventory_hostname }} ansible_tel/template.txt
      delegate_to: 127.0.0.1
      when: "'DES-3028' in ansible_sysdescr"
      
   -  name: Configure DES-3026
      script: ansible_tel/dlink-telnet-ansible.py {{ inventory_hostname }} ansible_tel/template.txt
      delegate_to: 127.0.0.1
      when: "'DES-3026' in ansible_sysdescr"
      
    -  name: Configure DGS-3627G
      script: ansible_tel/dlink-telnet-ansible.py {{ inventory_hostname }} ansible_tel/template.txt
      delegate_to: 127.0.0.1
      when: "'DGS-3627G' in ansible_sysdescr"
  
   -  name: Configure DES-3226S
      script: ansible_tel/dlink-telnet-ansible.py {{ inventory_hostname }} ansible_tel/template.txt
      delegate_to: 127.0.0.1
      when: "'DES-3226S' in ansible_sysdescr"
```      
      
      
      [https://docs.ansible.com/ansible/playbooks_tests.html](https://docs.ansible.com/ansible/playbooks_tests.html)
      [http://docs.ansible.com/ansible/playbooks_conditionals.html](http://docs.ansible.com/ansible/playbooks_conditionals.html)
      [http://docs.ansible.com/ansible/playbooks_loops.html](http://docs.ansible.com/ansible/playbooks_loops.html)
      [http://docs.ansible.com/ansible/playbooks_filters.html#combining-hashes-dictionaries](http://docs.ansible.com/ansible/playbooks_filters.html#combining-hashes-dictionaries)
      
```
config sntp primary {{ gateway }} secondary {{ ntp_server }} poll-interval 720
enable sntp
config time_zone operator + hour 3 minute 0
config dst disable
```    

      
      Установил дополнительный модуль, скачал и распаковал в library (папка с дополнительными модулями)
      В  ansible.cfg указала library = library/

      
      
      NTP


124 - 3200 1210 Mes
123 - 3200 1210 Mes
122 - 3200 1210 Mes
120 - 3200 1210 Mes
118 - 3200 3526 - 3028 - 1210 Mes
117  3200 3526 - 3028 - 1210 Mes
172 - 3200 1210 Mes

81.20.196.53

3200
```
enable sntp
config time_zone operator + hour 3 min 0
config sntp primary {{ ntp1 }} secondary {{ gateway }} poll-interval 720      
config dst disable
```

1210
```
config sntp primary 192.168.124.1 secondary 81.20.192.19 poll-interval 720
enable sntp
config time_zone operator + hour 3 minute 0
config dst disable
```

Неплохо. Но стоит добавить вот еще что.

1. Парамеры командной строки, которые 100% необходимы для выполнения сценария, можно поместить в файл ansible.cfg (который должен лежать в директории, откуда запускается сценарий). И никаких больше --ask-sudo-pass --ask-vault-password при каждом запуске.

Пример ansible.cfg:

[ssh_connection]
ssh_args = -o ForwardAgent=yes

[privilege_escalation]
become_ask_pass=yes




CLASS5 - NAPALM-Ansible

    What is NAPALM?
    NAPALM for Information Gathering
    NAPALM Merge Operations
    NAPALM Replace Operations

