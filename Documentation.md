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

## Updated subnetting text

Required addresses = devices + gateways (PIP + R1 + R2 = 3 on the router VLANs) + 2 (network and broadcast).

**Alex Network Subnet VLSM:**
```
(VLAN 30) 60 Devices + 3 Gateways (PIP, R1, R2) = 63 Hosts, Block Size: 2^7 = 128, CIDR Suffix: /25
(VLAN 40) 50 Devices + 3 Gateways (PIP, R1, R2) = 53 Hosts, Block Size: 2^6 = 64,  CIDR Suffix: /26
(VLAN 20) 20 Devices + 3 Gateways (PIP, R1, R2) = 23 Hosts, Block Size: 2^5 = 32,  CIDR Suffix: /27
(VLAN 50) 12 Devices + 3 Gateways (PIP, R1, R2) = 15 Hosts, Block Size: 2^5 = 32,  CIDR Suffix: /27
(VLAN 10) 9  Devices + 3 Gateways (PIP, R1, R2) = 12 Hosts, Block Size: 2^4 = 16,  CIDR Suffix: /28
(VLAN 60) 3  Devices + 3 Gateways (PIP, R1, R2) = 6  Hosts, Block Size: 2^3 = 8,   CIDR Suffix: /29
(VLAN 70) 1  Devices + 3 Gateways (PIP, R1, R2) = 4  Hosts, Block Size: 2^3 = 8,   CIDR Suffix: /29
(BSE-R1-ALEX -> BSE-EDGE-ALEX) 2 Devices + 0 Gateways = 2 Hosts, Block Size: 2^2 = 4, CIDR Suffix: /30
(BSE-R2-ALEX -> BSE-EDGE-ALEX) 2 Devices + 0 Gateways = 2 Hosts, Block Size: 2^2 = 4, CIDR Suffix: /30

---(VLAN 30)---
172.16.0.0/25
SNM: 255.255.255.128
WCM: 0.0.0.127
---(VLAN 40)---
172.16.0.128/26
SNM: 255.255.255.192
WCM: 0.0.0.63
---(VLAN 20)---
172.16.0.192/27
SNM: 255.255.255.224
WCM: 0.0.0.31
---(VLAN 50)---
172.16.0.224/27
SNM: 255.255.255.224
WCM: 0.0.0.31
---(VLAN 10)---
172.16.1.0/28
SNM: 255.255.255.240
WCM: 0.0.0.15
---(VLAN 60)---
172.16.1.16/29
SNM: 255.255.255.248
WCM: 0.0.0.7
---(VLAN 70)---
172.16.1.24/29
SNM: 255.255.255.248
WCM: 0.0.0.7
---(BSE-R1-ALEX -> BSE-EDGE-ALEX)---
172.16.1.32/30
SNM: 255.255.255.252
WCM: 0.0.0.3
---(BSE-R2-ALEX -> BSE-EDGE-ALEX)---
172.16.1.36/30
SNM: 255.255.255.252
WCM: 0.0.0.3
```

**Cairo Network Subnet VLSM:**
```
(VLAN 30) 28 Devices + 3 Gateways (PIP, R1, R2) = 31 Hosts, Block Size: 2^6 = 64, CIDR Suffix: /26
(VLAN 10) 7  Devices + 3 Gateways (PIP, R1, R2) = 10 Hosts, Block Size: 2^4 = 16, CIDR Suffix: /28
(VLAN 60) 1  Devices + 3 Gateways (PIP, R1, R2) = 4  Hosts, Block Size: 2^3 = 8,  CIDR Suffix: /29
(BSE-R1-CAI -> BSE-EDGE-CAI) 2 Devices + 0 Gateways = 2 Hosts, Block Size: 2^2 = 4, CIDR Suffix: /30
(BSE-R2-CAI -> BSE-EDGE-CAI) 2 Devices + 0 Gateways = 2 Hosts, Block Size: 2^2 = 4, CIDR Suffix: /30

---(VLAN 30)---
192.168.1.0/26
SNM: 255.255.255.192
WCM: 0.0.0.63
---(VLAN 10)---
192.168.1.64/28
SNM: 255.255.255.240
WCM: 0.0.0.15
---(VLAN 60)---
192.168.1.80/29
SNM: 255.255.255.248
WCM: 0.0.0.7
---(BSE-R1-CAI -> BSE-EDGE-CAI)---
192.168.1.88/30
SNM: 255.255.255.252
WCM: 0.0.0.3
---(BSE-R2-CAI -> BSE-EDGE-CAI)---
192.168.1.92/30
SNM: 255.255.255.252
WCM: 0.0.0.3
```
