---
layout: post
title:  "k9-ctd-ports-network"
date:   2009-05-09 11:47:51 +0400
categories: PSI
tags: PSI
---

# k9-ctd-ports-network
ctd-s4
Fa0/5                          up             up       LPK-C01-BRAS01-MNGT-7/1


ctd-s0
Fa0/2                          up             up       #SAPPHIRE LAN eth1
Fa0/3                          down           down     #LPK-C01-SRV02-AP02-IPMI


ctd-s1
Gi0/1                          up             up       #VMSERV2
Gi0/3                          up             up       #LAZURITE.SC.INT
Gi0/6                          up             up       #LPK-C01-SRV02-AP02-Eth0
Gi0/12                         up             up       #VMSERV2-iSCSI-2018
Gi0/16                         up             up       # Sapphire.sc.ru





ctd-s8

  Port No       :15
    Active      :Yes
    Name        :srv-Guard

  
  
  Port No       :17                                 
    Active      :Yes
    Name        :Emerald-eth0

  
  Port No       :18
    Active      :Yes
    Name        :Emerald-eth1

  
  Port No       :19
    Active      :Yes
    Name        :billhost-eth1

  
  Port No       :20
    Active      :Yes
    Name        :VMSERV2-iSCSI                      

  
  Port No       :21
    Active      :Yes
    Name        :HP-iSCSI-A4

  
  Port No       :22
    Active      :Yes
    Name        :

  
  Port No       :23
    Active      :Yes
    Name        :billhost-eth0

  


ctd-s2
ge-0/0/15       up    up   BEELINE
xe-0/0/25       up    up   Retnbackbone-to-C6
xe-0/0/26       up    up   RETN-Inet



k9-s9
-------------------------------------------------------------------------------
 1        Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: Netbynet                                              
 2        Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: RETN-link3-ORTPTS                                     
 3        Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: Lipka                                                 
 4        Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: AMETHYST.SC.INT                                       
 5        Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: K9-R0-Gi0/0                                           
 6        Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: K9-R0-Gi0/1                                           

                            
 9        Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: LPK-C01-SRV01-AP01-Eth0                              
 10       Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: Gipromez-S0                                           
 11       Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: Crystal                                               
 12       Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: 192.168.115.22-Bar7-alfabank                          
 13       Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: NAS1-iSCSI-and-mngt                                   
 14       Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: zabbix1.sc.int                                        
                                          
                                         
 17       Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: Billhost2                                             
 18       Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: Billhost2-LAN                                                                               
 20       Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: "Equant-new-port"                                     
 21   (C) Enabled   Auto/Disabled           1000M/Full/None         Enabled     
           Description: ast3.sc.ru                                            
 21   (F) Enabled   Auto/Disabled           Link Down               Enabled     
           Description:                                                       
 22   (C) Enabled   Auto/Disabled           1000M/Full/None         Enabled     
           Description: VMSERV1                                               
 22   (F) Enabled   Auto/Disabled           Link Down               Enabled     
           Description:                                                       
                                   




k9-s12  
                                                            
                                                
                 
                                                  
 12     Enabled   Auto/Disabled          LinkDown                 Enabled 
        Auto    
 Desc: PROMOX                                                              
                                                                           
                                                                 
 17     Enabled   Auto/Disabled          100M/Full/None           Enabled 
        Auto    
 Desc: LPK-C01-SRV01-AP01-IPMI                                                  


 
 Desc:                                                                          
 26(C)  Enabled   Auto/Disabled          LinkDown                 Enabled 
        Auto    
 Desc: Kassa-PetrovRynka                                                        
 26(F)  Enabled   Auto/Disabled          100M/Full/None           Enabled 
                
 Desc:                                                                          

 
 



k9-s13
System Name                : k9-s13.sc.int
System Location            : Fedorov
            




k9-s8
 1        Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: to tkd1.1                                             
 2        Enabled   Auto/Disabled           Link Down               Enabled    
           Description: to tkd1.5                                             
 3        Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: to tkd2.1                                             
 4        Enabled   Auto/Disabled           Link Down               Enabled    
           Description: to tkd2.5                                             
 5        Enabled   Auto/Disabled           Link Down               Enabled    
           Description: tkd4.1                                                
 6        Enabled   Auto/Disabled           Link Down               Enabled    
           Description: tkd4.3                                                
 7        Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: tkd3.1                                                
 8        Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: tkd3.3                                                
 9        Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: frunze27-611                                          
 10       Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: tv-kisa-s0                                            
 11       Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: kommunalnaya 12                                       
 12       Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: nedelina15a                                           
 13       Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: MSS-NEW                                               
 14       Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: Oktyabrskaya74                                        
 15       Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: OKT22-115.106                                         
 16       Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: Profiplus                                             
 17       Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: H.Metallurg                                           
 18       Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: Kuznechnaya10                                         
 19       Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: forQinQ-K9-S9-Gi24                                    
 20       Enabled   Auto/Disabled           1000M/Full/None         Enabled    
           Description: skorohodova11                                         
 21   (C) Enabled   Auto/Disabled           1000M/Full/None         Enabled     
           Description: Link-to-k9-s1                                         
 21   (F) Enabled   Auto/Disabled           Link Down               Enabled     
           Description:                                                       
 22   (C) Enabled   Auto/Disabled           1000M/Full/None         Enabled     
           Description: kvmhost1                                              
 22   (F) Disabled  Auto/Disabled           Link Down               Enabled     
           Description:                                                       
 23   (C) Enabled   Auto/Disabled           1000M/Full/None         Enabled     
           Description: Link_to_13_district                                   
 23   (F) Enabled   Auto/Disabled           Link Down               Enabled     
           Description:     
 24   (C) Enabled   Auto/Disabled           1000M/Full/None         Enabled     
           Description: Link-to-k9-s9                                         
 24   (F) Enabled   Auto/Disabled           Link Down               Enabled     
           Description:                                                       
 25       Enabled   Auto/Disabled           Link Down               Enabled     
           Description:                                                       
 26       Enabled   Auto/Disabled           Link Down               Enabled     
           Description:                                                       
 27       Enabled   Auto/Disabled           Link Down               Enabled     
           Description:                                                       
        
        
        

k9-s1
                                                        
                                                        
 10     Enabled   Auto/Disabled          100M/Full/None           Enabled 
        Auto    
 Desc: NAS1_mngt                                                                
                                              
 20     Enabled   Auto/Disabled          LinkDown                 Enabled 
        Auto    
 Desc: K9-S0-port24                                                             
 21     Enabled   Auto/Disabled          LinkDown                 Enabled 
        Auto    
 Desc: TV-s0.sc.int                                                             
                                                                
                                                             
 24     Enabled   Auto/Disabled          100M/Full/None           Enabled 
        Auto    
 Desc: 192.168.1.33                                    
                                                          
                                                                      
                                       
                                       
                                       
                                       
                                       k9-s0
                                       k9-s7
                                       Недоступны (им пизда?)
              

