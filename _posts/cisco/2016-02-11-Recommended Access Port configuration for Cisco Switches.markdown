---
layout: post
title:  "Recommended Access Port configuration for Cisco Switches"
date:   2016-02-11 08:14:38 +0300
categories: Recommended Access Port configuration for Cisco Switches
tags: cisco
---

# Recommended Access Port configuration for Cisco Switches
Recommended Access Port configuration for Cisco Switches
Submitted by Admin on Mon, 12/19/2011 - 22:19

Commonly most Network engineers will only put in the bare minimum configs (in blue) to get the network running. In reality this can cause disastrous problems for your network future.
If you are setting up new or rolling out updated Cisco Switch config’s you might want to consider the below commands (in red) as part of your default template. These should be your minimum requirements however you may need to adjust for your setup.

In the scenarios below I have used VLan 10 for data and 11 for voice
Scenarios:

Access Port with no Voice:
interface range FastEthernet0/1 - 24
 description DATA
 switchport mode access
 switchport access vlan 10
 no snmp trap link-status
 storm-control broadcast level 4.00
 storm-control multicast level 10.00
 storm-control action shutdown
 storm-control action trap
 spanning-tree portfast
 spanning-tree bpduguard enable

Standard Access Port with Cisco VoIP Phones:
interface range FastEthernet0/1 - 24
 description DATA+VOICE
 switchport mode access
 switchport access vlan 10
 switchport voice vlan 11
 no snmp trap link-status
 storm-control broadcast level 4.00
 storm-control multicast level 10.00
 storm-control action shutdown
 storm-control action trap
 auto qos voip cisco-phone
 spanning-tree portfast
 spanning-tree bpduguard enable

Standard Access Port with non Cisco VoIP Phones:
interface range FastEthernet0/1 - 24
 description DATA+VOICE
 switchport trunk native vlan 10
 switchport trunk allowed vlan 10,11
 switchport mode trunk
 no snmp trap link-status
 storm-control broadcast level 4.00
 storm-control multicast level 10.00
 storm-control action shutdown
 storm-control action trap
 auto qos voip trust
 spanning-tree portfast
 spanning-tree bpduguard enable

A brief description of the commands:

description
It’s always nice to have a meaningful description on an Interface especially if you have a team of Network Engineers who can’t be across every device plugged into the network. Access ports are easy and don’t generally need complicated descriptions. 

switchport mode access
Set’s the port as an access port mode where typically only one vlan is allowed to send and receive traffic.

switchport access vlan 10
When used with “switchport mode access” it configures the switch to the correct access vlan. In this case vlan 10 (Data Vlan)

switchport voice vlan 11
When used with “switchport mode access” and "switchport access vlan 10" it configures the switch to the correct voice vlan. In this case vlan 11 (Voice Vlan). The switch also tells the Cisco phone via CDP which voice vlan to use. In reality the port then becomes a trunk port when a cisco phone is plugged in. The voice (vlan 11) traffic becomes tagged while the data (vlan 10) traffic is still untagged.

switchport mode trunk
Hard sets the interface into trucking mode where multiple vlan can traverse through that interface.
If you happen to run non cisco phones you will need to setup your interfaces this way as these phones won’t understand the CDP information sent out from the switch.
Note you may need to issue “switchport trunk encapsulation dot1q” before the command can be issued. This specifies which trunking protocol to use, in this case IEEE 802.1Q which is the most commonly used.

switchport trunk native vlan 10
When used with “switchport mode trunk” it specifies which vlan is to have all the vlans traffic untagged when the traffic exits the interface. In this case vlan 10 (data vlan)

switchport trunk allowed vlan 10,11
This command only allows the specified vlans to traverse through the interface, You want to restrict the amount of vlans going through the interface as much as possible to reduce the amount of broadcast traffic and security purposed. I also recommend you do not allow vlan 1 to travers through trunks

no snmp trap link-status
If you are using monitoring software which receive SNMP traps from your switches I recommend using command if you do not care about Users/PC ports going up and down. This can reduce load on the switch CPU and hundreds of events in your monitoring software. Remember not to put this commands on your important uplinks etc.

storm-control broadcast level 4.00 (in per cent %)
storm-control multicast level 10.00 (in per cent %)
storm-control action shutdown
storm-control action trap
I recommend you apply some kind of broadcast and multicast control on your network access ports. This can help in the event of virus outbreaks etc. If running an application such as Ghostcast you will however need to avoid these commands.
With the “storm-control broadcast level 10” command used alone it will start dropping broadcasts at 10% and above.
With “storm-control action shutdown” configured, if the configured % values are reached the switch will automatically shut down the interface. You will then have to manually issue a “no shut” on the interface. You can also configure errdisable recovery to automatically bring the interface back up after a specified about of time.
The “storm-control action trap” command will send a SNMP trap whenever the configured % value is reached.

auto qos voip cisco-phone
If you are running cisco phones on your network this command can save a lot of hassle of configuring all interfaces with the correct qos settings. As a word of warning some of the older IOS versions appear to not completely configure all the required settings and/or may need some adjustment afterwards. Please upgrade the IOS first and check that “priority-queue out” gets put into the interface config.

spanning-tree portfast
Highly recommended on Access Ports. This will bring up an Interface into the forwarding state almost instantly instead of the usual 30 seconds spanning-tree usually takes. Saves a lot of issues on windows domain networks and DHCP.

spanning-tree bpduguard enable
Another highly recommended command. If a switch detects a spanning-tree BPDU enter on the specified interface from another cisco device it will automatically shut down the interface. This is common situation where someone has plugged in a non-authorised cisco switch into the network or if someone has tried to create a loop in the network. This allows the Network Admin to gain more control of how devices are plugged into the network. Errdisable recovery can be configured to bring the interface back up after a specified amount of time. (say if a cable was plugged in by mistake and has been resolved)