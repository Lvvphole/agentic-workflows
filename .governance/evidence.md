# Evidence

## Purpose

Define the evidence that each workflow run and repository change must preserve.

## Evidence record

Record these fields when they apply:

- Repository name.
- Trigger event.
- Actor.
- Base identity.
- Candidate identity.
- Commit SHA when a commit exists.
- Pull request number.
- Workflow source path and SHA-256.
- Compiled lock-file path and SHA-256.
- `gh aw` version.
- Deterministic commands or required checks.
- Deterministic result for each required check.
- Agentic workflow version and model or engine identifier when available.
- Safe output type and target when a safe output is proposed or applied.
- Final status: `PASS`, `FAIL`, or `BLOCKED`.
- Run URL or immutable artifact reference.

## Provenance

Keep generated evidence tied to the exact candidate identity.

Do not copy a `PASS` result from an earlier candidate to a later candidate.

Do not replace missing evidence with model recollection.

## Proposal and result provenance

Treat an accepted proposal and an execution result as different evidence objects.

Before a consequential tool action, record the accepted proposal.

Bind the proposal to these fields when they apply:

- Session identity.
- Tool-use identity.
- Tool identity.
- Canonical tool-input digest.
- Contract identifier and contract digest.
- Base and candidate identity.
- Authorization decision.
- Proposal digest.

After execution, retrieve the exact accepted proposal before using the result.

A result without an existing accepted proposal is inadmissible.

A mismatched tool, input, contract, proposal, or candidate binding is inadmissible.

Missing or mismatched provenance returns `BLOCKED`.

Do not record provenance failure while allowing successful continuation.

Post-action evidence inherits its contract identity from the accepted proposal.

Do not rebind a result to a different active contract after execution.

## Evidence classes

Label material facts as `VERIFIED`, `OBSERVED`, or `INFERRED` when the distinction affects a state transition.

A completion claim must identify the `VERIFIED` evidence that supports it.

A tool result is `OBSERVED` until the applicable verifier accepts it.

## Repair and failure evidence

When an agent creates a repair candidate, record predecessor and successor candidate identities.

A successor needs fresh verification.

For complete failure, preserve the closed pull request and failed head SHA as learning evidence.

Record the failed gates and findings that become successor acceptance criteria.

Do not rewrite frozen failure evidence after the successor work starts.
