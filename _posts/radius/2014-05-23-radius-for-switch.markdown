---
layout: post
title:  "radius-for-switch"
date:   2014-05-23 12:40:08 +0400
categories: radius
tags: radius
---

# radius-for-switch
radius-server host 1 172.31.3.3 key DqEaro4v
aaa authentication login radius local
aaa authentication enable radius radius
aaa authorization exec radius
aaa accounting system radius

[https://zyxel.ru/kb/2026/](https://zyxel.ru/kb/2026/)


DES1210
# access authentication control
enable authen_policy
disable aaa_server_password_encryption
config authen parameter response_timeout 0
config authen parameter attempt 10
create authen server_host 172.31.3.3 protocol radius port 1812 key "DqEaro4v" timeout 5 retransmit 2 acct_port 1813
create authen server_group tacacs+
create authen server_group radius
config authen server_group radius add server_host 172.31.3.3 protocol radius
create authen_login method_list_name default
config authen_login default method local    
create authen_login method_list_name rad_ext
config authen_login method_list_name rad_ext method radius none   
create authen_enable method_list_name default
config authen_enable default method local    
create authen_enable method_list_name rad_ext_ena
config authen_enable method_list_name rad_ext_ena method radius none   
config authen application console login method_list_name default
config authen application telnet login method_list_name rad_ext
config authen application ssh login method_list_name default
config authen application http login method_list_name rad_ext
config authen application console enable method_list_name default
config authen application telnet enable method_list_name rad_ext_ena
config authen application ssh enable method_list_name default
config authen application http enable method_list_name rad_ext_ena
config admin local_enable *@&2jmj7l5rSw0yVb/vlWAYkK/YBwmwMs6D




enable lldp
config lldp message_tx_hold_multiplier 4
config lldp message_tx_interval 30
config lldp reinit_delay 2
config lldp tx_delay 2
config lldp ports 1-28 mgt_addr ipv4 192.168.118.203 disable
config lldp ports 1-28 admin_status tx_and_rx
config lldp ports 1-24 notification disable
config lldp ports 1-24 basic_tlvs all disable
config lldp ports 1-24 dot1_tlv_pvid disable
config lldp ports 1-24 dot1_tlv_vlan_name vlanid 1-4094 disable
config lldp ports 25-28 notification enable
config lldp ports 25-28 basic_tlvs port_description system_name system_description system_capabilities enable
config lldp ports 25-28 dot1_tlv_pvid enable
config lldp ports 25-28 dot1_tlv_vlan_name vlanid 1-4094 enable
config lldp ports 1-28 dot1_tlv_protocol_identity eapol disable
config lldp ports 1-28 dot1_tlv_protocol_identity lacp disable
config lldp ports 1-28 dot1_tlv_protocol_identity gvrp disable
config lldp ports 1-28 dot1_tlv_protocol_identity stp disable
config lldp ports 1-28 dot3_tlvs all disable


DES3200

create authen server_host 172.31.3.3 protocol radius port 1812 key "DqEaro4v" timeout 5 retransmit 2
config authen server_group radius delete server_host 0.0.0.0 protocol radius
config authen server_group radius add server_host 172.31.3.3 protocol radius
config authen_login default method local
create authen_login method_list_name rad_ext
config authen_login method_list_name rad_ext method radius
config authen_enable default method local_enable
create authen_enable method_list_name rad_ext_ena
config authen_enable method_list_name rad_ext_ena method radius
config authen application console login default
config authen application console enable default
config authen application telnet login method_list_name rad_ext                
config authen application telnet enable method_list_name rad_ext_ena
config authen application ssh login default
config authen application ssh enable default
config authen application http login method_list_name rad_ext
config authen application http enable method_list_name rad_ext_ena
config authen parameter response_timeout 0
config authen parameter attempt 10
enable authen_policy
disable authen_policy_encryption 
config admin local_enable


Bo80:BasJ,B32768




















enable lldp
config lldp message_tx_hold_multiplier 4
config lldp message_tx_interval 30
config lldp reinit_delay 2
config lldp tx_delay 2
config lldp ports 1-10 mgt_addr ipv4 192.168.118.203 disable
config lldp ports 1-10 admin_status tx_and_rx
config lldp ports 1-10 notification disable
config lldp ports 1-8 basic_tlvs all disable
config lldp ports 1-8 dot1_tlv_pvid disable
config lldp ports 1-8 dot1_tlv_vlan_name vlanid 1-4094 disable
config lldp ports 9-10 notification enable
config lldp ports 9-10 basic_tlvs port_description system_name system_description system_capabilities enable
config lldp ports 9-10 dot1_tlv_pvid enable
config lldp ports 9-10 dot1_tlv_vlan_name vlanid 1-4094 enable
config lldp ports 1-8 dot1_tlv_protocol_identity eapol disable
config lldp ports 1-8 dot1_tlv_protocol_identity lacp disable
config lldp ports 1-8 dot1_tlv_protocol_identity gvrp disable
config lldp ports 1-8 dot1_tlv_protocol_identity stp disable
config lldp ports 1-8 dot3_tlvs all disable



config authen server_host 172.31.3.3 protocol radius port 1812 key "DqEaro4v" timeout 5 retransmit 2 acct_port 1813
