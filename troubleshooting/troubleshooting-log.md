# Network Troubleshooting Log

## Incident 001: Web server unreachable due to incorrect subnet mask

**Device:** WEB-SERVER (`192.168.10.69`)

**Symptom:** After assigning a static IP address, the web server could not
reach its default gateway or other PCs.

**Root cause:** The mask was left at `255.255.255.0` (`/24`) instead of the
IT VLAN's `/27` mask, `255.255.255.224`. The `/24` mask made the server treat
addresses outside its actual subnet as local, preventing correct communication
through its configured gateway. `255.255.255.254` is not the correct mask for
this subnet either.

**Resolution:** Set the web server's static network configuration to:

- IP address: `192.168.10.69`
- Subnet mask: `255.255.255.224`
- Default gateway: `192.168.10.94`
- DNS server: `192.168.10.67`

**Evidence:** The [before-fix screenshot](../evidence/18-web-server-incorrect-subnet-mask.png)
shows the `/24` mask. The [corrected configuration screenshot](../evidence/17-web-server-ip-configuration.png)
shows the `/27` mask, gateway, and DNS server.

**Verification:** Mask correction is evidenced. Successful post-fix pings to
`192.168.10.94` and a peer PC, followed by HTTP testing, are still needed to
verify restored connectivity.

**Status:** Incorrect mask identified and corrected; connectivity verification
pending.

## Incident 002: Web hostname could not be resolved

**Client:** FIN-PC1

**Requested URL:** `http://www.abyssinia.com`

**Symptom:** The Packet Tracer browser displayed **Host Name Unresolved**
when the client tried to browse to the company web hostname.

**Root cause:** DNS Service on DNS-SERVER (`192.168.10.67`) was Off, so clients
could not resolve the configured hostname to the web server address.

**Resolution:** Turned DNS Service On and confirmed the DNS A record
`www.abyssinia.com` points to WEB-SERVER at `192.168.10.69`.

**Evidence:** The [client failure screenshot](../evidence/21-dns-failure-hostname-unresolved.png)
shows the unresolved hostname. The DNS-Off state was observed during
troubleshooting; the supplied [DNS service and record screenshot](../evidence/19-dns-www-abyssinia-com-record.png)
captures the subsequent DNS Service On state and the A record pointing to `.69`.
The [successful browser screenshot](../evidence/22-dns-browser-success.png)
shows FIN-PC1 loading the page from `http://www.abyssinia.com`.

**Verification:** FIN-PC1 successfully loaded the web page using the hostname
after DNS was enabled, verifying client-side name resolution and HTTP access.

**Status:** Resolved and verified from FIN-PC1.
