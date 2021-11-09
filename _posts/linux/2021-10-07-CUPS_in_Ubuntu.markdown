 ---
layout: post
title:  "CUPS in Ubuntu/mint"
date:   2021-10-07 22:21:47 +0300
categories: linux
tags: 

---

# CUPS in Ubuntu/mint


```
 2035  cd /home/garry/Документы/linux-capt-drv-v271-uken/64-bit_Driver/Debian
 2036  ls
 2037  dpkg -i cndrvcups-common_3.21-1_amd64.deb
 2038  sudo dpkg -i cndrvcups-common_3.21-1_amd64.deb
 2039  sudo apt install -f
 2040  ls
 2041  dpkg -i cndrvcups-capt_2.71-1_amd64.deb 
 2042  sudo dpkg -i cndrvcups-capt_2.71-1_amd64.deb 
 2043  sudo apt install -f
 2044  systemctl start cups
 2045  systemctl enable cups
 2046  sudo systemctl enable cups
 2047  sudo /usr/sbin/lpadmin -p LBP3010 -m CNCUPSLBP3050CAPTK.ppd -v ccp:/var/ccpd/fifo0
 2048  sudo /usr/sbin/ccpdadmin -p LBP3010 -o /dev/usb/lp0
 2049  sudo systemctl status ccpd
 2050  sudo systemctl start ccpd
 2051  sudo systemctl enable ccpd


sudo apt install cups-pdf
```

[i-SENSYS LBP3010 - Support - Download drivers, software and manuals - Canon Europe](https://www.canon-europe.com/support/consumer_products/products/printers/laser/i-sensys_lbp3010.html?type=drivers&driverdetailid=tcm:13-1057853&os=linux%20%2864-bit%29&language=en)

[Ubuntu + Принтер LBP3010 - Шпаргалки администратору](https://www.sites.google.com/site/admcrib/home/ubuntu-pecat/ubuntu-lbp3010)

[Настраиваем принтер Canon LBP3010 в Ubuntu 10.10 / Хабр](https://habr.com/ru/post/107893/)

[Изучение CUPS в linux и решение проблем с печатью в linux/bsd системах](http://allpro.com.ua/linux-cups.html)

[https://wiki.archlinux.org/title/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic](https://wiki.archlinux.org/title/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Foomatic)