# Enterprise Network Design & Implementation

### Cisco Packet Tracer | Networking Portfolio Project

## Project Overview

This project demonstrates the design, configuration, and validation of a simulated enterprise network connecting a headquarters office with a remote branch.

The network was implemented using Cisco Packet Tracer and includes VLAN segmentation, inter-VLAN routing, DHCP, OSPF dynamic routing, and extended Access Control Lists (ACLs).

## Network Architecture

The simulated infrastructure consists of:

- 2 Cisco routers (2911)
- 2 Cisco switches (2960)
- 7 end-user computers
- 3 departmental VLANs
- 1 remote office LAN
- 1 point-to-point WAN connection

## Technologies Implemented

- IPv4 addressing and VLSM subnetting
- VLAN configuration and IEEE 802.1Q trunking
- Router-on-a-Stick inter-VLAN routing
- DHCP server configuration
- OSPF single-area dynamic routing
- Extended ACLs for traffic filtering
- Network troubleshooting and connectivity validation

## IP Addressing Scheme

| Network | Subnet | Gateway |
|---|---|---|
| Production — VLAN 30 | 192.168.10.0/26 | 192.168.10.1 |
| Sales — VLAN 10 | 192.168.10.64/27 | 192.168.10.65 |
| Marketing — VLAN 20 | 192.168.10.96/28 | 192.168.10.97 |
| Remote Office | 192.168.20.0/24 | 192.168.20.1 |
| WAN Link | 10.0.0.0/30 | R1: 10.0.0.1 / R2: 10.0.0.2 |

## Security Policy

An extended ACL named `SALES_POLICY` was configured to block traffic originating from the Sales VLAN and destined for the Production VLAN.

Other permitted communication paths remain operational.

## Network Validation

The following tests are included in the validation plan:

- VLAN and trunk verification
- DHCP address allocation
- OSPF neighbor adjacency verification
- Routing table verification
- Inter-VLAN connectivity testing
- Remote office connectivity
- ACL traffic filtering

Test evidence and screenshots are provided in the repository.

## Troubleshooting Scenario

A simulated access-port failure was introduced by administratively disabling a switch interface.

The issue was diagnosed using Cisco IOS show commands and resolved by restoring the interface configuration.

## Tools

- Cisco Packet Tracer
- Cisco IOS CLI
- GitHub
- Markdown

## Learning Outcomes

Through this project, I practiced designing, implementing, validating, and troubleshooting a segmented enterprise network.

The project was developed independently as part of my technical portfolio while studying Electronic Engineering.

## Project Files

The Packet Tracer topology is available in the `packet-tracer/` directory.

Configuration evidence, screenshots, and technical documentation are included in their respective folders.
