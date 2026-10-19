---
title: "Lab: HTB Academy — Introduction to Web Applications"
date: 2026-10-10
categories:
  - labs
tags:
  - cybershujaa
  - htb
  - web-security
  - sql-injection
  - flask
---

*Building a small Flask and SQLite app from scratch, then attacking it with curl, finding a SQL injection, and fixing it.*

**Problem Statement**
Work through HackTheBox Academy's "Introduction to Web Applications" module (architecture, front-end and back-end components, common vulnerability classes), then apply it end to end: build a web application, test it for vulnerabilities, and remediate what turns up.

**Approach**
Covered the module's front-end topics (HTML, CSS, JavaScript, data exposure, HTML injection, XSS and CSRF) and back-end topics (servers, databases, frameworks and APIs, public CVEs and CVSS scoring) with the exercises for each. For the applied lab, built a visitor-greeting app: HTML/JS front end calling a Flask API backed by SQLite, bound to localhost only. Then tested it build-then-break-then-fix style, by hand with `curl` and browser DevTools. A single quote in the `name` parameter crashed the server, confirming unsanitized input, and a crafted payload inserted a row the application logic never intended. After patching, the same payloads were replayed to confirm the fixes held.

**Tools Used**
Python, Flask, SQLite, curl, browser DevTools, HTB Academy

**Findings**
- **SQL injection in the visitor insert (High, CVSS-style 8.1).** The query was built by string concatenation. Fixed with a parameterized query, and the re-test stored the payload as one literal value.
- **Server version disclosure (Low, 3.7).** The `Server` header gave away the Werkzeug and Python versions, which makes CVE lookups trivial for an attacker. Fixed by overriding the version-reporting attributes.
- **State-changing logic on HTTP GET (Low, 3.1).** A database write happened on a GET request, which makes it CSRF-prone. Fixed by splitting the endpoint so GET only reads and writes require POST.

**Key Lessons**
Front-end code is fully visible and editable by the user, so it can never be where security is enforced; validation and authorization belong on the back end. The SQL injection came from bypassing the framework's safer defaults in favor of string concatenation, a reminder that frameworks only protect you when you use them as intended. The other two findings were small on their own, but version fingerprinting is usually step one of a larger attack chain, and a GET that mutates state turns a harmless-looking URL into an attack vector. The most useful part was building the app first: it is much easier to see why each fix matters after writing the vulnerable code yourself.

[Full lab writeup (PDF)](/assets/files/labs/introduction-to-web-application.pdf){: .btn .btn--primary}
