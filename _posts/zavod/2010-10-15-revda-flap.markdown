---
layout: post
title:  "revda-flap"
date:   2010-10-15 19:16:12 +0400
categories: zavod
tags: zavod
---

# revda-flap
Jan 23 11:45:19: %SW_MATM-4-MACFLAP_NOTIF: Host 001e.be4f.9c39 in vlan 12 is flapping between port Fa0/1 and port Fa0/3
Fa0/1                          up             up       # Link to Maxi_Group-C1
Fa0/2                          up             up       # Video-conference ethernet segment
Fa0/3                          up             up       # Maxi-Group LAN
Maxi_Group-C1(Revda)#sh int Fa0/1.12
FastEthernet0/1.12 is up, line protocol is up 
  Hardware is MV96340 Ethernet, address is 001e.be4f.9c39 (bia 001e.be4f.9c39)