# Enterprise Multi-Site Network Design

Academic project focused on the design and implementation of a secure corporate network using Cisco Packet Tracer.

The project simulates the network infrastructure of a company with a headquarters (HQ) and remote branches, applying network segmentation, dynamic routing, redundancy and secure access to internal services.

---

## Project Objectives

- Design a scalable enterprise network from scratch.
- Connect the headquarters with remote offices.
- Separate departments using VLANs.
- Implement inter-VLAN routing.
- Provide automatic IP address assignment using DHCP.
- Configure dynamic routing between sites with OSPF.
- Ensure high availability for critical services.
- Protect sensitive resources using ACLs.
- Publish an internal web server through Static NAT.
- Prepare the infrastructure for future expansion.

---

## Technologies Used

- Cisco Packet Tracer
- Cisco Multilayer Switches
- Cisco Access Switches
- Cisco Routers

### Networking Technologies

- VLANs
- Inter-VLAN Routing
- Trunk Links (802.1Q)
- DHCP
- OSPF
- HSRP
- ACLs
- Static NAT
- IPv4
- IPv6 (Branch 2 planning)

---

## Network Architecture

The network consists of:

- Headquarters (HQ)
- Branch Office 1 (B1)
- Branch Office 2 (IPv6 design)
- Departmental VLAN segmentation
- Server network
- Compute server network
- Private web server
- Public web server via Static NAT
- Guest network

---

## Implemented Features

- VLAN creation for every department
- Inter-VLAN routing using Multilayer Switches
- Trunk configuration between switches
- Redundant DHCP servers
- DHCP Relay (`ip helper-address`)
- OSPF dynamic routing
- High Availability using HSRP
- Access Control Lists (ACLs)
- Static NAT for public web publishing
- Internal and external web access validation
- Guest network segmentation

---

## Security Features

- Department isolation using VLANs
- ACLs protecting compute servers
- Restricted access to sensitive resources
- Static NAT for secure publication of web services
- Network segmentation for internal and guest users

---

## Repository Structure

```
enterprise-network-design/
│
├── packet-tracer/
│   └── enterprise-network.pkt
│
├── images/
│   ├── topology.png
│   ├── vlans.png
│   ├── ospf-neighbors.png
│   ├── routing-table1.png
│   ├── routing-table2.png
│   ├── routing-table3.png
│   ├── acl-server-access.png
│   ├── dhcp-working.png
│   ├── hsrp.png
│   ├── private-web.png
│   ├── public-web.png
│   └── ping-between-sites.png
│
└── README.md
```

---

## Skills Developed

- Enterprise network design
- VLAN planning
- IP addressing
- Layer 3 switching
- Dynamic routing with OSPF
- High availability using HSRP
- DHCP configuration
- Network segmentation
- Access Control Lists (ACLs)
- Static NAT
- Cisco Packet Tracer simulation
- Network troubleshooting

---

## Screenshots

### Network Topology

Complete enterprise network implemented in Cisco Packet Tracer.

![Topology](screenshots/topology.png)

---

### VLAN Configuration

Department VLANs configured on the HQ multilayer switch.

![VLANs](screenshots/vlans.png)

---

### OSPF Neighbors

Successful OSPF adjacency between network devices.

![OSPF](screenshots/ospf-neighbors.png)

---

### Routing Tables

Dynamic routes learned through OSPF.

![Routing](screenshots/routing-table1.png)

---

### Access Control Lists

ACL protecting the compute server network.

![ACL](screenshots/acl-server-access.png)

---

### DHCP Operation

Automatic IP assignment using redundant DHCP servers.

![DHCP](screenshots/dhcp-working.png)

---

### HSRP Configuration

Gateway redundancy for critical services.

![HSRP](screenshots/hsrp.png)

---

### Private Web Server

Internal access to the corporate web server.

![Private Web](screenshots/private-web.png)

---

### Public Web Server

Access to the published web server using Static NAT.

![Public Web](screenshots/public-web.png)

---

### Connectivity Test

Successful communication between different network segments.

![Ping](screenshots/ping-between-sites.png)

---

## Future Improvements

- Complete IPv6 deployment for Branch 2.
- Implement secure remote-access VPN.
- Add monitoring and security event detection.
- Improve firewall policies.
- Perform performance and scalability testing.

---

## Academic Information

**Degree:** Bachelor's Degree in Telecommunications Engineering

**Course:** Computer Networks / Enterprise Network Design

**Simulation Tool:** Cisco Packet Tracer
