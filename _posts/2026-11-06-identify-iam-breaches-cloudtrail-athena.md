---
title: "Lab: Identifying IAM Breaches with CloudTrail and Athena"
date: 2026-11-06
categories:
  - labs
tags:
  - cybershujaa
  - aws
  - cloudtrail
  - athena
  - incident-response
header:
  og_image: /assets/images/labs/identify-iam-breaches-cloudtrail-athena.png
  teaser: /assets/images/labs/identify-iam-breaches-cloudtrail-athena.png
---

*Querying CloudTrail logs with SQL — through both the AWS Console and the CLI — to confirm a brute-force attack, size it, and identify which accounts were compromised.*

**Problem Statement**
Following reports that internal credentials had leaked publicly, investigate whether a company's AWS environment was targeted: confirm whether a brute-force attack took place, measure its scale, identify the attacker's source IP and tooling, and determine which IAM accounts were actually compromised.

**Approach**
Worked the same investigation two ways. First through the AWS Console's Athena query editor, which runs SQL directly against CloudTrail logs stored in S3: queried `ConsoleLogin` events for a successful response on the suspected attack date, which returned two hits — a successful root login and a successful login by one specific IAM user, since a brute-force attack generates mostly failures and successful logins are what actually matter. Counting all login events on that date sized the attack at over 1,700 attempts, with all but two failing. Extracting the distinct source IP and user-agent pairs showed every attempt came from a single IP using two different user agents — one consistent with an automated Go-based login-spraying tool, the other a real browser string suggesting the same attacker also logged in manually. Repeated the identical investigation through the AWS CLI: connected over WireGuard, submitted the Athena query with `start-query-execution` (which returns an async query ID rather than results), retrieved the results with `get-query-results`, and parsed the plaintext export with `awk` to confirm the same compromised user and source IP. A final query excluding the attack date and grep'ing the results for anomalous patterns surfaced a user agent that was itself an MD5-format string on a different day — a strong signal of custom or modified attacker tooling worth following up separately.

**Tools Used**
AWS Console (Athena query editor), AWS CLI, WireGuard, `awk`, `grep`

**Key Lessons**
The clearest signal in the whole investigation wasn't the volume of failed logins, it was the handful of successes — a brute-force attack is only dangerous where it actually lands, and CloudTrail plus Athena makes that trivial to isolate with one filtered query. Running the exact same analysis through both the Console and the CLI and getting identical results was also the point: a SOC needs repeatable queries that don't depend on a human clicking through a UI, since the CLI version is what actually gets automated into ongoing monitoring. An unusual user agent on a day outside the known attack window was the most interesting finding of the whole exercise — it's a reminder that attacker activity doesn't always announce itself inside the obvious time window, and an investigation should check adjacent dates, not just the one that triggered the alert.

[Full lab writeup (PDF)](/assets/files/labs/identify-iam-breaches-cloudtrail-athena.pdf){: .btn .btn--primary}
