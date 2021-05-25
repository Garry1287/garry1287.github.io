---
layout: post
title:  "aaa-radius-cisco"
date:   2011-03-20 08:18:23 +0300
categories: aaa-radius-cisco
tags: cisco
---

# aaa-radius-cisco
aaa authentication login default group radius local
aaa authentication enable default group radius enable
aaa authorization exec default group radius local 



Зелёная самая тупая


line con 0
 password 7 131F031E021C
 login
line vty 0 4
 access-class 1 in
 password 7 131F031E021C
 login
 transport input lat pad udptn telnet rlogin ssh acercon
line vty 5 1441
 password 7 131F031E021C
 login
!


если добавить При выполнении команды “login local” устройство, установив соединение, будет требовать ввести логин и пароль для входа.

то тогда надо заводить локальных зверей






scheduler allocate 4000 200



 R1(config)#login delay 5
R1(config)#login block-for 60 attempts 3 within 30

radius-server host 10.192.10.190 auth-port 2012 acct-port 2013 


[https://www.cisco.com/c/ru_ru/support/docs/security-vpn/terminal-access-controller-access-control-system-tacacs-/10384-security.html](https://www.cisco.com/c/ru_ru/support/docs/security-vpn/terminal-access-controller-access-control-system-tacacs-/10384-security.html)


10.192.10.186
10.192.10.194

10.192.10.54


10.192.10.62
10.192.10.70

10.192.10.126
10.192.10.74

10.192.11.26
10.192.11.58
10.192.11.86
10.192.11.94

10.60.246.11
10.74.0.254
10.74.254.2
10.74.254.3
10.74.254.5
10.74.254.6
