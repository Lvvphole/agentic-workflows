# DETERMINISTIC_CI_CD Task Contract

## Purpose

Change deterministic CI, CD, build, test, deployment, security-gate, or acceptance-gate logic.

## Inputs

### Governing

- `.governance/authority.md`
- `.governance/execution.md`
- `.governance/security.md`
- `.governance/testing.md`
- `.governance/verification.md`
- `.governance/evidence.md`
- `.governance/completion.md`
- `.governance/releases.md`

### Reference

- `ARCHITECTURE.md`
- affected pipeline contract
- repository-specific deterministic acceptance requirements

### Working

- current pipeline behavior;
- authorized target behavior;
- affected deterministic tests.

## Engineering Rules

- **Applicability:** Yes
- Resolve the canonical engineering-rules authority through `.governance/authority.md` when the task is code-capable.
- Verify the required identity, read the canonical rules, and satisfy the Pre-Code Readiness Gate before code-capable mutation.
- If the authority is missing or the gate is unsatisfied, return `BLOCKED`.

## Process

1. Confirm the deterministic pipeline contract and affected consumers.
2. Complete Engineering Rules readiness.
3. Change only the authorized deterministic logic.
4. Run behavior-specific pipeline checks and required security checks.
5. Submit exact source and generated artifacts for verification.

## Outputs

- pipeline candidate;
- deterministic gate results;
- generated-artifact identities when applicable;
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
