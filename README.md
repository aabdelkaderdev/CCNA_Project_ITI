# University Hospital Network — Cisco Packet Tracer

This project designs and documents a two-site university hospital network for Alexandria and Cairo. It was built in **Cisco Packet Tracer 9.0.1** as a CCNA networking project by the Black Sun Empire (BSE) team.

## Project files

| File | Description |
| --- | --- |
| [`BSE Final.pkt`](BSE%20Final.pkt) | Main Packet Tracer simulation. Open this file in Packet Tracer to inspect the topology, device configurations, and services. |
| [`BSE Report.pdf`](BSE%20Report.pdf) | Design report with the addressing plans, implementation notes, screenshots, and verification summary. |
| [`Topology Design/Topology Final.png`](Topology%20Design/Topology%20Final.png) | Final network topology diagram. |
| [`Topology Design/(Proof Of Concept) Cisco Hierarchical Network Topology Diagram.png`](Topology%20Design/%28Proof%20Of%20Concept%29%20Cisco%20Hierarchical%20Network%20Topology%20Diagram.png) | Hierarchical topology proof of concept. |
| `Engineer A (Ramadan)/`, `Engineer B (Youssef)/`, `Engineer C (Abdelkader)/` | Team working copies, configuration notes, and supporting evidence. |

## Network overview

The simulation connects hospital networks in Alexandria and Cairo through an ISP. Each site has an edge router, redundant internal routers, core and access switches, and departmental and service VLANs. Router-on-a-Stick provides inter-VLAN routing, while HSRP provides default-gateway failover.

The design includes:

- VLSM-based IPv4 addressing for departmental VLANs, server networks, router links, and the inter-site connection.
- VLAN segmentation, 802.1Q trunks, VTP, Rapid-PVST, and redundant core-switch links using EtherChannel (LACP in Alexandria and PAgP in Cairo).
- HSRP between the internal routers at each site.
- Dynamic routing across the sites: OSPF in Alexandria, RIPv2 inside Cairo, and route redistribution at the Cairo edge.
- Standalone DHCP services and DHCP relay for client VLANs.
- AAA with local account fallback, SSH management, and an FTP server for configuration backups.
- An Alexandria DMZ web server, static NAT, and PAT for outbound connectivity through the simulated ISP.

### VLANs

| VLAN | Alexandria | Cairo |
| --- | --- | --- |
| 10 | Administration | Administration |
| 20 | HR | — |
| 30 | Clinical Services | Clinical Services |
| 40 | IP Cameras | — |
| 50 | Access Control | — |
| 60 | Internal Servers | Internal Servers |
| 70 | Public Web Server / DMZ | — |
| 99 | — | Native VLAN on trunks |

## Addressing summary

The report contains the full VLSM tables, gateway assignments, and point-to-point subnets. The site address spaces are:

- **Alexandria:** `172.16.0.0/16` (allocated subnets include `172.16.0.0/25`, `172.16.0.128/26`, and smaller departmental and infrastructure networks).
- **Cairo:** `192.168.1.0/24` (departmental, server, and router-link subnets are allocated from this block).
- **Alexandria–Cairo WAN:** `172.16.1.40/30`.

See Section 3 of [`BSE Report.pdf`](BSE%20Report.pdf) for the complete subnet plans and Section 7 for routing details.

## Open the simulation

1. Install Cisco Packet Tracer 8.2.2 or a compatible version.
2. Open [`BSE Final.pkt`](BSE%20Final.pkt).
3. Select a device to inspect its CLI, interfaces, and configuration. Use the report to follow the topology and verification evidence.

The `.pkt` file is an interactive simulation, not a software package; it does not require a build or installation step.

## Verification and documentation

The report documents verification of routing adjacencies and routes, DHCP leases, HSRP failover and recovery, EtherChannel, SSH access, connectivity, NAT, and FTP configuration backups. Screenshots and explanations are included in the PDF; device-level settings can be inspected in Packet Tracer.

## Team

**Black Sun Empire (BSE)**

- Abdelrahman Mohamed Ramadan
- Abdelrahman Namir Ahmed Abdelkader
- Youssef Tarek Ibrahim Shaker

Course: CCNA · Instructor: Mohamed Abdalla
