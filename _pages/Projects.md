---
permalink: /projects/
title: "Projects"
layout: single
author_profile: true
feature_row:
  - image_path: /assets/images/labs/identify-iam-breaches-cloudtrail-athena.png
    alt: "Identifying IAM breaches with CloudTrail and Athena"
    title: "IAM breach investigation"
    url: /labs/identify-iam-breaches-cloudtrail-athena/
    btn_label: "Read the write-up"
    btn_class: "btn--primary"
  - image_path: /assets/images/labs/key-vault-and-encryption.png
    alt: "Azure Key Vault privilege escalation chain"
    title: "Azure privilege escalation"
    url: /labs/key-vault-and-encryption/
    btn_label: "Read the write-up"
    btn_class: "btn--primary"
  - image_path: /assets/images/labs/kms-keys-with-finders-keypers.png
    alt: "Auditing KMS key blast radius"
    title: "KMS blast radius"
    url: /labs/kms-keys-with-finders-keypers/
    btn_label: "Read the write-up"
    btn_class: "btn--primary"
---

### Secure MT5-to-Web Bridge
Built DLLs (C++/C#) that stream live MetaTrader 5 trading data to browser dashboards and Excel in real time. Full pipeline: MT5 Expert Advisor → DLL → WebSocket → Node.js/FastAPI server → browser. Implemented WSS with both self-signed and CA-trusted SSL certificates depending on deployment target, added token-based client authentication, and deployed via Cloudflare Tunnel and Render for always-on hosting.

**Stack:** C++, C#, Node.js, FastAPI, WSS/SSL, Cloudflare Tunnel
[View on GitHub](https://github.com/Sir-kirika/mt5bridge){: .btn .btn--primary}

---

### Web Application Security Lab
Built a small Flask and SQLite app, attacked it with cURL, found a SQL injection vulnerability, and fixed it with parameterised queries. Also removed a state-changing GET endpoint and the server version banner to reduce information disclosure.

**Stack:** Python, Flask, SQLite, cURL, SQL injection
[Read the write-up](/labs/introduction-to-web-applications/){: .btn .btn--primary}

---

### Cloud Security Labs (AWS and Azure)
Hands-on investigations from the Cyber Shujaa Cloud and Network Security track:

{% include feature_row %}

- [Identifying IAM breaches with CloudTrail and Athena](/labs/identify-iam-breaches-cloudtrail-athena/): confirmed and sized a brute-force attack with SQL queries.
- [Role-based access control attack chain](/labs/role-based-access-control/): traced an AWS attack from a hidden config file to an External ID-protected role.
- [Key Vault and encryption](/labs/key-vault-and-encryption/): followed an Azure privilege-escalation chain to plaintext secrets and unencrypted data.
- [KMS blast radius](/labs/kms-keys-with-finders-keypers/): mapped every resource a shared KMS key encrypts.
- [Keeping secrets out of Git](/labs/keep-secrets-out-of-git/): caught a credentials file before it entered commit history.

**Stack:** AWS IAM, CloudTrail, Athena, KMS, Azure Key Vault, Git

---

### Network Defence Labs
Network hardening and traffic analysis with Cisco Packet Tracer, Wireshark and tcpdump:
- [VLANs and secure switch configuration](/labs/vlans-and-secure-switch-configuration/): hardened against rogue DHCP, trunk manipulation and spanning-tree abuse.
- [Site-to-site IPsec VPNs](/labs/configuring-site-to-site-vpns/): verified that only policy-matching traffic is encrypted.
- [WLAN security](/labs/packet-tracer-wlan-configuration/): compared WPA2-Personal with WPA2-Enterprise and RADIUS.
- [Network traffic analysis](/labs/htb-network-traffic-analysis/): recovered plaintext credentials from captured HTTP traffic.

**Stack:** Cisco IOS, Packet Tracer, Wireshark, tcpdump

---

### Smart Meter Security System (Final-Year Project)
Anti-tampering system for pre-pay smart meters: locks the intake point, grants access only to authorised users, and reports tampering attempts to a central database. An early, hands-on introduction to access control and intrusion detection.

**Stack:** Embedded systems, access control

---

### Quantitative FX Research
Self-directed research applying Hidden Markov Models to detect volatility regimes across FX pairs, and Kuramoto synchronisation theory to study coordinated trader behaviour around gold and major USD pairs. Includes an 8-year walk-forward backtesting and optimisation pipeline built in Python.

**Stack:** Python, HMM, backtesting

---

### Notepad Calculator
Desktop note-taking app combining free-form notes with inline arithmetic, with variable assignment and reuse, light/dark themes, and undo/redo. Designed and coded solo, from the UI down to the expression-parsing logic.

**Stack:** Python, Kivy
