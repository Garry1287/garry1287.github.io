---
layout: post
title:  "backup-server"
date:   2011-10-24 18:24:23 +0400
categories: backup-server
tags: backup-server
---

# backup-server
/usr/bin/mysqldump -u root -p915Nyg710 --opt lipbalkon > /home/garry/backup/lipbalkon.sql
/bin/tar -czf /home/garry/backup/lipbalkon.tar.gz /home/lipbalkon/
/usr/bin/mysqldump -u root -p915Nyg710 --opt um > /home/garry/backup/um.sql
/bin/tar -czf /home/garry/backup/um.tar.gz /var/home/umit-agro.sc.ru/
/bin/chown garry:users /home/garry/backup/*