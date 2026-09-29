---
permalink: /labs/tryhackme-dns-in-detail/
title: "TryHackMe: DNS in Detail"
layout: single
author_profile: true
---

**Problem Statement**
Complete the TryHackMe "DNS in Detail" room — understand how DNS resolves domain names to IP addresses, the domain hierarchy, common record types, and use `nslookup` to simulate real DNS queries against a practice domain.

**Approach**
Worked through the room's explanation of the DNS hierarchy (TLD → second-level domain → subdomain) and record types (A, AAAA, CNAME, MX, TXT), then ran `nslookup -type=A www.google.com` locally to see a real A-record lookup returning multiple IPv4 and IPv6 addresses. Used the room's built-in DNS query simulator to look up a practice domain's CNAME, TXT record, MX priority value, and A record — confirming each answer against the room's checker.

**Tools Used**
TryHackMe ("DNS in Detail" room), `nslookup`, Windows Command Prompt

**Key Lessons**
A single domain lookup isn't one hop — it's a chain: local cache → recursive resolver (usually the ISP) → root server → TLD server → authoritative server, with the result cached locally for the record's TTL. Seeing `google.com` resolve to multiple IPv4 and IPv6 addresses in one query was a concrete example of how large services use DNS itself for load distribution and redundancy, not just naming.

[Full lab writeup (PDF)](/assets/files/labs/tryhackme-dns-in-detail.pdf){: .btn .btn--primary}

[← Back to all Lab Challenges](/lab-challenges/)
