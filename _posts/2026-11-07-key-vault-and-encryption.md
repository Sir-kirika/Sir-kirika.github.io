---
title: "Lab: Key Vault and Encryption — Azure Privilege Escalation Chain"
date: 2026-11-07
categories:
  - labs
tags:
  - cybershujaa
  - azure
  - key-vault
  - rbac
  - pwned-labs

header:
  og_image: /assets/images/labs/key-vault-and-encryption.png
  teaser: /assets/images/labs/key-vault-and-encryption.png

---

*Continuing from a compromised low-privilege Azure account, through a Key Vault storing plaintext contractor credentials, to read access on a table full of unencrypted payment data.*

**Problem Statement**
Starting from credentials for a low-privileged Azure AD identity obtained in a prior lab, establish authenticated access, enumerate identity and resource data, identify any excessive or misconfigured permissions, and determine whether the compromised account (or anything found along the way) can reach sensitive customer data.

**Approach**
Authenticated against the tenant with the Azure CLI, Azure PowerShell, and the Microsoft Graph PowerShell SDK, each of which keeps its own separate token. A planned MFA bypass via a deliberately compromised external authentication method didn't surface in the sign-in UI as expected, so that path was documented as blocked rather than forced. Basic identity enumeration (`az ad signed-in-user show`) was still enough to confirm the account and its group memberships, one of which granted broad directory-read access and explained why further enumeration was even possible from a standard user account. Resource enumeration turned up exactly one visible resource: a Key Vault named after external contractors. Listing its contents revealed several secrets, each named after a person, and retrieving them returned plaintext username/password pairs — meaning the vault's own naming convention identified the next identity to pivot to before the credential itself was even read. Switching sessions to that contractor account (bypassing MFA this time via the compromised provider, successfully) revealed its own group memberships, one of which mapped to a custom RBAC role granting direct read access to a specific storage table. Querying that table returned customer records containing full unencrypted payment card data.

**Tools Used**
Azure CLI, Azure PowerShell (Az), Microsoft Graph PowerShell SDK, WireGuard

**Findings**
No single misconfiguration caused this. It was the combination: a Key Vault storing plaintext credentials readable by a low-privileged account with only basic reader roles, a contractor account left active with standing privileged access after its engagement presumably ended, a custom RBAC role granting direct data-plane read access to a storage table, unencrypted payment card data at rest in that table, and a compromised external authentication provider silently bypassing MFA at every step along the chain.

**Key Lessons**
Reading a Key Vault's contents is only half the lesson — the vault's secret *names* did most of the targeting work before any value was retrieved, since naming secrets after people is effectively documenting the privilege escalation path for anyone who gets read access. RBAC policies are also not a substitute for encryption: a custom role scoped only to one table still exposed full card numbers and CVVs in plaintext, meaning the access control worked exactly as configured while the underlying data protection simply didn't exist. The clearest takeaway is that MFA, Key Vault permissions, stale contractor accounts, and encryption-at-rest are four independent controls — and this chain worked because all four had a gap at the same time, not because any one of them was catastrophically broken.

[Full lab writeup (PDF)](/assets/files/labs/key-vault-and-encryption.pdf){: .btn .btn--primary}
