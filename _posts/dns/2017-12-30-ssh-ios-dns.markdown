---
layout: post
title:  "ssh-ios-dns"
date:   2017-12-30 12:21:37 +0300
categories: dns
tags: dns
---

# ssh-ios-dns
ip domain lookup - включает трансляцию имён в ip адреса основанную на dns. Этот параметр включен по умолчанию.

ip name-server - этот параметр задаёт адрес одного или нескольких серверов имён (dns).

ip domain name - задаёт имя домена по умолчанию для пользователей Cisco IOS software для разрешения "неопознаных" доменных имён (имена без десятичных доменных имён.

можно указать список доменов 


ip dns server - включаем собственно форвард на циске 






! включаем внутренний DNS сервер (ciso выступает как dns)
ip dns server   

ip subnet-zero
ip domain-name sc.int
ip name-server 192.168.121.1
ip name-server 81.20.192.16
ip name-server 81.20.192.17




! включаем шифрование паролей
service password-encryption
! используем новую модель ААА и локальную базу пользователей
aaa new-model
aaa authentication login default local
! заводим пользователя с максимальными правами
username admin privilege 15 secret PASSWORD


! даем имя роутеру
hostname <...>
ip domain-name router.domain
! генерируем ключик для SSH
crypto key generate rsa modulus 1024
! тюнингуем SSH
ip ssh time-out 60
ip ssh authentication-retries 2
ip ssh version 2
! и разрешаем его на удаленной консоли
line vty 0 4
 transport input telnet ssh
 privilege level 15



Архивирование конфигов
! включаем архивирование всех изменений конфига, скрывая пароли в логах
archive
 log config
  logging enable
  hidekeys
! историю изменения конфига можно посмотреть командой
show archive log config all



Настройка Internet и Firewall


! настраиваем фильтр входящего трафика (по умолчанию все запрещено)
ip access-list extended FIREWALL
 permit tcp any any eq 22

! включаем инспектирование трафика между локальной сетью и Интернетом
ip inspect name INSPECT_OUT dns
ip inspect name INSPECT_OUT icmp
ip inspect name INSPECT_OUT ntp
ip inspect name INSPECT_OUT tcp router-traffic
ip inspect name INSPECT_OUT udp router-traffic
ip inspect name INSPECT_OUT icmp router-traffic

! настраиваем порт в Интернет и вешаем на него некоторую защиту
interface FastEthernet0/0
 description === Internet ===
 ip address ???.???.???.??? 255.255.255.???
 ip virtual-reassembly
 ip verify unicast reverse-path
 no ip redirects
 no ip directed-broadcast
 no ip proxy-arp
 no cdp enable
 ip inspect INSPECT_OUT out
 ip access-group FIREWALL in






Я бы ещё добавил несколько хинтов:
изредка бывает, что ключ… слетает! Проверить наличие своего ключа можно командой
sh cry key mypubkey rsa


Иногда стоит привязка имени ключа к его «телу». При перевыработке ключа имя может остаться (например, defaultkey.domain.ru), а собственно небо поменякется.
Ключи можно вырабатывать не только дефолтовые, но и задавать им метки, чтобы впоследствии вырабатывать по ним сертификаты, например.
Чтобы убить ключи надо дать команду
cry key zeroize rsa [название ключа]
и потом тоже сохраниться 


1. cisco> enable
2. cisco# clock set 17:10:00 28 Aug 2009
3. cisco# configure terminal
4. cisco(config)# ip domain name test.dom
5. cisco(config)# crypto key generate rsa
6. cisco(config)# service password-encryption
7. cisco(config)# username user privilege 15 password 7 Pa$$w0rd
8. cisco(config)# aaa new-model
9. cisco(config)# line vty 0 4
10. cisco(config-line)# transport input ssh
11. cisco(config-line)# logging synchronous
12. cisco(config-line)# exec-timeout 60 0
13. cisco(config-line)# exit
14. cisco(config)# exit
15. cisco# copy running-config startup-config



[http://www.cisco.com/cisco/web/support/RU/9/92/92052_ssh.html](http://www.cisco.com/cisco/web/support/RU/9/92/92052_ssh.html)


Отключение ненужных сервисов

no service tcp-small-servers
no service udp-small-servers
no service finger
no service config
no service pad
no ip finger
no ip source-route
no ip http server
no ip http secure-server
no ip bootp server
