---
layout: post
title:  "timezone-centos"
date:   2008-12-18 00:54:15 +0300
categories: timezone-centos
tags: centos
---

# timezone-centos

timezone
[https://www.centosblog.com/how-to-change-your-centos-server-timezone/](https://www.centosblog.com/how-to-change-your-centos-server-timezone/)
[http://www.server-world.info/en/note?os=CentOS_7&p=timezone](http://www.server-world.info/en/note?os=CentOS_7&p=timezone)


Example 1: set time zone to Melbourne, Australia

cp /usr/share/zoneinfo/Australia/Melbourne /etc/localtime

Example 2: set time zone to UTC

cp /usr/share/zoneinfo/UTC /etc/localtime

To confirm the time set on your system, run the date command, example:

date
Thu Jul 26 09:53:11 EST 2012

If you want to sync this time to your hardware (BIOS) clock, run the following command:

hwclock --systohc




ИЛИ

 show the list of timezones

[root@dlp ~]#
timedatectl list-timezones

Asia/Aden
Asia/Almaty
Asia/Amman
Asia/Anadyr
Asia/Aqtau
Asia/Aqtobe
Asia/Ashgabat
...
...
...
Pacific/Rarotonga
Pacific/Saipan
Pacific/Tahiti
Pacific/Tarawa
Pacific/Tongatapu
Pacific/Wake
Pacific/Wallis

# set timezone

[root@dlp ~]#
timedatectl set-timezone Asia/Tokyo
# show status

[root@dlp ~]#
timedatectl

      Local time: Wed 2014-07-09 18:31:16 JST
  Universal time: Wed 2014-07-09 09:31:16 UTC
        RTC time: Wed 2014-07-09 09:31:15
        Timezone: Asia/Tokyo (JST, +0900)
     NTP enabled: yes
NTP synchronized: yes
 RTC in local TZ: no
      DST active: n/a

