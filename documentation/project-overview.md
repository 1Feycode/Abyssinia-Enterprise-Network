
# Project Overview

## 1. Organization
Abyssinia Technologies PLC

## 2. Background
Abyssinia Technologies PLC is a growing technology
company that requires a structured network
infrastructure to support communication and
resource sharing between its departments.

## 3. Existing Problem
The organization requires an organized and scalable
network infrastructure capable of supporting its
current employees and future expansion.

## 4. Proposed Solution
Design a hierarchical enterprise network consisting
of a distribution switch, departmental access
switches, workstations, an internal server, and a
WAN edge router representation.

## 5. Departments

| Department | Current Employees | Planned Capacity |
|---|---:|---:|
| Administration | 18 | 40 |
| IT | 12 | 25 |
| HR | 10 | 20 |
| Finance | 8 | 15 |
| Total | 48 | 100 |

## 6. Project Scope
This implementation phase focuses on the physical topology,
IPv4 addressing, VLSM, VLAN segmentation, inter-VLAN routing,
DHCP, DNS, SSH management, static routing, and basic troubleshooting.

## 7. Current Implementation Status
The project currently includes:
- Department-based VLANs: IT=20, Finance=30, HR=40, Admin=50
- Native VLAN 99 and management VLAN 100
- Trunk links between access switches and the DSW-CORE switch
- Inter-VLAN routing on DSW-CORE
- DHCP pools for each departmental subnet
- Static DNS server on the IT VLAN at 192.168.10.67
- SSH access enabled on all switches
- Routing between internal subnets and the WAN router

## 8. Expected Outcome
A working VLAN-based enterprise network foundation that supports
segmentation, inter-VLAN communication, centralized DHCP, and
basic secure administrative access. Further enhancements such as
NAT, ACLs, OSPF, and more advanced WAN security remain for later phases.
