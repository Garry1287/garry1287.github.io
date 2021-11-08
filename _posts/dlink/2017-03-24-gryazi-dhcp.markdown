---
layout: post
title:  "Настройка dhcp по схеме в г.Грязи"
date:   2017-03-24 13:54:28 +0300
categories: dlink
tags: dlink
---

# gryazi-dhcp

```
#  Pravda61
subnet 172.28.5.0 netmask 255.255.255.224 {
        range 172.28.5.2 172.28.5.30;
        option subnet-mask 255.255.255.224;
        option domain-name "pravda61-s0.gryazi.loc";
        option broadcast-address 172.28.5.31;
        option routers 172.28.5.1;
        option domain-name-servers 172.28.0.4,217.150.34.129;
} 

#  Pravda64
subnet 172.28.5.32 netmask 255.255.255.224 {
        range 172.28.5.34 172.28.5.62;
        option subnet-mask 255.255.255.224;
        option domain-name "pravda64-s0.gryazi.loc";
        option broadcast-address 172.28.5.63;
        option routers 172.28.5.33;
        option domain-name-servers 172.28.0.4,217.150.34.129;
}

#  Pravda62
subnet 172.28.5.64 netmask 255.255.255.224 {
        range 172.28.5.67 172.28.5.93;
        option subnet-mask 255.255.255.224;
        option domain-name "pravda62-s0.gryazi.loc";
        option routers 172.28.5.65;
        option broadcast-address 172.28.5.95;
        option domain-name-servers 172.28.0.4,217.150.34.129;
}

#  Pravda66
subnet 172.28.5.96 netmask 255.255.255.224 {
        range 172.28.5.98 172.28.5.126;
        option subnet-mask 255.255.255.224;
        option domain-name "pravda66-s0.gryazi.loc";
        option broadcast-address 172.28.5.127;
        option routers 172.28.5.97;
        option domain-name-servers 172.28.0.4,217.150.34.129;
}

#  8marta19
subnet 172.28.5.128 netmask 255.255.255.224 {
        range 172.28.5.130 172.28.5.158;
        option subnet-mask 255.255.255.224;
        option domain-name "8marta19-s0.gryazi.loc";
        option broadcast-address 172.28.5.159;
        option routers 172.28.5.129;
        option domain-name-servers 172.28.0.4,217.150.34.129;
}
#  8marta21
subnet 172.28.5.160 netmask 255.255.255.224 {
        range 172.28.5.162 172.28.5.190;
        option subnet-mask 255.255.255.224;
        option domain-name "8marta21-s0.gryazi.loc";
        option broadcast-address 172.28.5.191;
        option routers 172.28.5.161;
        option domain-name-servers 172.28.0.4,217.150.34.129;
}

# Pravda57
subnet 172.28.5.192 netmask 255.255.255.224 {
        range 172.28.5.194 172.28.5.222;
        option subnet-mask 255.255.255.224;
        option domain-name "pravda57-s0.gryazi.loc";
        option broadcast-address 172.28.5.223;
        option routers 172.28.5.193;
}

# Pravda59
subnet 172.28.5.224 netmask 255.255.255.224 {
        range 172.28.5.226 172.28.5.254;
        option subnet-mask 255.255.255.224;
        option domain-name "pravda59-s0.gryazi.loc";
        option broadcast-address 172.28.5.255;
        option routers 172.28.5.225;
        option domain-name-servers 172.28.0.4,217.150.34.129;
}
```
