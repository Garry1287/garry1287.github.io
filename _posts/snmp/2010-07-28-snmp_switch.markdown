---
layout: post
title:  "snmp_switch"
date:   2010-07-28 10:43:27 +0400
categories: snmp
tags: snmp
---

# snmp_switch
MES

snmp-server get-community HKeGeUfo 
snmp-server set-community SFgJZAc2 



3200

delete snmp community public
delete snmp community private
delete snmp user initial
delete snmp group initial
delete snmp view restricted all
delete snmp view CommunityView all
delete snmp group public
delete snmp group private
delete snmp group ReadGroup                                                    
delete snmp group WriteGroup
create snmp view restricted 1.3.6.1.2.1.1 view_type included
create snmp view restricted 1.3.6.1.2.1.11 view_type included
create snmp view restricted 1.3.6.1.6.3.10.2.1 view_type included
create snmp view restricted 1.3.6.1.6.3.11.2.1 view_type included
create snmp view restricted 1.3.6.1.6.3.15.1.1 view_type included
create snmp view CommunityView 1 view_type included
create snmp view CommunityView 1.3.6.1.6.3 view_type excluded
create snmp view CommunityView 1.3.6.1.6.3.1 view_type included
create snmp group initial v3  noauth_nopriv read_view restricted notify_view restricted 
create snmp group HKeGeUfo v1 read_view CommunityView write_view CommunityView notify_view CommunityView 
create snmp group HKeGeUfo v2c read_view CommunityView write_view CommunityView notify_view CommunityView 
create snmp group SFgJZAc2 v1 read_view CommunityView notify_view CommunityView 
create snmp group SFgJZAc2 v2c read_view CommunityView notify_view CommunityView 
create snmp group ReadGroup v1 read_view CommunityView notify_view CommunityView 
create snmp group ReadGroup v2c read_view CommunityView notify_view CommunityView 
create snmp group WriteGroup v1 read_view CommunityView write_view CommunityView notify_view CommunityView 
create snmp group WriteGroup v2c read_view CommunityView write_view CommunityView notify_view CommunityView 
create snmp community HKeGeUfo view CommunityView read_write
create snmp community SFgJZAc2 view CommunityView read_only
create snmp user initial initial 
disable community_encryption








1210

enable snmp
delete snmp community public
delete snmp community private
disable community_encryption
create snmp user ReadOnly ReadOnly v1
create snmp user ReadOnly ReadOnly v2c
create snmp user ReadWrite ReadWrite v1
create snmp user ReadWrite ReadWrite v2c
create snmp group initial v3 noauth_nopriv read_view restricted notify_view restricted
create snmp group HKeGeUfo v1 read_view CommunityView write_view CommunityView notify_view CommunityView
create snmp group HKeGeUfo v2c read_view CommunityView write_view CommunityView notify_view CommunityView
create snmp group ReadOnly v1 read_view ReadWrite notify_view ReadWrite
create snmp group ReadOnly v2c read_view ReadWrite notify_view ReadWrite
create snmp group SFgJZAc2 v1 read_view CommunityView notify_view CommunityView
create snmp group SFgJZAc2 v2c read_view CommunityView notify_view CommunityView
create snmp group ReadGroup v1 read_view CommunityView notify_view CommunityView
create snmp group ReadGroup v2c read_view CommunityView notify_view CommunityView
create snmp group ReadWrite v1 read_view ReadWrite write_view ReadWrite notify_view ReadWrite
create snmp group ReadWrite v2c read_view ReadWrite write_view ReadWrite notify_view ReadWrite
create snmp group WriteGroup v1 read_view CommunityView write_view CommunityView notify_view CommunityView
create snmp group WriteGroup v2c read_view CommunityView write_view CommunityView notify_view CommunityView
create snmp view ReadWrite 1 1 view_type included
create snmp community HKeGeUfo ReadWrite
create snmp community SFgJZAc2 ReadOnly
disable snmp authenticate traps
config snmp coldstart_traps disable
config snmp warmstart_traps disable
disable snmp linkchange_traps
config snmp linkchange_traps ports 1-28 disable
disable snmp rstpport_state_change traps
disable snmp firmware_upgrade_state traps
disable snmp port_security_violation traps
disable snmp IMPB_violation traps
disable snmp LBD traps
disable snmp DHCP_screening traps
disable snmp duplicate_IP_detected traps


