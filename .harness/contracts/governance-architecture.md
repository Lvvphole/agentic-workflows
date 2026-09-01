# GOVERNANCE_ARCHITECTURE Task Contract

## Purpose

Change an accepted governance structure, routing responsibility, authority boundary, or control-plane architecture.

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
- affected governing sources
- accepted architecture evidence

### Working

- authorized architecture change;
- affected contract and routing graph.

## Engineering Rules

- **Applicability:** Conditional — required when code-capable artifacts are in scope.
- Resolve the canonical engineering-rules authority through `.governance/authority.md` when the task is code-capable.
- Verify the required identity, read the canonical rules, and satisfy the Pre-Code Readiness Gate before code-capable mutation.
- If the authority is missing or the gate is unsatisfied, return `BLOCKED`.

## Process

1. Confirm explicit authority for the architecture change.
2. Record alternatives and trade-offs for consequential choices.
3. Make the smallest sufficient architecture change.
4. Run affected routing, contract, and governance checks.
5. Submit the exact candidate for verification.

## Outputs

- updated architecture/governance candidate;
- affected contract evidence;
- verification evidence.

## Verifier

Deterministic verifier designated by this contract or its authorized task instance.

## Stop Conditions

- required authority or admitted input is missing;
- scope expansion is required but not authorized;
- the required verifier is unavailable;
- unexpected repository drift occurs;
- a required governance or contract condition returns `BLOCKED`.

The contract may narrow repository governance. It cannot weaken governance or enlarge explicit human authority.
