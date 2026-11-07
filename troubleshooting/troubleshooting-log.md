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

**Root cause:** The subnet mask was left at an incorrect/default value instead
of being set to the IT VLAN's `/27` mask. The initial mask value was not
recorded. The correct mask is `255.255.255.224` (`/27`), not
`255.255.255.254`.

**Resolution:** Set the web server's static network configuration to:

- IP address: `192.168.10.69`
- Subnet mask: `255.255.255.224`
- Default gateway: `192.168.10.94`
- DNS server: `192.168.10.67`

**Verification:** The current web-server IP-configuration screenshot shows the
correct address, mask, gateway, and DNS server. Capture successful pings to
`192.168.10.94` and a peer PC, then test HTTP access to complete verification.

**Status:** Mask corrected in the current configuration; post-fix connectivity
verification pending.
