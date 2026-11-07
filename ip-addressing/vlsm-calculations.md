# VLSM Addressing Plan

## Address block

Department and management networks are allocated from `192.168.10.0/24`.
Subnets are assigned from largest to smallest to prevent overlap and preserve
contiguous address space.

The host calculation is `2^h - 2`, where `h` is the number of host bits and
the two excluded addresses are the network and broadcast addresses.

## Department allocations

| Department | Planned hosts | Prefix | Mask | Network | Usable range | Broadcast |
|---|---:|---:|---|---|---|---|
| Administration | 40 | /26 | `255.255.255.192` | `192.168.10.0` | `192.168.10.1`-`192.168.10.62` | `192.168.10.63` |
| IT | 25 | /27 | `255.255.255.224` | `192.168.10.64` | `192.168.10.65`-`192.168.10.94` | `192.168.10.95` |
| HR | 20 | /27 | `255.255.255.224` | `192.168.10.96` | `192.168.10.97`-`192.168.10.126` | `192.168.10.127` |
| Finance | 15 | /27 | `255.255.255.224` | `192.168.10.128` | `192.168.10.129`-`192.168.10.158` | `192.168.10.159` |
| Management | 5 switch addresses | /27 | `255.255.255.224` | `192.168.10.192` | `192.168.10.193`-`192.168.10.222` | `192.168.10.223` |

Administration needs 40 hosts, so 5 host bits (30 usable) are insufficient;
6 host bits provide 62 usable addresses. IT and HR each fit in a /27 with 30
usable addresses. Finance needs 15 hosts, so a /28 (14 usable) is insufficient
and a /27 is used.

## Transit and simulated upstream links

These links are separate from the assigned internal `/24`:

| Link | Network | Endpoint assignments |
|---|---|---|
| DSW-CORE to R1-WAN | `176.16.0.0/30` | DSW-CORE `176.16.0.1`; R1-WAN `176.16.0.2` |
| R1-WAN to simulated upstream | `200.64.100.0/24` | Next hop `200.64.100.1`; R1-WAN `200.64.100.2` |

The upstream addresses represent a Packet Tracer simulation, not a claim of
public Internet connectivity.

## Remaining internal address space

The following ranges remain unallocated (64 addresses total):

- `192.168.10.160/27` (`192.168.10.160`-`192.168.10.191`)
- `192.168.10.224/27` (`192.168.10.224`-`192.168.10.255`)

Each `/27` contains 30 usable host addresses. Confirm future requirements
before assigning either range.

See the [device and address table](ip-addressing-table.csv) for gateway,
server, management, and DHCP pool assignments.
