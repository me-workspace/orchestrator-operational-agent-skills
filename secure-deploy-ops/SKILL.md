---
name: secure-deploy-ops
description: Use this skill whenever deploying, updating, restarting, or configuring anything on a production server/VPS — "deploy", "naikkan ke server", "restart service", "update nginx/env/config", "rollback", or post-deploy verification. Also for server hardening checks (SSH, firewall, backups). Do NOT use for local development or code review (use code-review-hardening).
---

# Secure Deploy & Server Ops

Production first rule: **you can only deploy what you can roll back.** Never skip the backup and the diff.

## Pre-deploy checklist (all mandatory)
1. **Backup the exact files/DB you will touch** to a timestamped dir (e.g. `_predeploy_bak/YYYYMMDD-HHMMSS-<slug>/`). For DB changes: dump first.
2. **Diff live vs staged** before overwriting: `diff --strip-trailing-cr <live> <staged>`. Production may carry fixes that never landed in git — an unstaged diff means STOP and reconcile, or you will silently revert a production fix.
3. **Scan what you ship**: no secrets, no `.env`, no debug flags, no hardcoded IPs.
4. **Know the rollback command** and write it down in the plan before executing.

## Deploy
- Prefer atomic swaps (extract to staging dir → swap symlink/dir → reload) over in-place edits.
- One change per deploy. Batch changes multiply blame-surface when something breaks.
- Config edits: validate before reload (`nginx -t`, `systemd-analyze verify`, app config check).

## Post-deploy verification (never declare done without this)
1. Service up: `systemctl status <svc>` / process alive.
2. Smoke test the real path: hit the actual endpoint/page a user hits, not just `/health`.
3. Tail logs for 1–2 minutes for new errors.
4. If a payment/webhook/auth flow was touched, execute one real (or sandbox) transaction.

Report honestly: what was deployed, verification output, anything skipped.

## Rollback triggers
Roll back immediately (don't debug live) when: error rate spikes, auth/payment breaks, or data writes look wrong. Restore from the pre-deploy backup, verify, then debug offline.

## Hardening baseline (when asked to audit a server)
- SSH: key-only auth (`PasswordAuthentication no`), no root login, fail2ban.
- Firewall: default-deny inbound; only 22/80/443 + explicitly needed ports; internal services bind 127.0.0.1.
- Secrets: in env files mode 600, owned by the service user; never in repo or logs.
- Backups: automated, **off-box**, restore actually tested. A backup never restored is a hope, not a backup.
- Updates: unattended security updates on; note kernel reboots needed.
- Least privilege: services run as non-root users; systemd sandboxing (`ProtectSystem`, `ReadWritePaths`) where possible.
