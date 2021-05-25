---
layout: post
title:  "gen-zt-config"
date:   2011-04-07 02:02:47 +0400
categories: gen-zt-config
tags: gen-zt-config
---

# gen-zt-config
%s/\$MASK/\$\{MASK\}/gc
%s/\$GW/\$\{GW\}/gc
%s/\$NET/\$\{NET\}/gc
%s/\$MGVL/\$\{MGVL\}/gc
%s/\$IVLAN/\$\{IVLAN\}/gc
%s/\$MVLAN/\$\{MVLAN\}/gc
%s/\$HVLAN/\$\{HVLAN\}/gc
%s/\$BVLAN/\$\{BVLAN\}/gc
%s/\$PIPOE/\$\{PIPOE\}/gc
%s/\$ADDRESS/\$\{ADDRESS\}/gc
%s/\$GIPOE/\$\{GIPOE\}/gc
%s/\$GL2TP/\$\{GL2TP\}/gc



'${MNGT_VLAN}'







%s/\$\{IP\}/\'\$\{IP\}\'/gc
%s/\$\{MASK\}/\'\$\{MASK\}\'/gc
%s/\$\{GW\}/\'\$\{GW\}\'/gc
%s/\$\{NET\}/\'\$\{NET\}\'/gc
%s/\$\{MGVL\}/\'\$\{MGVL\}\'/gc
%s/\$\{IVLAN\}/\'\$\{IVLAN\}\'/gc
%s/\$\{MVLAN\}/\'\$\{MVLAN\}\'/gc
%s/\$\{HVLAN\}/\'\$\{HVLAN\}\'/gc
%s/\$\{BVLAN\}/\'\$\{BVLAN\}\'/gc
%s/\$\{PIPOE\}/\'\$\{PIPOE\}\'/gc
%s/\$\{ADDRESS\}/\'\$\{ADDRESS\}\'/gc
%s/\$\{GIPOE\}/\'\$\{GIPOE\}\'/gc
%s/\$\{GL2TP\}/\'\$\{GL2TP\}\'/gc
