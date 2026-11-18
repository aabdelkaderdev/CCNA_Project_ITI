## Acronym dictionary

**Addressing and gateways**
- **PIP** = Phantom IP Address, the HSRP virtual gateway that hosts use as their default gateway
- **GW** = Gateway, the default gateway a device points to (the PIP for VLANs on the routers)
- **R1 / R2** = the two gateway routers at each site (R1 is HSRP active, R2 is standby)
- **SVI** = Switch Virtual Interface, the management IP of a switch inside VLAN 10
- **VLSM** = Variable Length Subnet Masking
- **CIDR** = Classless Inter-Domain Routing (the /xx suffix)
- **SNM** = Subnet Mask
- **WCM** = Wildcard Mask
- **NID** = Network ID (the base network of the address plan)
- **P2P** = Point-to-Point (a /30 link between two routers)
- **DHCP** = Dynamic Host Configuration Protocol
- **NAT / PAT** = Network Address Translation / Port Address Translation

**Switching and redundancy**
- **VLAN** = Virtual LAN
- **VTP** = VLAN Trunking Protocol
- **802.1Q** = the VLAN trunking standard
- **ROAS** = Router-on-a-Stick (trunk subinterfaces G0/1.x on the router)
- **HSRP** = Hot Standby Router Protocol
- **STP** = Spanning Tree Protocol
- **LACP** = Link Aggregation Control Protocol (IEEE EtherChannel, used at ALEX)
- **PAgP** = Port Aggregation Protocol (Cisco EtherChannel, used at CAI)
- **Po1** = Port-channel 1

**Routing and WAN**
- **OSPF** = Open Shortest Path First
- **RIPv2** = Routing Information Protocol version 2
- **ABR / ASBR** = Area Border Router / Autonomous System Boundary Router
- **DCE** = Data Circuit-terminating Equipment (the serial end that sets the clock)
- **ISP** = Internet Service Provider

**Sites, devices and VLAN names**
- **BSE** = team prefix on device names
- **ALEX / CAI** = Alexandria (primary site) / Cairo (secondary site)
- **EDGE** = the site's edge router
- **SW** = Switch
- **ELV** = Extra Low Voltage systems (cameras and access control)
- **HR** = Human Resources
- **DMZ** = Demilitarized Zone (the public web server VLAN)
- **AAA** = Authentication, Authorization, Accounting
- **FTP** = File Transfer Protocol
WCM: 0.0.0.3
---(BSE-R2-CAI -> BSE-EDGE-CAI)---
192.168.1.92/30
SNM: 255.255.255.252
WCM: 0.0.0.3
```
