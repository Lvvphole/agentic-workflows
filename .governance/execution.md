# Execution

## Purpose

Define execution order, mutation discipline, repair bounds, complete-failure behavior, and stop conditions.

## Mutation Lifecycle

For a mutation-capable task:

1. Select the active task contract through `CONTEXT.md`.
2. Confirm task and remote-write authority.
3. Read the governing and reference inputs named by the contract.
4. For code-capable work, satisfy the Engineering Rules route and Pre-Code Readiness Gate.
5. Record the current base and candidate identity before mutation.
6. Perform only the authorized increment.
7. Inspect the actual mutation result.
8. If the mutation was authorized and produced the expected repository change, record the resulting candidate identity before another mutation.
9. Run the deterministic checks required by the active contract and `.governance/testing.md`.
10. Submit the exact candidate and evidence to the verifier selected by the active contract.
11. Preserve evidence and apply `.governance/completion.md`.

Do not skip a required stage.

## Candidate Identity and Drift

An authorized mutation is an expected candidate transition, not repository drift.

After each authorized mutation, inspect the actual result and refresh the candidate identity before any later mutation or verification.

Stop when repository state changes in a way that is not attributable to the immediately preceding authorized mutation or another explicitly authorized concurrent transition.

Unexpected, external, concurrent, or unauthorized drift returns `BLOCKED` until the state is re-established by the applicable authority.

Never reuse verification from the predecessor identity after an authorized mutation.

## Review-Repair Envelope

Use one accepted finding for one repair candidate.

Change one file for one review-repair candidate unless the active contract explicitly establishes a different accepted envelope.

Keep repair inside the authorized path set. Do not add unrelated behavior, architecture, public surface, or new files unless the active contract explicitly authorizes them.

Use at most two repair attempts for one failed gate when the contract does not specify a stricter bound. Do not make a third attempt.

After the repair bound is exhausted, preserve the candidate and return the required terminal state. Exhaustion does not authorize exploration, scope growth, test changes, or a new repair strategy.

## Complete-Failure Lifecycle

Enter this lifecycle only when the acceptance authority selected by the active contract, or an explicit human decision, declares complete failure.

A complete-failure determination supplies a failure state. It does not grant remote-write authority.

On complete failure:

1. Stop mutation and fix-forward on the failed candidate immediately.
2. Freeze the failed base, candidate identity, diff, failed gates, findings, and relevant run evidence.
3. Preserve the failure as immutable successor acceptance criteria and learning evidence.
4. If closing the failed pull request is required but not already authorized, return `BLOCKED` before the remote write and request human authority.
5. When closing the pull request is explicitly authorized, close it and record the resulting remote state as evidence.
6. Start successor redesign from the last accepted base, not from the failed head.
7. Do not create, push, or publish a successor branch or pull request without explicit authority for those remote mutations.
8. Materialize the successor before publication.
9. Run the required deterministic checks and verifier against the exact successor candidate.
10. Record commands, results, identities, and hashes before publication.
11. Commit or push only the exact verified successor bytes when those actions are separately authorized.

The predecessor remains `FAIL` even when its evidence improves a successor.

## Stop Conditions

Stop immediately when any required condition exists:

- required human or contract authority is missing;
- the required verifier is unavailable;
- required evidence or an admitted input is unavailable;
- the canonical engineering-rules authority is required but unavailable or mismatched;
- unexpected repository drift occurs;
- the next action requires scope expansion not authorized by the active contract;
- a remote or protected transition lacks required authority;
- a repair-attempt bound is exhausted;
- governance or the active contract requires `STOP`, `BLOCKED`, `REDUCE`, or `REDESIGN`;
- new evidence invalidates the active frozen task or construction contract.

Preserve the current candidate and admissible evidence when execution stops. Do not fix-forward through a stop condition.
