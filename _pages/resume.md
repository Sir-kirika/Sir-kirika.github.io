---
permalink: /resume/
title: "Resume"
layout: single
author_profile: true
---

*[Download PDF version](/assets/files/resume.pdf){: .btn .btn--primary}*

## Professional Summary

Electrical and Electronics Engineering graduate with 3+ years of professional software development, now specialising in application, cloud and data security. I build security into code: encrypted WSS data pipelines with SSL/TLS and token-based authentication, and a Flask application where I found and fixed a SQL injection flaw using parameterised queries. Currently on the Cyber Shujaa Cloud and Network Security track, with 15+ documented hands-on labs covering AWS and Azure IAM, KMS and CloudTrail investigations, secrets management, VLAN hardening and IPsec VPNs. Seeking to support vulnerability assessment, security controls and secure development practices in a junior security role.

[LinkedIn](https://www.linkedin.com/in/james-kirika) · [GitHub](https://github.com/Sir-kirika) · [Lab write-ups](/lab-challenges/)

## Core Skills

- **Application & Data Security:** SQL injection testing and remediation, secure coding, secrets management (keeping credentials out of Git), TLS/SSL certificate management, token-based authentication, encryption and key management (AWS KMS, Azure Key Vault)
- **Cloud Security:** AWS IAM and role-based access control, CloudTrail log analysis with Athena (SQL), Azure privilege-escalation analysis, least-privilege principles
- **Network Security & Monitoring:** Wireshark, tcpdump, Cisco Packet Tracer, VLAN and Layer 2 hardening, site-to-site IPsec VPN, WPA2-Enterprise/RADIUS, TCP/IP, DNS, OSI model
- **Programming & Tools:** Python, C++, C#, Node.js, MQL4/MQL5, Bash, SQL, cURL, Git/GitHub, REST APIs, HackTheBox Academy, TryHackMe
- **Soft Skills:** fast self-directed learner, analytical problem solving, clear technical documentation (public lab write-ups), client communication, meeting tight deadlines, working under supervision and independently

## Education & Certifications

**Cyber Shujaa — Cloud and Network Security Track**
*Sep 2026 – Present (in progress)*
Structured training in networking fundamentals, cloud security and hands-on labs; write-ups published on this site.

**Bachelor of Technology, Electrical and Electronics Engineering — Murang'a University of Technology**
*Jan 2017 – Dec 2021 · Second Class Honours, Upper Division*
Final-year project: anti-tampering smart meter system that restricts access to authorised users and reports tampering attempts to a central database.

Also: First Aid and firefighting training.

## Technical Projects & Security Labs

**Secure MT5-to-Web Bridge** (C++, C#, Node.js, WSS) — [GitHub](https://github.com/Sir-kirika/mt5bridge)
- Built a real-time pipeline from MetaTrader 5 to browser dashboards and Excel, secured with WSS, self-signed and CA-trusted SSL certificates, and token-based client authentication.
- Deployed for always-on use through Cloudflare Tunnel and Render.

**Web Application Security Lab** (Python, Flask, SQLite)
- Built a Flask/SQLite app, exploited a SQL injection vulnerability with cURL, and fixed it with parameterised queries.
- Removed a state-changing GET endpoint and the server version banner to reduce information disclosure.

**Cloud Security Labs** (AWS, Azure) — Cyber Shujaa
- Confirmed and sized a brute-force attack on AWS IAM by querying CloudTrail logs with Athena (Console and CLI).
- Traced attack chains through AWS role-based access control with External ID, and an Azure privilege-escalation chain ending at plaintext secrets in Key Vault and unencrypted data.
- Mapped the full "blast radius" of shared KMS keys, and caught a credentials file before it entered Git history.

**Network Defence Labs** (Cisco Packet Tracer, Wireshark, HTB Academy, TryHackMe)
- Hardened switches against rogue DHCP, trunk manipulation and spanning-tree abuse; built an IPsec site-to-site VPN and verified that only policy-matching traffic is encrypted; configured WPA2-Enterprise with RADIUS.
- Recovered plaintext credentials from captured HTTP traffic and extracted files from FTP captures using tcpdump and Wireshark.

All write-ups: [Lab Challenges](/lab-challenges/)

## Professional Experience

**Software Engineer (Freelance) — MQL5 Freelance**
*Apr 2023 – Present*
- Write MQL4/MQL5 indicators, scripts and Expert Advisors for MetaTrader clients, and convert Pine Script strategies to MQL4/5.
- Build C++ and C# DLL bridges that stream live MT5 data to web dashboards over WSS, with SSL certificates and token authentication.
- Debug, troubleshoot and support delivered software; praised by clients for reliability and for meeting tight deadlines.

**Technician — LED Power Technology**
*Jan 2022 – Dec 2022*
- Installed and maintained CCTV and IP camera systems: structured cabling, camera mounting and network switch configuration.

**Attachee — Kenya Power and Lighting Company (KPLC)**
*Jan 2021 – Apr 2021*
- Installed and read smart and large-power meters and current transformers, working to safety and ethical standards.