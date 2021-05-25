---
layout: post
title:  "dns-checkzone"
date:   2012-07-11 00:29:34 +0400
categories: dns
tags: dns
---

# dns-checkzone
named-checkzone

topaz:/var/lib/named/master # named-checkzone sc.ru sc.ru
sc.ru:1: no TTL specified; using SOA MINTTL instead
dns_master_load: sc.ru:335: lipetskgortrans.sc.ru: CNAME and other data
zone sc.ru/IN: loading from master file sc.ru failed: CNAME and other data
zone sc.ru/IN: not loaded due to errors.
topaz:/var/lib/named/master # vi sc.ru


Нужно придумать проверку
