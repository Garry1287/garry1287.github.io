---
layout: post
title:  "addpac_dhcp"
date:   2016-02-05 06:07:48 +0300
categories: voip
tags: voip
---

# addpac_dhcp
ip dhcp pool LAN
 network 192.168.0.0 255.255.255.0
  range 192.168.0.12 192.168.0.100
  default-lease-time 18000
  routers 192.168.0.11
  domain-name-servers 81.20.192.16 81.20.192.17
  domain-name Muradjan



dhcp server