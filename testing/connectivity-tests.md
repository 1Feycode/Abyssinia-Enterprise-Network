# Connectivity Test Report

## Test environment

- Organization: Abyssinia Technologies PLC
- Simulator: Cisco Packet Tracer
- Reference client: IT-PC1 (`192.168.10.72/27`); other screenshots show clients
  from all four departments
- Evidence files: [screenshots](../evidence/README.md)

## Results

| ID | Test | Expected | Observed result | Status | Evidence |
|---|---|---|---|---|---|
| T01 | IT-PC1 / IT-PC2 client-to-client (same VLAN) | Reachable | Both ping commands received 4/4 replies, but IT-PC1 pinged `.72`, matching its captured own address; the paired targets are not verified as peer addresses | Inconclusive; repeat with confirmed peer IPs | [IT-PC1](../evidence/26-it-pc1-ping-192-168-10-72.png) / [IT-PC1 IP configuration](../evidence/03-ip-configuration-it.png) / [IT-PC2](../evidence/25-it-pc2-ping-192-168-10-71.png) |
| T02 | ADMIN-PC1 / ADMIN-PC2 client-to-client (same VLAN) | Reachable | ADMIN-PC1 pinged `.8` and ADMIN-PC2 pinged `.7`; each received 4/4 replies | Verified | [ADMIN-PC1](../evidence/30-admin-pc1-ping-192-168-10-8.png) / [ADMIN-PC2](../evidence/29-admin-pc2-ping-192-168-10-7.png) |
| T03 | HR-PC1 / HR-PC2 client-to-client (same VLAN) | Reachable | Both commands received 4/4 replies; HR-PC1's captured address is `.104`, but the target `.103` is not independently tied to HR-PC2 | Inconclusive; confirm peer IP | [HR-PC1](../evidence/24-hr-pc1-ping-192-168-10-103.png) / [HR-PC1 IP configuration](../evidence/04-ip-configuration-hr.png) / [HR-PC2](../evidence/23-hr-pc2-ping-192-168-10-105.png) |
| T04 | FIN-PC1 / FIN-PC2 client-to-client (same VLAN) | Reachable | Both commands received 4/4 replies; FIN-PC1's captured address is `.136`, but the target `.137` is not independently tied to FIN-PC2 | Inconclusive; confirm peer IP | [FIN-PC1](../evidence/28-fin-pc1-ping-192-168-10-137.png) / [FIN-PC1 IP configuration](../evidence/05-ip-configuration-finance.png) / [FIN-PC2](../evidence/27-fin-pc2-ping-192-168-10-135.png) |
| T05 | IT-PC1 to HR-PC1 (`192.168.10.104`, IT-initiated inter-VLAN) | Reachable; IT-initiated ping is permitted by the ACL | Pre-ACL capture shows three replies out of four; no post-ACL result | Pending post-ACL retest | [Pre-ACL ping](../evidence/07-inter-vlan-connectivity.png) |
| T06 | IT-PC1 to DSW-CORE transit interface (`176.16.0.1`) | Reachable | Four replies, zero loss | Verified | [Ping output](../evidence/08-core-router-link-connectivity.png) |
| T07 | IT-PC1 to R1-WAN transit interface (`176.16.0.2`) | Reachable | Four replies, zero loss | Verified | [Ping output](../evidence/09-router-lan-connectivity.png) |
| T08 | IT-PC1 to R1-WAN simulated upstream interface (`200.64.100.2`) | Reachable in simulation | Four replies, zero loss | Verified to router interface only | [Ping output](../evidence/10-simulated-wan-connectivity.png) |
| T09 | IT-PC1 opens web server at `http://192.168.10.69` | Page loads | HTTP service is On; client page load not recorded after server separation | Not tested | [HTTP service](../evidence/20-web-server-http-service.png) |
| T10 | Resolve `www.abyssinia.com` from a client | Name resolves to `192.168.10.69` | FIN-PC1 successfully loaded the web page by hostname after DNS Service was enabled | Verified | [Failure](../evidence/21-dns-failure-hostname-unresolved.png) / [DNS enabled](../evidence/19-dns-www-abyssinia-com-record.png) / [successful page load](../evidence/22-dns-browser-success.png) |
| T11 | Authorized IT client logs into IT-Server FTP (`192.168.10.68`) and lists files | Login and listing succeed | Connected, authenticated as `ftp_lab`, and listed the FTP directory | Verified | [FTP login and listing](../evidence/15-ftp-server-login-directory-listing.png) |
| T12 | Authorized IT client uploads and downloads a test file through FTP | Both transfers succeed | No transfer result shown | Not tested | — |
| T13 | WEB-SERVER with corrected `/27` mask reaches its gateway and an IT peer | Both destinations reply | Before-fix `/24` and corrected `/27` configurations are captured; no post-fix ping result | Pending | [Before](../evidence/18-web-server-incorrect-subnet-mask.png) / [after](../evidence/17-web-server-ip-configuration.png) configuration |
| T14 | IT-PC1 to HR endpoint (`192.168.10.103`, IT-initiated inter-VLAN) | Reachable; IT-initiated ping is permitted by the ACL | Pre-ACL capture: first request timed out; next three replied; endpoint identity is unconfirmed | Pending post-ACL retest | [Pre-ACL ping](../evidence/31-it-pc1-ping-192-168-10-103.png) |
| T15 | IT-PC1 to Finance endpoint (`192.168.10.137`, IT-initiated inter-VLAN) | Reachable; IT-initiated ping is permitted by the ACL | Pre-ACL capture: first request timed out; next three replied; endpoint identity is unconfirmed | Pending post-ACL retest | [Pre-ACL ping](../evidence/32-it-pc1-ping-192-168-10-137.png) |
| T16 | IT-PC1 to Administration endpoint (`192.168.10.6`, IT-initiated inter-VLAN) | Reachable; IT-initiated ping is permitted by the ACL | Pre-ACL capture: first request timed out; next three replied; endpoint identity is unconfirmed | Pending post-ACL retest | [Pre-ACL ping](../evidence/33-it-pc1-ping-192-168-10-6.png) |
| T17 | HR-PC1 (`192.168.10.104`) to IT-PC1 (`192.168.10.72`) | ICMP echo requests to IT hosts are blocked by the VLAN 20 ACL | Not tested after ACL configuration | Pending in Packet Tracer | — |
| T18 | IT-PC1 (`192.168.10.72`) to HR-PC1 (`192.168.10.104`) | IT-initiated ping and replies are allowed | Not tested after ACL configuration | Pending in Packet Tracer | — |

The same-VLAN client pings in T01-T04 each show four replies and no packet
loss in the captured commands, but T01, T03, and T04 are inconclusive as
client-to-client tests because the ping destinations are not verified as the
other endpoint's assigned IP (T01's `.72` matches IT-PC1's documented IP).
Confirm the target addresses for all endpoint ping tests. The inter-VLAN
captures in T05 and T14-T16 are baseline evidence from before the ACL was
applied; verify the policy with T17
and T18 and repeat the IT-initiated pings after applying it. The ACL is in the
DSW-CORE text template; it has not been applied to the Packet Tracer `.pkt`
simulation or verified there. It blocks routed pings to IT hosts, not pings to
the VLAN 20 gateway itself. T08 confirms reachability to the router's own
simulated WAN interface; it does not prove upstream or Internet access. T09's
direct-IP test from IT-PC1 is still pending. T10 is verified: FIN-PC1 initially
reported an unresolved hostname while DNS was disabled, then successfully
loaded the page by hostname after DNS was enabled. This is a lab-local DNS
mapping, not public DNS for the `.com` domain. The older browser screenshot at
`.67` predates the separation. T11 confirms FTP login and directory listing on
`192.168.10.68`; T12 still needs upload and download evidence.

## Addressing and switching evidence

Screenshots also show DHCP configuration for IT, HR, Finance, and Administration
clients, a static server address, a learned MAC address table, and switch
interface status:

- [IT-PC1 IP configuration](../evidence/03-ip-configuration-it.png)
- [HR-PC1 IP configuration](../evidence/04-ip-configuration-hr.png)
- [FIN-PC1 IP configuration](../evidence/05-ip-configuration-finance.png)
- [ADMIN-PC1 IP configuration](../evidence/06-ip-configuration-admin.png)
- [DNS server IP configuration](../evidence/13-dns-server-ip-configuration.png)
- [DNS A record for `www.abyssinia.com`](../evidence/19-dns-www-abyssinia-com-record.png)
- [Web server HTTP service status](../evidence/20-web-server-http-service.png)
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
