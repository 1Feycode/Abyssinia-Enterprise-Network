# Connectivity Test Report

## Test environment

- Organization: Abyssinia Technologies PLC
- Simulator: Cisco Packet Tracer
- Client shown in command-prompt evidence: IT-PC1 (`192.168.10.72/27`)
- Evidence files: [screenshots](../evidence/README.md)

## Results

| ID | Test | Expected | Observed result | Status | Evidence |
|---|---|---|---|---|---|
| T01 | IT-PC1 to IT-PC2 (same VLAN) | Reachable | No result recorded | Not tested | — |
| T02 | ADMIN-PC1 to ADMIN-PC2 (same VLAN) | Reachable | No result recorded | Not tested | — |
| T03 | HR-PC1 to HR-PC2 (same VLAN) | Reachable | No result recorded | Not tested | — |
| T04 | FIN-PC1 to FIN-PC2 (same VLAN) | Reachable | No result recorded | Not tested | — |
| T05 | IT-PC1 to HR-PC1 (`192.168.10.104`, inter-VLAN) | Reachable; no ACL blocks this path | Three replies out of four; first request timed out | Partial; repeat after ARP learning | [Ping output](../evidence/07-inter-vlan-connectivity.png) |
| T06 | IT-PC1 to DSW-CORE transit interface (`176.16.0.1`) | Reachable | Four replies, zero loss | Verified | [Ping output](../evidence/08-core-router-link-connectivity.png) |
| T07 | IT-PC1 to R1-WAN transit interface (`176.16.0.2`) | Reachable | Four replies, zero loss | Verified | [Ping output](../evidence/09-router-lan-connectivity.png) |
| T08 | IT-PC1 to R1-WAN simulated upstream interface (`200.64.100.2`) | Reachable in simulation | Four replies, zero loss | Verified to router interface only | [Ping output](../evidence/10-simulated-wan-connectivity.png) |
| T09 | IT-PC1 opens web server at `http://192.168.10.69` | Page loads | No result recorded after web server separation | Not tested | — |
| T10 | Resolve the web server hostname from a client | Name resolves to `192.168.10.69` | No lookup result recorded | Not tested | — |
| T11 | Authorized IT client logs into IT-Server FTP (`192.168.10.68`) and lists files | Login and listing succeed | Connected, authenticated as `ftp_lab`, and listed the FTP directory | Verified | [FTP login and listing](../evidence/15-ftp-server-login-directory-listing.png) |
| T12 | Authorized IT client uploads and downloads a test file through FTP | Both transfers succeed | No transfer result shown | Not tested | — |

T05's first timeout may occur while ARP resolves the destination. Repeat the
ping and record the full result before treating cross-VLAN connectivity as
stable. T08 confirms reachability to the router's own simulated WAN interface;
it does not prove upstream or Internet access. T09 and T10 need to be rerun against the separate web server and DNS service.
The older browser screenshot at `.67` predates the separation. T11 confirms FTP
login and directory listing on `192.168.10.68`; T12 still needs upload and
download evidence.

## Addressing and switching evidence

Screenshots also show DHCP configuration for IT, HR, Finance, and Administration
clients, a static server address, a learned MAC address table, and switch
interface status:

- [IT-PC1 IP configuration](../evidence/03-ip-configuration-it.png)
- [HR-PC1 IP configuration](../evidence/04-ip-configuration-hr.png)
- [FIN-PC1 IP configuration](../evidence/05-ip-configuration-finance.png)
- [ADMIN-PC1 IP configuration](../evidence/06-ip-configuration-admin.png)
- [DNS server IP configuration](../evidence/13-dns-server-ip-configuration.png)
- [IT-Server FTP IP configuration](../evidence/16-ftp-server-ip-configuration.png)
- [Web server IP configuration](../evidence/17-web-server-ip-configuration.png)
- [ASW-IT MAC address table](../evidence/11-switch-mac-address-table.png)
- [ASW-IT interface status](../evidence/12-switch-interface-status.png)

## Useful commands

On Packet Tracer end devices:

```text
ipconfig
ping <destination-ip>
arp -a
tracert <destination-ip>
```

On Cisco switches and routers:

```text
show ip interface brief
show vlan brief
show interfaces trunk
show ip route
show mac address-table
show interfaces status
show cdp neighbors
```

Record command output or genuine screenshots for every pending test. Do not
report an expected result as an observed result.
