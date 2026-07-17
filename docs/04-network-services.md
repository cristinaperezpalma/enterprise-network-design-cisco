# Network Services

## Overview

The enterprise network integrates multiple services to provide reliable connectivity, centralized management, secure remote access, and high availability. Critical services include DHCP, NAT, VPN, wireless networking, web hosting, and centralized server infrastructure.

The Headquarters (HQ) hosts all core services, while Branch 1 accesses them remotely through the WAN infrastructure. Branch 2 operates using native IPv6 with SLAAC for automatic address assignment.

---

# DHCP Services

Dynamic IPv4 address allocation is centrally managed from the Headquarters.

Two dedicated DHCP servers located in **VLAN 600** provide IP configuration to all IPv4 corporate networks.

Branch 1 receives DHCP services remotely through the WAN infrastructure, while Branch 2 does not require DHCP because all IPv6 hosts configure themselves automatically using SLAAC.

---

# DHCP High Availability

To eliminate single points of failure, the DHCP service is implemented using two independent servers:

- **SRV-DHCP1**
- **SRV-DHCP2**

Both servers operate using split address pools, allowing address allocation to continue even if one server becomes unavailable.

This design increases service availability and improves network reliability.

<p align="center">
<img src="../screenshots/dhcp-working.png" width="900">
</p>

---

# IP Helper Address

Because DHCP requests are Layer 2 broadcasts, they cannot cross VLAN boundaries.

Cisco multilayer switches use **IP Helper Address** to relay DHCP requests from client VLANs to the centralized DHCP servers located in VLAN 600.

The helper addresses configured are:

- **192.168.60.2**
- **192.168.60.3**

This configuration allows all departments to receive automatic IP addressing regardless of their VLAN.

---

# DNS

The project references the Domain Name System (DNS) as part of the enterprise infrastructure.

However, the documentation does not include specific DNS server configurations, records, or implementation details.

---

# Corporate Web Server

The corporate web server is hosted at Headquarters inside **VLAN 800**, where it is isolated from the rest of the internal infrastructure.

Server characteristics:

- Private IP address: **192.168.80.10**
- Dedicated server VLAN
- Protected by the perimeter firewall
- High availability gateway provided by HSRP

Internal users access the service directly using its private address.

<p align="center">
<img src="../screenshots/private-web.png" width="900">
</p>

---

# Static NAT for Public Web Access

The web server is published to the Internet using **Static NAT**.

A one-to-one address translation maps the internal server to a public IP address, allowing external users to access the corporate website securely.

Internal Address

- **192.168.80.10**

Public Address

- **198.51.100.1**

This approach exposes only the required service while keeping the remainder of the internal infrastructure private.

<p align="center">
<img src="../screenshots/public-web.png" width="900">
</p>

---

# Dynamic NAT and Internet Access

Internet access for internal users is provided through **Dynamic NAT with PAT**.

Private IPv4 addresses are translated into public addresses before reaching the Internet.

The enterprise also implements redundant Internet connectivity using two independent ISPs.

Primary Public IP:

- **198.51.100.1**

Backup Public IP:

- **198.51.100.5**

Automatic failover is achieved using floating static routes with different administrative distances.

---

# VPN Services

The project includes secure Virtual Private Network (VPN) connectivity to protect communications across the enterprise.

Two VPN solutions are implemented:

- Remote Access VPN
- Site-to-Site VPN

---

# Remote Access VPN

The Remote Access VPN allows teleworkers to connect securely to the Headquarters network.

VPN Configuration:

| Parameter | Value |
|-----------|-------|
| Public IP | 198.51.100.1 |
| Group Name | VPN TELE |
| Group Key | cisco123 |

This configuration provides encrypted access to internal corporate resources from external networks.

---

# Site-to-Site VPN

A permanent Site-to-Site VPN securely connects Headquarters with Branch 1.

This encrypted tunnel protects communications between both locations while allowing transparent access to internal resources.

---

# Wireless Network

Wireless connectivity is provided through Cisco Aironet access points connected to the access layer switches.

The wireless infrastructure supports both:

- Corporate users
- Guest users

Separate wireless networks improve both security and usability.

---

# Guest Network

Guest wireless access is isolated from the corporate infrastructure.

Main characteristics include:

- SSID: **Invitados**
- VLAN 900
- Network: **192.168.90.0/24**
- Independent DHCP pool
- Internet-only access
- Internal network isolation through ACLs

This design allows visitors to access the Internet without exposing internal corporate resources.

---

# Server Infrastructure

All enterprise servers are centralized at the Headquarters data center.

The infrastructure includes:

| Service | VLAN |
|----------|------|
| DHCP Servers | VLAN 600 |
| Compute & Storage Servers | VLAN 700 |
| Corporate Web Server | VLAN 800 |

Servers are connected directly to the multilayer switches using dedicated Gigabit Ethernet links to maximize performance.

---

# Service Validation

Several validation tests confirmed the correct operation of all implemented services.

The following functionality was successfully verified:

- Automatic DHCP address assignment
- Internal web server access
- External web access through Static NAT
- Successful VPN connection establishment

The validation confirms that all critical enterprise services operate correctly under normal conditions.

---

# Design Decisions

Several architectural decisions were made to improve reliability and simplify network management.

These include:

- Centralized server infrastructure at Headquarters.
- Dual DHCP servers for high availability.
- Static addressing for critical servers.
- Static NAT for secure publication of the corporate website.
- Dynamic NAT for Internet connectivity.
- VPN deployment for secure remote communications.
- Guest network isolation through VLAN segmentation and ACLs.

Together, these decisions provide a scalable, secure, and fault-tolerant enterprise network suitable for future expansion.

---

# Skills Demonstrated

- DHCP deployment
- DHCP Relay (IP Helper Address)
- Static NAT
- Dynamic NAT (PAT)
- Web server publication
- Remote Access VPN
- Site-to-Site VPN
- Enterprise wireless networking
- Guest network isolation
- High availability services
- Enterprise server infrastructure
