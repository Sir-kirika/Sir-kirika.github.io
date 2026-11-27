---
title: "Lab: Role-Based Access Control — Pwned Labs AWS Attack Chain"
date: 2026-11-02
categories:
  - labs
tags:
  - cybershujaa
  - aws
  - iam
  - rbac
  - pwned-labs
---

*Tracing a full attack chain against a simulated company's AWS environment — from a hidden config file on a web server to an assumable IAM role protected by an External ID.*

**Problem Statement**
Gain an initial foothold on a target web server through directory enumeration, pivot into the target's AWS environment using any discovered credentials, and escalate privileges through IAM, S3, and Secrets Manager enumeration toward an externally-assumable IAM role.

**Approach**
Connected to the isolated lab environment over WireGuard and confirmed the target was reachable. An `nmap` scan showed only port 80 open, and the homepage itself was a static template with nothing linked beyond it — so the next step was `ffuf` with a DirBuster wordlist to brute-force hidden paths. The first pass returned mostly false positives, since the server returned its default homepage (200 OK) for any invalid path instead of a proper 404; filtering by response size cleared that noise and surfaced a genuine hit: an unauthenticated `config.json` containing a live AWS access key pair. That key authenticated as a distinct IAM identity, more privileged than the lab's starting user, confirming the leak was real and usable. From there, `aws-enumerator` (after fixing a transcription error in the secret key) mapped out the identity's permissions, which included listing Secrets Manager entries. One secret's description pointed directly at an external-partner cost-optimization role, and retrieving it returned a second set of login-style credentials rather than AWS keys. The next stage required extracting temporary session credentials directly from the AWS Console's network traffic via browser DevTools, since the compromised identity lacked CloudShell access.

**Tools Used**
WireGuard, `nmap`, `ffuf`, SecLists wordlists, AWS CLI, `aws-enumerator`, browser DevTools (Network tab)

**Findings**
A chain of individually small issues combined into a real escalation path: an unauthenticated config file exposing live AWS credentials, a Secrets Manager secret readable by an over-broad IAM identity, and (per its description) an IAM role intended to be assumable by an external partner via an External ID condition — the kind of trust relationship that's easy to misconfigure into something assumable by more than intended.

**Key Lessons**
The entire chain started from a single exposed configuration file — not a zero-day, not a clever exploit, just a file that should never have been reachable without authentication. That's consistent with how most real-world cloud compromises start. Equally important: the engagement didn't go cleanly. Multiple freshly-issued temporary credential sets failed with signature and token errors during the final extraction step, likely a mix of clipboard corruption and credentials expiring faster than they could be applied — and after disproportionate time on that single step, the assessment was documented honestly as incomplete rather than faked to a clean finish. In a real engagement, knowing when a technique isn't working and documenting that clearly is as valuable as the exploit chain itself.

[Full lab writeup (PDF)](/assets/files/labs/role-based-access-control.pdf){: .btn .btn--primary}
