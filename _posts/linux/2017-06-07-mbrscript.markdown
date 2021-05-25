---
layout: post
title:  "mbrscript"
date:   2017-06-07 03:50:58 +0300
categories: linux
tags: linux
---

# mbrscript
  dd if=/dev/sdb of=/root/backup.mbr bs=512 count=1
  dd if=/root/backup.mbr of=/dev/sdb bs=512 count=1
