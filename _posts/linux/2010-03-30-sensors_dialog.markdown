---
layout: post
title:  "sensors_dialog"
date:   2010-03-30 13:01:31 +0400
categories: linux
tags: linux
---

# sensors_dialog
sensors-detect
# sensors-detect revision 5861 (2010-09-21 17:21:05 +0200)
# System: VMware, Inc. VMware Virtual Platform
# Board: Intel Corporation 440BX Desktop Reference Platform

This program will help you determine which kernel modules you need
to load to use lm_sensors most effectively. It is generally safe
and recommended to accept the default answers to all questions,
unless you know what you're doing.

Some south bridges, CPUs or memory controllers contain embedded sensors.
Do you want to scan for them? This is totally safe. (YES/no): YES
Module cpuid loaded successfully.
Silicon Integrated Systems SIS5595...                       No
VIA VT82C686 Integrated Sensors...                          No
VIA VT8231 Integrated Sensors...                            No
AMD K8 thermal sensors...                                   No
AMD Family 10h thermal sensors...                           No
AMD Family 11h thermal sensors...                           No
Intel digital thermal sensor...                             Success!
    (driver `coretemp')
Intel AMB FB-DIMM thermal sensor...                         No
VIA C7 thermal sensor...                                    No
VIA Nano thermal sensor...                                  No

Some Super I/O chips contain embedded sensors. We have to write to
standard I/O ports to probe them. This is usually safe.
Do you want to scan for Super I/O sensors? (YES/no): YES
Probing for Super-I/O at 0x2e/0x2f
Trying family `National Semiconductor'...                   Yes
Found unknown chip with ID 0x0f00
Probing for Super-I/O at 0x4e/0x4f
Trying family `National Semiconductor'...                   No
Trying family `SMSC'...                                     No
Trying family `VIA/Winbond/Nuvoton/Fintek'...               No
Trying family `ITE'...                                      No

Some systems (mainly servers) implement IPMI, a set of common interfaces
through which system health data may be retrieved, amongst other things.
We first try to get the information from SMBIOS. If we don't find it
there, we have to read from arbitrary I/O ports to probe for such
interfaces. This is normally safe. Do you want to scan for IPMI
interfaces? (YES/no): YES
Probing for `IPMI BMC KCS' at 0xca0...                      No
Probing for `IPMI BMC SMIC' at 0xca8...                     No

Some hardware monitoring chips are accessible through the ISA I/O ports.
We have to write to arbitrary I/O ports to probe them. This is usually
safe though. Yes, you do have ISA I/O ports even if you do not have any
ISA slots! Do you want to scan the ISA I/O ports? (YES/no): YES
Probing for `National Semiconductor LM78' at 0x290...       No
Probing for `National Semiconductor LM79' at 0x290...       No
Probing for `Winbond W83781D' at 0x290...                   No
Probing for `Winbond W83782D' at 0x290...                   No

Lastly, we can probe the I2C/SMBus adapters for connected hardware
monitoring devices. This is the most risky part, and while it works
reasonably well on most systems, it has been reported to cause trouble
on some systems.
Do you want to probe the I2C/SMBus adapters now? (YES/no): YES
Using driver `i2c-piix4' for device 0000:00:07.3: Intel 82371AB PIIX4 ACPI
Module i2c-dev loaded successfully.

Now follows a summary of the probes I have just done.
Just press ENTER to continue: 

Driver `coretemp':
  * Chip `Intel digital thermal sensor' (confidence: 9)



Мониторинг железа в Линукс
[http://www.ashep.org/2010/izmeryaem-temperaturu-v-linux/#.UWZoK1IcSxL](http://www.ashep.org/2010/izmeryaem-temperaturu-v-linux/#.UWZoK1IcSxL)
[http://www.kusto.com.ru/temperature/](http://www.kusto.com.ru/temperature/)
[http://www.odmin4eg.ru/2013/%D1%83%D0%B7%D0%BD%D0%B0%D1%82%D1%8C-%D0%BC%D0%BE%D0%B4%D0%B5%D0%BB%D1%8C-%D0%BC%D0%B0%D1%82%D0%B5%D1%80%D0%B8%D0%BD%D1%81%D0%BA%D0%BE%D0%B9-%D0%BF%D0%BB%D0%B0%D1%82%D1%8B-linux/](http://www.odmin4eg.ru/2013/%D1%83%D0%B7%D0%BD%D0%B0%D1%82%D1%8C-%D0%BC%D0%BE%D0%B4%D0%B5%D0%BB%D1%8C-%D0%BC%D0%B0%D1%82%D0%B5%D1%80%D0%B8%D0%BD%D1%81%D0%BA%D0%BE%D0%B9-%D0%BF%D0%BB%D0%B0%D1%82%D1%8B-linux/)
[http://www.tux.in.ua/articles/413](http://www.tux.in.ua/articles/413)
[http://www.osp.ru/os/2002/11/182080/](http://www.osp.ru/os/2002/11/182080/)
[https://wiki.archlinux.org/index.php/Hddtemp](https://wiki.archlinux.org/index.php/Hddtemp)
[https://wiki.archlinux.org/index.php/Monitorix](https://wiki.archlinux.org/index.php/Monitorix)
[https://wiki.archlinux.org/index.php/Fan_Speed_Control_%28%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9%29](https://wiki.archlinux.org/index.php/Fan_Speed_Control_%28%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9%29)


Мониторнг дисков
[http://technet.microsoft.com/ru-ru/library/dd262028.aspx](http://technet.microsoft.com/ru-ru/library/dd262028.aspx)
[http://www.welinux.ru/post/6790/](http://www.welinux.ru/post/6790/)




