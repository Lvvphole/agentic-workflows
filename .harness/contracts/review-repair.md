# REVIEW_REPAIR Task Contract

## Purpose

Address one accepted review finding within a bounded repair envelope.

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

- affected implementation or contract context

### Working

- exact accepted review finding;
- reviewed predecessor identity;
- authorized repair envelope.

## Engineering Rules

- **Applicability:** Yes
- Resolve the canonical engineering-rules authority through `.governance/authority.md` when the task is code-capable.
- Verify the required identity, read the canonical rules, and satisfy the Pre-Code Readiness Gate before code-capable mutation.
- If the authority is missing or the gate is unsatisfied, return `BLOCKED`.

## Process

1. Confirm the finding is accepted by the task authority or active review contract.
2. Freeze one finding as the repair target.
3. Complete Engineering Rules readiness.
4. Perform only the bounded repair.
5. Run the finding-specific check and required regression checks.
6. Stop when the repair bound is exhausted or another stop condition fires.

## Outputs

- one repair candidate;
- finding-specific check result;
- verification evidence or terminal `BLOCKED`.

## Verifier

Deterministic verifier designated by this contract or its authorized task instance.

## Stop Conditions

- required authority or admitted input is missing;
- scope expansion is required but not authorized;
- the required verifier is unavailable;
- unexpected repository drift occurs;
- a required governance or contract condition returns `BLOCKED`.

The contract may narrow repository governance. It cannot weaken governance or enlarge explicit human authority.
