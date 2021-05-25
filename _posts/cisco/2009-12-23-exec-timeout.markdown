---
layout: post
title:  "exec-timeout"
date:   2009-12-23 12:17:13 +0300
categories: exec-timeout
tags: cisco
---

# exec-timeout
exec-timeout 480 0


line vty 0 4
  exec-timeout 480 0
 exit
line vty 5 15
  exec-timeout 480 0
 
