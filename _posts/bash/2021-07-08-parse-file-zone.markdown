---
layout: post
title:  "Setting default value for a BASH variable
date: 2021-07-08 14:25:11 +0300
categories: bash ros
---



# Вытащил ip адреса из файла зоны bind

```
;========================================================
; Elec CS
;=======================================================
eleces1		A	10.240.21.162
eleces2		A       10.240.21.163
elecssw         A       10.240.21.164
elecssw1        A       10.240.21.165
elecssw2        A       10.240.21.166
elecsmg1        A       10.240.21.167
elecsmg2        A       10.240.21.168

;========================================================
; Gryazi CS
;=======================================================
gryazies1       A       10.240.80.18
gryazissw       A       10.240.80.19
gryazismg1      A       10.240.80.20
gryazissw1	A	10.240.80.21
gryazissw2	A	10.240.80.22
gryazismg2	A	10.240.80.23
gryazies2	A	10.240.80.25

```

```
grep -v ";" mydocs/ip-voip/db.voip.lipetsk.net | sed '/^$/d' | awk '{print $3}' > mydocs/ip-voip/ip-address-si3000.txt
```

Избавление от записей CNAME и пробелов, которые почему-то не удалились
```
cat mydocs/ip-voip/ip-address-si3000.txt | grep "10.240" > ip-addr-si3000.txt
```