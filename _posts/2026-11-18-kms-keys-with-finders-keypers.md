---
title: "Lab: Auditing the Blast Radius of KMS Keys with Finders Keypers"
date: 2026-11-18
categories:
  - labs
tags:
  - cybershujaa
  - aws
  - kms
  - encryption
  - auditing
---

*AWS has no built-in command that lists every resource a KMS key encrypts — so when a key is shared across services, finding its full "blast radius" before touching it takes dedicated tooling.*

**Problem Statement**
Acting as a cloud security engineer documenting encryption key usage for audit purposes: find every resource encrypted by a specific customer-managed KMS key, save the results as a reusable inventory, and assess what would actually happen to those resources if the key were disabled, rotated, or replaced.

**Approach**
Cloned Finders Keypers (an open-source Python CLI from Fog Security) and set it up in an isolated virtual environment so its dependencies stayed contained. Configured a dedicated, read-only-scoped AWS CLI profile for the audit, since the tool only needs read access and an audit identity should never carry write permissions. Resolved the target key's friendly alias to its full ARN first — Finders Keypers requires the ARN specifically, because an alias is just a pointer that can be silently repointed to a different key later. Running the tool against that ARN returned three resources sharing the one key: an S3 bucket, a DynamoDB table, and a Secrets Manager secret. Several service modules in the scan errored out, consistent with the audit identity's deliberately limited read permissions rather than a tool failure. Re-running in verbose mode added structured metadata for each finding (service, resource type, and usage context), and redirecting that output to a file produced a saved, comparable inventory rather than a one-off terminal scan.

**Tools Used**
Finders Keypers, Python virtual environments, AWS CLI, `boto3`

**Key Lessons**
The core problem this lab solves is a real gap in AWS itself: there's no native way to ask "what does this key protect?" A key's blast radius has to be discovered, not assumed, and assuming it is exactly how a routine key rotation turns into an unplanned multi-service outage. The three lifecycle options aren't equally risky: automatic rotation keeps the same key ARN and retains old key material for existing data, making it the lowest-risk change; disabling a key is reversible but causes an immediate outage across everything it protects; and scheduling deletion is fine right up until the waiting period ends, at which point it is permanent and unrecoverable. Moving resources to a different key is the option nobody can automate away, since each resource has to be individually reconfigured and its data re-encrypted while the old key stays enabled in the meantime. The practical habit this lab teaches: run a blast-radius scan before any key change, keep the inventory as evidence, and run it again afterward to confirm nothing was missed.

[Full lab writeup (PDF)](/assets/files/labs/kms-keys-with-finders-keypers.pdf){: .btn .btn--primary}
