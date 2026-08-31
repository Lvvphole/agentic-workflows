# Execution

## Purpose

Define the allowed execution lifecycle for the central workflow catalog.

## Primary pipeline

Use this order for a normal code or workflow change:

1. Receive a pull request or push event.
2. Run deterministic CI.
3. Record deterministic PASS or FAIL.
4. Block merge when a required check fails.
5. Merge only after the required checks pass and merge authority exists.
6. Run deterministic CD after the accepted main-branch state exists.
7. Deploy to staging when the deployment contract permits it.
8. Require production authorization before production promotion.
9. Deploy the exact accepted artifact to production.
10. Run post-deploy deterministic verification.

Do not let an agentic workflow skip a stage in this sequence.

## Agentic roles

### CI Doctor

Trigger only from a deterministic CI failure or an explicit manual run.

Read the failed run evidence.

Produce a diagnosis report.

The initial rollout is report-only.

### PR Evidence Reviewer

Read the pull request diff and applicable governance.

Report missing evidence, scope violations, or unsupported completion claims.

Do not produce the acceptance result.

### Documentation Drift

Run after an accepted change or on an explicit review event.

Report documentation that is inconsistent with the accepted behavior.

### Repository Health

Run on a bounded schedule.

Report stale failures, workflow drift, dependency problems, or verification gaps.

### Bounded Repair

Keep this role disabled during the initial rollout.

Enable it only after report-only CI Doctor behavior has a separate acceptance record.

When enabled, allow one bounded repair candidate per trigger unless the active contract defines a smaller limit.

## Repair envelope

A repair must stay inside the path set that the active task authorizes.

A repair must not add unrelated behavior.

A repair must not add a new file unless the active contract requires that file.

A repair must not increase line count when the active repair contract prohibits line growth.

Use at most two repair attempts for one failed gate unless a smaller bound applies.

After the bound is exhausted, stop and return `BLOCKED`.

## Stop conditions

Stop immediately when one of these conditions exists:

- Required authority is missing.
- The required verifier is unavailable.
- Repository state changed after the candidate identity was recorded.
- A repair would require scope expansion.
- A protected state transition lacks explicit authority.
- The repair-attempt bound is exhausted.

Preserve the current candidate and its evidence when execution stops.
