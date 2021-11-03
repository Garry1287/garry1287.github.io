---
layout: post
title:  "Полезные ссылки - ansible"
date:   2017-01-06 00:34:31 +0300
categories: devops
tags: devops ansible
---

# Полезные ссылки - ansible

[https://habrahabr.ru/post/304732/](https://habrahabr.ru/post/304732/)
[https://natenka.gitbooks.io/pyneng/content/book/12_ssh_telnet/2_telnetlib.html](https://natenka.gitbooks.io/pyneng/content/book/12_ssh_telnet/2_telnetlib.html)
[https://natenka.gitbooks.io/ansible-dlya-setevih-inzhenerov/content/book/1_ansible_basics/configuration.html](https://natenka.gitbooks.io/ansible-dlya-setevih-inzhenerov/content/book/1_ansible_basics/configuration.html)
[https://github.com/ansible/ansible/blob/devel/lib/ansible/modules/network/ios/ios_config.py](https://github.com/ansible/ansible/blob/devel/lib/ansible/modules/network/ios/ios_config.py)
[https://natenka.gitbooks.io/ansible-dlya-setevih-inzhenerov/content/book/1_ansible_basics/ad-hoc.html](https://natenka.gitbooks.io/ansible-dlya-setevih-inzhenerov/content/book/1_ansible_basics/ad-hoc.html)
[https://natenka.gitbooks.io/pyneng/content/book/12_ssh_telnet/5a_threading.html](https://natenka.gitbooks.io/pyneng/content/book/12_ssh_telnet/5a_threading.html)
[http://packetpushers.net/ansible-cisco-snmp/](http://packetpushers.net/ansible-cisco-snmp/)
[http://jedelman.com/home/automating-cisco-nexus-switches-with-ansible/](http://jedelman.com/home/automating-cisco-nexus-switches-with-ansible/)
[http://stackoverflow.com/questions/17662391/read-file-into-string-and-do-a-loop-in-expect-script](http://stackoverflow.com/questions/17662391/read-file-into-string-and-do-a-loop-in-expect-script)
[https://netgoliath.wordpress.com/2016/06/14/easy-network-automation-with-ansible-expect/](https://netgoliath.wordpress.com/2016/06/14/easy-network-automation-with-ansible-expect/)
[https://www.packetgeek.net/2015/08/using-ansible-to-push-cisco-ios-configurations/](https://www.packetgeek.net/2015/08/using-ansible-to-push-cisco-ios-configurations/)


[https://habrahabr.ru/company/infobox/blog/252239/](https://habrahabr.ru/company/infobox/blog/252239/)
[https://github.com/netopsio/netlib/blob/master/README.md](https://github.com/netopsio/netlib/blob/master/README.md)

[https://github.com/Mierdin/ansible-switchconfig](https://github.com/Mierdin/ansible-switchconfig)


[http://yaml-online-parser.appspot.com/](http://yaml-online-parser.appspot.com/)

[https://www.linuxspace.org/archives/14047](https://www.linuxspace.org/archives/14047)
[https://habrahabr.ru/company/infobox/blog/252001/](https://habrahabr.ru/company/infobox/blog/252001/)
[https://github.com/jtdub/net-ansible](https://github.com/jtdub/net-ansible)

[https://github.com/netopsio/ansible-dynamic-inventory](https://github.com/netopsio/ansible-dynamic-inventory)



[https://serversforhackers.com/running-ansible-2-programmatically](https://serversforhackers.com/running-ansible-2-programmatically)

[http://patg.net/ansible](http://patg.net/ansible),comware,switches/2014/10/16/ansible-comware/


                                                       
SUMMARY

Expect module should have an expected_results option that would have the same structure of the responses options ( dict of lists). Every response to a pattern would have a correspondent expected_result, like in the example below:
```
- name: "Expected results example"
  delegate_to: localhost
  register: result
  expect:
    command: "/usr/bin/telnet {{ inventory_hostname }}"
    echo: true
    expected_results:
      '#:'
        - 'command1 success message pattern'
        - 'command2 success message pattern'
        - 'command3 success message pattern'
    responses:
      'username:':
        - 'myuser'
      'password:':
        - 'mypass'
      '#':
        - 'command1'
        - 'command2'
        - 'command3'
 ```       
[https://habrahabr.ru/post/328486/](https://habrahabr.ru/post/328486/)
[http://stackoverflow.com/questions/38393343/how-to-use-ansible-expect-module-for-multiple-different-responses](http://stackoverflow.com/questions/38393343/how-to-use-ansible-expect-module-for-multiple-different-responses)
[http://docs.ansible.com/ansible/expect_module.html](http://docs.ansible.com/ansible/expect_module.html)
[https://github.com/ansible/ansible-modules-extras/issues/3254](https://github.com/ansible/ansible-modules-extras/issues/3254)
        
        
        
        [https://pythonworld.ru/osnovy/pep-8-rukovodstvo-po-napisaniyu-koda-na-python.html](https://pythonworld.ru/osnovy/pep-8-rukovodstvo-po-napisaniyu-koda-na-python.html)
[http://defpython.ru/pep8](http://defpython.ru/pep8)



```
SNMPv2-MIB::sysDescr.0 = STRING: DES-3200-28/C1 Fast Ethernet Switch
when: ansible_sysdescr == "D-Link DES-3200-28 Fast Ethernet Switch"
SNMPv2-MIB::sysDescr.0 = STRING: DES-3526 Fast-Ethernet Switch
```


В коментах полно о разделениее production/dev/
[https://habrahabr.ru/post/304732/](https://habrahabr.ru/post/304732/)
