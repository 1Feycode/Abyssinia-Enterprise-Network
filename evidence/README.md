# Project Evidence

These screenshots were captured from the Packet Tracer implementation. They
are evidence of the screen state shown, not proof of untested behavior. See the
[test report](../testing/connectivity-tests.md) for observed results and
limitations.

| Screenshot | What it shows |
|---|---|
| [02-device-connections.png](02-device-connections.png) | Packet Tracer topology and device connections, including the IT file/FTP server |
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
| [13-dns-server-ip-configuration.png](13-dns-server-ip-configuration.png) | Static server IP configuration |
| [14-intranet-web-page.png](14-intranet-web-page.png) | Abyssinia page loaded by IP address; does not verify DNS lookup |
| [15-ftp-server-login-directory-listing.png](15-ftp-server-login-directory-listing.png) | IT-PC1 logs into IT-Server at `192.168.10.68` and lists files; no transfer is shown |
| [16-ftp-server-ip-configuration.png](16-ftp-server-ip-configuration.png) | IT-Server static IPv4 address, subnet mask, gateway, and DNS settings |

Do not add fabricated or sample screenshots. Capture any remaining tests from
the actual simulation, save them with descriptive filenames, and update the
test report with the result.
