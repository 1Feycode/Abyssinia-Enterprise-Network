
# VLSM Calculations

## Assigned Network
192.168.10.0/24

## Calculation Formula
2^h - 2 >= Required Host Addresses

Where h represents the number of host bits.

## Departmental Calculations

### Administration
Required hosts: 40

2^5 - 2 = 30 (insufficient)
2^6 - 2 = 62 (sufficient)

Prefix: /26
Mask: 255.255.255.192
Network: 192.168.10.0
Broadcast: 192.168.10.63
Usable: 192.168.10.1 - 192.168.10.62

### IT
Required hosts: 25

2^5 - 2 = 30

Prefix: /27
Mask: 255.255.255.224
Network: 192.168.10.64
Broadcast: 192.168.10.95
Usable: 192.168.10.65 - 192.168.10.94

### Human Resources
Required hosts: 20

2^5 - 2 = 30

Prefix: /27
Mask: 255.255.255.224
Network: 192.168.10.96
Broadcast: 192.168.10.127
Usable: 192.168.10.97 - 192.168.10.126

### Finance
Required hosts: 15

2^5 - 2 = 30

Prefix: /27
Mask: 255.255.255.224
Network: 192.168.10.128
Broadcast: 192.168.10.159
Usable: 192.168.10.129 - 192.168.10.158

## Remaining Address Space
192.168.10.160 - 192.168.10.255

Total remaining addresses: 96

These addresses are available for future subnet
planning, subject to network requirements.
