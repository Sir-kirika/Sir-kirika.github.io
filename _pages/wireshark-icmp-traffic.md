---
permalink: /labs/wireshark-icmp-traffic/
title: "Using Wireshark to Examine Network Traffic"
layout: single
author_profile: true
---

**Problem Statement**
Capture and analyze live ICMP traffic at both the local network level and across the internet, to observe how IP addresses get resolved to MAC addresses — and when that resolution does or doesn't happen.

**Approach**
Captured Wi-Fi traffic with Wireshark, applied an ICMP filter, and pinged a local device (phone) to observe the ARP request/reply exchange preceding the ping. Cross-referenced source/destination MAC addresses against known device interfaces to confirm the capture was accurate. Repeated the exercise pinging remote hosts (yahoo.com, cisco.com, google.com) and compared the destination MAC address in each capture against the destination IP.

**Tools Used**
Wireshark, Windows Command Prompt (`ping`), `ipconfig /all`

**Key Lessons**
MAC addresses are Layer 2 and only meaningful on the local segment. For local pings, the device ARPs for the target's MAC before any ICMP traffic flows. For remote pings, no ARP request is ever sent for the remote IP — the destination MAC in every remote capture was the local router's, not the remote server's — because the device just hands the frame to its default gateway once it determines the destination is off-subnet.

[Full lab writeup (PDF)](/assets/files/labs/wireshark-icmp-traffic.pdf){: .btn .btn--primary}

[← Back to all Lab Challenges](/lab-challenges/)
