---
layout: post
title:  "ubuntu_vlan"
date:   2013-03-03 06:46:32 +0400
categories: linux
tags: linux
---

# ubuntu_vlan
auto lo
iface lo inet loopback

# The primary network interface
auto eth0
iface eth0 inet static
        #address 192.168.1.149
        #netmask 255.255.255.0
        #network 192.168.1.0
        #broadcast 192.168.1.255
        #gateway 192.168.1.11
        # dns-* options are implemented by the resolvconf package, if installed
        #dns-nameservers 192.168.1.11


auto eth0.10
iface eth0.10 inet static
        address 192.168.1.149
        netmask 255.255.255.0
        network 192.168.1.0
        broadcast 192.168.1.255
        gateway 192.168.1.11
        # dns-* options are implemented by the resolvconf package, if installed
        dns-nameservers 192.168.1.11
        vlan_raw_device eth0

auto eth0.29
iface eth0.29 inet static
        address 172.0.0.1
        netmask 255.0.0.0
	broadcast 172.255.255.255
        vlan_raw_device eth0
	up route add -net 239.0.0.0 netmask 255.0.0.0 dev eth0.29




/proc/net/vlan/config	





sleep 10


/usr/local/bin/getstream -c /etc/iptv-conf/TK1/gcardtk1 &
#start dvb-stream Trikolor 1

/usr/local/bin/getstream -c /etc/iptv-conf/TK1/gcardtk2 &
#start dvb-stream Trikolor 2


~                                           