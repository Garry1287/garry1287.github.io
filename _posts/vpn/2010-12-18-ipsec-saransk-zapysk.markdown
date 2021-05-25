---
layout: post
title:  "ipsec-saransk-zapysk"
date:   2010-12-18 23:01:55 +0300
categories: vpn
tags: vpn
---

# ipsec-saransk-zapysk
killall -9 racoon
/etc/init.d/racoon stop
setkey -F
setkey -FP
/etc/init.d/racoon start