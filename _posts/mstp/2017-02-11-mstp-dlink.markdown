---
layout: post
title:  "mstp-dlink"
date:   2017-02-11 15:53:59 +0300
categories: mstp
tags: mstp
---

# mstp-dlink

1-8
и 25-26

enable stp
config stp version mstp
config stp mst_config_id name torg
config stp mst_config_id revision_level 1

create stp instance_id 2
config stp instance_id 2 add_vlan 125, 177, 499, 912, 22, 25, 3021, 3022, 3024, 413, 408, 409, 410, 407, 412

config stp priority 4096 instance_id 0
config stp priority 4096 instance_id 2



# Задать приоритеты портов так, чтобы порт 1 стал активным
для v2, и порт 13 - для v3. Приоритет = 16*n, по умолчанию = 128

config stp mst_ports 1 instance_id 2 priority 96
config stp mst_ports 13 instance_id 3 priority 96
config stp ports 3-12 edge true
config stp ports 15-20 edge true



show stp instance_id
show stp ports







spanning-tree mst configuration
 name PSI 
 instance 1 vlan 9-10, 60, 110, 200-207, 260, 272, 276, 281, 303, 628-629
 instance 1 vlan 648, 651, 684, 691, 693-694, 700, 816-817, 822, 833, 837
 instance 1 vlan 855, 895, 1014, 4007
 instance 2 vlan 54-55, 57-58, 68, 172, 294, 298, 520, 577, 671, 773, 787
 instance 2 vlan 846, 894, 1011-1012, 4001
 instance 3 vlan 2, 11, 16, 21-25, 100-109, 113, 120, 151-153, 156, 165
 instance 3 vlan 284, 899, 953-954

spanning-tree mst 2 priority 8
no spanning-tree vlan 1,3-8,12-15,17-20,26-53,56,59-67,69-99,111-112,114-119
no spanning-tree vlan 121-150,154-155,157-164,166-171,173-199,208-259,261-271
no spanning-tree vlan 273-275,277-280,282-283,285-293,295-302,304-576,578-627
no spanning-tree vlan 630-647,649-650,652-670,672-683,685-690,692,695-699,701
no spanning-tree vlan 702-772,774-786,788-815,817-821,823-832,834-836,838-845
no spanning-tree vlan 847-854,856-893,896-898,900-952,955-1010,1013,1015-4000
no spanning-tree vlan 4002-4006,4008-4094


