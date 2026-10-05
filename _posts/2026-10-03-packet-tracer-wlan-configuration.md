---
title: "Lab: Packet Tracer WLAN Configuration"
date: 2026-10-03
categories:
  - labs
tags:
  - cybershujaa
  - cisco
  - wireless
  - wpa2
  - radius
---

*Configuring a home wireless router with WPA2-Personal, then an enterprise WLC network running both WPA2-PSK and WPA2-Enterprise with RADIUS authentication — side by side, to see the real difference.*

**Problem Statement**
Configure wireless connectivity two ways: a home wireless router with WPA2-PSK security for a handful of personal devices, and a Wireless LAN Controller (WLC) based enterprise network offering both WPA2-PSK and WPA2-Enterprise (802.1X) WLANs — then verify connectivity on each.

**Approach**
On the home router, changed the DHCP scope and starting address, configured the 2.4GHz SSID on channel 6, set WPA2-Personal with a passphrase, and changed the default admin password before connecting a laptop, tablet, and smartphone to confirm they could reach each other and a web server. On the WLC side, configured two VLAN interfaces (one per WLAN) with their own subnets, gateways, and DHCP associations, then stood up an internal DHCP scope for the controller's own management network. Added external server integration — a RADIUS server for authentication and an SNMP server for logging — before creating the two WLANs: one on WPA2-PSK with a shared passphrase, the other on WPA2-Enterprise using 802.1X against the RADIUS server. Both WLANs used FlexConnect local switching and local authentication. Connected one wireless host to each WLAN and tested connectivity by ping and by browsing to the web server.

**Tools Used**
Cisco Packet Tracer, Wireless LAN Controller (WLC) GUI, RADIUS/SNMP server configuration, WPA2-PSK, WPA2-Enterprise (802.1X)

**Key Lessons**
Running both security models side by side made the trade-off concrete rather than theoretical. WPA2-PSK is one shared passphrase for every device on the network — fast to set up, but it gives zero per-user accountability: if the passphrase leaks, every device needs reconfiguring, and there's no way to tell which device did what. WPA2-Enterprise authenticates each user individually against a RADIUS server, which means per-user credentials, per-user revocation, and an actual audit trail — at the cost of needing a working AAA backend and more moving parts to configure correctly. The debugging during this lab reinforced that wireless failures are rarely about wireless itself; every issue traced back to a boring mismatch — a wrong shared secret, an interface mapped to the wrong VLAN, a DHCP scope that didn't line up with the gateway. That's a pattern worth remembering: wireless security design is really just applied network fundamentals with an extra authentication layer on top.

[Full lab writeup (PDF)](/assets/files/labs/packet-tracer-wlan-configuration.pdf){: .btn .btn--primary}
