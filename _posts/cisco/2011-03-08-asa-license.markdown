---
layout: post
title:  "Лицензирование Asa cisco"
date:   2011-03-08 11:09:29 +0300
categories: cisco
tags: cisco asa
---

# Лицензирование Asa cisco
```
UC-NLMK-URAL-ASA# show activation-key
Serial Number:  JMX1628X0P9
Running Activation Key: 0x6e1ef96d 0x681e793f 0x9c903908 0x8f64783c 0x061511b9 

Licensed features for this platform:
Maximum Physical Interfaces    : Unlimited 
Maximum VLANs                  : 50        
Inside Hosts                   : Unlimited 
Failover                       : Disabled
VPN-DES                        : Enabled   
VPN-3DES-AES                   : Disabled  
Security Contexts              : 0         
GTP/GPRS                       : Disabled  
SSL VPN Peers                  : 2         
Total VPN Peers                : 250       
Shared License                 : Disabled
AnyConnect for Mobile          : Disabled  
AnyConnect for Cisco VPN Phone : Disabled  
AnyConnect Essentials          : Disabled  
Advanced Endpoint Assessment   : Disabled  
UC Phone Proxy Sessions        : 2         
Total UC Proxy Sessions        : 2         
Botnet Traffic Filter          : Disabled  

This platform has a Base license.

The flash activation key is the SAME as the running key.
```

## Поддержка 3DES/AES на Cisco ASA sec K8
Итак предположим вам досталась Cisco ASA 5500 серии с лицензией K8. Вы с густью обнаружили что она не поддерживает ни 3DES ни AES... печально... Но не повод расстраиваться. Cisco не берет деньги за апгрейд на лицензию K9 - это бесплатная процедура.
Что понадобиться - гостевая учетная запись на сайте Cisco.com (завести его можно за 10 минут), и терминальное подключение к ASA (telnet, ssh, console).
Заходим на cisco ASA и вводим show version
Ищем серийный номер.
Заходим сюда:

[https://tools.cisco.com/SWIFT/Licensing/PrivateRegistrationServlet?FormId=139](https://tools.cisco.com/SWIFT/Licensing/PrivateRegistrationServlet?FormId=139)

[https://tools.cisco.com/SWIFT/LicensingUI/loadDemoLicensee?FormId=139](https://tools.cisco.com/SWIFT/LicensingUI/loadDemoLicensee?FormId=139)

вводим серийный номер и заполняем поля.
По e-mail получаем ключ.
В терминале cisco ASA вводим:

```
conf t
activation-key 4e3ec458 f483d227 b48285a8 9bc444d4 8c081fa5
exit
wr
reload
```

Потом
```
ssl encryption rc4-sha1 aes128-sha1 aes256-sha1 3des-sha1

  domain name {имя}
  hostname {имя}
  crypto key generate rsa
  ! Включаем сам https сервер, по умолчанию часто включен. При включении 
  ! генерирует самоподписанный сертификат.
  http server enable 
  ! Разрешаем https
  http 192.168.1.128 255.255.255.128 inside
  http 1.2.3.4 255.255.255.255 outside
```


```
access-list 55 permit 10.192.10.252
access-list 55 permit 10.192.10.253                                                                                                                                                                                                                      
access-list 55 deny any                                                                                                                    
snmp-server tftp-server-list 55 
```


PAK приходит в письме
PID и UID получаем командой 
show license udi                                                                                                                                   
Device#   PID                   SN              UDI                                                                                                          
-----------------------------------------------------------------------------                                                                                
*0        CISCO2911/K9          JTV1635T41W     CISCO2911/K9:JTV1635T41W                                                                                     
            

Вводим на сайте
[https://tools.cisco.com/SWIFT/LicensingUI/bulkPakHome](https://tools.cisco.com/SWIFT/LicensingUI/bulkPakHome)                                                                             

Получаем по почте или скачиваем, а потом
```
copy tftp flash
license install flash:uck9_license.lic
```


[http://www.anticisco.ru/blogs/?p=722](http://www.anticisco.ru/blogs/?p=722)

[http://habrahabr.ru/post/116722/](http://habrahabr.ru/post/116722/)

[http://www.cisco.com/en/US/docs/routers/access/sw_activation/SA_on_ISR.html#wp1057952](http://www.cisco.com/en/US/docs/routers/access/sw_activation/SA_on_ISR.html#wp1057952)

[http://www.anticisco.ru/forum/viewtopic.php?p=12989](http://www.anticisco.ru/forum/viewtopic.php?p=12989)

[http://silver-golem.livejournal.com/390651.html](http://silver-golem.livejournal.com/390651.html)

[http://www.cisco.com/en/US/prod/collateral/iosswrel/ps8802/ps10587/ps10591/ps10621/product_bulletin_c25-561938.html](http://www.cisco.com/en/US/prod/collateral/iosswrel/ps8802/ps10587/ps10591/ps10621/product_bulletin_c25-561938.html)

[http://www.powerc.ru/blog-conf-t/podderzka3desaesnaciscoasaseck8](http://www.powerc.ru/blog-conf-t/podderzka3desaesnaciscoasaseck8)

[http://sr-maks.livejournal.com/19107.html](http://sr-maks.livejournal.com/19107.html)

[http://www.cisco.com/c/en/us/td/docs/ios-xml/ios/csa/configuration/15-mt/csa-15-mt-book.html](http://www.cisco.com/c/en/us/td/docs/ios-xml/ios/csa/configuration/15-mt/csa-15-mt-book.html)


NPE (No Payload Encryption) - ios без шифрования, ограничение ФСБ


В 12 релизе были вобще-то еще большие градации на ранних релизах для старых железок типа 1700/2600/3600 
и общее кол-во при попкупе было более 20 штук. Достаточно посмотреть таблицу№6 в ссылке

Не удивительно что прежде чем внедрять активацию они 2 раза пересмотрели кол-во лицензии и уменьшили их кол-во и цену.
 Сейчас в этом плане они адекватнее стали. Доступ к L2base прошивкам для свичей к примеру бесплатен.






Для Вены получил письмо от немцев, пересланное от cisco со ссылкой на доступ к [https://edelivery.cisco.com/esd/downloadCart.do?view&backLink=mailBasedAccessCart](https://edelivery.cisco.com/esd/downloadCart.do?view&backLink=mailBasedAccessCart)

откуда я скачал лицензии с PAK, которые уже нужно зарегистрировать на [https://tools.cisco.com/SWIFT/LicensingUI/loadDemoLicensee?FormId=139](https://tools.cisco.com/SWIFT/LicensingUI/loadDemoLicensee?FormId=139)
откуда уже качается лицензии для активации на ASA




Лицензирование IOS NG2 - новые модели.

[http://www.cisco.com/c/en/us/products/collateral/cloud-systems-management/software-activation-on-integrated-services-routers-isr/white_paper_c11_556985.html](http://www.cisco.com/c/en/us/products/collateral/cloud-systems-management/software-activation-on-integrated-services-routers-isr/white_paper_c11_556985.html)

[http://nettips.ru/article/cisco_2911_change_ios.html](http://nettips.ru/article/cisco_2911_change_ios.html)

[http://telecombook.ru/archive/network/cisco/other/92-cisco-ios-15](http://telecombook.ru/archive/network/cisco/other/92-cisco-ios-15)

[http://www.anticisco.ru/blogs/2011/04/ios-%D0%B4%D0%BB%D1%8F-isr-%D0%B2%D0%B5%D1%80%D1%81%D0%B8%D0%B8-%D0%B2%D0%BE%D0%B7%D0%BC%D0%BE%D0%B6%D0%BD%D0%BE%D1%81%D1%82%D0%B8-%D0%BB%D0%B8%D1%86%D0%B5%D0%BD%D0%B7%D0%B8%D0%B8/](http://www.anticisco.ru/blogs/2011/04/ios-%D0%B4%D0%BB%D1%8F-isr-%D0%B2%D0%B5%D1%80%D1%81%D0%B8%D0%B8-%D0%B2%D0%BE%D0%B7%D0%BC%D0%BE%D0%B6%D0%BD%D0%BE%D1%81%D1%82%D0%B8-%D0%BB%D0%B8%D1%86%D0%B5%D0%BD%D0%B7%D0%B8%D0%B8/)

[http://www.anticisco.ru/blogs/2011/04/ios-%D0%B4%D0%BB%D1%8F-isr-%D0%B2%D0%B5%D1%80%D1%81%D0%B8%D0%B8-%D0%B2%D0%BE%D0%B7%D0%BC%D0%BE%D0%B6%D0%BD%D0%BE%D1%81%D1%82%D0%B8-%D0%BB%D0%B8%D1%86%D0%B5%D0%BD%D0%B7%D0%B8%D0%B8/](http://www.anticisco.ru/blogs/2011/04/ios-%D0%B4%D0%BB%D1%8F-isr-%D0%B2%D0%B5%D1%80%D1%81%D0%B8%D0%B8-%D0%B2%D0%BE%D0%B7%D0%BC%D0%BE%D0%B6%D0%BD%D0%BE%D1%81%D1%82%D0%B8-%D0%BB%D0%B8%D1%86%D0%B5%D0%BD%D0%B7%D0%B8%D0%B8/)

[http://www.cisco.com/c/en/us/products/collateral/cloud-systems-management/software-activation-on-integrated-services-routers-isr/white_paper_c11_556985.html](http://www.cisco.com/c/en/us/products/collateral/cloud-systems-management/software-activation-on-integrated-services-routers-isr/white_paper_c11_556985.html)

[http://www.anticisco.ru/blogs/2011/04/ios-%D0%B4%D0%BB%D1%8F-isr-%D0%B2%D0%B5%D1%80%D1%81%D0%B8%D0%B8-%D0%B2%D0%BE%D0%B7%D0%BC%D0%BE%D0%B6%D0%BD%D0%BE%D1%81%D1%82%D0%B8-%D0%BB%D0%B8%D1%86%D0%B5%D0%BD%D0%B7%D0%B8%D0%B8/](http://www.anticisco.ru/blogs/2011/04/ios-%D0%B4%D0%BB%D1%8F-isr-%D0%B2%D0%B5%D1%80%D1%81%D0%B8%D0%B8-%D0%B2%D0%BE%D0%B7%D0%BC%D0%BE%D0%B6%D0%BD%D0%BE%D1%81%D1%82%D0%B8-%D0%BB%D0%B8%D1%86%D0%B5%D0%BD%D0%B7%D0%B8%D0%B8/)



## Cisco Feature Navigator
[http://tools.cisco.com/ITDIT/CFN/](http://tools.cisco.com/ITDIT/CFN/)

[https://software.cisco.com/download/release.html?mdfid=284367038&softwareid=280805680&os=&release=15.6.1T0a&relind=AVAILABLE&rellifecycle=&reltype=latest&i=](https://software.cisco.com/download/release.html?mdfid=284367038&softwareid=280805680&os=&release=15.6.1T0a&relind=AVAILABLE&rellifecycle=&reltype=latest&i=)

[http://www.anticisco.ru/index.php?sn=glos](http://www.anticisco.ru/index.php?sn=glos)

[https://software.cisco.com/selection/research.html#?mode=&tid=&pid=284367038&sid=&cr=&crt=&hid=&fid=](https://software.cisco.com/selection/research.html#?mode=&tid=&pid=284367038&sid=&cr=&crt=&hid=&fid=)

[http://www.cisco.com/c/en/us/support/routers/800-series-routers/products-device-support-tables-list.html](http://www.cisco.com/c/en/us/support/routers/800-series-routers/products-device-support-tables-list.html)

[https://software.cisco.com/download/release.html?mdfid=284367038&flowid=48154&softwareid=280805680&release=15.3.3M6&relind=AVAILABLE&rellifecycle=MD&reltype=latest](https://software.cisco.com/download/release.html?mdfid=284367038&flowid=48154&softwareid=280805680&release=15.3.3M6&relind=AVAILABLE&rellifecycle=MD&reltype=latest)

[http://www.cisco.com/c/en/us/td/docs/routers/access/3800/software/activation/swact.html](http://www.cisco.com/c/en/us/td/docs/routers/access/3800/software/activation/swact.html)


Здесь сравнение 
[http://www.cisco.com/c/en/us/products/collateral/routers/887-integrated-services-router-isr/data_sheet_c78_459542.html](http://www.cisco.com/c/en/us/products/collateral/routers/887-integrated-services-router-isr/data_sheet_c78_459542.html)


Лицензирование 800 серии
[http://ciscosales.ru/informaciya/articles/licenzirovanie_marshrutizatorov_cisco_800_serii/](http://ciscosales.ru/informaciya/articles/licenzirovanie_marshrutizatorov_cisco_800_serii/)

[http://www.cisco.com/c/en/us/products/collateral/security/ios-sslvpn/product_data_sheet0900aecd80405e25.html](http://www.cisco.com/c/en/us/products/collateral/security/ios-sslvpn/product_data_sheet0900aecd80405e25.html)

[http://ciscosales.ru/informaciya/articles/chem_otlichaetsya_marshrutizator_cisco_881_ot_c881/](http://ciscosales.ru/informaciya/articles/chem_otlichaetsya_marshrutizator_cisco_881_ot_c881/)

[http://www.cisco.com/c/en/us/products/collateral/routers/800-series-routers/white_paper_c11_499859.html](http://www.cisco.com/c/en/us/products/collateral/routers/800-series-routers/white_paper_c11_499859.html)

[http://www.cisco.com/c/en/us/products/collateral/routers/887-integrated-services-router-isr/data_sheet_c78_459542.html](http://www.cisco.com/c/en/us/products/collateral/routers/887-integrated-services-router-isr/data_sheet_c78_459542.html)

[http://www.cisco.com/c/en/us/products/collateral/routers/800-series-routers/data_sheet_c78-519930.html](http://www.cisco.com/c/en/us/products/collateral/routers/800-series-routers/data_sheet_c78-519930.html)




## Новый URL
[https://slexui.cloudapps.cisco.com/SWIFT/LicensingUI/Quickstart#.](https://slexui.cloudapps.cisco.com/SWIFT/LicensingUI/Quickstart#.)

[https://tools.cisco.com/SWIFT/Licensing](https://tools.cisco.com/SWIFT/Licensing) 

```
Ioshkar-Ola-NLMK-Sort#copy tftp                                                                                                                                                         
Mar 30 16:27:53: %CCH323-2-GTWY_REGSTR_FAILED: Gateway VChM-Penza failed to register with Gatekeeper Zn_GK2 even after 2 retriesflash                                                   
Address or name of remote host []? 10.192.10.190                                                                                                                                        
Source filename []? FGL21071178_20170330060351.lic                                                                                                                                      
Destination filename [FGL21071178_20170330060351.lic]?                                                                                                                                  
Accessing tftp://10.192.10.190/FGL21071178_20170330060351.lic...                                                                                                                        
Loading FGL21071178_20170330060351.lic from 10.192.10.190 (via GigabitEthernet0/0): !                                                                                                   
[OK - 4396 bytes]                                                                                                                                                                       

4396 bytes copied in 0.632 secs (6956 bytes/sec)                                                                                                                                        

Ioshkar-Ola-NLMK-Sort#sh lic                                                                                                                                                            
Ioshkar-Ola-NLMK-Sort#sh license                                                                                                                                                        
Index 1 Feature: ipbasek9                                                                                                                                                               
Index 2 Feature: securityk9_npe                                                                                                                                                         
```




```
Index 3 Feature: uck9                           
        Period left: Life time
        License Type: Permanent
        License State: Active, In Use
        License Count: Non-Counted
        License Priority: Medium
Index 4 Feature: datak9                         
        Period left: Not Activated
        Period Used: 0  minute  0  second  
        License Type: EvalRightToUse
        License State: Active, Not in Use, EULA not accepted
        License Count: Non-Counted
        License Priority: None
Index 5 Feature: FoundationSuiteK9_npe          
        Period left: Not Activated
        Period Used: 0  minute  0  second  
        License Type: EvalRightToUse
        License State: Active, Not in Use, EULA not accepted
        License Count: Non-Counted
        License Priority: None
Index 6 Feature: AdvUCSuiteK9                   

 Period left: Not Activated
        Period Used: 0  minute  0  second  
        License Type: EvalRightToUse
        License State: Active, Not in Use, EULA not accepted
        License Count: Non-Counted
        License Priority: None
Index 7 Feature: ios-ips-update                 
        Period left: Not Activated
        Period Used: 0  minute  0  second  
        License Type: EvalRightToUse
        License State: Active, Not in Use, EULA not accepted
        License Count: Non-Counted
        License Priority: None
Index 8 Feature: SNASw                          
        Period left: Not Activated
        Period Used: 0  minute  0  second  
        License Type: EvalRightToUse
        License State: Active, Not in Use, EULA not accepted
        License Count: Non-Counted
        License Priority: None
Index 9 Feature: cme-srst                       
ailed to register with Gatekeeper Zn_GK2 even after 2 retries   Period left: Not Activated
        Period Used: 0  minute  0  second  
        License Type: EvalRightToUse
        License State: Active, Not in Use, EULA not accepted
        License Count: 0/0  (In-use/Violation)
        License Priority: None
Index 10 Feature: mgmt-plug-and-play             
Index 11 Feature: mgmt-lifecycle                 
Index 12 Feature: mgmt-assurance                 
Index 13 Feature: mgmt-onplus                    
Index 14 Feature: mgmt-compliance      
```

