---
layout: post
title:  "exim-read-mail"
date:   2010-11-15 12:05:03 +0300
categories: mail
tags: mail
---

# exim-read-mail
 	[исправить]

Перейдите в секцию ROUTERS файла конфигурации /usr/local/etc/exim/configure 
и перед роутером dnslookup добавьте:

   archive_all:
   driver = accept
   transport = tr_archive_all
   unseen

В секции TRANSPORTS добавьте:

   tr_archive_all:
   driver = appendfile
   maildir_format
   mode = 0660
   mode_fail_narrower = false
   envelope_to_add = true
   return_path_add = true
   directory = /var/mail/archive@domain.com

Перезагрузите Exim. Теперь вся входящая и исходящая почта будет сохраняться 
в директории /var/mail/archive@domain.com.
