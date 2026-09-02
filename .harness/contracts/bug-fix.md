# BUG_FIX Task Contract

## Purpose

Repair a verified defect in existing observable behavior.

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

- affected behavioral contract
- relevant architecture or interface contract

### Working

- verified defect evidence;
- faulty baseline identity;
- required regression behavior.

## Engineering Rules

- **Applicability:** Yes
- Resolve the canonical engineering-rules authority through `.governance/authority.md` when the task is code-capable.
- Verify the required identity, read the canonical rules, and satisfy the Pre-Code Readiness Gate before code-capable mutation.
- If the authority is missing or the gate is unsatisfied, return `BLOCKED`.

## Process

1. Confirm the defect is reproducible or otherwise `VERIFIED` by the designated authority.
2. Freeze the required observable behavior without freezing an unproven root cause.
3. Complete Engineering Rules readiness.
4. Make the smallest repair inside authorized scope.
5. Run the required regression evidence and affected deterministic checks.
6. Submit the exact repaired candidate for verification.

## Outputs

- repaired candidate;
- baseline-versus-successor regression evidence;
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
