# COMPLETE_FAILURE Task Contract

## Purpose

Process a complete failure without fix-forward and convert frozen failure evidence into successor acceptance criteria.

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

- `ARCHITECTURE.md`
- failed task contract
- accepted predecessor architecture

### Working

- complete-failure determination;
- failed base and head identity;
- failed gates and findings;
- accepted base identity.

## Engineering Rules

- **Applicability:** Conditional — required for code-capable successor construction.
- Resolve the canonical engineering-rules authority through `.governance/authority.md` when the task is code-capable.
- Verify the required identity, read the canonical rules, and satisfy the Pre-Code Readiness Gate before code-capable mutation.
- If the authority is missing or the gate is unsatisfied, return `BLOCKED`.

## Process

1. Confirm complete failure was declared by the active acceptance authority or explicit human decision.
2. Stop mutation of the failed candidate.
3. Freeze failure evidence before successor construction.
4. Require explicit human authority before any remote close, branch, push, or pull-request transition.
5. Redesign from the last accepted base and frozen evidence.
6. Complete Engineering Rules readiness before any code-capable successor construction.
7. Verify the exact successor before any separately authorized publication.

## Outputs

- immutable failure corpus;
- successor acceptance criteria;
- successor candidate when authorized;
- fresh successor verification evidence.

## Verifier

The verifier designated by the successor task contract. The failed predecessor remains `FAIL` and cannot be retroactively accepted.

## Stop Conditions

- required authority or admitted input is missing;
- scope expansion is required but not authorized;
- the required verifier is unavailable;
- unexpected repository drift occurs;
- a required governance or contract condition returns `BLOCKED`.

The contract may narrow repository governance. It cannot weaken governance or enlarge explicit human authority.
