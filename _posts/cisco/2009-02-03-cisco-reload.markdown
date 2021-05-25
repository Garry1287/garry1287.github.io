---
layout: post
title:  "cisco-reload"
date:   2009-02-03 10:25:11 +0300
categories: cisco-reload
tags: cisco
---

# cisco-reload
Перезагрузка:
просто перезагрузка
reload
перезагрузка в определенное время:
reload at hh:mm [month day] [reason]
перезагрузка через определенное время:
reload in [hh:]mm [reason]
отмена отложенной перезагрузки:
reload cancel


 456          -        X           -           -           
 25           -        X           -           -       

 25   phys-mngt                        00-19-5B-ED-83-32 6     Dynamic
 456  kalinina1b                       00-A0-D1-AA-65-D7 6     Dynamic
 456  kalinina1b                       00-E0-4D-0E-4C-CA 6     Dynamic
 456  kalinina1b                       70-F3-95-B2-23-C8 6     Dynamic
 456  kalinina1b                       E0-CB-4E-02-9A-02 6     Dynamic
 456  kalinina1b                       F4-6D-04-C3-AA-54 6     Dynamic



Before configuring this task, perform the "Identifying Voice Traffic to Optimize Using an Access List" section.
SUMMARY STEPS

1. enable

2. configure terminal

3. ip sla monitor responder

4. exit

5. Move to the network device that is the PfR master controller.

6. enable

7. configure terminal

8. pfr-map map-name sequence-number

9. match ip address {access-list access-list-name | prefix-list prefix-list-name}

10. set active probe probe-type ip-address [target-port number] [codec codec-name]

11. set probe frequency seconds

12. set jitter threshold maximum

13. set mos threshold minimum percent percent

14. set resolve {cost priority value | delay priority value variance percentage | jitter priority value variance percentage | loss priority value variance percentage | mos priority value variance percentage | range priority value | utilization priority value variance percentage}

15. set resolve mos priority value variance percentage

16. set delay {relative percentage | threshold maximum}

17. exit

18. pfr master

19. policy-rules map-name

20. end

21. show pfr master active-probes forced

22. show pfr master policy {sequence-number | policy-name | default}
DETAILED STEPS



