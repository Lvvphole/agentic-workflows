# Evidence

## Purpose

Define how repository and workflow evidence is classified, recorded, and bound to the exact candidate.

## Evidence Record

Record fields that apply to the active contract, including:

- repository or candidate source;
- actor and trigger;
- active task contract identity;
- base identity;
- candidate identity;
- changed path set;
- commit SHA when one exists;
- deterministic check identities and results;
- verifier identity and result;
- generated-artifact hashes when applicable;
- remote action and authorization evidence when applicable;
- terminal status;
- immutable run or artifact reference when available.

## Provenance

Keep evidence tied to the exact candidate identity.

Do not copy a `PASS` result from one candidate to another.

Do not replace missing evidence with model recollection or inference.

A mutation after verification creates a new candidate identity and requires fresh verification.

## Proposal and Result Provenance

Treat an accepted proposal and an execution result as different evidence objects when consequential tool actions are in scope.

Bind the accepted proposal to its tool identity, canonical input, active contract, candidate identity, and authorization decision when those fields apply.

Inspect the actual execution result before any dependent action.

A result with missing or mismatched proposal, tool, input, contract, candidate, or authorization binding is inadmissible and returns `BLOCKED` when the active contract requires that provenance.

## Evidence Classes

Use `VERIFIED`, `OBSERVED`, and `INFERRED` as defined by `.governance/authority.md`.

A tool result is `OBSERVED` until the applicable acceptance authority promotes the relevant fact within its jurisdiction.

Evidence records do not promote themselves to `VERIFIED`.

## Repair and Complete Failure

For a repair candidate, record predecessor and successor identities.

For complete failure, preserve the failed pull-request state, failed head identity, failed gates, findings, and accepted base.

If the failed pull request is closed under explicit authority, record the closed state as additional evidence. Closure is not required to preserve the failure identity when remote-write authority is temporarily unavailable.

Do not rewrite frozen failure evidence after successor work starts.
