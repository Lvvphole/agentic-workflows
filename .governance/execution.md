# Execution

## Purpose

Define the allowed execution lifecycle for the central workflow catalog.

## Primary pipeline

Use this order for a normal code or workflow change:

1. Receive a pull request or push event.
2. Run deterministic CI.
3. Record deterministic `PASS` or `FAIL`.
4. Block merge when a required check fails.
5. Merge only after required checks pass and merge authority exists.
6. Run deterministic CD after an accepted main-branch state exists.
7. Deploy to staging when the deployment contract permits it.
8. Require production authorization before production promotion.
9. Deploy the exact accepted artifact to production.
10. Run post-deploy deterministic verification.

Do not let an agentic workflow skip a stage in this sequence.

## Agentic roles

### CI Doctor

Trigger only from a deterministic CI failure or explicit manual run.

Read the failed run evidence.

Produce a diagnosis report.

Keep the initial rollout report-only.

### PR Evidence Reviewer

Read the pull request diff and applicable governance.

Report missing evidence, scope violations, or unsupported completion claims.

Do not produce the acceptance result.

### Documentation Drift

Run after an accepted change or explicit review event.

Report documentation that conflicts with accepted behavior.

### Repository Health

Run on a bounded schedule.

Report stale failures, workflow drift, dependency problems, or verification gaps.

### Bounded Repair

Keep this role disabled during the initial rollout.

Enable it only after report-only CI Doctor behavior has a separate acceptance record.

## Review-repair envelope

Use one accepted finding for one repair candidate.

Change one file for one review-repair candidate.

Create one commit for one accepted review-repair candidate.

Keep the repair inside the authorized path set.

Do not add unrelated behavior.

Do not add a new file during review repair.

Do not expand architecture or public surface during review repair.

Do not increase line count when the active repair contract prohibits line growth.

Use at most two repair attempts for one failed gate.

Do not make a third repair attempt.

After the second failed attempt, preserve the candidate and return `BLOCKED`.

Repair exhaustion does not authorize exploration, scope growth, test changes, or a new repair strategy.

## Complete-failure lifecycle

Enter this lifecycle only after an authoritative verifier or explicit human decision declares complete failure.

Stop mutation of the failed pull request.

Do not patch the failed pull request or add another repair attempt to its branch.

Close the failed pull request.

Keep the closed pull request and failed head SHA as frozen evidence.

Record the accepted base SHA, failed head SHA, diff, failed gates, findings, and relevant run evidence.

Convert the failure evidence into successor acceptance criteria and learning corpus.

Do not weaken the predecessor oracle, tests, findings, or failure evidence.

Start the redesign from the last accepted base, not from the failed head.

Create a new branch for the redesign.

Redesign the architecture from the frozen failure evidence and new verified context.

Run required deterministic tests on the materialized successor before publication.

Verify the exact successor candidate before publication.

Record commands, results, candidate identities, and hashes before publication.

Show the verification evidence before publication.

Do not create the successor commit until the required local evidence exists.

After the evidence exists, commit the verified bytes and push that commit.

Open a new pull request only from the verified successor branch.

## Stop conditions

Stop immediately when one of these conditions exists:

- Required authority is missing.
- The required verifier is unavailable.
- Repository state changed after candidate identity was recorded.
- A repair requires scope expansion.
- A protected state transition lacks explicit authority.
- The repair-attempt bound is exhausted.

Preserve the current candidate and its evidence when execution stops.
