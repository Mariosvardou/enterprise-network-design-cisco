# Incident 001 — Access Port Connectivity Failure

## Incident Description

A workstation in the Sales department (PC0) experienced a complete loss of network connectivity in the simulated enterprise network.

## Symptoms

- PC0 could not reach its default gateway.
- Network communication was unavailable.
- The switch access port was not forwarding traffic.

## Investigation

The issue was investigated using Cisco IOS commands:

```text
show interfaces status
show running-config
```

The investigation identified that interface FastEthernet0/1 on SW1 was administratively disabled.

## Root Cause

The switch access port connected to PC0 had been disabled using the `shutdown` command.

## Resolution

The interface was re-enabled using:

```text
configure terminal
interface fastEthernet 0/1
no shutdown
end
```

## Validation

After restoring the interface, connectivity was tested using ICMP ping commands.

Expected results:

- PC0 → Sales Gateway: Successful
- PC0 → Remote Office: Successful
- PC0 → Production: Blocked by ACL

## Lessons Learned

This incident demonstrates the importance of verifying physical and interface status before investigating higher-layer protocols such as DHCP, OSPF, or ACLs.

A structured troubleshooting approach helps isolate network failures efficiently.
