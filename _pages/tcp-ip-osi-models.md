---
permalink: /labs/tcp-ip-osi-models/
title: "Investigating the TCP/IP and OSI Models in Packet Tracer"
layout: single
author_profile: true
---

**Problem Statement**
Using Packet Tracer's Simulation mode, trace a single HTTP request end-to-end to observe encapsulation and de-encapsulation as it happens at each OSI/TCP-IP layer.

**Approach**
Generated web traffic from a client to a server, then stepped through each event in the simulation's event list, inspecting the OSI Model and PDU Details tabs at every hop. Tracked how In Layers and Out Layers differ for the same event, followed the DNS query that resolved the hostname before the HTTP request was sent, and watched the TCP connection lifecycle from establishment through to a final `CLOSED` state.

**Tools Used**
Cisco Packet Tracer (Simulation mode)

**Key Lessons**
Outbound and inbound views of the same event are mirror images — source/destination IPs, MACs, and ports all swap, and the Layer 7 description flips from "sending" to "receiving." DNS resolution happens before the HTTP request is ever sent. And while HTTP operates at Layer 7, it's entirely dependent on the layers beneath it — TCP for reliable delivery and connection state, IP for addressing, Ethernet for the physical hop — a dependency that's easy to state abstractly but much clearer once watched frame-by-frame.

[Full lab writeup (PDF)](/assets/files/labs/tcp-ip-osi-models.pdf){: .btn .btn--primary}

[← Back to all Lab Challenges](/lab-challenges/)
