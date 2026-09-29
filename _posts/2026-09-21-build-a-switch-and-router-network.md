---
title: "Lab: Build a Switch and Router Network"
date: 2026-09-21
categories:
  - labs
tags:
  - cybershujaa
  - cisco
  - routing
  - packet-tracer
---

*Cabling and configuring a switch, router, and two PCs from scratch — IPv4/IPv6 addressing, encrypted passwords, and interface verification with Cisco IOS.*

**Problem Statement**
Given a topology diagram and IP addressing table, cable a switch, router, and two PCs, then configure each device from scratch so both PCs can reach each other across the router — with full IPv4 and IPv6 support.

**Approach**
Cabled the devices to match the topology, then assigned static IP information to both PCs. On the router: set a hostname, disabled DNS lookup, configured encrypted privileged-EXEC and VTY passwords, added an unauthorized-access banner, activated both interfaces with IPv4/IPv6 addressing, added interface descriptions, enabled IPv6 unicast routing, and saved the running config to startup. Verified connectivity with a ping between the two PCs before and after configuration — confirming the initial timeout was due to unconfigured devices, not a topology error.

**Tools Used**
Cisco Packet Tracer, Cisco IOS CLI (`show ip route`, `show ipv6 route`, `show ip interface brief`, `show interfaces`)

**Key Lessons**
The routing table's `C` (connected) and `L` (local) codes reflect the router's own record of directly reachable networks. A misconfigured default gateway fails silently — packets are sent to an address nothing owns, with no error raised — which reinforces why verifying interface and gateway configuration matters before assuming a network problem is "downstream."

[Full lab writeup (PDF)](/assets/files/labs/build-a-switch-and-router-network.pdf){: .btn .btn--primary}
