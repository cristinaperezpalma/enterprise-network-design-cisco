# Enterprise Network Design

A complete enterprise network infrastructure designed and implemented in **Cisco Packet Tracer**, following enterprise networking best practices.

The project simulates a multi-site company composed of a Headquarters (HQ) and two remote branches, implementing secure communication, high availability, dynamic routing, VLAN segmentation, and enterprise network services.

---

## Project Overview

This project was developed as part of a Computer Networks course with the objective of designing a scalable, secure and fault-tolerant enterprise network from scratch.

The infrastructure includes:

- Headquarters (HQ)
- Branch Office 1 (IPv4)
- Branch Office 2 (IPv6)
- Enterprise server infrastructure
- Public and private web services
- High availability mechanisms
- Dynamic routing
- Network segmentation
- Internet access simulation

---

## Features

- Hierarchical Collapsed Core Architecture
- Department-based VLAN segmentation
- Inter-VLAN Routing
- OSPF Dynamic Routing
- IPv4 & IPv6 Addressing
- DHCP Redundancy
- HSRP Gateway Redundancy
- Access Control Lists (ACLs)
- Static NAT
- Public and Private Web Servers
- Guest Network
- WAN Connectivity Between Sites

---

## Technologies

| Category | Technologies |
|-----------|--------------|
| Simulation | Cisco Packet Tracer |
| Switching | Cisco 3650 Multilayer Switches, Cisco 2960 |
| Routing | OSPF, OSPFv3 |
| Network Services | DHCP, NAT |
| High Availability | HSRP |
| Security | ACLs, VLAN Segmentation |
| Addressing | IPv4, IPv6, SLAAC |
| Standards | IEEE 802.1Q |

---

# Network Topology

The following figure shows the complete enterprise network implemented in Packet Tracer.

![Enterprise Network](screenshots/topology.png)

---

# Project Structure

```
enterprise-network-design/
│
├── docs/
│   ├── 01-network-architecture.md
│   ├── 02-vlan-design.md
│   ├── 03-dynamic-routing-ospf.md
│   ├── 04-network-services.md
│   ├── 05-security.md
│   ├── 06-high-availability.md
│   └── 07-testing.md
│
├── packet-tracer/
│   └── enterprise-network.pkt
│
├── screenshots/
│
├── README.md
└── LICENSE
```

---

# Documentation

Detailed technical documentation is available inside the **docs** directory.

| Document | Description |
|----------|-------------|
| [01 - Network Architecture](docs/01-network-architecture.md) | Enterprise architecture and design decisions |
| [02 - VLAN Design](docs/02-vlan-design.md) | VLAN segmentation and inter-VLAN routing |
| [03 - Dynamic Routing](docs/03-dynamic-routing-ospf.md) | OSPF configuration and routing |
| [04 - Network Services](docs/04-network-services.md) | DHCP, servers and network services |
| [05 - Security](docs/05-security.md) | ACLs, NAT and security mechanisms |
| [06 - High Availability](docs/06-high-availability.md) | HSRP and redundancy |
| [07 - Testing](docs/07-testing.md) | Connectivity validation and verification |

---

# Project Highlights

## VLAN Segmentation

The enterprise network is divided into multiple VLANs to isolate departments, improve security and reduce broadcast traffic.

![VLANs](screenshots/vlans.png)

---

## Dynamic Routing

Inter-site communication is achieved through OSPF, allowing automatic route exchange across the infrastructure.

![OSPF Neighbors](screenshots/ospf-neighbors.png)

---

## High Availability

Gateway redundancy is implemented using HSRP to ensure service continuity in case of device failure.

![HSRP](screenshots/hsrp.png)

---

## Access Control

Extended ACLs restrict access to the compute servers, allowing only authorized departments.

![ACL](screenshots/acl-server-access.png)

---

## DHCP Services

Redundant DHCP servers provide automatic IP address allocation across the network.

![DHCP](screenshots/dhcp-working.png)

---

## Web Services

### Private Web Server

Internal users can access the corporate web server.

![Private Web](screenshots/private-web.png)

### Public Web Server

Static NAT publishes the internal web server to the simulated Internet.

![Public Web](screenshots/public-web.png)

---

## Connectivity Validation

Connectivity between different departments and remote sites has been successfully verified.

![Ping Validation](screenshots/ping-between-sites.png)

---

# Learning Outcomes

This project allowed me to gain practical experience with:

- Enterprise network design
- Hierarchical network architectures
- Layer 2 and Layer 3 switching
- VLAN implementation
- Inter-VLAN routing
- Dynamic routing with OSPF
- DHCP deployment
- Network redundancy
- ACL configuration
- Static NAT
- IPv4 and IPv6 networking
- Cisco Packet Tracer

---

# Repository Contents

- Complete Packet Tracer project
- Technical documentation
- Configuration screenshots
- Network validation results

---

# License

This project is licensed under the **MIT License**.

See the [LICENSE](LICENSE) file for more information.
