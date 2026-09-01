# RELEASE_CONSUMER Task Contract

## Purpose

Publish an accepted catalog version or update a consuming repository to an accepted version.

## Inputs

### Governing

- `.governance/authority.md`
- `.governance/security.md`
- `.governance/testing.md`
- `.governance/verification.md`
- `.governance/evidence.md`
- `.governance/releases.md`
- `.governance/completion.md`

### Reference

- release candidate or consumer acceptance contract
- affected immutable version identities

### Working

- accepted catalog candidate or proposed consumer update;
- required local consumer checks.

## Engineering Rules

- **Applicability:** Conditional — required when release preparation changes code-capable artifacts.
- Resolve the canonical engineering-rules authority through `.governance/authority.md` when the task is code-capable.
- Verify the required identity, read the canonical rules, and satisfy the Pre-Code Readiness Gate before code-capable mutation.
- If the authority is missing or the gate is unsatisfied, return `BLOCKED`.

## Process

1. Confirm explicit authority for each remote or protected release transition.
2. Run catalog and consumer checks required by the active release contract.
3. Verify the exact immutable candidate.
4. Publish or adopt only when separately authorized and verification requirements are satisfied.
5. Preserve release and consumer evidence.

## Outputs

- release or consumer candidate;
- catalog and consumer verification evidence;
- authorized transition record when performed.

## Verifier

Deterministic verifier designated by this contract or its authorized task instance.

## Stop Conditions

- required authority or admitted input is missing;
- scope expansion is required but not authorized;
- the required verifier is unavailable;
- unexpected repository drift occurs;
- a required governance or contract condition returns `BLOCKED`.

The contract may narrow repository governance. It cannot weaken governance or enlarge explicit human authority.
