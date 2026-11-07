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
core connects separate DNS, web, and FTP servers and R1-WAN; R1-WAN connects
to a simulated upstream cloud.

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
- **DNS server:** static `192.168.10.67/27`, gateway `192.168.10.94`. It
  provides DNS; FIN-PC1 successfully loaded the web page by hostname.
- **Web server:** static `192.168.10.69/27`, gateway `192.168.10.94`. Its IP
  configuration and HTTP service are captured. FIN-PC1 successfully browsed
  to `http://www.abyssinia.com`; the earlier browser screenshot targeting `.67`
  predates the separate web server.
- **IT-Server:** file-storage server at `192.168.10.68/27` using FTP. Evidence
  shows a successful client login and directory listing; file upload/download
  still needs to be verified.
- **R1-WAN:** routed core transit, simulated upstream interface, static routes,
  and NAT overload configuration.

## 4. Security and design boundaries

The DSW-CORE reference template applies the named extended ACL
`IT-INBOUND-PING-RESTRICTION` outbound on VLAN 20. It denies routed ICMP echo
requests to IT host addresses and permits all other IP traffic. Because traffic
to the SVI's own gateway address is handled by the switch rather than
forwarded out the SVI, this ACL does not block pings to `192.168.10.94`.
IT clients can initiate pings to other VLANs and receive replies. Same-VLAN
client traffic is switched locally and is not filtered by this SVI ACL. The
policy is not full isolation or a general inter-VLAN firewall. The ACL is
present in the template but has not yet been confirmed in the Packet Tracer
simulation. Switch templates enable SSH and shut down unused access ports; they
use credential placeholders that must be replaced locally.

The `.pkt` file may contain credentials from the simulation. Rotate or remove
those credentials before publishing the file. The simulated upstream network
does not represent verified Internet connectivity.

## 5. Verification summary

Screenshots show successful same-VLAN ping commands, DNS-based browsing from
FIN-PC1, FTP login and directory listing, and pings to the core transit,
router transit, and router simulated-WAN interfaces. However, the IT-PC1
same-VLAN ping target matches its captured own address, so that screenshot
does not prove client-to-client reachability. Several IT-initiated inter-VLAN
captures show an initial timeout followed by three replies. The ACL behavior,
FTP file transfers, direct-IP HTTP access from IT-PC1, and reachability beyond
the router remain unverified. See the [connectivity test report](../testing/connectivity-tests.md)
for exact results and evidence.

## 6. Recommendations

1. Apply the VLAN 20 ping ACL and capture both a denied ping from another VLAN
   to an IT host and a successful ping initiated by an IT client. Note that
   this ACL does not block pinging the VLAN 20 gateway.
2. Capture direct-IP HTTP access to `192.168.10.69`; hostname-based browsing
   from FIN-PC1 is already evidenced.
3. Test an authorized FTP file upload and download; current evidence confirms
   login and directory listing only.
4. Consider additional inter-department ACLs and restrict management access.
5. Confirm same-VLAN ping destinations match the other clients' current
   addresses, then recapture any inconclusive tests.
6. Validate NAT and routing to a simulated host beyond R1-WAN.
7. Consider redundant links, switch hardening, and a consistent configuration
   backup process as future improvements.
