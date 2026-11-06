
# ABYSSINIA TECHNOLOGIES PLC

# ENTERPRISE HEADQUARTERS NETWORK
# DESIGN AND IMPLEMENTATION REPORT

## 1. Executive Summary

This project proposes an enterprise network infrastructure
for Abyssinia Technologies PLC.

The design supports four departments, 48 current
employees, and a planned capacity of 100 employees.

The proposed architecture uses hierarchical switching
and an IPv4 addressing scheme based on VLSM.

## 2. Introduction

The company requires a structured and scalable network
to support communication and resource sharing between
its departments.

## 3. Problem Statement

The company requires an organized network architecture
that supports its current operations and future growth.

## 4. Project Objectives

- Design an enterprise network topology.
- Calculate departmental subnets using VLSM.
- Configure Cisco network devices.
- Assign static IP addresses.
- Verify connectivity.
- Identify and resolve configuration errors.

## 5. Requirements Analysis

Administration: 40 planned hosts
IT: 25 planned hosts
HR: 20 planned hosts
Finance: 15 planned hosts

Assigned network: 192.168.10.0/24

## 6. Network Architecture

The network follows a hierarchical physical design with a core
switch connected to four departmental access switches. Each
access switch connects to the local department PCs and printers,
while the core switch provides VLAN segmentation and inter-VLAN
routing.

The topology includes a WAN router connected to the external ISP
network and a DNS server in the IT VLAN connected to the DSW-CORE.

## 7. IP Addressing Design

The assigned network is 192.168.10.0/24 and VLSM was used to
allocate departmental subnets as follows:

- Administration: 192.168.10.0/26
- IT: 192.168.10.64/27
- HR: 192.168.10.96/27
- Finance: 192.168.10.128/27
- DNS server: 192.168.10.67/27
- Management VLAN: 192.168.10.192/27

The core switch uses SVI gateways for each VLAN, while the router
uses 192.168.10.222/27 on the LAN side and 176.16.0.2/30 on the WAN side.
## 8. Hardware and Software Requirements

Hardware:
- Cisco 2911 router
- Cisco 3560 multilayer switch
- Cisco 2960 access switches
- Workstations
- Internal server

Software:
- Cisco Packet Tracer
- Visual Studio Code

## 9. Implementation

The implementation includes:
- DSW-CORE as the layer-3 switching and DHCP server
- ASW-IT, ASW-FINANCE, ASW-HR, and ASW-ADMIN as departmental access switches
- VLAN assignment by department: IT=20, FINANCE=30, HR=40, ADMIN=50
- Native VLAN 99 and management VLAN 100
- Trunks configured between the core and each access switch
- DHCP pools configured for each department subnet
- DNS server at 192.168.10.67 in the IT VLAN
- SSH enabled on each switch with local authentication

## 10. Testing and Verification

Current configuration verification confirms the following:
- VLANs are created and assigned correctly
- Access ports are mapped to their department VLANs
- Trunks allow only the required VLANs
- Inter-VLAN routing is enabled on DSW-CORE
- DHCP pools are configured for each department subnet
- Static routes are configured for internal reachability and WAN access

Actual ping and command-output testing remains to be completed in the lab environment.
## 11. Troubleshooting

Document each identified fault, its root cause,
corrective action, and verification results.

## 12. Limitations

This phase does not implement:
- VLAN segmentation
- Inter-VLAN routing
- DHCP
- OSPF
- ACLs
- Firewall policies
- Network redundancy

## 13. Future Recommendations

Future development should introduce departmental
VLANs, trunk links, inter-VLAN routing, DHCP,
OSPF, ACLs, firewall security, and monitoring.

## 14. Conclusion

Summarize the implemented design, subnet allocation,
testing results, and future expansion opportunities.
