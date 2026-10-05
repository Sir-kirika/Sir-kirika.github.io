---
title: "Lab: VLANs and Secure Switch Configuration"
date: 2026-09-30
categories:
  - labs
tags:
  - cybershujaa
  - cisco
  - vlans
  - switch-security
---

*Segmenting a switched network with VLANs and hardening it against the common Layer 2 attacks — rogue DHCP, trunk manipulation, and spanning-tree abuse.*

**Problem Statement**
Configure a small switched network (one router, two Catalyst 2960 switches, two PCs) with VLAN segmentation, then apply a set of Layer 2 security controls to protect it from unauthorized access, rogue DHCP servers, and spanning-tree manipulation — confirmed with an end-to-end connectivity test.

**Approach**
Cabled and configured the router and both switches with basic settings, then created VLAN 10 for user traffic and its SVI. Set up 802.1Q trunking between the two switches using VLAN 333 as an unused native VLAN — a deliberate choice, since leaving the native VLAN at its default (VLAN 1) is a known VLAN-hopping risk — and disabled DTP negotiation so trunks can't be renegotiated by a rogue device. Moved all unused ports into a dead-end VLAN 999 ("ParkingLot") and shut them down. Configured port security on the PC-facing access ports to cap the number of allowed MAC addresses, with different violation modes and aging settings tested on each switch. Enabled DHCP snooping with rate limiting on the untrusted ports to block rogue DHCP servers and DHCP flooding, then verified the snooping binding table. Finally enabled PortFast and BPDU guard on the access ports connected to the PCs, and confirmed both were active before testing full connectivity between the two PCs and their default gateway.

**Tools Used**
Cisco Packet Tracer, Cisco IOS CLI (`show interfaces trunk`, `show interface status`, `show port-security`, `show spanning-tree`)

**Key Lessons**
Most of this lab is about closing gaps that look harmless until someone exploits them. Using an unused VLAN as the trunk's native VLAN and disabling DTP both exist specifically to block VLAN hopping — an attacker on an access port spoofing trunk negotiation, or exploiting the native VLAN's untagged traffic, is a real and well-documented Layer 2 attack. DHCP snooping protects against a rogue device on the network simply handing out its own (malicious) DHCP leases — something no amount of VLAN segmentation alone would stop, since DHCP requests are broadcast within a VLAN by design. BPDU guard was the one that reframed how I think about "fast" ports: PortFast exists purely for convenience (skip STP's listening/learning delay for a host port), but pairing it with BPDU guard is what makes it safe — if that "host" port ever receives a BPDU (meaning a switch, not a PC, got plugged in), the port shuts down instead of silently becoming part of the spanning tree. Speed and security aren't separate settings here, they're a pair.

[Full lab writeup (PDF)](/assets/files/labs/vlans-and-secure-switch-configuration.pdf){: .btn .btn--primary}
