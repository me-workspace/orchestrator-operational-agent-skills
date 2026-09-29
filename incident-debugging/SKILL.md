---
name: incident-debugging
description: Use this skill whenever something is broken and the cause is unknown - "error di production", "kenapa gagal", "user komplain", "service down", "bug aneh", stack traces, 500s, timeouts, wrong data. Drives a disciplined evidence-first diagnosis instead of guess-and-patch. Do NOT use for planned code review or deploys.
---

# Incident Debugging

Rule zero: **reproduce or trace before you touch anything.** A fix without a confirmed root cause is a new bug with better marketing.

## 1. Stabilize (only if actively bleeding)
If users are losing money/data right now: mitigate first (rollback last deploy, disable the feature flag, restart the crashed service) and say explicitly that this is mitigation, not the fix.

## 2. Gather evidence - in this order
1. **Exact symptom**: error text, status code, screenshot, affected user/id, first-seen time.
2. **What changed?** Deploys, config edits, cron runs, dependency/API changes near first-seen time. Most incidents are caused by the most recent change.
3. **Logs around the failure**: app log, web server log, `journalctl -u <svc> --since`, DB slow log. Grep for the request id / user id, not just the error string.
4. **Scope**: one user or all? One endpoint or everything? Constant or intermittent? Intermittent → suspect race, resource exhaustion, or an external dependency.

## 3. Hypothesize and test
- Write the top 2-3 hypotheses ranked by evidence. For each: what observation would confirm/refute it?
- Test the cheapest discriminating check first (read a log, run one query, curl one endpoint) - not the most invasive.
- Change **one variable at a time**. If you must experiment on production state, back up what you touch first.
- Beware pattern-matching: a familiar-looking symptom can have a different cause. Confirm on THIS system's evidence.

## 4. Fix
- Fix the root cause, minimally. Resist drive-by refactors in an incident patch.
- Check for the same bug class elsewhere (grep for the same pattern).
- Verify the fix against the original reproduction, then run the normal post-deploy smoke test.

## 5. Close out
Short write-up: symptom → root cause → fix → verification → prevention (test added? monitor added? checklist updated?). If a prevention item is skipped, list it as open debt, don't let it evaporate.
