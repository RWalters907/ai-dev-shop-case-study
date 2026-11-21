# Verification Summary

Ryan Walters · November 2026

## Test Method

I tested the committed work-order lock and a local hardening candidate in disposable Git worktrees. The test harness used synthetic assignments and started competing processes together. The test environment used Git 2.56.1, Bash 5.2.37, and Python 3.12.14 on Linux.

## Observed Results

| Verification Test | Observed Result |
| --- | --- |
| Committed Lock | Exactly one session acquired the lock in each of 10 rounds. Each round had 20 competing claims. |
| Local Hardening Candidate | Exactly one session acquired the lock in each of 25 rounds. Each round had 20 competing claims. |
| Ownership Handoffs | The successor retained its lock in all 30 handoffs. Each handoff tested eight competing release attempts and a stale release after the successor had acquired its lock. |
| Compatibility And Recovery | The candidate released a prior-format lock. It retained the lock after owner exit. Separate worktrees could hold the same work-order key independently. |
| Diagnostic Privacy | Status, contention, and failed-release diagnostics omitted the ownership token. New locks used owner-only permissions. |

## Evidence Limits

The results cover cooperating sessions in the tested local worktrees. The hardening candidate was tested locally. Production recurrence, cost savings, and cross-machine coordination remain unmeasured.
