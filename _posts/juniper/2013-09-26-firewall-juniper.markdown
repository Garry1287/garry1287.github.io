---
layout: post
title:  "Firewall в juniper"
date:   2013-09-26 09:34:59 +0400
categories: juniper Networking
tags: juniper
---

# Firewall в juniper
```
firewall {                              
    family inet {                       
        filter block.services {         
            term 10 {                   
                from {                  
                    source-prefix-list {
                        lan-mngt;       
                    }                   
                    destination-port [ telnet ssh snmp ];
                }                       
                then accept;            
            }                           
            term 20 {                   
                from {                  
                    destination-port [ telnet ssh snmp ];
                }                       
                then {                  
                    discard;            
                }                       
            }                           
            term 30 {                   
                then accept;            
            }                           
        }                               
    }                                   
}

set interfaces lo0 unit 0 family inet filter input block.services 
```

независимо от того
так или иначе
наличие или отсутствие
вне зависимости от того
ли
Стоит ли
Whether or not to
Whether or not to echo out your response strings
