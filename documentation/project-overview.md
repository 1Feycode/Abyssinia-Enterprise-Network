# Project Overview

## Organization and need

Abyssinia Technologies PLC is represented as a growing organization with a
headquarters network for Administration, Information Technology, Human
Resources, and Finance. The design supports 48 current employees and plans for
100 employees.

## Objectives

- Organize departmental traffic with VLANs and a hierarchical switch design.
- Allocate IPv4 subnets for departments and network management.
- Provide inter-VLAN routing and dynamically assigned client addresses.
- Connect the internal network to a simulated WAN through a router.
- Record implementation evidence and distinguish verified results from
  outstanding tests.

## Department capacity

| Department | Current employees | Planned capacity | VLAN | Subnet |
|---|---:|---:|---:|---|
| Administration | 18 | 40 | 50 | `192.168.10.0/26` |
| IT | 12 | 25 | 20 | `192.168.10.64/27` |
| HR | 10 | 20 | 40 | `192.168.10.96/27` |
| Finance | 8 | 15 | 30 | `192.168.10.128/27` |
| **Total** | **48** | **100** |  |  |

Management uses VLAN 100 and `192.168.10.192/27`. VLAN 99 is reserved as the
trunk native VLAN. The Layer 3 transit link and simulated WAN use separate
address blocks, as detailed in the [address plan](../ip-addressing/).

## Implemented design

- DSW-CORE is the Layer 3 distribution switch, departmental default gateway,
  and DHCP server.
- Four access switches connect departmental endpoints over 802.1Q trunks.
- The core also connects a DNS/web server with static address
  `192.168.10.67/27`; it provides DNS and hosts the company web page.
- A separate IT-Server is intended for departmental file storage using FTP.
  Its configured IP address and FTP operation still need to be recorded and
  tested.
- R1-WAN provides a routed transit to the core, a simulated upstream interface,
  static routes, and configured NAT overload.
- SSH configuration is included in the switch templates.

The current configuration routes between department VLANs and has no ACLs
blocking that traffic. NAT and the upstream route are configured in the text
template, but end-to-end upstream access has not been demonstrated by the
available evidence.

## Scope and limitations

This is a Packet Tracer learning project, not a production deployment. DNS
lookup by hostname, FTP file transfer, same-department client-to-client tests,
ACL policy, redundancy, and end-to-end WAN access remain to be verified or
implemented. Add the FTP server address to the address table after checking its
Packet Tracer configuration.

See the [network design report](network-design-report.md), [implementation
procedure](implementation-procedure.md), and [connectivity test report](../testing/connectivity-tests.md)
for details.
