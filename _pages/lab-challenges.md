---
permalink: /lab-challenges/
title: "Lab Challenges"
layout: single
author_profile: true
---

Hands-on networking and security labs from the Cyber Shujaa Cloud and Network Security track.

---

## Build a Switch and Router Network

**Problem Statement**
Given a topology diagram and IP addressing table, cable a switch, router, and two PCs, then configure each device from scratch so both PCs can reach each other across the router — with full IPv4 and IPv6 support.

**Approach**
Cabled the devices to match the topology, then assigned static IP information to both PCs. On the router: set a hostname, disabled DNS lookup, configured encrypted privileged-EXEC and VTY passwords, added an unauthorized-access banner, activated both interfaces with IPv4/IPv6 addressing, added interface descriptions, enabled IPv6 unicast routing, and saved the running config to startup. Verified connectivity with a ping between the two PCs before and after configuration — confirming the initial timeout was due to unconfigured devices, not a topology error.

**Tools Used**
Cisco Packet Tracer, Cisco IOS CLI (`show ip route`, `show ipv6 route`, `show ip interface brief`, `show interfaces`)

**Key Lessons**
The routing table's `C` (connected) and `L` (local) codes reflect the router's own record of directly reachable networks. A misconfigured default gateway fails silently — packets are sent to an address nothing owns, with no error raised — which reinforces why verifying interface and gateway configuration matters before assuming a network problem is "downstream."

[Full lab writeup (PDF)](/assets/files/labs/build-a-switch-and-router-network.pdf){: .btn .btn--primary}

---

## Using Wireshark to Examine Network Traffic

**Problem Statement**
Capture and analyze live ICMP traffic at both the local network level and across the internet, to observe how IP addresses get resolved to MAC addresses — and when that resolution does or doesn't happen.

**Approach**
Captured Wi-Fi traffic with Wireshark, applied an ICMP filter, and pinged a local device (phone) to observe the ARP request/reply exchange preceding the ping. Cross-referenced source/destination MAC addresses against known device interfaces to confirm the capture was accurate. Repeated the exercise pinging remote hosts (yahoo.com, cisco.com, google.com) and compared the destination MAC address in each capture against the destination IP.

**Tools Used**
Wireshark, Windows Command Prompt (`ping`), `ipconfig /all`

**Key Lessons**
MAC addresses are Layer 2 and only meaningful on the local segment. For local pings, the device ARPs for the target's MAC before any ICMP traffic flows. For remote pings, no ARP request is ever sent for the remote IP — the destination MAC in every remote capture was the local router's, not the remote server's — because the device just hands the frame to its default gateway once it determines the destination is off-subnet.

[Full lab writeup (PDF)](/assets/files/labs/wireshark-icmp-traffic.pdf){: .btn .btn--primary}

---

## Investigating the TCP/IP and OSI Models in Packet Tracer

**Problem Statement**
Using Packet Tracer's Simulation mode, trace a single HTTP request end-to-end to observe encapsulation and de-encapsulation as it happens at each OSI/TCP-IP layer.

**Approach**
Generated web traffic from a client to a server, then stepped through each event in the simulation's event list, inspecting the OSI Model and PDU Details tabs at every hop. Tracked how In Layers and Out Layers differ for the same event, followed the DNS query that resolved the hostname before the HTTP request was sent, and watched the TCP connection lifecycle from establishment through to a final `CLOSED` state.

**Tools Used**
Cisco Packet Tracer (Simulation mode)

**Key Lessons**
Outbound and inbound views of the same event are mirror images — source/destination IPs, MACs, and ports all swap, and the Layer 7 description flips from "sending" to "receiving." DNS resolution happens before the HTTP request is ever sent. And while HTTP operates at Layer 7, it's entirely dependent on the layers beneath it — TCP for reliable delivery and connection state, IP for addressing, Ethernet for the physical hop — a dependency that's easy to state abstractly but much clearer once watched frame-by-frame.

[Full lab writeup (PDF)](/assets/files/labs/tcp-ip-osi-models.pdf){: .btn .btn--primary}
