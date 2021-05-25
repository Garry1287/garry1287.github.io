---
layout: post
title:  "iptables-restore"
date:   2015-12-14 21:42:20 +0300
categories: firewall
tags: firewall
---

# iptables-restore
Чтоб долго не мучаться…
case "$1" in
test)
echo «Stop»
stop
echo «Starting...»
echo «Iptables will be autostopped after 60 secs...»
start
echo «If you can see this string, press \»Ctrl+C\" for apply rules."
sleep 60 && stop
echo «Iptables stopped after timeout… Check rules...»
;;
start)
start
;;

После /etc/init.d/iptables test жмем рару раз Enter…
Если померло, то не увидим на экране движение…
Если не померло, то жмем Ctrl+C…

Удачи… 