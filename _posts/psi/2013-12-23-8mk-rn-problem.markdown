---
layout: post
title:  "8mk-rn-problem"
date:   2013-12-23 08:34:48 +0400
categories: PSI
tags: PSI
---

# 8mk-rn-problem
Mar 22 11:27:11 81.20.204.41 1444: .Mar 22 11:27:05: %SYS-4-CHUNKSIBLINGSEXCEED:
 Number of siblings in a chunk has gone above the threshold. Threshold:10000 Sibling-Count:25336 Chunk:0x30CDDCAC 
Name:NAT Fragment0 C -Process= "Chunk Manager", ipl= 4, pid= 1                                                          
Mar 22 11:27:11 81.20.204.41 1445: -Traceback= 23B5F24Cz 23B5F230z   


Mar 22 11:26:47 81.20.204.41 1439: .Mar 22 11:26:45: %SYS-4-CHUNKSIBLINGSEXCEED: Number of siblings in a chunk has gone above the threshold. 
Threshold:10000 Sibling-Count:25255 Chunk:0x30CDDCAC Name:NAT Fragment0 C -Process= "Chunk Manager", ipl= 4, pid= 1





ROM: System Bootstrap, Version 15.0(1r)M15, RELEASE SOFTWARE (fc1)






Error Message     

%SYS-4-CHUNKSIBLINGSEXCEED : Number of siblings in a chunk has gone above the threshold. Threshold:%d Sibling-Count:%d Chunk:0x%x Name:%s

Explanation    Number of siblings in a chunk with no header has gone above the default/configured threshold (configured using memory chunk siblings threshold count) which may lead to high cpu utilization/CPUHOG while freeing the chunk.

Recommended Action    Copy the message exactly as it appears on the console or in the system log. Research and attempt to resolve the issue using the tools and utilities provided at [http://www.cisco.com/tac.](http://www.cisco.com/tac.) With some messages, these tools and utilities will supply clarifying information. Search for resolved software issues using the Bug Toolkit at [http://www.cisco.com/pcgi-bin/Support/Bugtool/launch_bugtool.pl.](http://www.cisco.com/pcgi-bin/Support/Bugtool/launch_bugtool.pl.) If you still require assistance, open a case with the Technical Assistance Center via the Internet at [http://tools.cisco.com/ServiceRequestTool/create/](http://tools.cisco.com/ServiceRequestTool/create/), or contact your Cisco technical support representative and provide the representative with the information that you have gathered. Attach the following information to your case in nonzipped, plain-text (.txt) format: the output of the show logging and show tech-support commands and your pertinent troubleshooting logs. 