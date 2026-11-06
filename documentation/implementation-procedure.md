
# Network Implementation Procedure

## Step 1: Requirements Analysis
Analyze departmental employee counts and
future capacity requirements.

## Step 2: IP Address Planning
Use 192.168.10.0/24 as the assigned address block.
Calculate VLSM subnet allocations.

## Step 3: Topology Design
Build the hierarchical physical topology:
- WAN router representation
- Distribution switch
- Four access switches
- Eight workstations
- One internal server

## Step 4: Device Configuration
Configure switch hostnames, disable DNS lookup, enable SSH,
create VLANs, and assign management interfaces on each device.

## Step 5: VLAN and Trunk Configuration
Create VLANs for IT, Finance, HR, Admin, native VLAN 99,
and management VLAN 100. Configure trunk links from each access
switch to the DSW-CORE switch and shut down unused ports.

## Step 6: Inter-VLAN Routing and DHCP
Enable IP routing on DSW-CORE and create SVI interfaces for each
VLAN. Configure DHCP pools for departmental networks and point
clients to the static DNS server at 192.168.10.67.

## Step 7: End-Device Configuration
Assign the DNS server a static IP in the IT VLAN and configure
client devices to receive IPs through DHCP or static addressing
as required by the topology.

## Step 8: Static Routing and Verification
Configure static routes on the DSW-CORE and router, then verify:
- Physical link status
- VLAN membership
- Trunk status
- IP configuration
- DHCP lease assignment
- Same-subnet and inter-VLAN connectivity
- Routing to the WAN network

## Step 9: Troubleshooting
Investigate:
- Incorrect subnet mask
- Duplicate IP address
- Insufficient subnet capacity
- Missing default gateway
- Routing or trunk misconfiguration

## Step 10: Documentation
Record configuration details, test results, faults, solutions,
proof screenshots, and final project status for submission.
