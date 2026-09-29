---
permalink: /labs/htb-web-requests/
title: "HTB Academy: Web Requests"
layout: single
author_profile: true
---

**Problem Statement**
Work through HackTheBox Academy's "Web Requests" module — HTTP/HTTPS fundamentals, request and response headers, HTTP methods and status codes, Basic Authentication, and full CRUD operations against a REST API — using cURL, browser DevTools, and the browser Console.

**Approach**
Started with basic cURL requests (`-O` to save output, `-v`/`-vvv` for verbose request/response detail, `-k` to skip certificate checks) and cross-checked the same requests in browser DevTools. Worked through the four header categories (general, entity, request, response) and used `-I`/`-i` to inspect response headers directly, then set a custom `User-Agent` with `-A`. Covered HTTP methods (GET/POST/HEAD/PUT/DELETE/OPTIONS/PATCH) and status code classes, then tested HTTP Basic Auth three ways — `-u` flag, credentials embedded in the URL, and manually setting the `Authorization` header with `-H` — confirming all three reached the protected page identically. Captured an authenticated session cookie and reused it via cURL and the browser. Finally, performed full CRUD (Create/Read/Update/Delete) against a REST API — GET to read entries, POST to create, PUT to update, DELETE to remove — culminating in a challenge requiring an update-then-delete-then-search sequence to reveal a hidden flag.

**Tools Used**
cURL, browser DevTools (Network tab), browser Console (`fetch`), REST API testing, `jq`

**Key Lessons**
Seeing the same request three ways — cURL, DevTools, and a Console `fetch` — surfaced different failure modes for each: shell quoting broke a JSON payload in cURL, while a page's Content-Security-Policy blocked a `fetch` call outright because the target was plain `http://` and the CSP only allowed HTTPS `connect-src`. Testing Basic Auth three different ways drove home how weak it really is on its own — the `Authorization` header is just base64-encoded `username:password`, not encryption, and can be replayed by anyone who captures it. The broader takeaway: HTTP is inherently plaintext and stateless, and everything that makes it safer in practice — HTTPS, secure cookies, CSP, real authentication — is something a server or browser has to deliberately add on top.

[Full lab writeup (PDF)](/assets/files/labs/htb-web-requests.pdf){: .btn .btn--primary}

[← Back to all Lab Challenges](/lab-challenges/)
