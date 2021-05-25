---
layout: post
title:  "opensuse-repo13.1"
date:   2009-12-11 22:43:19 +0300
categories: linux
tags: linux
---

# opensuse-repo13.1
  │Priority     │Enabled│Autorefresh│Name                              │Service│URL                                                                                                                         │ 
  │ 99 (Default)│       │           │virtualbox                        │       │[http://download.virtualbox.org/virtualbox/rpm/opensuse/12.3/](http://download.virtualbox.org/virtualbox/rpm/opensuse/12.3/)                                                                │ 
  │ 99 (Default)│       │           │openSUSE-13.1-Update-Debug        │       │[http://download.opensuse.org/debug/update/13.1/](http://download.opensuse.org/debug/update/13.1/)                                                                             │ 
  │ 99 (Default)│       │           │LibreOffice                       │       │[http://download.opensuse.org/repositories/LibreOffice:/Stable/openSUSE_13.1/](http://download.opensuse.org/repositories/LibreOffice:/Stable/openSUSE_13.1/)                                                │ 
  │ 99 (Default)│       │     x     │openSUSE-13.1-Update-Debug-Non-Oss│       │[http://download.opensuse.org/debug/update/13.1-non-oss/](http://download.opensuse.org/debug/update/13.1-non-oss/)                                                                     │ 
  │ 99 (Default)│   x   │     x     │SuSE                              │       │[http://download.videolan.org/SuSE/13.1/](http://download.videolan.org/SuSE/13.1/)                                                                                     │ 
  │ 99 (Default)│   x   │     x     │openSUSE-13.1-Non-Oss             │       │[http://download.opensuse.org/distribution/13.1/repo/non-oss/](http://download.opensuse.org/distribution/13.1/repo/non-oss/)                                                                │ 
  │ 99 (Default)│   x   │     x     │java                              │       │[http://download.opensuse.org/repositories/Java:/packages/openSUSE_13.1/](http://download.opensuse.org/repositories/Java:/packages/openSUSE_13.1/)                                                     │ 
  │ 99 (Default)│   x   │     x     │openSUSE-13.1-Oss                 │       │[http://download.opensuse.org/distribution/13.1/repo/oss/](http://download.opensuse.org/distribution/13.1/repo/oss/)                                                                    │ 
  │ 99 (Default)│   x   │           │openSUSE-13.1-1.10                │       │cd:///?devices=/dev/disk/by-id/ata-Optiarc_DVD_RW_AD-7203A,/dev/sr0                                                         │ 
  │ 99 (Default)│       │     x     │openSUSE-13.1-Source              │       │[http://download.opensuse.org/source/distribution/13.1/repo/oss/](http://download.opensuse.org/source/distribution/13.1/repo/oss/)                                                             │ 
  │ 99 (Default)│   x   │     x     │Packman Repository                │       │[http://ftp.gwdg.de/pub/linux/packman/suse/openSUSE_13.1/](http://ftp.gwdg.de/pub/linux/packman/suse/openSUSE_13.1/)                                                                    │ 
  │ 99 (Default)│   x   │     x     │openSUSE-13.1-Update              │       │[http://download.opensuse.org/update/13.1/](http://download.opensuse.org/update/13.1/)                                                                                   │ 
  │ 99 (Default)│   x   │     x     │libdvdcss repository              │       │[http://opensuse-guide.org/repo/13.1/](http://opensuse-guide.org/repo/13.1/)                                                                                        │ 
  │ 99 (Default)│   x   │     x     │openSUSE-13.1-Update-Non-Oss      │       │[http://download.opensuse.org/update/13.1-non-oss/](http://download.opensuse.org/update/13.1-non-oss/)                                                                           │ 
  │ 99 (Default)│   x   │     x     │Tumbleweed                        │       │[http://download.opensuse.org/repositories/openSUSE:/Tumbleweed/standard/](http://download.opensuse.org/repositories/openSUSE:/Tumbleweed/standard/)                                                    │ 
  │ 99 (Default)│       │     x     │openSUSE-13.1-Debug               │       │[http://download.opensuse.org/debug/distribution/13.1/repo/oss/](http://download.opensuse.org/debug/distribution/13.1/repo/oss/)                                                              │ 
  │

zypper mr -da

 zypper ar [http://download.opensuse.org/distribution/13.2/repo/oss](http://download.opensuse.org/distribution/13.2/repo/oss) oss
zypper ar [http://download.opensuse.org/distribution/13.2/repo/non-oss](http://download.opensuse.org/distribution/13.2/repo/non-oss) non-oss
zypper ar [http://download.opensuse.org/update/13.2](http://download.opensuse.org/update/13.2) update 


zypper clean --all

rpmdb --rebuilddb

zypper ref 
zypper -n dup -l