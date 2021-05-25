---
layout: post
title:  "access-list-bras"
date:   2018-11-27 07:56:46 +0300
categories: access-list-bras
tags: cisco
---

# access-list-bras
ip route 10.1.5.0 255.255.255.0 172.19.1.253
ip route 10.1.6.0 255.255.255.0 172.19.1.253
ip route 10.1.7.0 255.255.255.0 172.19.1.253
ip route 10.1.8.0 255.255.255.0 172.19.1.253
ip route 10.1.9.0 255.255.255.0 172.19.1.253
ip route 10.1.10.0 255.255.255.0 172.19.1.253
ip route 10.1.11.0 255.255.255.0 172.19.1.253
ip route 10.1.12.0 255.255.255.0 172.19.1.253
ip route 10.1.13.0 255.255.255.0 172.19.1.253
ip route 10.1.14.0 255.255.255.0 172.19.1.253
ip route 10.1.15.0 255.255.255.0 172.19.1.253
ip route 10.1.16.0 255.255.255.0 172.19.1.253
ip route 10.1.17.0 255.255.255.0 172.19.1.253
ip route 10.1.18.0 255.255.255.0 172.19.1.253
ip route 10.1.19.0 255.255.255.0 172.19.1.253
ip route 10.1.20.0 255.255.255.0 172.19.1.253
ip route 10.1.21.0 255.255.255.0 172.19.1.253
ip route 10.1.22.0 255.255.255.0 172.19.1.253
ip route 10.1.23.0 255.255.255.0 172.19.1.253
ip route 10.1.24.0 255.255.255.0 172.19.1.253
ip route 10.1.25.0 255.255.255.0 172.19.1.253
ip route 10.1.26.0 255.255.255.0 172.19.1.253
ip route 10.1.27.0 255.255.255.0 172.19.1.253
ip route 10.1.28.0 255.255.255.0 172.19.1.253
ip route 10.1.29.0 255.255.255.0 172.19.1.253
ip route 10.1.30.0 255.255.255.0 172.19.1.253
ip route 91.192.61.53 255.255.255.255 172.19.1.253






access-list 100 permit tcp 10.1.5.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.6.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.7.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.8.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.9.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.10.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.11.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.12.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.13.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.14.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.15.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.16.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.17.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.18.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.19.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.20.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.21.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.22.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.23.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.24.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.25.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.26.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.27.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.28.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.29.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.30.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 172.20.0.0 0.3.255.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 95.179.0.0 0.0.127.255 host 81.20.192.12 eq 1723
access-list 100 permit tcp 93.180.0.0 0.0.63.255 host 81.20.192.12 eq 1723
access-list 100 permit tcp host 91.192.62.28 host 81.20.192.12 eq 1723
access-list 100 permit tcp host 94.232.14.120 host 81.20.192.12 eq 1723
access-list 100 deny   tcp any host 172.31.3.1 eq 1723
access-list 100 deny   tcp any host 81.20.192.12 eq 1723
access-list 100 deny   tcp any host 81.20.196.123 eq 1723
access-list 100 deny   tcp any host 81.20.196.124 eq 1723
access-list 100 permit ip any any













access-list 100 permit tcp 10.1.5.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.6.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.7.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.8.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.9.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.10.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.11.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.12.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.13.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.14.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.15.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.16.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.17.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.18.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.19.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.20.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.21.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.22.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.23.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.24.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.25.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.26.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.27.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.28.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.29.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 10.1.30.0 0.0.0.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 172.20.0.0 0.3.255.255 host 172.31.3.1 eq 1723
access-list 100 permit tcp 95.179.0.0 0.0.127.255 host 81.20.192.15 eq 1723
access-list 100 permit tcp 93.180.0.0 0.0.63.255 host 81.20.192.15 eq 1723
access-list 100 permit tcp host 91.192.62.28 host 81.20.192.15 eq 1723
access-list 100 permit tcp host 94.232.14.120 host 81.20.192.15 eq 1723
access-list 100 deny   tcp any host 172.31.3.1 eq 1723
access-list 100 deny   tcp any host 81.20.192.15 eq 1723
access-list 100 deny   tcp any host 81.20.200.253 eq 1723
access-list 100 deny   tcp any host 81.20.200.254 eq 1723
access-list 100 permit ip any any

