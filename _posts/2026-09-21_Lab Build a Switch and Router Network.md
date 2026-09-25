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

A foundational Cisco lab: cable a switch, router, and two PCs to a given topology, then configure everything to match an addressing table — hostname, encrypted passwords, VTY/console access, an unauthorized-access banner, and dual-stack (IPv4 + IPv6) interfaces on the router.

The first ping between the PCs failed with a timeout, which was expected — nothing had been configured yet. That's the point of doing it in order: see the failure state before fixing it, rather than starting from a working network and never understanding why it works.

**Key takeaway:** the routing table's `C` (connected) and `L` (local) codes are the router's own bookkeeping of what it can reach directly. When I intentionally considered what happens if `G0/0/1` were misaddressed, the failure mode is instructive — PC-A wouldn't just fail to ping PC-B, it would silently send everything to a gateway address that no device actually owns. No error, just packets going nowhere. That's a good reminder that routing misconfigurations tend to fail quietly, not loudly.

Commands used to verify: `show ip route`, `show ipv6 route`, `show ip interface brief`, `show interfaces` — a decent toolkit for confirming Layer 1–3 status, addressing, and reachability on any Cisco device.