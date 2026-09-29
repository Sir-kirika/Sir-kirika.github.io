---
title: "Lab: HTB Academy — Network Traffic Analysis"
date: 2026-09-21
categories:
  - labs
tags:
  - cybershujaa
  - htb
  - tcpdump
  - wireshark
  - ftp
---

*tcpdump and Wireshark from fundamentals to a live capture — extracting a file over FTP and recovering plaintext credentials from HTTP traffic.*

**Problem Statement**
Work through HackTheBox Academy's "Intro to Network Traffic Analysis" module — tcpdump fundamentals, the Wireshark GUI and TShark, then apply both to static pcap files and a live capture to extract a file transferred over FTP, find credentials exposed in cleartext HTTP, and identify a suspicious host.

**Approach**
Started with tcpdump basics — listing interfaces, disabling name resolution, reading Ethernet headers, combining switches, and saving/reading `.pcap` files — then moved to filtering by host and source port. Repeated the same workflow in Wireshark/TShark, then used GUI display filters (`http`, `http && image-jfif`) to follow a TCP stream and extract an embedded file from a pre-captured `.pcap`. Connected to a live lab environment over RDP/VPN to capture and analyze fresh traffic: filtered FTP traffic to find an anonymous login and extract a transferred file (`flag.jpeg`, pulled via `RETR` in passive mode), then filtered HTTP `POST` traffic and followed the stream to recover a suspect's username in plaintext. Cross-checked the finding using Wireshark's Conversations and Protocol Hierarchy views.

**Tools Used**
tcpdump, Wireshark, TShark, XFreeRDP, VPN, GUI display filters

**Key Lessons**
The FTP server (`172.16.10.20:21`, vsFTPd 3.0.3) accepted an anonymous login and transmitted the entire session — credentials, commands, and file contents — in cleartext; nothing about that traffic required decryption, just the right filter. The HTTP investigation reinforced the same point from a different angle: a plaintext login form exposes real credentials in a `POST` body, visible to anyone who can see the wire. Correlating one suspicious host (`172.16.10.2`) across FTP, HTTP, and the conversation/protocol hierarchy views tied isolated findings into one coherent picture — a good reminder that network security often comes down to visibility and knowing what to filter for, not tool complexity.

[Full lab writeup (PDF)](/assets/files/labs/htb-network-traffic-analysis.pdf){: .btn .btn--primary}
