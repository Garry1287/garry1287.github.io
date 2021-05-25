---
layout: post
title:  "speed-shablon"
date:   2014-09-17 03:12:31 +0400
categories: PSI
tags: PSI
---

# speed-shablon
100Mb
rate-limit input 102400000 19200000 38400000 conform-action transmit exceed-action drop
rate-limit output 102400000 19200000 38400000 conform-action transmit exceed-action drop

10Mb
rate-limit input 10240000 1920000 3840000 conform-action transmit exceed-action drop
rate-limit output 10240000 1920000 3840000 conform-action transmit exceed-action drop

15Mb
rate-limit input 15120000 2835000 5670000 conform-action transmit exceed-action drop
rate-limit output 15120000 2835000 5670000 conform-action transmit exceed-action drop

2MB
rate-limit input 2048000 384000 768000 conform-action transmit exceed-action drop
rate-limit output 2048000 384000 768000 conform-action transmit exceed-action drop

3MB
rate-limit input 3072000 576000 1152000 conform-action transmit exceed-action drop
rate-limit output 3072000 576000 1152000 conform-action transmit exceed-action drop


8Mb
rate-limit input 8192000 1536000 3072000 conform-action transmit exceed-action drop
rate-limit output 8192000 1536000 3072000 conform-action transmit exceed-action drop


1Mb
rate-limit input 1024000 192000 384000 conform-action transmit exceed-action drop
rate-limit output 1024000 192000 384000 conform-action transmit exceed-action drop


6MB
rate-limit input 6144000 1152000 2304000 conform-action transmit exceed-action drop
rate-limit output 6144000 1152000 2304000 conform-action transmit exceed-action drop


5MB
rate-limit input 5120000 960000 1920000 conform-action transmit exceed-action drop
rate-limit output 5120000 960000 1920000 conform-action transmit exceed-action drop

rate-limit input 4096000 768000 1536000 conform-action transmit exceed-action drop
rate-limit output 4096000 768000 1536000 conform-action transmit exceed-action drop



%s/service-policy input ClientPolicy-50Mb/rate-limit input 51200000 9600000 19200000 conform-action transmit exceed-action drop/gc
%s/service-policy output ClientPolicy-50Mb/rate-limit output 51200000 9600000 19200000 conform-action transmit exceed-action drop/gc

%s/service-policy input ClientPolicy-60Mb/rate-limit input 61440000 11520000 23040000 conform-action transmit exceed-action drop/gc
%s/service-policy output ClientPolicy-60Mb/rate-limit output 61440000 11520000 23040000 conform-action transmit exceed-action drop/gc

%s/service-policy input ClientPolicy-15Mb/rate-limit input 15120000 2835000 5670000 conform-action transmit exceed-action drop/gc
%s/service-policy output ClientPolicy-15Mb/rate-limit output 15120000 2835000 5670000 conform-action transmit exceed-action drop/gc

%s/service-policy input ClientPolicy-2Mb/rate-limit input 2048000 384000 768000 conform-action transmit exceed-action drop/gc
%s/service-policy output ClientPolicy-2Mb/rate-limit output 2048000 384000 768000 conform-action transmit exceed-action drop/gc

%s/service-policy input ClientPolicy-20Mb/rate-limit input 20480000 3840000 7680000 conform-action transmit exceed-action drop/gc
%s/service-policy output ClientPolicy-20Mb/rate-limit output 20480000 3840000 7680000 conform-action transmit exceed-action drop/gc


%s/service-policy input ClientPolicy-4Mb/rate-limit input 4096000 768000 1536000 conform-action transmit exceed-action drop/gc
%s/service-policy output ClientPolicy-4Mb/rate-limit output 4096000 768000 1536000 conform-action transmit exceed-action drop/gc

%s/service-policy input ClientPolicy-5Mb/rate-limit input 5120000 960000 1920000 conform-action transmit exceed-action drop/gc
%s/service-policy output ClientPolicy-5Mb/rate-limit output 5120000 960000 1920000 conform-action transmit exceed-action drop/gc

%s/service-policy input ClientPolicy-6Mb/rate-limit input 6144000 1152000 2304000 conform-action transmit exceed-action drop/gc
%s/service-policy output ClientPolicy-6Mb/rate-limit output 6144000 1152000 2304000 conform-action transmit exceed-action drop/gc

%s/service-policy input ClientPolicy-8Mb/rate-limit input 8192000 1536000 3072000 conform-action transmit exceed-action drop/gc
%s/service-policy output ClientPolicy-8Mb/rate-limit output 8192000 1536000 3072000 conform-action transmit exceed-action drop/gc


%s/service-policy input ClientPolicy-1Mb/rate-limit input 1024000 192000 384000 conform-action transmit exceed-action drop/gc
%s/service-policy output ClientPolicy-1Mb/rate-limit input 1024000 192000 384000 conform-action transmit exceed-action drop/gc



%s/service-policy input ClientPolicy-3Mb/rate-limit input 3072000 576000 1152000 conform-action transmit exceed-action drop/gc
%s/service-policy output ClientPolicy-3Mb/rate-limit output 3072000 576000 1152000 conform-action transmit exceed-action drop/gc

%s/service-policy input ClientPolicy-300Mb/rate-limit input 307200000 57600000 115200000 conform-action transmit exceed-action drop/gc
%s/service-policy output ClientPolicy-300Mb/rate-limit output 307200000 57600000 115200000 conform-action transmit exceed-action drop/gc


%s/service-policy input ClientPolicy-100Mb/rate-limit input 102400000 19200000 38400000 conform-action transmit exceed-action drop/gc
%s/service-policy output ClientPolicy-100Mb/rate-limit input 102400000 19200000 38400000 conform-action transmit exceed-action drop/gc

%s/service-policy input ClientPolicy-10Mb/rate-limit input 10240000 1920000 3840000 conform-action transmit exceed-action drop/gc
%s/service-policy output ClientPolicy-10Mb/rate-limit input 10240000 1920000 3840000 conform-action transmit exceed-action drop/gc


%s/service-policy input ClientPolicy-30Mb/rate-limit input 30720000 5760000 11520000 conform-action transmit exceed-action drop/gc
%s/service-policy output ClientPolicy-30Mb/rate-limit output 30720000 5760000 11520000 conform-action transmit exceed-action drop/gc


%s/service-policy input ClientPolicy-40Mb/rate-limit input 40960000 7680000 15360000 conform-action transmit exceed-action drop/gc
%s/service-policy output ClientPolicy-40Mb/rate-limit output 40960000 7680000 15360000 conform-action transmit exceed-action drop/gc

%s/service-policy input ClientPolicy-25Mb/rate-limit input 25600000 4800000 9600000 conform-action transmit exceed-action drop/gc
%s/service-policy output ClientPolicy-25Mb/rate-limit output 25600000 4800000 9600000 conform-action transmit exceed-action drop/gc

%s/service-policy input ClientPolicy-80Mb/rate-limit input 81920000 15360000 30720000 conform-action transmit exceed-action drop/gc
%s/service-policy output ClientPolicy-80Mb/rate-limit output 81920000 15360000 30720000 conform-action transmit exceed-action drop/gc
