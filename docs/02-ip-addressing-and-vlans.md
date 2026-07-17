# IP Addressing and VLAN Design

## Overview

This document describes the IP addressing scheme and VLAN segmentation implemented in the enterprise network.

The addressing plan has been designed to provide scalability, simplify network administration, reduce broadcast traffic, and improve security by separating departments into independent VLANs. IPv4 is deployed at Headquarters (HQ) and Branch 1 (B1), while Branch 2 (B2) operates exclusively with IPv6.

---

# IPv4 Addressing Plan

## Headquarters (HQ)

| VLAN | Department / Service | Network |
|------|----------------------|----------------|
| 100 | Research | 192.168.10.0/24 |
| 200 | Commercial | 192.168.20.0/24 |
| 300 | Sales | 192.168.30.0/24 |
| 400 | Training | 192.168.40.0/24 |
| 500 | Technical Support | 192.168.50.0/24 |
| 600 | DHCP Servers | 192.168.60.0/24 |
| 700 | Compute Servers | 192.168.70.0/24 |
| 800 | Internal Web Server | 192.168.80.0/24 |
| 900 | Guest Network | 192.168.90.0/24 |

---

## Branch 1 (B1)

| VLAN | Department | Network |
|------|------------|----------------|
| 100 | Research | 192.168.11.0/24 |
| 200 | Commercial | 192.168.21.0/24 |
| 300 | Sales | 192.168.31.0/24 |
| 400 | Training | 192.168.41.0/24 |
| 500 | Technical Support | 192.168.51.0/24 |

---

## WAN Addressing

Communication between Headquarters and Branch 1 is established using dedicated point-to-point WAN links with /30 IPv4 addressing.

---

# IPv6 Addressing Plan

Branch 2 operates entirely using IPv6.

## Corporate Prefix

```
2001:DB8:CAFE::/48
```

## Branch 2 Networks

| VLAN | Department | IPv6 Prefix |
|------|------------|----------------------------|
| 100 | Research | 2001:DB8:CAFE:2100::/64 |
| 400 | Training | 2001:DB8:CAFE:2400::/64 |

### WAN Link

```
2001:DB8:CAFE:2F::/64
```

Hosts automatically configure their IPv6 addresses using SLAAC (Stateless Address Autoconfiguration).

---

# VLAN Design

The enterprise network is segmented using IEEE 802.1Q VLANs.

Each department is assigned to its own VLAN to improve security, reduce broadcast domains, and simplify administration.

Trunk links transport multiple VLANs between switches, while access ports connect end-user devices to their corresponding departmental VLAN.

A dedicated Guest Network (VLAN 900) provides Internet connectivity for visitors while remaining completely isolated from the corporate infrastructure.

---

# Department Distribution

## Headquarters (HQ)

The Headquarters hosts all five corporate departments:

- VLAN 100 – Research
- VLAN 200 – Commercial
- VLAN 300 – Sales
- VLAN 400 – Training
- VLAN 500 – Technical Support

---

## Branch 1 (B1)

Branch 1 replicates the same departmental structure as Headquarters:

- Research
- Commercial
- Sales
- Training
- Technical Support

---

## Branch 2 (B2)

Branch 2 is a smaller office that contains only:

- Research
- Training

Both departments operate exclusively with IPv6.

---

# DHCP Configuration

IPv4 address assignment is provided by two DHCP servers located in VLAN 600 at Headquarters.

The DHCP pools are divided between both servers to provide high availability. If one server becomes unavailable, the second server continues assigning IP addresses automatically.

Branch 2 does not use DHCP for IPv6. Instead, hosts obtain their IPv6 addresses automatically using SLAAC.

---

# IP Helper Address

Because DHCP broadcasts cannot cross Layer 3 boundaries, each VLAN interface forwards DHCP requests to both DHCP servers using the following helper addresses:

```text
ip helper-address 192.168.60.2
ip helper-address 192.168.60.3
```

This allows clients in every VLAN to receive IP configuration regardless of their subnet.

---

# Inter-VLAN Routing

Inter-VLAN routing is implemented using Switch Virtual Interfaces (SVIs).

- Headquarters performs routing on the redundant multilayer switches.
- Branch 1 performs routing on its local multilayer switch.
- Branch 2 enables IPv6 routing using `ipv6 unicast-routing` together with IPv6 SVIs.

This architecture allows communication between VLANs while maintaining logical network segmentation.

---

# Design Decisions

Several design choices were made to improve network efficiency and future scalability.

## IPv4 /24 Subnets

The use of /24 networks provides:

- Sufficient address space for each department.
- A consistent addressing scheme across all sites.
- Simpler network administration.
- Future scalability.
- Full compatibility with dynamic routing using OSPF.

## VLAN Segmentation

Departments are separated into individual VLANs to:

- Reduce broadcast traffic.
- Improve network performance.
- Increase security.
- Simplify policy management.
- Restrict access to sensitive resources such as the compute servers.

## SLAAC for IPv6

Branch 2 uses SLAAC to automatically generate IPv6 addresses, eliminating the need for a dedicated DHCPv6 server.

## Guest Network

The Guest VLAN (VLAN 900) is completely isolated from the corporate network and uses an independent DHCP pool, allowing visitors to access the Internet without reaching internal company resources.

---

# Related Screenshots

The following screenshots illustrate the addressing and VLAN configuration:

- **topology.png** – Enterprise network topology.
- **vlans.png** – VLAN configuration on the Headquarters multilayer switch.
- **dhcp-working.png** – Successful DHCP address assignment.
