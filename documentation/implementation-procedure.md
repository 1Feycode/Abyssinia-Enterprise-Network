# Implementation and Verification Procedure

Use this procedure with the Packet Tracer project and the reference
configurations in `configs/`. Replace credential placeholders with unique,
private values before applying any template.

## 1. Confirm the topology

Check that DSW-CORE connects to all four departmental access switches, the DNS
server (`192.168.10.67`), web server (`192.168.10.69`), FTP server
(`192.168.10.68`), and R1-WAN. Confirm endpoint links and labels.

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
4. Configure the DNS server at `192.168.10.67/27` and set DNS Service to
   **On**. Configure the separate web server at `192.168.10.69/27` and set
   HTTP to **On**. On the DNS server, add an A record:

   | Name | Type | Address |
   |---|---|---|
   | `www.abyssinia.com` | A Record | `192.168.10.69` |

   Click **Add** and **Save**. In this Packet Tracer lab, the name resolves
   using the configured DNS server; this does not create or imply public
   Internet DNS for `abyssinia.com`.
5. Configure the IT-Server and FTP service using the
   [FTP setup guide](#5-set-up-the-ftp-server).
6. Configure R1-WAN transit, simulated upstream addressing, static routes, and
   NAT as shown in its reference template.

## 5. Set up the FTP server

1. Connect **IT-Server** to a free access port on **ASW-IT**. Use a port
   assigned to VLAN 20, and wait for the link indicator to come up.
2. On IT-Server, open **Desktop → IP Configuration**, select **Static**, and
   enter:

   | Setting | Value |
   |---|---|
   | IPv4 address | `192.168.10.68` |
   | Subnet mask | `255.255.255.224` |
   | Default gateway | `192.168.10.94` |
   | DNS server | `192.168.10.67` |

3. Open **Services → FTP** and set the service to **On**.
4. Under **User Setup**, enter a username and a unique lab-only password.
   Select the permissions needed for the test. **Read**, **Write**, and
   **List** are enough to list and transfer files; leave **Delete** and
   **Rename** unchecked unless the lab specifically needs them.
5. Click **Add** and confirm the account appears in the FTP user list with the
   intended permissions.
6. From an IT client, open **Desktop → Command Prompt** and connect:

   ```text
   ping 192.168.10.68
   ftp 192.168.10.68
   ```

   Enter the FTP username and password when prompted. At the `ftp>` prompt,
   run `dir` to verify the login and directory listing. If the Packet Tracer
   client supports file transfers, test `put <filename>` and `get <filename>`
   with a non-sensitive test file, then use `dir` to confirm the result.
7. Record the observed results and capture genuine screenshots for login,
   listing, and transfers in the [connectivity test report](../testing/connectivity-tests.md).

FTP sends credentials and files without encryption. Use only disposable lab
credentials and test files; do not use FTP for sensitive real-world data. Do
not include screenshots that expose passwords in the portfolio.

## 6. Verify and capture evidence

Run the checks in the [connectivity test report](../testing/connectivity-tests.md).
Capture screenshots from the actual simulation, ensure text and command output
are legible, and save them in `evidence/` with descriptive names. Update each
test's actual result and status; do not mark a test verified based only on its
expected result or a configured command.

## 7. Final review

- Check device names, VLAN membership, trunk status, interface status, DHCP
  leases, and routing tables.
- On the DNS server, confirm DNS Service is **On** and the
  `www.abyssinia.com` A record points to `192.168.10.69`.
- Verify client-to-client and cross-VLAN pings, resolve
  `www.abyssinia.com` from a client, browse to `http://www.abyssinia.com`, and
  test FTP file transfer.
- Confirm upstream/NAT behavior only against a reachable simulated destination.
- Review the `.pkt` file for lab credentials before publishing.
- Ensure diagrams, configuration templates, address tables, and evidence all
  describe the same topology and implementation.
