---
layout: post
title:  "backup-garry"
date:   2014-04-09 13:18:04 +0400
categories: backup linux
tags: backup
---

# backup-garry
30      6       *       *       *      



/usr/bin/rsync -avz -e ssh --delete-after /home/backup/  backup@crystal.sc.int:/home/backup/sapphire
/usr/bin/rsync -avz -e ssh --delete-after /home/berg/  backup@crystal.sc.int:/var/backup-berg


/usr/bin/rsync -avz --delete-after 

/home/garry/Documents
/home/garry/shared
/home/garry/seo
/home/garry/ncc-garry/определённые файлы
/home/garry/inventarization
/home/garry/bin
/home/garry/sh
/home/garry/.thunderbird
/home/garry/.firefox
/home/garry/books


 backup@crystal.sc.int:/home/backup/sapphire


--delete-after