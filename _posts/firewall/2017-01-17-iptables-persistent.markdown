---
layout: post
title:  "iptables-persistent"
date:   2017-01-17 13:03:09 +0300
categories: firewall
tags: firewall
---

# iptables-persistent
iptables-save

The actual iptables rules are created and customized on the command line with the command iptables for IPv4 and ip6tables for IPv6.

These can be saved in a file with the command iptables-save for IPv4.

Debian/Ubuntu: `iptables-save > /etc/iptables/rules.v4`

RHEL/CentOS: `iptables-save > /etc/sysconfig/iptables`

These files can be loaded again with the command iptables-restore for IPv4.

Debian/Ubuntu: `iptables-restore < /etc/iptables/rules.v4`

RHEL/CentOS: `iptables-restore < /etc/sysconfig/iptables`

If you would also like to use IPv6 rules, these can be stored in a separate file.

Debian/Ubuntu: `ip6tables-save > /etc/iptables/rules.v6`

RHEL/CentOS: `ip6tables-save > /etc/sysconfig/ip6tables`

The automatic loading of the configured iptables rules can be done by using the following methods:
iptables-persistent for Debian/Ubuntu

Since Ubuntu 10.04 LTS (Lucid) and Debian 6.0 (Squeeze) there is a package with the name "iptables-persistent" which takes over the automatic loading of the saved iptables rules. To do this, the rules must be saved in the file /etc/iptables/rules.v4 for IPv4 and /etc/iptables/rules.v6 for IPv6.

For use, the package must simply be installed.
```
apt-get install iptables-persistent
```
If the installation fails, please check whether systemd has already had failures before the installation of iptables-persisent. Those systemd errors can cause the iptables-persistent installation to fail.[1]

Older iptables-persistent versions (e.g. like those in Debian Squeeze) still do not support IPv6 rules. There is only one file with the name /etc/iptables/rules for IPv4. Check the Init-Script for which files are loaded in your iptables-persistent version.

Please check that your rules are loaded as desired following the first reboot after configuration.
iptables Service for RedHat Enterprise Linux (RHEL) and CentOS
