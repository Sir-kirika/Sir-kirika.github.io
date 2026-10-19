---
title: "Lab: Configuring Site-to-Site IPsec VPNs"
date: 2026-10-10
categories:
  - labs
tags:
  - cybershujaa
  - cisco
  - ipsec
  - vpn
---

*Building an IPsec tunnel between two routers and proving, from the packet counters, that only the traffic that matches the policy gets encrypted.*

**Problem Statement**
Configure a site-to-site IPsec VPN between routers R1 and R3 so that traffic between their LANs is encrypted across an untrusted middle network (R2), then verify that the tunnel only carries the traffic it was told to protect.

**Approach**
Confirmed baseline connectivity first with a ping from PC-A to PC-C. Enabled the Security Technology package on R1 (license change plus a reload) and verified it with `show version`. Defined "interesting traffic" with an extended ACL that matches only the R1 LAN to R3 LAN flow. Built the VPN in two phases: an IKE Phase 1 ISAKMP policy (AES-256, pre-shared key authentication, Diffie-Hellman group 5), then a Phase 2 IPsec transform set (`esp-aes` with `esp-sha-hmac`) bound to a crypto map along with the peer address and the ACL. Applied the crypto map to the outgoing serial interface. Repeated the mirror-image configuration on R3, with the ACL, peer address, and interface reversed. R2 got no VPN configuration at all. Verified with `show crypto ipsec sa`: counters before any traffic, after a ping from PC-A to PC-C (interesting), and after a ping from PC-A to PC-B (uninteresting).

**Tools Used**
Cisco Packet Tracer, Cisco IOS CLI (`crypto isakmp`, `crypto ipsec`, `crypto map`, `show crypto ipsec sa`, `show version`)

**Key Lessons**
Both peers have to agree on everything: ISAKMP policy, key, transform set, and a crypto-map ACL that is the mirror image of the other side's. One mismatch and the tunnel never forms, and the failure is quiet. The tunnel is also lazy by design. The `show crypto ipsec sa` counters sat at 0 until interesting traffic arrived, then jumped to 7 after the PC-A to PC-C ping, and the first ping timed out while IKE negotiated. Pinging PC-B left the counters unchanged, which is the clearest proof that the ACL, not the tunnel, decides what is protected. R2 forwarded everything without any VPN config, which shows IPsec protecting traffic between the two peers regardless of what sits in the middle. One caveat worth knowing: Packet Tracer tops out at DH group 5, and a production network should use group 14 or higher.

[Full lab writeup (PDF)](/assets/files/labs/configuring-site-to-site-vpns.pdf){: .btn .btn--primary}
