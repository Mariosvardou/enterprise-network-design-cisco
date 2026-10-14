# IP Addressing and VLSM Documentation

## 1. Overview

This document describes the IPv4 addressing scheme implemented in the Enterprise Network Design & Implementation project.

Variable Length Subnet Masking (VLSM) was used to allocate different subnet sizes to the headquarters departments according to their network requirements.

The enterprise network consists of three headquarters VLANs, a point-to-point router connection, and a remote office LAN.

## 2. IPv4 Addressing Table

| Department / Network | Network Address | Subnet Mask | CIDR | Default Gateway |
|---|---|---|---|---|
| Production (VLAN 30) | 192.168.10.0 | 255.255.255.192 | /26 | 192.168.10.1 |
| Sales (VLAN 10) | 192.168.10.64 | 255.255.255.224 | /27 | 192.168.10.65 |
| Marketing (VLAN 20) | 192.168.10.96 | 255.255.255.240 | /28 | 192.168.10.97 |
| R1–R2 Link | 10.0.0.0 | 255.255.255.252 | /30 | N/A |
| Remote Office | 192.168.20.0 | 255.255.255.0 | /24 | 192.168.20.1 |

## 3. VLSM Calculations

The number of usable host addresses in an IPv4 subnet is calculated as:

**Usable Hosts = 2^(32 − Prefix Length) − 2**

This formula applies to the conventional subnets used in this project.

### Production — VLAN 30

- Network: `192.168.10.0/26`
- Host bits: 6
- Total addresses: 64
- Usable hosts: 62
- First usable address: `192.168.10.1`
- Last usable address: `192.168.10.62`
- Broadcast address: `192.168.10.63`

### Sales — VLAN 10

- Network: `192.168.10.64/27`
- Host bits: 5
- Total addresses: 32
- Usable hosts: 30
- First usable address: `192.168.10.65`
- Last usable address: `192.168.10.94`
- Broadcast address: `192.168.10.95`

### Marketing — VLAN 20

- Network: `192.168.10.96/28`
- Host bits: 4
- Total addresses: 16
- Usable hosts: 14
- First usable address: `192.168.10.97`
- Last usable address: `192.168.10.110`
- Broadcast address: `192.168.10.111`

## 4. Router Interface Addressing

| Router | Interface | IP Address | Prefix |
|---|---|---|---|
| R1 | Gi0/0.10 | 192.168.10.65 | /27 |
| R1 | Gi0/0.20 | 192.168.10.97 | /28 |
| R1 | Gi0/0.30 | 192.168.10.1 | /26 |
| R1 | Gi0/1 | 10.0.0.1 | /30 |
| R2 | Gi0/1 | 10.0.0.2 | /30 |
| R2 | Gi0/0 | 192.168.20.1 | /24 |

## 5. DHCP Configuration

R1 acts as the DHCP server for all three headquarters VLANs.

| DHCP Pool | Allocation Range | Default Gateway |
|---|---|---|
| SALES | 192.168.10.70–192.168.10.94 | 192.168.10.65 |
| MARKETING | 192.168.10.100–192.168.10.110 | 192.168.10.97 |
| PRODUCTION | 192.168.10.10–192.168.10.62 | 192.168.10.1 |

Reserved addresses were excluded from DHCP allocation to avoid conflicts with gateway addresses and other potential statically configured devices.

The configured DNS server address is `8.8.8.8`. External DNS connectivity was not part of the simulation validation.

## 6. Remote Office Addressing

The remote office LAN uses `192.168.20.0/24`.

PC6 is configured with:

- IPv4 Address: `192.168.20.10`
- Subnet Mask: `255.255.255.0`
- Default Gateway: `192.168.20.1`

## 7. Addressing Design Summary

VLSM enables efficient allocation of IPv4 address space by assigning different subnet sizes to departments.

The addressing scheme supports departmental segmentation, centralized DHCP services, inter-VLAN routing, and dynamic routing between the headquarters and remote office.
