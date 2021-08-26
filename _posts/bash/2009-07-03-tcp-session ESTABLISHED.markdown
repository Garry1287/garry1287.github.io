---
layout: post
title:  "tcp-session ESTABLISHED"
date:   2009-07-03 22:51:39 +0400
categories: Networking
tags: Установленные tcp-сессии
---

# php-hosting
netstat -lantp | grep ESTABLISHED |awk '{print $5}' | awk -F: '{print $1}' | sort -u

 iotop
top




