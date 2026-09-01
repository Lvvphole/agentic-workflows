# MUTATION Task Contract

## Purpose

Perform an authorized repository mutation when no more specific route applies.

## Inputs

### Governing

- `.governance/authority.md`
- `.governance/execution.md`
- `.governance/security.md`
- `.governance/testing.md`
- `.governance/verification.md`
- `.governance/evidence.md`
- `.governance/completion.md`

### Reference

- affected architecture or interface contracts when required by the mutation

### Working

- explicit human task;
- current base and candidate identity;
- affected artifacts.

## Engineering Rules

- **Applicability:** Conditional
- Resolve the canonical engineering-rules authority through `.governance/authority.md` when the task is code-capable.
- Verify the required identity, read the canonical rules, and satisfy the Pre-Code Readiness Gate before code-capable mutation.
- If the authority is missing or the gate is unsatisfied, return `BLOCKED`.

## Process

1. Confirm no more specific route applies.
2. Freeze authorized scope and required evidence.
3. Complete Engineering Rules readiness when code-capable.
4. Perform the smallest sufficient authorized mutation.
5. Run required checks and submit the exact candidate for verification.

## Outputs

- authorized candidate;
- test results;
- verification evidence;
- completion disposition.

## Verifier

Deterministic verifier designated by this contract or its authorized task instance.

## Stop Conditions

- required authority or admitted input is missing;
- scope expansion is required but not authorized;
- the required verifier is unavailable;
- unexpected repository drift occurs;
- a required governance or contract condition returns `BLOCKED`.

The contract may narrow repository governance. It cannot weaken governance or enlarge explicit human authority.
