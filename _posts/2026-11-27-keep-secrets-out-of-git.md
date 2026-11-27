---
title: "Lab: Keep Secrets Out of Git"
date: 2026-11-27
categories:
  - labs
tags:
  - cybershujaa
  - devsecops
  - git
  - secrets-management
  - labex
header:
  og_image: /assets/images/labs/role-based-access-control.png
  teaser: /assets/images/labs/role-based-access-control.png
---

*A credentials file was one `git commit` away from permanent history — caught not by a clever trick, but by checking the staging area before committing, the way any commit should be reviewed.*

**Problem Statement**
In a repository where a credentials file had been staged alongside a legitimate code change by an overly broad `git add`, work through the full control cycle: detect the exposure, remove it from the index without losing the real business change, prevent a repeat, and verify that neither the working tree nor the full commit history contains the secret.

**Approach**
`git status` showed two different kinds of change sitting side by side: a legitimate, unstaged edit to an application file, and a new credentials file already staged and one commit away from permanent history. Comparing `git diff` (unstaged) against `git diff --cached` (staged) made the distinction concrete — one diff was an ordinary business change, the other contained a live-looking API token in plaintext. Running an offline, Gitleaks-style scanner against the file confirmed it: one finding, high entropy, consistent with a real token rather than a placeholder. The fix was `git rm --cached` to pull the file out of the index while leaving it untouched on disk, paired with a narrow, root-anchored `.gitignore` rule for that one file specifically, rather than a broad wildcard pattern that would also hide files that should be tracked. A safe example file with a placeholder value replaced it, documenting the required configuration without supplying a working credential. Before committing, the safe files were staged, re-scanned (clean), and the cached diff reviewed again to confirm no secret was present. After committing, a full-history scan — not just a working-tree scan — confirmed the token had never entered Git history at any point, and a quick run of the application confirmed the real business change still worked.

**Tools Used**
Git (`status`, `diff --cached`, `rm --cached`), an offline Gitleaks-style secret scanner, `.gitignore`

**Key Lessons**
The staging area is the last real checkpoint before a secret becomes permanent — once something is committed, deleting it afterward does not remove it from history, so the only honest response to a committed secret is to treat it as compromised and rotate it. The lab also made the case for layering two different kinds of check rather than trusting either alone: an automated scanner catches patterns a human skims past, while a human review of the exact staged diff catches context a scanner can't reason about. One real mistake happened along the way too — the first attempt at writing the ignore rule was typed at the shell prompt instead of inside the file, leaving `.gitignore` empty, and it only surfaced because the fix was verified with `git status` instead of assumed to have worked. That's the same habit as the rest of the lab: check the actual state, don't assume the command did what you meant.

[Full lab writeup (PDF)](/assets/files/labs/keep-secrets-out-of-git.pdf){: .btn .btn--primary}
