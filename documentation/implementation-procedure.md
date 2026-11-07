# Implementation and Verification Procedure

Use this procedure with the Packet Tracer project and the reference
configurations in `configs/`. Replace credential placeholders with unique,
private values before applying any template.

## 1. Confirm the topology

Check that DSW-CORE connects to all four departmental access switches, the
DNS/web server, and R1-WAN. Confirm endpoint links and labels. The diagram also
contains a separate IT-Server; document its role and address or remove it.

## 2. Apply the address plan

Use the [VLSM calculations](../ip-addressing/vlsm-calculations.md) and
[address table](../ip-addressing/ip-addressing-table.csv). Confirm that client
addresses, gateways, masks, and DNS values are in the correct VLAN subnet and
do not overlap static assignments or DHCP exclusions.

## 3. Configure switching

1. Create department VLANs 20, 30, 40, and 50, native VLAN 99, and management
   VLAN 100.
2. Assign each access switch's endpoint ports to its department VLAN.
3. Configure the core and access uplinks as trunks with native VLAN 99 and only
   the VLANs required on each link.
4. Configure management SVIs and the correct global `ip default-gateway` on
   each Layer 2 access switch.
5. Shut down unused access ports.

## 4. Configure Layer 3 and services

1. On DSW-CORE, enable IP routing and configure the department and management
   SVIs with the documented gateway addresses.
2. Configure the core-to-router physical interface as a routed port before
   assigning its `176.16.0.1/30` address.
3. Create DHCP exclusions and department pools. Verify each pool's network,
   gateway, and DNS option.
4. Configure the DNS/web server at `192.168.10.67/27`. Enable DNS and HTTP
   services and create a DNS record for hostname testing.
5. Configure the IT-Server at `192.168.10.68/27` with gateway
   `192.168.10.94`. Enable FTP and verify login, directory listing, and file
   upload/download using an authorized test account.
6. Configure R1-WAN transit, simulated upstream addressing, static routes, and
   NAT as shown in its reference template.

## 5. Verify and capture evidence

Run the checks in the [connectivity test report](../testing/connectivity-tests.md).
Capture screenshots from the actual simulation, ensure text and command output
are legible, and save them in `evidence/` with descriptive names. Update each
test's actual result and status; do not mark a test verified based only on its
expected result or a configured command.

## 6. Final review

- Check device names, VLAN membership, trunk status, interface status, DHCP
  leases, and routing tables.
- Verify client-to-client and cross-VLAN pings, DNS lookup by hostname, HTTP
  access, and FTP file transfer.
- Confirm upstream/NAT behavior only against a reachable simulated destination.
- Review the `.pkt` file for lab credentials before publishing.
- Ensure diagrams, configuration templates, address tables, and evidence all
  describe the same topology and implementation.
