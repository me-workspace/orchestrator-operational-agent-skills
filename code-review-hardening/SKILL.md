---
name: code-review-hardening
description: Use this skill whenever asked to review code — a diff, PR, branch, file, or "cek kode ini" — for bugs, security issues, or quality. Triggers include "review", "audit kode", "ada bug?", "aman gak?", "sebelum merge", or any request to assess code before deploy. Covers correctness, security (OWASP-style), performance, and maintainability. Do NOT use for writing new features or for infra/server audits (use secure-deploy-ops for deploy checks).
---

# Code Review & Hardening

Review in two passes, verify before reporting, rank by severity. Never pad the report with style nits when real defects exist.

## Pass 1 — Correctness
For each changed function/path, ask:
1. **Inputs**: what happens on empty, null, zero, negative, huge, unicode, duplicate input?
2. **State**: race conditions, re-entrancy, idempotency (retries, double-submit, webhook replays)?
3. **Errors**: are failures swallowed? Does a partial failure leave inconsistent state (DB written, external call failed)?
4. **Boundaries**: off-by-one, timezone/locale, float money math, pagination edges.
5. **Contracts**: does the change break callers? Grep for all call sites before claiming safe.

## Pass 2 — Security
Check in this order (most common real-world first):
1. **Injection**: SQL (string-built queries), command (`exec`/`spawn` with user input), path traversal (`../`), template injection.
2. **AuthN/AuthZ**: every new endpoint — who can call it? IDOR (object id from user without ownership check). Admin-only actions gated server-side, not just in UI.
3. **Secrets**: keys/tokens hardcoded, logged, or committed. `.env` in repo.
4. **Payment/webhook**: signature verification, amount taken from server not client, replay protection.
5. **Data exposure**: verbose errors to client, PII in logs, mass-assignment.
6. **Dependencies**: new packages — typosquatting, unmaintained, install scripts.

## Verify before reporting
A finding is only reportable if you can state a **concrete failure scenario**: input/state → wrong output/exploit. Trace the actual code path; if you cannot construct the scenario, mark it "perlu konfirmasi" or drop it. False positives destroy trust in the review.

## Report format
```
## Temuan (urut severity)
1. [CRITICAL|HIGH|MEDIUM|LOW] file:line — satu kalimat defect.
   Skenario gagal: <input/state konkret → akibat>.
   Saran fix: <minimal, spesifik>.
```
- CRITICAL: exploitable remotely / data loss / money movement.
- HIGH: wrong results or exploit needing some preconditions.
- MEDIUM: robustness gap likely hit eventually.
- LOW: maintainability/perf polish.

End with a one-line verdict: **layak merge / merge dengan syarat / jangan merge**. If zero findings survive verification, say so plainly — do not invent findings.
