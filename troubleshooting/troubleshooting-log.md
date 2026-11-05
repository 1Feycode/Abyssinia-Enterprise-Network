
# Network Troubleshooting Log

Organization: Abyssinia Technologies PLC

## Incident 001: Incorrect Subnet Mask

Problem:
IT-PC1 has an incorrect subnet mask.

Initial configuration:
IP: 192.168.10.65
Mask: 255.255.255.0

Expected configuration:
IP: 192.168.10.65
Mask: 255.255.255.224

Root Cause:
Incorrect subnet mask.

Resolution:
Correct the subnet mask and repeat connectivity tests.

Verification:
Record actual ping and IP configuration results.

Status: Pending practical verification.

--------------------------------------------------

## Incident 002: Duplicate IP Address

Problem:
Two Finance PCs have the same IP address.

Root Cause:
Duplicate static IP assignment.

Resolution:
Assign unique IP addresses to both devices.

Verification:
Use ipconfig, arp -a, and ping.

Status: Pending practical verification.

--------------------------------------------------

## Incident 003: Insufficient Subnet Capacity

Problem:
Administration requires 65 usable host addresses.

Current allocation:
192.168.10.0/26

Available usable addresses:
62

Root Cause:
The existing subnet is too small.

Resolution:
Recalculate the entire VLSM allocation.
A /25 is needed for 65 hosts, but the
other departments' subnets must also fit.

Status: Analysis completed; redesign pending.
