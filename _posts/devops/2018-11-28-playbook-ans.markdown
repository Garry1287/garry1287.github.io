---
layout: post
title:  "Примеры playbook для ansible"
date:   2018-11-28 12:48:45 +0300
categories: devops
tags: devops ansible
---

# Примеры playbook для ansible

```
---
- hosts: netdevices
  connection: local
  gather_facts: no
  
  tasks:
  - name: Create SNMP Configuration
    template:
      src=templates/snmp-contact.j2
      dest=input/{{ hostname }}.conf
    delegate_to: 127.0.0.1

  - name: Configure SNMP Contact on network device
    command: scripts/netsible.py {{ hostname }} input/{{ hostname }}.conf 
    delegate_to: 127.0.0.1
```


snmp-contact.j2. Here is what the template looks like:
```
config t
snmp-server contact {{ contact_name }}
end
copy run start
```


```
#!/usr/bin/env python

from netlib.netlib.user_creds import simple_yaml
from netlib.netlib.conn_type import SSH

from os.path import expanduser
import sys

creds = simple_yaml()
base_dir = expanduser("~/net-ansible")
hostname = sys.argv[1]
command_file = sys.argv[2]
ssh = SSH(hostname, creds['username'], creds['password'])

ssh.connect()
ssh.set_enable(creds['enable'])

with open(base_dir + "/" + command_file) as f:
    for line in f.readlines():
        line = line.strip()
        ssh.command(line)
f.close()

ssh.close()
```

[https://www.packetgeek.net/2015/08/using-ansible-to-push-cisco-ios-configurations/](https://www.packetgeek.net/2015/08/using-ansible-to-push-cisco-ios-configurations/)



The hostname variable is called from host_vars. Here is the host_var for a test device, called core1a:

hostname: core1a

The contact_name variable is called from group_vars/all. Here is what my group_var/all looks like:




```
---
- name: Fetching Juniper Commands
  hosts: target_hosts
  gather_facts: no
  serial: 100%
 
  tasks:
  - set_fact:
      script_dir: "scripts"
  - name: Executing the expect script
    script: ./{{ script_dir }}/get_commands.expect {{ ansible_ssh_host }} {{ commands }} {{ inventory_hostname }} {{ log_dir }}
contact_name: netdude@packetgeek.net
```