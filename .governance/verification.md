# Verification

## Purpose

Define what evidence establishes correctness for the exact candidate and which verifier may decide acceptance.

## Acceptance Invariant

The verifier selected by the active task contract decides whether required evidence establishes `PASS` or `FAIL` within its jurisdiction.

The proposer, executor, coding agent, or agentic workflow does not decide acceptance of its own output.

Testing results are inputs to verification. Testing is not verification.

## Candidate Identity

Bind every verification result to the exact candidate.

Record at least:

- repository or materialized candidate identity;
- base identity;
- candidate digest or commit SHA;
- changed path set;
- required generated-artifact identities when applicable;
- verifier identity, version, or command;
- required test/check identities and results.

Any mutation after verification invalidates that verification for the new candidate.

## Oracle Requirements

A verifier must use the oracle or acceptance predicates designated by the active contract.

The oracle must be capable of rejecting a candidate that violates the target contract.

Do not substitute model confidence, coverage percentage, compilation alone, lexical matching alone, or an unrelated passing check for the required oracle.

Return `BLOCKED` when the required trusted verifier or semantic comparator is unavailable.

## Governance Bootstrap Cases

A governance-bootstrap verifier must be able to reject at least these conditions when applicable:

1. a route references a missing task contract;
2. `AGENTS.md` performs task classification instead of routing to `CONTEXT.md`;
3. a code-capable route can mutate before Engineering Rules readiness;
4. testing success directly becomes completion `PASS` without verification;
5. evidence changes candidate identity or rebinds a result to another candidate;
6. a verifier result manufactures human or remote-write authority;
7. an authorized mutation is treated as unexpected repository drift;
8. unexpected or concurrent drift is allowed to continue;
9. a stale verification result accepts a changed candidate;
10. `CLAUDE.md` contains independent governance instead of only `@AGENTS.md`.

Preserve valid predecessor acceptance cases unless an authoritative requirement proves them wrong.

## Agentic Workflow Verification

For a new or changed agentic workflow, verify both the source contract and the compiled execution contract when compilation applies.

Do not accept an agentic workflow only because it compiles.

## Independent Verification Unavailable

When required independent verification is unavailable:

- return `BLOCKED`;
- preserve the candidate;
- report that a candidate exists but is not accepted;
- use a deterministic local gate as acceptance authority only when the active contract explicitly designates it;
- require human authorization before substituting a different verifier.
