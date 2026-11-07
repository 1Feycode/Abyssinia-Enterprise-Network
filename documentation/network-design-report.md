# Enterprise Headquarters Network
## Design and Implementation Report

## 1. Executive summary

This Packet Tracer project models a headquarters network for Abyssinia
Technologies PLC. It serves four departments, plans for growth from 48 to 100
employees, and uses departmental VLANs, a multilayer switch, DHCP, and a
simulated WAN edge. Screenshots provide evidence for selected client,
switching, server, and routing checks. Tests without evidence are listed as
pending rather than assumed successful.

## 2. Requirements and architecture

The design separates Administration, IT, HR, and Finance at Layer 2 and uses
DSW-CORE for inter-VLAN routing and departmental default gateways. Four access
switches connect departmental endpoints to the core using 802.1Q trunks. The
core connects the DNS/web server and R1-WAN; R1-WAN connects to a simulated
upstream cloud.

### VLANs and subnets

| Purpose | VLAN | Subnet | Gateway / address |
|---|---:|---|---|
| Administration | 50 | `192.168.10.0/26` | `192.168.10.1` |
| IT | 20 | `192.168.10.64/27` | `192.168.10.94` |
| HR | 40 | `192.168.10.96/27` | `192.168.10.126` |
| Finance | 30 | `192.168.10.128/27` | `192.168.10.158` |
| Management | 100 | `192.168.10.192/27` | `192.168.10.193` |
| Core-to-router transit | — | `176.16.0.0/30` | Core `.1`, router `.2` |
| Simulated upstream | — | `200.64.100.0/24` | Router `.2`, next hop `.1` |

The departmental and management allocations are within
`192.168.10.0/24`. The transit and simulated upstream networks are separate
links. The detailed host assignments and exclusions are in the
[IP address table](../ip-addressing/ip-addressing-table.csv); the subnet
calculations are in [VLSM calculations](../ip-addressing/vlsm-calculations.md).

## 3. Device roles and services

- **DSW-CORE:** VLAN gateways, inter-VLAN routing, DHCP pools, and default route
  toward R1-WAN.
- **ASW-IT, ASW-FINANCE, ASW-HR, ASW-ADMIN:** endpoint access ports and trunks
  to DSW-CORE; management addresses are in VLAN 100.
- **DNS/web server:** static `192.168.10.67/27`, gateway `192.168.10.94`.
  Provides DNS and hosts the company web page. The evidence shows its IP
  configuration and HTTP access by IP address.
- **IT-Server:** file-storage server at `192.168.10.68/27` using FTP. Evidence
  shows a successful client login and directory listing; file upload/download
  still needs to be verified.
- **R1-WAN:** routed core transit, simulated upstream interface, static routes,
  and NAT overload configuration.

## 4. Security and design boundaries

Department VLANs provide Layer 2 segmentation, but the current core routes
between them and no inter-VLAN ACLs are configured. Do not describe departments
as access-isolated. Switch templates enable SSH and shut down unused access
ports; they use credential placeholders that must be replaced locally.

The `.pkt` file may contain credentials from the simulation. Rotate or remove
those credentials before publishing the file. The simulated upstream network
does not represent verified Internet connectivity.

## 5. Verification summary

Available screenshots show a DHCP address on IT-PC1, successful pings to the
core transit interface, router transit interface, and router's simulated WAN
interface, plus an HTTP page loaded from the server by IP. An inter-VLAN ping
from IT-PC1 to an HR address received three of four replies after an initial
timeout. Repeat this test to confirm steady-state behavior.

Same-VLAN client-to-client tests, DNS resolution by hostname, FTP file
upload/download, and end-to-end upstream access are not evidenced. The detailed
results and screenshot links are in the [connectivity test report](../testing/connectivity-tests.md).

## 6. Recommendations

1. Re-run the initial-timeout inter-VLAN test and test client pairs within each
   department.
2. Enable and verify DNS records, then test name resolution rather than only
   opening the web server by IP.
3. Test an authorized FTP file upload and download; current evidence confirms
   login and directory listing only.
4. Define and test inter-department ACLs and restrict management access.
5. Validate NAT and routing to a simulated host beyond R1-WAN.
6. Consider redundant links, switch hardening, and a consistent configuration
   backup process as future improvements.
