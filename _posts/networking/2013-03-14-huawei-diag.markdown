---
layout: post
title:  "huawei-diag"
date:   2013-03-14 15:04:45 +0400
categories: Networking
tags: Networking
---

# huawei-diag
 
CTD-Z0(config)#show pvc all
  ( Interface:  Frame/Slot/Port )
  ( Port:  FE's VLAN, others port )
              Source                          Sink                   Traffic
   CID  Type    Interface    VPI  VCI  Type   Interface    VPI   VCI   RX   TX
  ----- ---- -------------- ---- ----  ---- -------------- ---- ---- ---- ----
      1  ADL 0/1/13            1   35   LAN 0/0/505          --   --    1    1
      2  ADL 0/1/1             0   33   LAN 0/0/574          --   --    1    1
      3  ADL 0/3/3             0   33   LAN 0/0/907          --   --    1    1
      4  ADL 0/1/3             0   33   LAN 0/0/3063         --   --    1    1
      5  ADL 0/1/4             2   36   LAN 0/0/502          --   --    1    1
      6  ADL 0/1/5             3   37   LAN 0/0/503          --   --    1    1
      7  ADL 0/1/6             4   38   LAN 0/0/504          --   --    1    1
      8  ADL 0/1/7             0   33   LAN 0/0/572          --   --    1    1
      9  ADL 0/1/8             0   33   LAN 0/0/561          --   --    1    1
     10  ADL 0/1/9             0   33   LAN 0/0/540          --   --    1    1
     11  ADL 0/1/10            0   33   LAN 0/0/541          --   --    1    1
     12  ADL 0/4/13            0   33   LAN 0/0/3045         --   --    1    1
     13  ADL 0/1/12            0   33   LAN 0/0/546          --   --    1    1
     14  ADL 0/1/14            2   36   LAN 0/0/539          --   --    1    1
     15  ADL 0/1/15            0   33   LAN 0/0/521          --   --    1    1
     16  ADL 0/1/16            0   33   LAN 0/0/562          --   --    1    1
     18  ADL 0/2/2             6   40   LAN 0/0/506          --   --    1    1
     19  ADL 0/2/3             0   33   LAN 0/0/3069         --   --    1    1
     20  ADL 0/2/4             2   36   LAN 0/0/532          --   --    1    1
     21  ADL 0/2/5             0   33   LAN 0/0/533          --   --    1    1
     22  ADL 0/2/6             4   32   LAN 0/0/535          --   --    1    1
     23  ADL 0/2/7             0   33   LAN 0/0/537          --   --    1    1
     24  ADL 0/2/8             7   41   LAN 0/0/536          --   --    1    1
     25  ADL 0/2/9             0   33   LAN 0/0/509          --   --    1    1
     26  ADL 0/2/10            0   33   LAN 0/0/3056         --   --    1    1
     27  ADL 0/2/11            0   33   LAN 0/0/571          --   --    1    1
     29  ADL 0/2/13            0   33   LAN 0/0/555          --   --    1    1
     30  ADL 0/2/14            0   33   LAN 0/0/573          --   --    1    1
     31  ADL 0/2/15            0   33   LAN 0/0/585          --   --    1    1
     32  ADL 0/2/16            0   33   LAN 0/0/576          --   --    1    1
     33  ADL 0/3/8             0   33   LAN 0/0/585          --   --    1    1
     34  ADL 0/3/2             2   36   LAN 0/0/512          --   --    1    1
     36  ADL 0/3/4             0   33   LAN 0/0/523          --   --    1    1
     37  ADL 0/3/5             0   33   LAN 0/0/587          --   --    1    1
     38  ADL 0/3/16            0   33   LAN 0/0/585          --   --    1    1
     39  ADL 0/3/6             0   33   LAN 0/0/586          --   --    1    1
     42  ADL 0/3/11            0   33   LAN 0/0/907          --   --    1    1
     44  ADL 0/3/12            0   33   LAN 0/0/582          --   --    1    1
     46  ADL 0/3/14            0   33   LAN 0/0/511          --   --    1    1
     47  ADL 0/3/15            0   33   LAN 0/0/508          --   --    1    1
     48  ADL 0/3/7             0   33   LAN 0/0/522          --   --    1    1
     49  ADL 0/4/1             0   33   LAN 0/0/3001         --   --    1    1
     50  ADL 0/4/16            0   33   LAN 0/0/3102         --   --    1    1
     51  ADL 0/4/3             0   33   LAN 0/0/3010         --   --    1    1
     52  ADL 0/4/4             0   33   LAN 0/0/3014         --   --    1    1
     53  ADL 0/4/5             0   33   LAN 0/0/3017         --   --    1    1
     54  ADL 0/4/6             0   33   LAN 0/0/3026         --   --    1    1
     55  ADL 0/4/7             0   33   LAN 0/0/3033         --   --    1    1
     56  ADL 0/4/8             0   33   LAN 0/0/952          --   --    1    1
     57  ADL 0/4/9             0   33   LAN 0/0/3037         --   --    1    1
     59  ADL 0/4/11            0   33   LAN 0/0/3040         --   --    1    1
     61  ADL 0/4/12            0   33   LAN 0/0/3049         --   --    1    1
     62  ADL 0/4/14            0   33   LAN 0/0/3998         --   --    1    1
     63  ADL 0/4/15            0   33   LAN 0/0/3047         --   --    1    1
     64  ADL 0/4/2             0   33   LAN 0/0/3079         --   --    1    1
  ----------------------------------------------------------------------------
  Record number: 55
 
CTD-Z0(config)# show board 0/1
  Frame   Slot   Board Type   Board State   Interface Type    PVC Number
  -----  ------  ----------  -------------  ---------------  ------------
      0       1        ADCE   Quasi-normal                -            14
  -----  ------  ----------  -------------  ---------------  ------------

  Port     State      LineProfileId  AlarmProfileId  ExtLineProfileId
  ----  ------------  -------------  --------------  ----------------
     1    Activating             8             1             -
     2    Activating            11             1             -
     3     Activated             9             1             -
     4          Fail            33             1             -
     5     Activated             9             1             -
     6    Activating             2             1             -
     7    Activating             8             1             -
     8          Fail             9             1             -
     9    Activating             8             1             -
    10     Activated             5             1             -
    11    Activating             5             1             -
    12    Activating             9             1             -
    13    Activating             9             1             -
    14    Activating             9             1             -
    15    Activating             3             1             -
    16    Activating             9             1             -
  ---------------------------------------------------------------------
 
CTD-Z0(config)#show board 0/21
  Invalid parameter:0/21
 
CTD-Z0(config)#show board 0/2 
  Frame   Slot   Board Type   Board State   Interface Type    PVC Number
  -----  ------  ----------  -------------  ---------------  ------------
      0       2        ADCE         Normal                -            14
  -----  ------  ----------  -------------  ---------------  ------------

  Port     State      LineProfileId  AlarmProfileId  ExtLineProfileId
  ----  ------------  -------------  --------------  ----------------
     1    Activating             8             1             -
     2     Activated             1             1             -
     3    Activating            33             1             -
     4    Activating            12             1             -
     5    Activating             9             1             -
     6    Activating             8             1             -
     7     Activated             8             1             -
     8    Activating             8             1             -
     9     Activated            11             1             -
    10    Activating            33             1             -
    11    Activating             4             1             -
    12    Activating             9             1             -
    13     Activated            11             1             -
    14    Activating             9             1             -
    15    Activating             9             1             -
    16    Activating            33             1             -
  ---------------------------------------------------------------------
 
CTD-Z0(config)#show board 0/32
  Invalid parameter:0/32
 
CTD-Z0(config)#show board 0/3 
  Frame   Slot   Board Type   Board State   Interface Type    PVC Number
  -----  ------  ----------  -------------  ---------------  ------------
      0       3        ADCE         Normal                -            12
  -----  ------  ----------  -------------  ---------------  ------------

  Port     State      LineProfileId  AlarmProfileId  ExtLineProfileId
  ----  ------------  -------------  --------------  ----------------
     1    Activating             9             1             -
     2    Activating             9             1             -
     3    Activating             9             1             -
     4    Activating            11             1             -
     5    Activating            11             1             -
     6    Activating             9             1             -
     7    Activating             9             1             -
     8    Activating             9             1             -
     9    Activating             8             1             -
    10    Activating            11             1             -
    11    Activating             4             1             -
    12    Activating             9             1             -
    13    Activating            14             1             -
    14    Activating             9             1             -
    15    Activating            33             1             -
    16    Activating            33             1             -
  ---------------------------------------------------------------------
 
CTD-Z0(config)#show board 0/4 
  Frame   Slot   Board Type   Board State   Interface Type    PVC Number
  -----  ------  ----------  -------------  ---------------  ------------
      0       4        ADCE         Normal                -            15
  -----  ------  ----------  -------------  ---------------  ------------

  Port     State      LineProfileId  AlarmProfileId  ExtLineProfileId
  ----  ------------  -------------  --------------  ----------------
     1    Activating             9             1             -
     2    Activating            33             1             -
     3    Activating             9             1             -
     4    Activating            11             1             -
     5     Activated            11             1             -
     6     Activated            11             1             -
     7    Activating            11             1             -
     8    Activating            11             1             -
     9    Activating             9             1             -
    10    Activating            11             1             -
    11    Activating            11             1             -
    12     Activated            33             1             -
    13     Activated            33             1             -
    14    Activating             2             1             -
    15    Activating             9             1             -
    16    Activating             1             1             -
  ---------------------------------------------------------------------











 
CTD-Z0(config-ADSL-0/4)#show line performance ? 
  Function: Show line performance statistics
  Usage   : show line performance{historic_15minutes <portid> <interval>| 
                                  last_15minutes <portid> | 
                                  current_15minutes <portid> | 
                                  last_24hours<portid>| 
                                  current_24hours<portid> | 
                                  ever_before <portid>} 
  Options : 
            historic_15minutes: historic 15 minutes statistics
            interval          : interval number
            last_15minutes    : last full 15 minutes statistics
            current_15minutes : current 15 minutes statistics
            last_24hours      : last full 24 hours statistics
            current_24hours   : current 24 hours statistics
            ever_before       : statistics since system start
            portid            : Port ID 
  e.g.    : show line performance last_15minutes 15



show line performance last_24hours 1  
















CTD-Z0(config-ADSL-0/4)#show line performance last_24hours 12
  <ATUC>
  The number of loss frame seconds                    : 0
  The number of loss of signal seconds                : 0
  The number of loss of link seconds                  : 0
  The number of loss of power seconds                 : 0
  The number of errored seconds                       : 411
  The number of line initialization attempts          : 0
  The number of fast retrain                          : 0
  The number of failed fast retrain                   : 0
  The number of severely errored seconds              : 0
  The number of unavailable seconds                   : 0
  The number of received blocks                       : 604800
  The number of transmitted blocks                    : 4924800
  The number of blocks with errors that were corrected: 4896
  The number of blocks with uncorrectable errors      : 463

  <ATUR>
  The number of loss frame seconds                    : 0
  The number of loss of signal seconds                : 0
  The number of loss of power seconds                 : 0
  The number of errored seconds                       : 9968
  The number of severely errored seconds              : 0
  The number of unavailable seconds                   : 0
  The number of received blocks                       : 4924800       
  The number of transmitted blocks                    : 604800
  The number of blocks with errors that were corrected: 60327609
  The number of blocks with uncorrectable errors      : 80845







 
CTD-Z0(config-ADSL-0/4)#show line performance last_24hours 13
  <ATUC>
  The number of loss frame seconds                    : 0
  The number of loss of signal seconds                : 0
  The number of loss of link seconds                  : 0
  The number of loss of power seconds                 : 0
  The number of errored seconds                       : 94
  The number of line initialization attempts          : 0
  The number of fast retrain                          : 0
  The number of failed fast retrain                   : 0
  The number of severely errored seconds              : 0
  The number of unavailable seconds                   : 0
  The number of received blocks                       : 345600
  The number of transmitted blocks                    : 4924800
  The number of blocks with errors that were corrected: 497
  The number of blocks with uncorrectable errors      : 96

  <ATUR>
  The number of loss frame seconds                    : 0
  The number of loss of signal seconds                : 0
  The number of loss of power seconds                 : 0
  The number of errored seconds                       : 2299
  The number of severely errored seconds              : 0
  The number of unavailable seconds                   : 0
  The number of received blocks                       : 4924800       
  The number of transmitted blocks                    : 345600
  The number of blocks with errors that were corrected: 88467096
  The number of blocks with uncorrectable errors      : 3056








CTD-Z0(config-ADSL-0/4)#show line operation 12
  Current line Operating Mode                            : G992.5-Annex M
  Channel mode                                           : Interleaved
  Downstream channel bit swap                            : Enable
  Upstream channel bit swap                              : Enable
  Downstream channel rate(Kbps)                          : 7659
  Upstream channel rate(Kbps)                            : 2176
  Downstream channel noise margin(dB)                    : 6.0
  Upstream channel noise margin(dB)                      : 5.5
  Downstream channel attenuation(dB)                     : 44.2
  Upstream channel attenuation(dB)                       : 19.5
  Downstream interleaved channel delay(ms)               : 15
  Upstream interleaved channel delay(ms)                 : 3
  Downstream max attainable rate(Kbps)                   : 8624
  Upstream max attainable rate(Kbps)                     : 2274
  Downstream output power(dBm)                           : 20.3
  Upstream output power(dBm)                             : 15.3
 









#show line rate-threshold all  
   Port  UpRate Threshold(Kbps)  DwRate Threshold(Kbps)
  -----  ----------------------  ----------------------
      1                       0                       0
      2                       0                       0
      3                       0                       0
      4                       0                       0
      5                       0                       0
      6                       0                       0
      7                       0                       0
      8                       0                       0
      9                       0                       0
     10                       0                       0
     11                       0                       0
     12                       0                       0
     13                       0                       0
     14                       0                       0
     15                       0                       0
     16                       0                       0
  -----------------------------------------------------






















Подозрительный порт




CTD-Z0(config-ADSL-0/2)#show line performance last_24hours 2
  <ATUC>
  The number of loss frame seconds                    : 7
  The number of loss of signal seconds                : 7
  The number of loss of link seconds                  : 0
  The number of loss of power seconds                 : 0
  The number of errored seconds                       : 93
  The number of line initialization attempts          : 2
  The number of fast retrain                          : 0
  The number of failed fast retrain                   : 0
  The number of severely errored seconds              : 7
  The number of unavailable seconds                   : 331
  The number of received blocks                       : 5078248
  The number of transmitted blocks                    : 5078248
  The number of blocks with errors that were corrected: 2336
  The number of blocks with uncorrectable errors      : 658

  <ATUR>
  The number of loss frame seconds                    : 4
  The number of loss of signal seconds                : 1
  The number of loss of power seconds                 : 8
  The number of errored seconds                       : 1628
  The number of severely errored seconds              : 9
  The number of unavailable seconds                   : 0
  The number of received blocks                       : 5078248       
  The number of transmitted blocks                    : 5078248
  The number of blocks with errors that were corrected: 1809631
  The number of blocks with uncorrectable errors      : 2565




 
CTD-Z0(config-ADSL-0/2)#show line performance last_24hours 9
  <ATUC>
  The number of loss frame seconds                    : 4
  The number of loss of signal seconds                : 4
  The number of loss of link seconds                  : 0
  The number of loss of power seconds                 : 0
  The number of errored seconds                       : 0
  The number of line initialization attempts          : 1
  The number of fast retrain                          : 0
  The number of failed fast retrain                   : 0
  The number of severely errored seconds              : 4
  The number of unavailable seconds                   : 31
  The number of received blocks                       : 5095771
  The number of transmitted blocks                    : 5095771
  The number of blocks with errors that were corrected: 246
  The number of blocks with uncorrectable errors      : 247

  <ATUR>
  The number of loss frame seconds                    : 2
  The number of loss of signal seconds                : 3
  The number of loss of power seconds                 : 83845
  The number of errored seconds                       : 0
  The number of severely errored seconds              : 0
  The number of unavailable seconds                   : 86367
  The number of received blocks                       : 5095771       
  The number of transmitted blocks                    : 5095771
  The number of blocks with errors that were corrected: 3
  The number of blocks with uncorrectable errors      : 1
 
CTD-Z0(config-ADSL-0/2)#





En
conf t
interface lan 0/0


> Password (<20 chars):

CTD-Z0>enable

CTD-Z0#configure terminal

CTD-Z0(config)#interface lan0/0
  Incorrect command:interface lan0/0

CTD-Z0(config)#interface ?
  -----------------------------------------------
        Mode [Config Mode], Next Command Word
  -----------------------------------------------

  adsl              Enter the ADSL configuration mode
  esc               Enter the esc mode
  lan               Enter the LAN configuration mode
  shdsl             Enter the SHDSL configuration mode

CTD-Z0(config)#interface lan0/0
  Incorrect command:interface lan0/0

CTD-Z0(config)#interface lan0
  Incorrect command:interface lan0

CTD-Z0(config)#interface lan 0/0

CTD-Z0(config-LAN-0/0)#vlan
<vlanId>{2-4095}:581
{common,stacking}:common
  Add VLAN successfully, VLANID = 581.

CTD-Z0(config-LAN-0/0)#

CTD-Z0(config-LAN-0/0)#exit

CTD-Z0(config)#interface adsl 0/3

CTD-Z0(config-ADSL-0/3)#deactivate 11
  Deactive command send successfully.

  2010/01/22 16:18:47 warn   ADSL: Port deactivated(0/3/11)
CTD-Z0(config-ADSL-0/3)#activate 11 9
  Active command send successfully.

  2010/01/22 16:19:11 warn   ADSL: Port activating(0/3/11)

CTD-Z0(config-ADSL-0/3)#deactivate 11
  Deactive command send successfully.

  2010/01/22 16:18:47 warn   ADSL: Port deactivated(0/3/11)
CTD-Z0(config-ADSL-0/3)#activate 11 9
  Active command send successfully.

  2010/01/22 16:19:11 warn   ADSL: Port activating(0/3/11)
CTD-Z0(config-ADSL-0/3)#exit


CTD-Z0(config)#pvc adsl 0/3/11 0 33
{adsl,shdsl,lan}:lan
<FrameId/SlotId>{(0)/(0)}:0/0
<vlanId>{1-4095}:581
<priority>{0-7}:
  Invalid value : [VALUE(priority) = ], Invalid parameter value data.

CTD-Z0(config)#pvc adsl 0/3/11 0 33 lan 0/0 581
<priority>{0-7}:0
{disable,innerVlanID}:disable
<rx-car>{on,off}:off
<tx-car>{on,off}:off
<rx-cttr>{1-20}:1
<tx-cttr>{1-20}:1
  Add PVC successfully, CID = 42.

CTD-Z0(config)#pvc adsl 0/3/11 0 33 lan 0/0 581 0 disable off off 1 1


CTD-Z0(config)#save
  System data have been changed.
  Do you want to save data to FLASH







CTD-Z0(config)#show pvc all                               
  ( Interface:  Frame/Slot/Port )                         
  ( Port:  FE's VLAN, others port )                       
              Source                          Sink                   Traffic
   CID  Type    Interface    VPI  VCI  Type   Interface    VPI   VCI   RX   TX
  ----- ---- -------------- ---- ----  ---- -------------- ---- ---- ---- ----
      1  ADL 0/1/13            1   35   LAN 0/0/505          --   --    1    1
      2  ADL 0/1/1             0   33   LAN 0/0/574          --   --    1    1
      3  ADL 0/1/2             0   33   LAN 0/0/524          --   --    1    1
      4  ADL 0/1/3             0   33   LAN 0/0/557          --   --    1    1
      5  ADL 0/1/4             2   36   LAN 0/0/502          --   --    1    1
      6  ADL 0/1/5             3   37   LAN 0/0/503          --   --    1    1
      7  ADL 0/1/6             4   38   LAN 0/0/504          --   --    1    1
      8  ADL 0/1/7             0   33   LAN 0/0/572          --   --    1    1
      9  ADL 0/1/8             0   33   LAN 0/0/561          --   --    1    1
     10  ADL 0/1/9             0   33   LAN 0/0/540          --   --    1    1
     11  ADL 0/1/10            0   33   LAN 0/0/541          --   --    1    1
     12  ADL 0/1/11            0   33   LAN 0/0/543          --   --    1    1
     13  ADL 0/1/12            0   33   LAN 0/0/546          --   --    1    1
     14  ADL 0/1/14            2   36   LAN 0/0/539          --   --    1    1
     15  ADL 0/1/15            0   33   LAN 0/0/521          --   --    1    1
     16  ADL 0/1/16            0   33   LAN 0/0/562          --   --    1    1
     17  ADL 0/2/1             0   33   LAN 0/0/558          --   --    1    1
     18  ADL 0/2/2             6   40   LAN 0/0/506          --   --    1    1
     19  ADL 0/2/3             8   35   LAN 0/0/529          --   --    1    1
     20  ADL 0/2/4             2   36   LAN 0/0/532          --   --    1    1
     21  ADL 0/2/5             0   33   LAN 0/0/533          --   --    1    1
     22  ADL 0/2/6             4   32   LAN 0/0/535          --   --    1    1
     23  ADL 0/2/7             5   39   LAN 0/0/537          --   --    1    1
     24  ADL 0/2/8             7   41   LAN 0/0/536          --   --    1    1
     25  ADL 0/2/9             0   33   LAN 0/0/509          --   --    1    1
     26  ADL 0/2/10            0   33   LAN 0/0/570          --   --    1    1
     27  ADL 0/2/11            0   33   LAN 0/0/571          --   --    1    1
     28  ADL 0/2/12            0   33   LAN 0/0/547          --   --    1    1
     29  ADL 0/2/13            0   33   LAN 0/0/555          --   --    1    1
     30  ADL 0/2/14            0   33   LAN 0/0/573          --   --    1    1
     31  ADL 0/2/15            0   33   LAN 0/0/575          --   --    1    1
     32  ADL 0/2/16            0   33   LAN 0/0/576          --   --    1    1
     33  ADL 0/3/1             0   33   LAN 0/0/501          --   --    1    1
     34  ADL 0/3/2             2   36   LAN 0/0/512          --   --    1    1
     35  ADL 0/3/3             5   39   LAN 0/0/515          --   --    1    1
     36  ADL 0/3/4             0   33   LAN 0/0/523          --   --    1    1
     37  ADL 0/3/5             6   40   LAN 0/0/516          --   --    1    1
     38  ADL 0/3/6             8   42   LAN 0/0/518          --   --    1    1
     39  ADL 0/3/7             0   33   LAN 0/0/549          --   --    1    1
     40  ADL 0/3/8             0   33   LAN 0/0/551          --   --    1    1
     41  ADL 0/3/9             0   33   LAN 0/0/552          --   --    1    1
     43  ADL 0/3/10            0   33   LAN 0/0/580          --   --    1    1
  ----------------------------------------------------------------------------
  Record number: 42                                                           
                                                                              



no pvc cid 4


show line operation 1


Определение скорости профайлов 
show adsl line-profile 

[https://docs.google.com/folder/d/0B6wW18mYskvBMDc2MWM5ZTYtNjZiMC00ZDE3LWExZjktYzEyYjI3OTI4MDFh/edit?pli=1&docId=0B6wW18mYskvBMHJiVFFmZ1I3Mjg](https://docs.google.com/folder/d/0B6wW18mYskvBMDc2MWM5ZTYtNjZiMC00ZDE3LWExZjktYzEyYjI3OTI4MDFh/edit?pli=1&docId=0B6wW18mYskvBMHJiVFFmZ1I3Mjg)
[http://vialovo.maxopka.su/hardware/7-ma5605](http://vialovo.maxopka.su/hardware/7-ma5605)

Китайская компания Huawei выпускает dslam'ы MA5605

Dslam'ы расширяемые, в начальной конфигурации - 16 портов.

Иногда клиенты жалуются на частые разрывы соединения с Интернет.

Причиной могут быть как вирусы, так и проблемы с телефонной линией от абонента до АТС.

MA5605 не имеет web-интерфейса. Взаимодействие с пользователем осуществляется при помощи командной строки.

Для того чтобы посмотреть параметры линии с dslam'а, необходимо сделать следующее:

Пуск->Выполнить

В появившемся окне набрать 'cmd' (без апострофов)

Появится окно командной строки.

Далее приведен пример с комментариями.

telnet <ip адрес dslam>

Huawei MA5605 Multi-service Access Module.

 

Copyright(C) 1998-2006 by Huawei Technologies Co., Ltd.

Current time is Sun  22:18:27, 2011/05/01.

> User name (<20 chars): root // По умолчанию root

> Password (<20 chars): // По умолчанию admin

MA5605>enable

MA5605#configure terminal

MA5605(config)#interface adsl 0/1 // Здесь 0/1 означает, что порт находится на модуле 1

// т. е. если порт находится на модуле 2 то следует ввести 0/2

MA5605(config-ADSL-0/1)#show line operation 1 // Здесь 1 - номер порта на модуле.

Current line Operating Mode                            : G992.3-Annex M // Режим модуляции

Channel mode                                           : Interleaved

Downstream channel bit swap                            : Disable

Upstream channel bit swap                              : Disable

Downstream channel rate(Kbps)                          : 1022 // Текущая скорость нисходящего потока

Upstream channel rate(Kbps)                            : 248 // Текущая скорость восходящего потока

Downstream channel noise margin(dB)                    : 14.1 // Соотношение сигнал/шум в нисходящем потоке

Upstream channel noise margin(dB)                      : 25.5 // Соотношение сигнал/шум в восходящем потоке

Downstream channel attenuation(dB)                     : 61.0 // Затухание сигнала в нисходящем потоке

Upstream channel attenuation(dB)                       : 36.5 // Затухание сигнала в восходящем потоке

Downstream interleaved channel delay(ms)               : 5

Upstream interleaved channel delay(ms)                 : 3

Downstream max attainable rate(Kbps)                   : 2880 // Максимальная скорость достижимая в нисходящем потоке

Upstream max attainable rate(Kbps)                     : 1010 // Максимальная скорость достижимая в восходящем потоке

Downstream output power(dBm)                           : 17.4 // Выходная мощность нисходящего потока

Upstream output power(dBm)                             : 12.8 // Выходная мощность восходящего потока

Стоит отметить, что разрывы соединения, чаще всего, обусловлены низким значением параметра  channel noise margin
(соотношение сигнал/шум) - меньше 7-ми дБ,

 

Для того чтобы увеличить значение этого параметра, нужно избегать скруток, неизолированных участков телефонного кабеля, использования "лапши" при прокладке линии в помещении. Если скрутки все же неизбежны, то провода в них нужно тщательно зачистить, а также пропаять и заизолировать место скрутки.
 
CTD-Z0(config)#show pvc all
  ( Interface:  Frame/Slot/Port )
  ( Port:  FE's VLAN, others port )
              Source                          Sink                   Traffic
   CID  Type    Interface    VPI  VCI  Type   Interface    VPI   VCI   RX   TX
  ----- ---- -------------- ---- ----  ---- -------------- ---- ---- ---- ----
      1  ADL 0/1/13            1   35   LAN 0/0/505          --   --    1    1
      2  ADL 0/1/1             0   33   LAN 0/0/574          --   --    1    1
      3  ADL 0/3/3             0   33   LAN 0/0/907          --   --    1    1
      4  ADL 0/1/3             0   33   LAN 0/0/3063         --   --    1    1
      5  ADL 0/1/4             2   36   LAN 0/0/502          --   --    1    1
      6  ADL 0/1/5             3   37   LAN 0/0/503          --   --    1    1
      7  ADL 0/1/6             4   38   LAN 0/0/504          --   --    1    1
      8  ADL 0/1/7             0   33   LAN 0/0/572          --   --    1    1
      9  ADL 0/1/8             0   33   LAN 0/0/561          --   --    1    1
     10  ADL 0/1/9             0   33   LAN 0/0/540          --   --    1    1
     11  ADL 0/1/10            0   33   LAN 0/0/541          --   --    1    1
     12  ADL 0/4/13            0   33   LAN 0/0/3045         --   --    1    1
     13  ADL 0/1/12            0   33   LAN 0/0/546          --   --    1    1
     14  ADL 0/1/14            2   36   LAN 0/0/539          --   --    1    1
     15  ADL 0/1/15            0   33   LAN 0/0/521          --   --    1    1
     16  ADL 0/1/16            0   33   LAN 0/0/562          --   --    1    1
     18  ADL 0/2/2             6   40   LAN 0/0/506          --   --    1    1
     19  ADL 0/2/3             0   33   LAN 0/0/3069         --   --    1    1
     20  ADL 0/2/4             2   36   LAN 0/0/532          --   --    1    1
     21  ADL 0/2/5             0   33   LAN 0/0/533          --   --    1    1
     22  ADL 0/2/6             4   32   LAN 0/0/535          --   --    1    1
     23  ADL 0/2/7             0   33   LAN 0/0/537          --   --    1    1
     24  ADL 0/2/8             7   41   LAN 0/0/536          --   --    1    1
     25  ADL 0/2/9             0   33   LAN 0/0/509          --   --    1    1
     26  ADL 0/2/10            0   33   LAN 0/0/3056         --   --    1    1
     27  ADL 0/2/11            0   33   LAN 0/0/571          --   --    1    1
     29  ADL 0/2/13            0   33   LAN 0/0/555          --   --    1    1
     30  ADL 0/2/14            0   33   LAN 0/0/573          --   --    1    1
     31  ADL 0/2/15            0   33   LAN 0/0/585          --   --    1    1
     32  ADL 0/2/16            0   33   LAN 0/0/576          --   --    1    1
     33  ADL 0/3/8             0   33   LAN 0/0/585          --   --    1    1
     34  ADL 0/3/2             2   36   LAN 0/0/512          --   --    1    1
     36  ADL 0/3/4             0   33   LAN 0/0/523          --   --    1    1
     37  ADL 0/3/5             0   33   LAN 0/0/587          --   --    1    1
     38  ADL 0/3/16            0   33   LAN 0/0/585          --   --    1    1
     39  ADL 0/3/6             0   33   LAN 0/0/586          --   --    1    1
     42  ADL 0/3/11            0   33   LAN 0/0/907          --   --    1    1
     44  ADL 0/3/12            0   33   LAN 0/0/582          --   --    1    1
     46  ADL 0/3/14            0   33   LAN 0/0/511          --   --    1    1
     47  ADL 0/3/15            0   33   LAN 0/0/508          --   --    1    1
     48  ADL 0/3/7             0   33   LAN 0/0/522          --   --    1    1
     49  ADL 0/4/1             0   33   LAN 0/0/3001         --   --    1    1
     50  ADL 0/4/16            0   33   LAN 0/0/3102         --   --    1    1
     51  ADL 0/4/3             0   33   LAN 0/0/3010         --   --    1    1
     52  ADL 0/4/4             0   33   LAN 0/0/3014         --   --    1    1
     53  ADL 0/4/5             0   33   LAN 0/0/3017         --   --    1    1
     54  ADL 0/4/6             0   33   LAN 0/0/3026         --   --    1    1
     55  ADL 0/4/7             0   33   LAN 0/0/3033         --   --    1    1
     56  ADL 0/4/8             0   33   LAN 0/0/952          --   --    1    1
     57  ADL 0/4/9             0   33   LAN 0/0/3037         --   --    1    1
     59  ADL 0/4/11            0   33   LAN 0/0/3040         --   --    1    1
     61  ADL 0/4/12            0   33   LAN 0/0/3049         --   --    1    1
     62  ADL 0/4/14            0   33   LAN 0/0/3998         --   --    1    1
     63  ADL 0/4/15            0   33   LAN 0/0/3047         --   --    1    1
     64  ADL 0/4/2             0   33   LAN 0/0/3079         --   --    1    1
  ----------------------------------------------------------------------------
  Record number: 55
 
CTD-Z0(config)# show board 0/1
  Frame   Slot   Board Type   Board State   Interface Type    PVC Number
  -----  ------  ----------  -------------  ---------------  ------------
      0       1        ADCE   Quasi-normal                -            14
  -----  ------  ----------  -------------  ---------------  ------------

  Port     State      LineProfileId  AlarmProfileId  ExtLineProfileId
  ----  ------------  -------------  --------------  ----------------
     1    Activating             8             1             -
     2    Activating            11             1             -
     3     Activated             9             1             -
     4          Fail            33             1             -
     5     Activated             9             1             -
     6    Activating             2             1             -
     7    Activating             8             1             -
     8          Fail             9             1             -
     9    Activating             8             1             -
    10     Activated             5             1             -
    11    Activating             5             1             -
    12    Activating             9             1             -
    13    Activating             9             1             -
    14    Activating             9             1             -
    15    Activating             3             1             -
    16    Activating             9             1             -
  ---------------------------------------------------------------------
 
CTD-Z0(config)#show board 0/21
  Invalid parameter:0/21
 
CTD-Z0(config)#show board 0/2 
  Frame   Slot   Board Type   Board State   Interface Type    PVC Number
  -----  ------  ----------  -------------  ---------------  ------------
      0       2        ADCE         Normal                -            14
  -----  ------  ----------  -------------  ---------------  ------------

  Port     State      LineProfileId  AlarmProfileId  ExtLineProfileId
  ----  ------------  -------------  --------------  ----------------
     1    Activating             8             1             -
     2     Activated             1             1             -
     3    Activating            33             1             -
     4    Activating            12             1             -
     5    Activating             9             1             -
     6    Activating             8             1             -
     7     Activated             8             1             -
     8    Activating             8             1             -
     9     Activated            11             1             -
    10    Activating            33             1             -
    11    Activating             4             1             -
    12    Activating             9             1             -
    13     Activated            11             1             -
    14    Activating             9             1             -
    15    Activating             9             1             -
    16    Activating            33             1             -
  ---------------------------------------------------------------------
 
CTD-Z0(config)#show board 0/32
  Invalid parameter:0/32
 
CTD-Z0(config)#show board 0/3 
  Frame   Slot   Board Type   Board State   Interface Type    PVC Number
  -----  ------  ----------  -------------  ---------------  ------------
      0       3        ADCE         Normal                -            12
  -----  ------  ----------  -------------  ---------------  ------------

  Port     State      LineProfileId  AlarmProfileId  ExtLineProfileId
  ----  ------------  -------------  --------------  ----------------
     1    Activating             9             1             -
     2    Activating             9             1             -
     3    Activating             9             1             -
     4    Activating            11             1             -
     5    Activating            11             1             -
     6    Activating             9             1             -
     7    Activating             9             1             -
     8    Activating             9             1             -
     9    Activating             8             1             -
    10    Activating            11             1             -
    11    Activating             4             1             -
    12    Activating             9             1             -
    13    Activating            14             1             -
    14    Activating             9             1             -
    15    Activating            33             1             -
    16    Activating            33             1             -
  ---------------------------------------------------------------------
 
CTD-Z0(config)#show board 0/4 
  Frame   Slot   Board Type   Board State   Interface Type    PVC Number
  -----  ------  ----------  -------------  ---------------  ------------
      0       4        ADCE         Normal                -            15
  -----  ------  ----------  -------------  ---------------  ------------

  Port     State      LineProfileId  AlarmProfileId  ExtLineProfileId
  ----  ------------  -------------  --------------  ----------------
     1    Activating             9             1             -
     2    Activating            33             1             -
     3    Activating             9             1             -
     4    Activating            11             1             -
     5     Activated            11             1             -
     6     Activated            11             1             -
     7    Activating            11             1             -
     8    Activating            11             1             -
     9    Activating             9             1             -
    10    Activating            11             1             -
    11    Activating            11             1             -
    12     Activated            33             1             -
    13     Activated            33             1             -
    14    Activating             2             1             -
    15    Activating             9             1             -
    16    Activating             1             1             -
  ---------------------------------------------------------------------











 
CTD-Z0(config-ADSL-0/4)#show line performance ? 
  Function: Show line performance statistics
  Usage   : show line performance{historic_15minutes <portid> <interval>| 
                                  last_15minutes <portid> | 
                                  current_15minutes <portid> | 
                                  last_24hours<portid>| 
                                  current_24hours<portid> | 
                                  ever_before <portid>} 
  Options : 
            historic_15minutes: historic 15 minutes statistics
            interval          : interval number
            last_15minutes    : last full 15 minutes statistics
            current_15minutes : current 15 minutes statistics
            last_24hours      : last full 24 hours statistics
            current_24hours   : current 24 hours statistics
            ever_before       : statistics since system start
            portid            : Port ID 
  e.g.    : show line performance last_15minutes 15



show line performance last_24hours 1  
















CTD-Z0(config-ADSL-0/4)#show line performance last_24hours 12
  <ATUC>
  The number of loss frame seconds                    : 0
  The number of loss of signal seconds                : 0
  The number of loss of link seconds                  : 0
  The number of loss of power seconds                 : 0
  The number of errored seconds                       : 411
  The number of line initialization attempts          : 0
  The number of fast retrain                          : 0
  The number of failed fast retrain                   : 0
  The number of severely errored seconds              : 0
  The number of unavailable seconds                   : 0
  The number of received blocks                       : 604800
  The number of transmitted blocks                    : 4924800
  The number of blocks with errors that were corrected: 4896
  The number of blocks with uncorrectable errors      : 463

  <ATUR>
  The number of loss frame seconds                    : 0
  The number of loss of signal seconds                : 0
  The number of loss of power seconds                 : 0
  The number of errored seconds                       : 9968
  The number of severely errored seconds              : 0
  The number of unavailable seconds                   : 0
  The number of received blocks                       : 4924800       
  The number of transmitted blocks                    : 604800
  The number of blocks with errors that were corrected: 60327609
  The number of blocks with uncorrectable errors      : 80845







 
CTD-Z0(config-ADSL-0/4)#show line performance last_24hours 13
  <ATUC>
  The number of loss frame seconds                    : 0
  The number of loss of signal seconds                : 0
  The number of loss of link seconds                  : 0
  The number of loss of power seconds                 : 0
  The number of errored seconds                       : 94
  The number of line initialization attempts          : 0
  The number of fast retrain                          : 0
  The number of failed fast retrain                   : 0
  The number of severely errored seconds              : 0
  The number of unavailable seconds                   : 0
  The number of received blocks                       : 345600
  The number of transmitted blocks                    : 4924800
  The number of blocks with errors that were corrected: 497
  The number of blocks with uncorrectable errors      : 96

  <ATUR>
  The number of loss frame seconds                    : 0
  The number of loss of signal seconds                : 0
  The number of loss of power seconds                 : 0
  The number of errored seconds                       : 2299
  The number of severely errored seconds              : 0
  The number of unavailable seconds                   : 0
  The number of received blocks                       : 4924800       
  The number of transmitted blocks                    : 345600
  The number of blocks with errors that were corrected: 88467096
  The number of blocks with uncorrectable errors      : 3056








CTD-Z0(config-ADSL-0/4)#show line operation 12
  Current line Operating Mode                            : G992.5-Annex M
  Channel mode                                           : Interleaved
  Downstream channel bit swap                            : Enable
  Upstream channel bit swap                              : Enable
  Downstream channel rate(Kbps)                          : 7659
  Upstream channel rate(Kbps)                            : 2176
  Downstream channel noise margin(dB)                    : 6.0
  Upstream channel noise margin(dB)                      : 5.5
  Downstream channel attenuation(dB)                     : 44.2
  Upstream channel attenuation(dB)                       : 19.5
  Downstream interleaved channel delay(ms)               : 15
  Upstream interleaved channel delay(ms)                 : 3
  Downstream max attainable rate(Kbps)                   : 8624
  Upstream max attainable rate(Kbps)                     : 2274
  Downstream output power(dBm)                           : 20.3
  Upstream output power(dBm)                             : 15.3
 









#show line rate-threshold all  
   Port  UpRate Threshold(Kbps)  DwRate Threshold(Kbps)
  -----  ----------------------  ----------------------
      1                       0                       0
      2                       0                       0
      3                       0                       0
      4                       0                       0
      5                       0                       0
      6                       0                       0
      7                       0                       0
      8                       0                       0
      9                       0                       0
     10                       0                       0
     11                       0                       0
     12                       0                       0
     13                       0                       0
     14                       0                       0
     15                       0                       0
     16                       0                       0
  -----------------------------------------------------






















Подозрительный порт




CTD-Z0(config-ADSL-0/2)#show line performance last_24hours 2
  <ATUC>
  The number of loss frame seconds                    : 7
  The number of loss of signal seconds                : 7
  The number of loss of link seconds                  : 0
  The number of loss of power seconds                 : 0
  The number of errored seconds                       : 93
  The number of line initialization attempts          : 2
  The number of fast retrain                          : 0
  The number of failed fast retrain                   : 0
  The number of severely errored seconds              : 7
  The number of unavailable seconds                   : 331
  The number of received blocks                       : 5078248
  The number of transmitted blocks                    : 5078248
  The number of blocks with errors that were corrected: 2336
  The number of blocks with uncorrectable errors      : 658

  <ATUR>
  The number of loss frame seconds                    : 4
  The number of loss of signal seconds                : 1
  The number of loss of power seconds                 : 8
  The number of errored seconds                       : 1628
  The number of severely errored seconds              : 9
  The number of unavailable seconds                   : 0
  The number of received blocks                       : 5078248       
  The number of transmitted blocks                    : 5078248
  The number of blocks with errors that were corrected: 1809631
  The number of blocks with uncorrectable errors      : 2565




 
CTD-Z0(config-ADSL-0/2)#show line performance last_24hours 9
  <ATUC>
  The number of loss frame seconds                    : 4
  The number of loss of signal seconds                : 4
  The number of loss of link seconds                  : 0
  The number of loss of power seconds                 : 0
  The number of errored seconds                       : 0
  The number of line initialization attempts          : 1
  The number of fast retrain                          : 0
  The number of failed fast retrain                   : 0
  The number of severely errored seconds              : 4
  The number of unavailable seconds                   : 31
  The number of received blocks                       : 5095771
  The number of transmitted blocks                    : 5095771
  The number of blocks with errors that were corrected: 246
  The number of blocks with uncorrectable errors      : 247

  <ATUR>
  The number of loss frame seconds                    : 2
  The number of loss of signal seconds                : 3
  The number of loss of power seconds                 : 83845
  The number of errored seconds                       : 0
  The number of severely errored seconds              : 0
  The number of unavailable seconds                   : 86367
  The number of received blocks                       : 5095771       
  The number of transmitted blocks                    : 5095771
  The number of blocks with errors that were corrected: 3
  The number of blocks with uncorrectable errors      : 1
 
CTD-Z0(config-ADSL-0/2)#






Данную проверку можно произвести, удостоверившись в наличии mac-адреса компьютера абонента на Ethernet-порту DSLAM’а. Для этого необходимо выдать команды следующего вида:
Azov_c2950(config)# int lan0/0
Azov_c2950(config)# show mac-pvc port 0/1/2




[http://www.mrt.sura.ru/service/huawei-ma5605.html](http://www.mrt.sura.ru/service/huawei-ma5605.html)
[https://any-key.net/adsl-line-parameters/](https://any-key.net/adsl-line-parameters/)
