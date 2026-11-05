
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

The network follows a hierarchical physical design
with a distribution switch connected to four
departmental access switches.

Include the Packet Tracer topology screenshot here.

## 7. IP Addressing Design

Include the complete VLSM calculation and
IP addressing table here.

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

Explain:
- Device placement
- Physical connections
- Switch hostname configuration
- Workstation IP configuration

## 10. Testing and Verification

Include actual ping results, switch command
outputs, and observations.

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
