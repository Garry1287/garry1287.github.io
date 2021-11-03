---
layout: post
title:  "Ansible-vault"
date:   2017-07-03 12:42:08 +0400
categories: devops
tags: devops ansible
---

# ansible-vault
ansible-vault
[https://stackoverflow.com/questions/30209062/ansible-how-to-encrypt-some-variables-in-an-inventory-file-in-a-separate-vault](https://stackoverflow.com/questions/30209062/ansible-how-to-encrypt-some-variables-in-an-inventory-file-in-a-separate-vault)
[http://docs.ansible.com/ansible/playbooks_vault.html](http://docs.ansible.com/ansible/playbooks_vault.html)

sudo ansible-vault encrypt_string "OurPassword" 
New Vault password: 
Confirm New Vault password: 

Затем вписал его в group_vars/all.yml
---

cli:
  host: "{{ inventory_hostname }}"
  username: "AnsVpnUser"
  password: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          38306263303262656265396339306663393232366431623839646330653864386164356464623339
          3263383566633236646638326338336330313362306235370a373562326436333130613730666331
          36613333396637303036303236616230313933626138303437323533396161623139306137313964
          6566653137353533310a636661626663393439656236663230366430646139626563656562353436
          3539
  transport: cli
  authorize: yes

snmp_community: Sh73ah91Kld


А был он вот таким

---

cli:
  host: "{{ inventory_hostname }}"
  username: "AnsVpnUser"
  password: "OurPassword"
  transport: cli
  authorize: yes

snmp_community: Sh73ah91Kld


Теперь запускаем
sudo ansible-playbook snmp_ro_config_verona.yml --ask-vault-pass





MesDesSwUser
username: "AnsPhysUser"
password: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          62373265653535626162333130643536386436366335396461663437393564393763636132336663
          6264326466663138616633663436613939303931363265620a613938353865326631393666643534
          61633630303832353765363166613539346439623564656663313466363265383831326438653535
          3932643032646162380a306163333062303532376339343033653335383231386232643363626236
          3364






```
ansible-vault create credentials.yml
ansible-vault encrypt credentials.yml
ansible-vault view credentials.yml
ansible-vault edit credentials.yml
ansible-vault decrypt credentials.yml
```
Запуск и спрашивать пароль
`ansible-playbook myplaybook.yml --ask-vault-pass`

Запуск без пароля с использованием файла с паролем
`ansible-playbook myplaybook.yml --vault-password-file my_vault_password.py`

Файл с паролем - обычный текстовый файл 

```
garry@home-pc:~/rt-work/test_zab_role$ cat vault.key
Nexponka
```



[https://hamsterden.ru/ansible-vault-playbooks/](https://hamsterden.ru/ansible-vault-playbooks/)

[💽 Шпаргалка Ansible Vault / Справочное руководство |](https://itsecforu.ru/2019/08/26/%F0%9F%92%BD-%D1%88%D0%BF%D0%B0%D1%80%D0%B3%D0%B0%D0%BB%D0%BA%D0%B0-ansible-vault-%D1%81%D0%BF%D1%80%D0%B0%D0%B2%D0%BE%D1%87%D0%BD%D0%BE%D0%B5-%D1%80%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82/)

https://hamsterden.ru/ansible-vault-playbooks/

[How to create a vault file with Ansible | Opensource.com](https://opensource.com/article/16/12/devops-security-ansible-vault)

[https://ittx.ru/note/2021/02/25/ansible-vault/](https://ittx.ru/note/2021/02/25/ansible-vault/)

[Access denied | www.golinuxcloud.com used Cloudflare to restrict access](https://www.golinuxcloud.com/ansible-vault-example-encrypt-string-playbook/)

[https://rtfm.co.ua/ansible-ispolzovanie-vault-zashifrovannogo-xranilishha/](https://rtfm.co.ua/ansible-ispolzovanie-vault-zashifrovannogo-xranilishha/)

[Encrypting content with Ansible Vault — Ansible Documentation](https://docs.ansible.com/ansible/latest/user_guide/vault.html)