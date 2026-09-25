---
permalink: /projects/
title: "Projects"
layout: single
author_profile: true
---

### Secure MT5-to-Web Bridge
Built DLLs (C++/C#) that stream live MetaTrader 5 trading data to browser dashboards and Excel in real time. Full pipeline: MT5 Expert Advisor → DLL → WebSocket → Node.js/FastAPI server → browser. Implemented WSS with both self-signed and CA-trusted SSL certificates depending on deployment target, added token-based client authentication, and deployed via Cloudflare Tunnel and Render for always-on hosting.

**Stack:** C++, C#, Node.js, FastAPI, WSS/SSL, Cloudflare Tunnel
[View on GitHub](https://github.com/Sir-kirika){: .btn .btn--primary}

---

### Quantitative FX Research
Self-directed research applying Hidden Markov Models to detect volatility regimes across FX pairs, and Kuramoto synchronization theory (borrowed from physics) to study coordinated trader behavior around gold and major USD pairs. Includes an 8-year walk-forward backtesting and optimization pipeline built in Python.

**Stack:** Python, HMM, backtesting

---

### Notepad Calculator
Desktop note-taking app combining free-form notes with inline arithmetic — supports variable assignment and reuse within a note, light/dark themes, and undo/redo. Designed and coded solo, from UI down to the expression-parsing logic.

**Stack:** Python, Kivy

---

### Smart Meter Security System (Final-Year Project)
Anti-tampering system for pre-pay smart meters — locks the intake point, grants access only to authorized users, and reports tampering attempts to a central database. An early, hands-on introduction to access control and intrusion detection.

**Stack:** Embedded systems, access control
