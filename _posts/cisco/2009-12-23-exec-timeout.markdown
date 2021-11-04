---
layout: post
title:  "Правильный exec-timeout в cisco"
date:   2009-12-23 12:17:13 +0300
categories: cisco
tags: cisco
---

# exec-timeout


```
line vty 0 4
  exec-timeout 480 0
 exit
line vty 5 15
  exec-timeout 480 0
``` 
