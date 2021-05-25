---
layout: post
title:  "openvpn-problem"
date:   2018-02-27 10:12:54 +0300
categories: vpn
tags: vpn
---

# openvpn-problem
[https://forums.openvpn.net/viewtopic.php?t=23166](https://forums.openvpn.net/viewtopic.php?t=23166)
Then regenerated the CRL:

Code: Select all

openssl ca  -gencrl -keyfile keys/ca.key -cert keys/ca.crt  -out keys/crl.pem -config ./openssl.cnf

change md5 to sha
