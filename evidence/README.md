# Project Evidence

These screenshots were captured from the Packet Tracer implementation. They
are evidence of the screen state shown, not proof of untested behavior. See the
[test report](../testing/connectivity-tests.md) for observed results and
limitations.

| Screenshot | What it shows |
|---|---|
| [Current topology diagram](../packet-tracer/Topology.png) | Updated topology with separate DNS, web, and FTP servers |
| [02-device-connections.png](02-device-connections.png) | Earlier Packet Tracer topology screenshot, before adding the separate web server |
| [03-ip-configuration-it.png](03-ip-configuration-it.png) | IT-PC1 DHCP address, mask, gateway, and DNS |
| [04-ip-configuration-hr.png](04-ip-configuration-hr.png) | HR-PC1 DHCP configuration |
| [05-ip-configuration-finance.png](05-ip-configuration-finance.png) | FIN-PC1 DHCP configuration |
| [06-ip-configuration-admin.png](06-ip-configuration-admin.png) | ADMIN-PC1 DHCP configuration |
| [07-inter-vlan-connectivity.png](07-inter-vlan-connectivity.png) | IT-PC1 ping to gateway and HR-PC1; first HR ping timed out |
| [08-core-router-link-connectivity.png](08-core-router-link-connectivity.png) | IT-PC1 ping to DSW-CORE transit address |
| [09-router-lan-connectivity.png](09-router-lan-connectivity.png) | IT-PC1 ping and traceroute to R1-WAN transit address |
| [10-simulated-wan-connectivity.png](10-simulated-wan-connectivity.png) | IT-PC1 ping and traceroute to R1-WAN's simulated upstream interface |
| [11-switch-mac-address-table.png](11-switch-mac-address-table.png) | ASW-IT learned MAC address table |
| [12-switch-interface-status.png](12-switch-interface-status.png) | ASW-IT interface status |
| [13-dns-server-ip-configuration.png](13-dns-server-ip-configuration.png) | DNS server static IP configuration (`192.168.10.67`) |
| [14-intranet-web-page.png](14-intranet-web-page.png) | Historical page loaded from `.67` before the web server was separated; not current web-server proof |
| [15-ftp-server-login-directory-listing.png](15-ftp-server-login-directory-listing.png) | IT-PC1 logs into IT-Server at `192.168.10.68` and lists files; no transfer is shown |
| [16-ftp-server-ip-configuration.png](16-ftp-server-ip-configuration.png) | IT-Server static IPv4 address, subnet mask, gateway, and DNS settings |
| [17-web-server-ip-configuration.png](17-web-server-ip-configuration.png) | Web server static IPv4 address `192.168.10.69`, mask, gateway, and DNS |
| [18-web-server-incorrect-subnet-mask.png](18-web-server-incorrect-subnet-mask.png) | Before-fix WEB-SERVER configuration showing incorrect `/24` mask `255.255.255.0` |
| [19-dns-www-abyssinia-com-record.png](19-dns-www-abyssinia-com-record.png) | DNS Service is On and the A record maps `www.abyssinia.com` to `192.168.10.69` |
| [20-web-server-http-service.png](20-web-server-http-service.png) | WEB-SERVER HTTP service is On; HTTPS is also On |
| [21-dns-failure-hostname-unresolved.png](21-dns-failure-hostname-unresolved.png) | FIN-PC1 browser shows “Host Name Unresolved” for `www.abyssinia.com` |
| [22-dns-browser-success.png](22-dns-browser-success.png) | FIN-PC1 successfully loads the page at `http://www.abyssinia.com` after DNS was enabled |
| [23-hr-pc2-ping-192-168-10-105.png](23-hr-pc2-ping-192-168-10-105.png) | HR-PC2 ping to `192.168.10.105`; four replies, no packet loss |
| [24-hr-pc1-ping-192-168-10-103.png](24-hr-pc1-ping-192-168-10-103.png) | HR-PC1 ping to `192.168.10.103`; four replies, no packet loss |
| [25-it-pc2-ping-192-168-10-71.png](25-it-pc2-ping-192-168-10-71.png) | IT-PC2 ping to `192.168.10.71`; four replies, no packet loss |
| [26-it-pc1-ping-192-168-10-72.png](26-it-pc1-ping-192-168-10-72.png) | IT-PC1 ping to `192.168.10.72`; four replies, no packet loss |
| [27-fin-pc2-ping-192-168-10-135.png](27-fin-pc2-ping-192-168-10-135.png) | FIN-PC2 ping to `192.168.10.135`; four replies, no packet loss |
| [28-fin-pc1-ping-192-168-10-137.png](28-fin-pc1-ping-192-168-10-137.png) | FIN-PC1 ping to `192.168.10.137`; four replies, no packet loss |
| [29-admin-pc2-ping-192-168-10-7.png](29-admin-pc2-ping-192-168-10-7.png) | ADMIN-PC2 ping to `192.168.10.7`; four replies, no packet loss |
| [30-admin-pc1-ping-192-168-10-8.png](30-admin-pc1-ping-192-168-10-8.png) | ADMIN-PC1 ping to `192.168.10.8`; four replies, no packet loss |
| [31-it-pc1-ping-192-168-10-103.png](31-it-pc1-ping-192-168-10-103.png) | IT-PC1 inter-VLAN ping to HR address `.103`; first request timed out, next three replied |
| [32-it-pc1-ping-192-168-10-137.png](32-it-pc1-ping-192-168-10-137.png) | IT-PC1 inter-VLAN ping to FIN-PC1 `.137`; first request timed out, next three replied |
| [33-it-pc1-ping-192-168-10-6.png](33-it-pc1-ping-192-168-10-6.png) | IT-PC1 inter-VLAN ping to Administration address `.6`; first request timed out, next three replied |
| [34-admin-pc1-ping-it-host-blocked.png](34-admin-pc1-ping-it-host-blocked.png) | ADMIN-PC1 ping to IT address `.71` is blocked; four “Destination host unreachable” responses from gateway `.1` |
| [35-it-pc1-ping-admin-host-allowed.png](35-it-pc1-ping-admin-host-allowed.png) | IT-PC1 ping to ADMIN-PC1 `.7` succeeds with four replies and no packet loss |

Do not add fabricated or sample screenshots. Capture any remaining tests from
the actual simulation, save them with descriptive filenames, and update the
test report with the result.
