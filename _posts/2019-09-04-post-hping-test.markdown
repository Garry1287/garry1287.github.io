---
layout: post
title:  "Тестирование потерь на каналах c помощью hping3"
date:   2019-09-04 14:30:15 +0300
categories: networking
---


# Алгоритм тестирования #

  
 Методика тестирования.
 ````
 hping3 -q --udp -p 10500 -c 100000 -d 800 -i u200 --tos a0 10.192.10.14
 hping3 -q --udp -p 10500 -c 100000 -d 800 -i u200 --tos a0 10.192.10.6
 ```
 
### 1.С сервера запускаем hping на какой-либо узел сети. 
  Чтобы зафлудить канал необходимо указывать как можно меньше интервал -i u100 (пинг каждый 100 милисекунд) и количество пакетов -с 10000, размер тоже влияет -d 800
  
### 2.На роутере делаем access-list, который будет ловить hping

```
ip access-list extended catch-udp
 permit udp host 10.192.11.22 host 10.192.10.6
 permit udp host 10.192.11.45 host 10.192.10.6
 permit icmp any any
 permit udp any any
ip access-list extended catch-udp-186
 permit udp host 10.192.11.22 host 10.192.10.186
 permit udp host 10.192.11.45 host 10.192.10.186
 permit icmp any any
 permit ip any any
ip access-list extended catch-udp-crystall-bee
 permit udp host 10.192.11.45 host 10.192.10.45
 permit udp host 10.192.11.45 host 10.192.10.46
 permit udp host 10.192.11.45 host 10.192.10.5
 permit udp host 10.192.11.45 host 10.192.10.6
 permit icmp any any
 permit udp any any
ip access-list extended catch-udp-emerald-zab
 permit udp host 10.192.11.61 host 10.192.11.22 precedence critical
 permit udp host 10.192.11.61 host 10.192.11.22
 permit icmp any any
 permit udp any any
 permit ip any any
ip access-list extended catch-udp-ruby-zab
 permit udp host 10.192.11.53 host 10.192.11.22 precedence critical
 permit udp host 10.192.11.53 host 10.192.11.22
 permit icmp any any
 permit udp any any
 permit ip any any
ip access-list extended catch-udp-zab-emerald
 permit udp host 10.192.11.22 host 10.192.11.61 precedence critical
 permit udp host 10.192.11.22 host 10.192.11.61
 permit icmp any any
 permit udp any any
 permit ip any any
ip access-list extended catch-udp-zab-ruby
 permit udp host 10.192.11.22 host 10.192.10.190
 permit udp host 10.192.11.22 host 10.192.11.53
 permit icmp any any
 permit udp any any
```
```
 На интерфейсе
 interface GigabitEthernet0/0.200
 description #IPVPN NLMK-CE0 newport
 bandwidth 204800
 encapsulation dot1Q 200
 ip vrf forwarding nlmk-vpn
 ip address 10.192.10.185 255.255.255.252
 ip access-group catch-udp-186 out
 ip flow egress
 no cdp enable
 service-policy output PLATINUM-ETH-200MB
```
 
### 3.Смотрим на потери в counts access list
Смотрим на загрузку канала. При правильно подобранных параметрах в пункте 1 должен быть 100% загружен или близко к этому. Необходимо экспериментально пробывать
с tos и без tos
    
Эта методика дает понимания о потерях на канале
    
    
# Просмотр статистики на сервере

На ruby(10.192.11.53) делаем правило в firewall
```
iptables -A INPUT -s 10.192.11.22/32 -p udp -m udp --dport 10500 -j ACCEPT
```
10.192.11.22 - это Zabbix

Смотреть статистику 
```
iptables -L -v
```
С zabbix пускаем hping3
```
hping3 --udp -p 10500 -c 100 10.192.11.53
```


Смотрим статистику
```
Chain INPUT (policy ACCEPT 921 packets, 99507 bytes)
 pkts bytes target     prot opt in     out     source               destination        
  100  2800 LOG        udp  --  any    any     10.192.11.22         anywhere             udp dpt:hip-nat-t LOG level warning prefix "From Zabbix hping3"
  100  2800 ACCEPT     udp  --  any    any     10.192.11.22         anywhere             udp dpt:hip-nat-t
```  

  
 - [https://neelpathak.wordpress.com/2013/11/06/network-scanning-with-hping3/](https://neelpathak.wordpress.com/2013/11/06/network-scanning-with-hping3/)
 - [https://www.blackmoreops.com/2015/04/21/denial-of-service-attack-dos-using-hping3-with-spoofed-ip-in-kali-linux/](https://www.blackmoreops.com/2015/04/21/denial-of-service-attack-dos-using-hping3-with-spoofed-ip-in-kali-linux/)
 - [https://www.darkmoreops.com/2014/08/21/dos-using-hping3-spoofed-ip-kali-linux/](https://www.darkmoreops.com/2014/08/21/dos-using-hping3-spoofed-ip-kali-linux/)
 - [https://allwebstuff.info/hping3-%D1%84%D0%BB%D1%83%D0%B4%D0%B8%D0%BC-%D0%BF%D0%BE-%D1%81%D0%B2%D0%BE%D0%B5%D0%BC%D1%83-%D1%81%D0%B0%D0%B9%D1%82%D1%83/](https://allwebstuff.info/hping3-%D1%84%D0%BB%D1%83%D0%B4%D0%B8%D0%BC-%D0%BF%D0%BE-%D1%81%D0%B2%D0%BE%D0%B5%D0%BC%D1%83-%D1%81%D0%B0%D0%B9%D1%82%D1%83/)
 - [https://tools.kali.org/information-gathering/hping3](https://tools.kali.org/information-gathering/hping3)
 - [https://habrahabr.ru/post/106752/](https://habrahabr.ru/post/106752/)
 - [https://codeby.net/stress-test-seti-dos-s-ispolzovaniem-hping3-i-spufingom-ip-v-kali-linux/](https://codeby.net/stress-test-seti-dos-s-ispolzovaniem-hping3-i-spufingom-ip-v-kali-linux/)
 - [https://nmap.org/book/idlescan.html](https://nmap.org/book/idlescan.html)
 - [http://wiki.hping.org/33](http://wiki.hping.org/33)
 - [http://wiki.hping.org/94](http://wiki.hping.org/94)