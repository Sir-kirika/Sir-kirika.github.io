---
title: "Lab: Investigating the TCP/IP and OSI Models in Packet Tracer"
date: 2026-09-11
categories:
  - labs
tags:
  - cybershujaa
  - tcp-ip
  - osi-model
  - packet-tracer
---

Used Packet Tracer's Simulation mode to watch a single HTTP request get encapsulated, sent, and decapsulated in real time — the kind of thing that's easy to memorize as a diagram and much more useful once you've actually watched it happen.

Tracking one web request end to end surfaced a few things that don't come across in a textbook diagram:

- **Outbound vs. inbound is a mirror image.** Comparing the In Layers and Out Layers columns on the same event showed source/destination IPs and MACs swap, source/destination ports flip (client's 1025 → server's 80 becomes server's 80 → client's 1025), and even the plain-English description at Layer 7 flips from "sending" to "receiving."
- **DNS resolves before anything else happens.** The client's first move wasn't the HTTP request itself — it was a DNS query for `www.osi.local`, resolved to `192.168.1.254`, before a single HTTP packet went anywhere.
- **The TCP connection has a visible lifecycle.** From SYN/connection-establishment through data transfer to a final event where the connection state moves to `CLOSED` — TCP's job doesn't end when the data arrives, it ends when both sides agree the session is done.

**Key takeaway:** HTTP lives at Layer 7, but it's completely dependent on everything underneath it — TCP for reliable delivery and connection state, IP for addressing, Ethernet for the physical hop, with DNS and ARP doing supporting resolution work along the way. Watching the encapsulation happen frame-by-frame made that dependency concrete instead of abstract.