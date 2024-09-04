# OLT-ZTE-C300-PROVISIONAMENTO
*PROVISIONADAS
conf t
interface gpon-olt_1/2/{pon}
onu {onu} type {onutype} sn {id}
exit
interface gpon-onu_1/{slot}/{pon}:{onu}
description {description}
tcont 1 profile 1GB_UP
gemport 1 name Gemport1 tcont 1
gemport 1 traffic-limit downstream 1GB_DW 
switchport mode hybrid vport 1
service-port 1 vport 1 user-vlan {vlan} vlan {vlan}
exit
pon-onu-mng gpon-onu_1/{slot}/{pon}:{onu}
service 1 gemport 1 vlan {vlan}
vlan port eth_0/1 mode tag vlan {vlan}
exit
exit 

*ONU DESPROVISIONADAS

show gpon onu uncfg

*DESPROVISIONAR

interface gpon-olt_1/{slot}/{pon}
no onu {onu}
exit

*ACHAR ONU ID
show pon onu information gpon-olt[Tab]
