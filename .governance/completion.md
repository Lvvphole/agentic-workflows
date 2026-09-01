# Completion

## Purpose

Define terminal states and the conditions under which an active task may be called done.

## PASS

Use `PASS` only when the verifier selected by the active task contract accepts all required evidence for the exact final candidate and no completion condition is missing.

A `PASS` record must identify the exact candidate and verifier evidence.

The proposer does not self-certify `PASS`.

## FAIL

Use `FAIL` when a required acceptance authority or deterministic gate runs and rejects the exact candidate under the active contract.

Preserve the failing evidence.

A complete-failure predecessor remains `FAIL` even when its evidence becomes successor acceptance criteria.

## BLOCKED

Use `BLOCKED` when required authority, contract state, admitted input, engineering-rules readiness, repository state, testing, evidence, or verification is unavailable or invalid.

`BLOCKED` is not `PASS`.

## Candidate Produced

A produced file, patch, workflow, review, repair, or materialized governance tree is a candidate.

A candidate is not accepted merely because it exists, was committed, was pushed, compiled, passed local tests, or received a model review.

## Completion Conditions

Do not report completion until:

- the active task contract is identified and valid;
- authorized scope is unchanged or an authorized scope change is recorded;
- required Engineering Rules readiness was satisfied before code-capable mutation;
- required deterministic checks ran on the exact final candidate;
- required generated artifacts are synchronized with source;
- the required verifier evaluated the exact final candidate;
- no required gate or verifier state is `FAIL` or `BLOCKED` for a claimed `PASS`;
- required evidence is preserved and bound to the final candidate;
- no remote or protected state transition occurred without required authority.

Any mutation after verification invalidates that verification and prevents completion until the new exact candidate is re-verified.

When any condition is unsatisfied, report the actual terminal state and the missing condition.
