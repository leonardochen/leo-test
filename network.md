---
layout: page
title: Network
permalink: /network/
---

# Boston

<div class="mermaid">
graph TD

subgraph Access
core1---core2
core1---fex102
core2---fex102
end

subgraph Non-redundant Transit
Singlehome---|VLAN1100|MX[MX100]
Singlehome---|VLAN TRUNK|core1
Singlehome---|VLAN TRUNK|core2
MX---|VLAN100|fex102
end

subgraph Legacy Transit
TWDX1---juniper1
TWDX2---juniper2
juniper1---|VLAN 100|core1
juniper2---|VLAN 100|core2
end

subgraph Customer Edge
TWDX3---|Pub Transit - AWS VPN|asr1
Markley_Amazon---|AWS DC 10G|asr1
Amazon---|AWS DC 10G|asr2
asr1---core1
asr2---core2
end

</div>

<div class="mermaid">

graph TD
subgraph Non-redundant Transit
Singlehome --- 1Kendall
Singlehome --- ADH
Singlehome --- MCS-ECS
Singlehome --- MCS
Singlehome --- Cogent
end

</div>


<div class="mermaid">

graph TD
subgraph Pritunl VPN
TWDX(TWDX)-->ASR1(ASR1)
ASR1(ASR1)-->CORE1(CORE1)
ASR1-->ASR2
ASR2-->CORE2
CORE1(CORE1)-->F5GW(F5GW Cluster)
CORE1-->CORE2
CORE2-->F5GW
F5GW(F5GW Cluster)-->PritunlVM1(PritunlVM1)
F5GW(F5GW Cluster)-->PritunlVM2(PritunlVM2)
end
  
</div>

# Boston - proposed network to support new F5 chassis/SFP+/10Gbase-t 

<div class="mermaid">
  graph TD

subgraph Core to SFP/QSFP
Nexus6K1-->|qsfp|Nexus3172PQ1
Nexus6K1-->|qsfp|Nexus3172PQ2

Nexus6K2-->|qsfp|Nexus3172PQ1
Nexus6K2-->|qsfp|Nexus3172PQ2
end

subgraph ToR 10Gbase-t
Nexus3172PQ1-->|sfp+|Nexus3172TQ1
Nexus3172PQ2-->|sfp+|Nexus3172TQ1
Nexus3172PQ1-->|sfp+|Nexus3172TQ2
Nexus3172PQ2-->|sfp+|Nexus3172TQ2
Nexus3172TQ1-->|10GBase-t|Host1
Nexus3172TQ2-->|10GBase-t|Host1
Nexus3172TQ1-->|10GBase-t|Host2
Nexus3172TQ2-->|10GBase-t|Host2
Nexus3172TQ1-->|10GBase-t|Host3
Nexus3172TQ2-->|10GBase-t|Host3
Nexus3172TQ1-->|10GBase-t|Host4
Nexus3172TQ2-->|10Gbase-t|Host4
end

subgraph F5 Viprion connectivity
Nexus3172PQ1-->|sfp+|F5_B2250A
Nexus3172PQ2-->|sfp+|F5_B2250A
Nexus3172PQ1-->|sfp+|F5_B2250B
Nexus3172PQ2-->|sfp+|F5_B2250B
end

</div>


# Kendall

<div class="mermaid">

graph TD
Cogent --- MX
Comcast --- MX
MX --- LAN

</div>

# cognius office to cognius AWS
<div class="mermaid">
graph LR
subgraph Cognius 210 -> Cognius AWS 10.40/16
CogniusOfficeHost-->CogniusMeraki
CogniusMeraki-->|VPN|CogoMeraki
CogoMeraki-->CogoCore
CogoCore-->ASR1
CogoCore-->ASR2
ASR1-->|VPN Tunnel1|CogniusAWS_10.40/16
ASR1-->|VPN Tunnel2|CogniusAWS_10.40/16
ASR2-->|Direct Connect 10Gb|CogniusAWS_10.40/16
end
</div>
  
