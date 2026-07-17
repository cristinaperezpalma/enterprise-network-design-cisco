# Routing and High Availability

## Overview

The enterprise network uses dynamic routing protocols and redundancy mechanisms to provide reliable communication between all corporate locations. IPv4 routing is implemented using OSPF, while the IPv6-only Branch 2 relies on OSPFv3. External Internet connectivity is handled through static routing, ensuring that only internal corporate networks participate in dynamic routing processes.

The routing infrastructure combines Cisco 3650 multilayer switches for internal routing with Cisco 2911 edge routers responsible for WAN connectivity, Internet access, and external communications.

---

## OSPF Configuration (IPv4)

Dynamic IPv4 routing is implemented using **OSPF Area 0**, allowing automatic route exchange between Headquarters (HQ) and Branch 1 (B1).

### Main Characteristics

- Single OSPF Area (Area 0)
- Automatic route advertisement
- Dynamic route learning
- Simplified network expansion
- Fast routing convergence

The Headquarters advertises all internal departmental networks, while Branch 1 advertises its local VLANs and WAN connections. This eliminates the need for static routing inside the corporate infrastructure and allows automatic adaptation to topology changes.

---

## OSPFv3 Configuration (IPv6)

Branch 2 operates exclusively with IPv6 and uses **OSPFv3** as its dynamic routing protocol.

The multilayer switch enables **IPv6 Unicast Routing**, allowing IPv6 prefixes to be exchanged dynamically with Headquarters through the dedicated WAN connection.

Main features include:

- IPv6-only routing
- Dynamic route exchange
- Automatic IPv6 prefix advertisement
- Simplified IPv6 network management

---

## Route Advertisement

Each site advertises its local networks dynamically through the routing protocol.

- Headquarters advertises all internal IPv4 networks.
- Branch 1 advertises its local VLANs together with its WAN network.
- Branch 2 advertises its IPv6 prefixes using OSPFv3.

This allows all corporate locations to communicate without manually configuring individual routes.

---

## Inter-Site Routing

Communication between corporate locations is established through dedicated private WAN links managed by the company.

### Headquarters ↔ Branch 1

- IPv4 connectivity
- Point-to-point WAN links (/30)
- Dynamic routing using OSPF

### Headquarters ↔ Branch 2

- IPv6 connectivity
- Dedicated IPv6 WAN link
- Dynamic routing using OSPFv3

WAN routers interconnect each branch with the Headquarters through Gigabit Ethernet interfaces.

---

## HSRP Configuration

High availability at Headquarters is provided through **Hot Standby Router Protocol (HSRP)**.

Two Cisco multilayer switches share a virtual default gateway for the server network, allowing uninterrupted connectivity if one switch becomes unavailable.

Main characteristics:

- Virtual Gateway: **192.168.80.1**
- Priority-based election
- Automatic failover
- Preemption enabled

<p align="center">
<img src="../screenshots/hsrp.png" width="900">
</p>

---

## High Availability

Several redundancy mechanisms improve the reliability of the enterprise infrastructure.

### Core Redundancy

The Headquarters implements two interconnected multilayer switches operating as a collapsed core with HSRP, eliminating single points of failure for gateway services.

### Internet Redundancy

Two independent Internet edge routers provide external connectivity through separate ISPs.

Primary ISP:

- 198.51.100.1

Backup ISP:

- 198.51.100.5

Floating static routes with different administrative distances automatically redirect traffic to the backup connection if the primary Internet link fails.

### Physical Redundancy

Redundant Gigabit Ethernet links connect access switches with the core infrastructure, providing alternative communication paths in case of cable or interface failures.

---

## Design Decisions

Several routing and redundancy decisions were made to improve scalability, reliability, and network availability.

These include:

- Adoption of a collapsed core architecture.
- Dynamic routing using OSPF and OSPFv3.
- HSRP virtual gateway redundancy.
- Redundant Internet connectivity.
- Redundant physical uplinks.
- Automatic route convergence.

These mechanisms simplify network management while minimizing service interruptions.

---

## Routing Verification

Several validation tests confirmed the correct operation of the routing infrastructure.

The following elements were successfully verified:

- OSPF neighbor establishment
- Dynamic route propagation
- Routing table convergence
- End-to-end connectivity
- HSRP redundancy
- Internet failover

### OSPF Neighbors

<p align="center">
<img src="../screenshots/ospf-neighbors.png" width="900">
</p>

### Routing Tables

<p align="center">
<img src="../screenshots/routing-table1.png" width="900">
</p>

<p align="center">
<img src="../screenshots/routing-table2.png" width="900">
</p>

<p align="center">
<img src="../screenshots/routing-table3.png" width="900">
</p>

### End-to-End Connectivity

<p align="center">
<img src="../screenshots/ping-between-sites.png" width="900">
</p>

The validation demonstrated successful dynamic route exchange between all corporate locations and confirmed automatic failover mechanisms for both gateway redundancy and Internet connectivity.

---

## Skills Demonstrated

- Enterprise routing design
- OSPF configuration
- OSPFv3 configuration
- Inter-VLAN routing
- WAN routing
- HSRP implementation
- High availability design
- Redundant Internet architecture
- Dynamic routing verification
- Enterprise network troubleshooting
