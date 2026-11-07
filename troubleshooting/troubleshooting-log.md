# Troubleshooting Scenarios

The scenarios below are planned lab exercises, not claims of faults observed
in the current simulation. Reproduce each issue, record the actual diagnostic
output, apply the correction, and update its status before presenting it as a
completed incident.

## Scenario 001: Incorrect subnet mask

**Symptom:** IT-PC1 is configured with `192.168.10.65/24` instead of the IT
subnet mask `255.255.255.224` (`/27`).

**Expected correction:** Keep the host address valid for the IT subnet and
correct the mask to `/27`. Confirm the gateway is `192.168.10.94`.

**Verification:** Capture `ipconfig` and repeat gateway and cross-VLAN pings.

**Status:** Scenario documented; reproduction and verification pending.

## Scenario 002: Duplicate IP address

**Symptom:** Two Finance endpoints are assigned the same IPv4 address.

**Expected correction:** Restore DHCP assignment or allocate unique static
addresses from the Finance subnet, excluding the gateway and DHCP exclusions.

**Verification:** Capture both endpoint configurations and test connectivity;
use `arp -a` or the switch MAC table as supporting diagnostics.

**Status:** Scenario documented; reproduction and verification pending.

## Scenario 003: Insufficient subnet capacity

**Exercise requirement:** A hypothetical department needs 65 usable host
addresses. This is not the current Administration requirement, which is 40.

**Analysis:** A `/26` supports 62 usable hosts and is insufficient. A `/25`
supports 126 usable hosts, but it would require redesigning the existing
`192.168.10.0/24` allocations to avoid overlap.

**Verification:** Recalculate all subnets, check for overlap, then validate
gateway and DHCP assignments in the revised simulation.

**Status:** Analysis documented; redesign and lab verification pending.
