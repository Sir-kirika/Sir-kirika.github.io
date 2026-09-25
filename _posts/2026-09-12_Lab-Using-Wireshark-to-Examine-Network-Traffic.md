---
title: "Lab: Using Wireshark to Examine Network Traffic"
date: 2026-09-12
categories:
  - labs
tags:
  - cybershujaa
  - wireshark
  - icmp
  - arp
---

Captured live traffic with Wireshark to see, packet by packet, what a `ping` actually does — both on the local network and across the internet.

**Local ping:** pinging a device on the same subnet triggers an ARP broadcast first — "who has this IP?" — before any ICMP traffic flows. The responding device replies directly with its MAC address, and only then does the actual ping exchange happen. Source and destination MAC addresses in the capture lined up exactly with the two devices involved.

**Remote ping (yahoo.com, cisco.com, google.com):** this is where it got interesting. The destination IP in each capture was the real, resolved IP of the remote site — but the destination MAC address was always the local router's MAC, never the remote server's. No ARP request was ever sent for the remote IP.

**Key takeaway:** MAC addresses are Layer 2 and only mean anything on the local segment. Once a destination IP falls outside the local subnet, the device doesn't bother resolving its MAC — it just hands the frame to the default gateway, because that's the only device it can reach directly at Layer 2. The router takes it from there. It's the clearest possible illustration of where Layer 2 addressing stops mattering and Layer 3 routing takes over.