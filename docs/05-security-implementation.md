# Security Implementation

## Overview

Security is a fundamental aspect of this enterprise network. The infrastructure combines network segmentation, access control, perimeter protection, address translation, and encrypted communications to protect internal resources while allowing secure access to public services.

The design follows a defense-in-depth approach by applying multiple security layers across the network.

---

## Security Objectives

The implementation was designed to achieve the following goals:

- Protect the internal corporate network from external threats.
- Isolate departments using VLAN segmentation.
- Restrict access to critical servers.
- Secure Internet-facing services.
- Protect communications between sites.
- Provide secure remote access for employees.
- Ensure high availability of security services.

---

## Network Segmentation

The enterprise network uses IEEE 802.1Q VLANs to isolate departments and critical infrastructure.

### Department VLANs

| VLAN | Department |
|------|------------|
|100|Research|
|200|Commercial|
|300|Sales|
|400|Training|
|500|Technical Support|

### Infrastructure VLANs

| VLAN | Purpose |
|------|---------|
|600|DHCP Servers|
|700|Compute & Storage Servers|
|800|Corporate Web Server (DMZ)|
|900|Guest Network|

This segmentation reduces broadcast domains, improves security, and simplifies network management.

---

## Access Control Lists (ACLs)

Extended ACLs protect the Compute Server VLAN (VLAN 700).

Only the Research and Technical Support departments from Headquarters and Branch 1 are authorized to access the compute servers.

Allowed networks include:

- HQ Research
- HQ Technical Support
- Branch 1 Research
- Branch 1 Technical Support

All other traffic destined for VLAN 700 is denied.

This policy follows the principle of least privilege and protects critical enterprise resources.

---

## Firewall Protection

A Cisco ASA firewall protects the perimeter of the corporate network.

The firewall is positioned between the internal infrastructure and the Internet edge routers, filtering inbound and outbound traffic before it reaches internal services.

Its primary responsibilities include:

- Perimeter traffic filtering
- Protection of public services
- Basic Layer 3 and Layer 4 security
- Isolation of the DMZ

---

## NAT Security

The enterprise uses both Dynamic NAT (PAT) and Static NAT.

### Dynamic NAT

Internal private IPv4 addresses are translated before accessing the Internet, hiding the internal addressing scheme from external networks.

### Static NAT

The corporate web server is published using Static NAT.

Internal address:

- 192.168.80.10

Public address:

- 200.1.1.1

This allows Internet users to access the web service without exposing the internal network.

---

## DMZ Design

The corporate web server is placed inside a dedicated DMZ located in VLAN 800.

The DMZ separates public services from the internal corporate network while allowing controlled Internet access through the firewall.

This architecture reduces the attack surface and limits the impact of potential compromises.

---

## Guest Network Isolation

Visitors connect to a dedicated wireless SSID named **Guests**.

The Guest Network operates on VLAN 900 and is completely isolated from the corporate infrastructure.

Guest users are allowed Internet access only.

ACLs prevent any communication with internal departments or servers.

---

## VPN Security

The project implements two VPN solutions.

### Remote Access VPN

Employees can securely connect from external locations.

The VPN provides encrypted access to internal corporate resources while authenticating users before network access is granted.

### Site-to-Site VPN

A permanent IPsec VPN tunnel protects communications between Headquarters and Branch 1.

This ensures confidentiality and integrity of data transmitted across the WAN.

---

## High Availability

Several mechanisms improve the resilience of the security infrastructure.

These include:

- HSRP virtual gateway redundancy
- Dual Internet providers
- Redundant DHCP servers
- Redundant multilayer core switches

These mechanisms minimize downtime in case of hardware or link failures.

---

## Security Validation

The security implementation was validated through multiple tests.

The following functionality was successfully verified:

- Authorized hosts can access the Compute Servers.
- Unauthorized departments are blocked by ACLs.
- Guest users cannot access internal resources.
- Public access to the corporate website works through Static NAT.
- VPN connections establish successfully.
- HSRP maintains gateway availability during failures.

Relevant validation screenshots are available in the `screenshots/` directory.

---

## Design Decisions

Several design choices were made to improve both security and scalability.

These include:

- VLAN-based network segmentation.
- Principle of least privilege using ACLs.
- DMZ isolation for public services.
- Centralized security through a Cisco ASA firewall.
- Encrypted VPN communications.
- Dual ISP redundancy for Internet connectivity.
- Structured IPv4 addressing to simplify ACL management.

Together, these decisions provide a secure, scalable, and fault-tolerant enterprise network suitable for medium-sized organizations.
