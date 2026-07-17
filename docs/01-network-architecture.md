# Network Architecture

## Overview

This project implements a secure, scalable, and highly available enterprise network that interconnects a Headquarters (HQ) with two remote branch offices (Branch 1 and Branch 2).

The infrastructure is designed to provide reliable LAN and WAN connectivity, support both IPv4 and IPv6 networking, ensure business continuity through redundancy mechanisms, and securely deliver internal and public services.

The network is designed to support approximately 260 employees while allowing future expansion without requiring major architectural changes.

---

## Network Topology

The network follows a hierarchical architecture based on a **collapsed core** design located at the Headquarters.

The infrastructure consists of:

- Headquarters (HQ)
- Branch 1 (B1)
- Branch 2 (B2)
- Private WAN links between sites
- Redundant Internet connectivity
- Centralized server infrastructure

![Enterprise Network Topology](../screenshots/topology.png)

---

## Headquarters (HQ)

The Headquarters contains the core infrastructure of the enterprise network.

Main components include:

- Two Cisco multilayer switches operating as a redundant collapsed core
- Multiple access switches connected through trunk links
- Server infrastructure
- Wireless access points
- Perimeter firewall
- Internet edge routers

The HQ hosts all critical enterprise services, including:

- DHCP servers
- Compute and storage servers
- Corporate web server
- Internal network services

---

## Branch 1 (B1)

Branch 1 represents a smaller version of the Headquarters.

Its infrastructure includes:

- One multilayer switch acting as the local core
- Access switches for end devices
- Inter-VLAN routing through Switch Virtual Interfaces (SVIs)
- WAN router connected to HQ through a point-to-point link

Dynamic routing is performed using OSPF.

---

## Branch 2 (B2)

Branch 2 is a smaller office operating exclusively with IPv6.

Its architecture includes:

- One multilayer switch
- Two access switches
- Two departmental VLANs
- SLAAC address assignment
- OSPFv3 routing towards Headquarters

Unlike the Headquarters, Branch 2 does not contain local servers or redundant infrastructure.

---

## Network Technologies

The project integrates several enterprise networking technologies.

### Network Segmentation

- IEEE 802.1Q VLANs
- Department isolation
- Guest network separation

### Routing

- OSPF for IPv4
- OSPFv3 for IPv6

### IP Addressing

- IPv4 /24 addressing
- IPv6 corporate prefix (2001:DB8:CAFE::/48)
- DHCP
- SLAAC

### High Availability

- HSRP
- Redundant DHCP servers
- Dual Internet connectivity

### Security

- Extended ACLs
- Static and Dynamic NAT
- Perimeter Firewall
- Site-to-Site VPN
- Remote Access VPN

---

## Hierarchical Architecture

The infrastructure follows a hierarchical enterprise model.

A centralized collapsed core performs routing, traffic distribution and policy enforcement, while access switches connect end-user devices and wireless access points.

This architecture simplifies management while improving scalability and performance.

---

## Collapsed Core Design

The Headquarters implements a collapsed core architecture using two Cisco multilayer switches.

This design combines the traditional Core and Distribution layers into a single level, reducing:

- Network latency
- Hardware requirements
- Operational complexity
- Deployment costs

At the same time, it centralizes:

- Inter-VLAN routing
- Routing protocols
- Security policies
- High availability mechanisms

---

## Department Segmentation

Departments are logically separated using VLANs.

| VLAN | Department | Locations |
|------|------------|-----------|
|100|Research|HQ, B1, B2|
|200|Commercial|HQ, B1|
|300|Sales|HQ, B1|
|400|Training|HQ, B1, B2|
|500|Technical Support|HQ, B1|
|900|Guest Network|HQ|

This segmentation improves security, reduces broadcast domains, and simplifies network administration.

---

## Server Infrastructure

All enterprise servers are located at the Headquarters.

The infrastructure includes:

- Dual DHCP servers
- Compute and storage servers
- Corporate web server

Critical services are isolated into dedicated VLANs.

Access to compute servers is restricted through ACL policies allowing only the Research and Technical Support departments.

---

## Inter-Site Connectivity

The Headquarters communicates with both branches through dedicated WAN links.

Routing is performed dynamically:

- HQ ↔ B1 using OSPF
- HQ ↔ B2 using OSPFv3

A Site-to-Site VPN protects communications between Headquarters and Branch 1.

---

## Scalability

The network has been designed to support future growth.

The use of:

- hierarchical architecture
- VLAN segmentation
- OSPF
- structured IP addressing

allows additional departments, branches, and devices to be incorporated with minimal modifications.

---

## High Availability

Several mechanisms provide fault tolerance throughout the infrastructure.

These include:

- Dual multilayer core switches
- HSRP virtual gateway
- Redundant DHCP servers
- Redundant Internet connectivity

These mechanisms minimize downtime and improve service continuity in case of device or link failures.
