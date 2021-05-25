---
layout: post
title:  "dlink-change-config"
date:   2011-04-17 23:13:39 +0400
categories: dlink
tags: dlink
---

# dlink-change-config

enable loopdetect
config loopdetect recover_timer 60
config loopdetect interval 10
config loopdetect mode port-based
config loopdetect trap none
config loopdetect ports 1-8 state enabled
config loopdetect ports 9-10 state disabled


enable lldp
config lldp message_tx_interval 30
config lldp tx_delay 2
config lldp message_tx_hold_multiplier 4
config lldp reinit_delay 2
config lldp notification_interval 5
config lldp forward_message enable
config lldp ports 9 dot1_tlv_vlan_name vlanid 1-4094 enable
config lldp ports 10 dot1_tlv_vlan_name vlanid 1-4094 enable
config lldp ports 1-8 notification disable
config lldp ports 1-8 admin_status tx_and_rx
config lldp ports 1-10 notification enable
config lldp ports 9-10 basic_tlvs port_description system_name system_description system_capabilities enable
config lldp ports 9-10 dot1_tlv_pvid enable 

config traffic control_trap both
config traffic control 1-8 broadcast enable multicast enable unicast disable action drop threshold 64 countdown 5 time_interval 5
config traffic control 9-10 broadcast disable multicast disable unicast disable action drop threshold 64 countdown 0 time_interval 5
  

enable syslog
create syslog host 1 ipaddress 192.168.113.1 severity all facility local7 udp_port 514  state enable 
config log_save_timing log_trigger


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
config snmp engineID 800000ab031cbdb9649460
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

config snmp system_name vchm-lipetsk-s0
config snmp system_location rudnik-vchm
config snmp system_contact iptech@sc.ru











config traffic control_trap both
config traffic control 1-24 broadcast enable multicast enable unicast disable action drop threshold 64 countdown 5 time_interval 5
config traffic control 25-28 broadcast disable multicast disable unicast disable action drop threshold 64 countdown 0 time_interval 5



enable loopdetect
config loopdetect recover_timer 60
config loopdetect interval 10
config loopdetect mode port-based
config loopdetect trap none
config loopdetect ports 1-24 state enabled
config loopdetect ports 25-28 state disabled


enable syslog
create syslog host 1 ipaddress 192.168.122.1 severity all facility local7 udp_port 514  state enable 
config log_save_timing log_trigger


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
config snmp engineID 800000ab031cbdb9649460
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
