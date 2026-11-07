# Abyssinia Technologies PLC
## Enterprise Headquarters Network

A Cisco Packet Tracer project documenting a small, expandable headquarters
network for four departments: Administration, IT, Human Resources, and Finance.
The design uses department VLANs, Layer 3 switching, DHCP, a simulated WAN edge,
an IT file/FTP server, and separate DNS and web servers.

> **Project status:** The Packet Tracer simulation and supporting evidence are
> included. Some connectivity checks are demonstrated in screenshots; the
> remaining checks are explicitly marked as pending in the test report.

## At a glance

| Area | Design |
|---|---|
| Current / planned staff | 48 / 100 |
| Departments | Administration, IT, HR, Finance |
| Switching | One multilayer distribution switch and four access switches |
| Department VLANs | IT 20, Finance 30, HR 40, Administration 50 |
| Shared VLANs | Native 99, management 100 |
| Internal addressing | `192.168.10.0/24`, subnetted with VLSM |
| Routing and services | Inter-VLAN routing and DHCP on DSW-CORE; static routing and NAT on R1-WAN |
| Simulation | Cisco Packet Tracer; the upstream cloud is simulated |

## Architecture

```mermaid
flowchart TB
    UP["Simulated upstream<br/>200.64.100.0/24"] --- R1["R1-WAN<br/>Gi0/1: 200.64.100.2"]
    R1 ---|"Transit 176.16.0.0/30"| CORE["DSW-CORE<br/>SVI gateways, DHCP, inter-VLAN routing"]
    CORE ---|"VLAN 20"| DNS["DNS server<br/>192.168.10.67"]
    CORE ---|"VLAN 20"| WEB["Web server<br/>192.168.10.69"]
    CORE ---|"802.1Q trunks"| IT["ASW-IT<br/>VLAN 20"]
    CORE ---|"802.1Q trunks"| HR["ASW-HR<br/>VLAN 40"]
    CORE ---|"802.1Q trunks"| FIN["ASW-FINANCE<br/>VLAN 30"]
    CORE ---|"802.1Q trunks"| ADMIN["ASW-ADMIN<br/>VLAN 50"]
    IT --- ITPC["IT clients"]
    IT --- FTP["IT-Server<br/>file storage / FTP<br/>192.168.10.68"]
    HR --- HRPC["HR clients and printer"]
    FIN --- FINPC["Finance clients and printer"]
    ADMIN --- ADMINPC["Administration clients and printer"]
```

The [Packet Tracer topology screenshot](packet-tracer/Topology.png) shows the
simulation workspace.

The multilayer switch provides departmental gateways and connects the access
switches, separate DNS and web servers, the FTP server, and the WAN router.
Department VLANs are routed by the core; the current configuration does not
include ACLs to restrict inter-department traffic. The web server's IP
configuration is captured; verify HTTP and DNS name resolution against the
separate services before marking them complete. The IT-Server provides file
storage over FTP at `192.168.10.68`; a successful login and directory listing
are captured, while file upload/download still needs verification.

## Evidence

The screenshots are captured from the Packet Tracer implementation. Each has a
descriptive filename and is indexed in the [evidence guide](evidence/README.md).

## Repository guide

| Path | Contents |
|---|---|
| [packet-tracer/](packet-tracer/) | Packet Tracer simulation, topology, and server page |
| [configs/](configs/) | Device configuration templates |
| [documentation/](documentation/) | Project overview, design report, and implementation procedure |
| [ip-addressing/](ip-addressing/) | VLSM calculations and device/address table |
| [testing/](testing/) | Test cases, observed results, and pending verification |
| [troubleshooting/](troubleshooting/) | Planned fault scenarios and verification status |
| [evidence/](evidence/) | Screenshots from the simulation |

## Reproduce the project

1. Open `packet-tracer/abyssinia-enterprise-network.pkt` in Cisco Packet Tracer.
2. Review the [address plan](ip-addressing/ip-addressing-table.csv) and device
   configurations in `configs/`.
3. Use the [implementation procedure](documentation/implementation-procedure.md)
   to check the topology and device settings.
4. Follow the [FTP server setup guide](documentation/implementation-procedure.md#5-set-up-the-ftp-server)
   to configure and test the IT file server.
5. Run the pending tests in
   [connectivity-tests.md](testing/connectivity-tests.md) and add genuine
   screenshots or command output before marking them verified.

The text configurations are reference templates. Replace local credential
placeholders before applying them. Before publishing or sharing the `.pkt`
file, review and rotate any credentials stored inside the simulation.

## Known limitations and next steps

- Verify same-VLAN client-to-client connectivity and repeat the inter-VLAN ping
  that showed one initial timeout.
- Verify that the DNS server resolves the web server's hostname to
  `192.168.10.69`, then open the site by hostname. The earlier browser screenshot
  targets `.67` and predates the separate web server.
- Verify FTP file upload and download from an authorized client; the captured
  evidence currently confirms login and directory listing only.
- Validate upstream routing/NAT beyond the router's own simulated WAN interface.
- Add and test ACL policy, management-plane restrictions, and redundancy as
  future improvements.

See the [design report](documentation/network-design-report.md) for the
implementation details and [test report](testing/connectivity-tests.md) for
what has and has not been verified.
