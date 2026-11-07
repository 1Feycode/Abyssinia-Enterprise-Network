# Network Troubleshooting Log

The entries distinguish reported incidents from planned lab exercises. Record
observed results and capture evidence before marking an incident fully verified.

## Scenario 001: Incorrect subnet mask (planned exercise)

**Symptom:** IT-PC1 is configured with `192.168.10.65/24` instead of the IT
subnet mask `255.255.255.224` (`/27`).

**Expected correction:** Keep the host address valid for the IT subnet and
correct the mask to `/27`. Confirm the gateway is `192.168.10.94`.

**Verification:** Capture `ipconfig` and repeat gateway and cross-VLAN pings.

**Status:** Exercise documented; reproduction and verification pending.

## Scenario 002: Duplicate IP address (planned exercise)

**Symptom:** Two Finance endpoints are assigned the same IPv4 address.

**Expected correction:** Restore DHCP assignment or allocate unique static
addresses from the Finance subnet, excluding the gateway and DHCP exclusions.

**Verification:** Capture both endpoint configurations and test connectivity;
use `arp -a` or the switch MAC table as supporting diagnostics.

**Status:** Exercise documented; reproduction and verification pending.

## Scenario 003: Insufficient subnet capacity (planned exercise)

**Exercise requirement:** A hypothetical department needs 65 usable host
addresses. This is not the current Administration requirement, which is 40.

**Analysis:** A `/26` supports 62 usable hosts and is insufficient. A `/25`
supports 126 usable hosts, but it would require redesigning the existing
`192.168.10.0/24` allocations to avoid overlap.

**Verification:** Recalculate all subnets, check for overlap, then validate
gateway and DHCP assignments in the revised simulation.

**Status:** Analysis documented; redesign and lab verification pending.

## Incident 004: Web server unreachable due to incorrect subnet mask

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

## Incident 005: Web hostname could not be resolved

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
