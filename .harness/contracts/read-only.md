# READ_ONLY Task Contract

## Purpose

Inspect, diagnose, explain, review, or gather evidence without repository mutation.

## Inputs

### Governing

- `.governance/authority.md`
- `.governance/evidence.md`
- `.governance/completion.md`

### Reference

- Only repository artifacts required by the explicit question.

### Working

- Current repository observations and supplied evidence.

## Engineering Rules

- **Applicability:** No
- This contract authorizes no code-capable mutation.

## Process

1. Confirm the task is non-mutating.
2. Read only admitted inputs.
3. Classify claims as `OBSERVED`, `INFERRED`, or `VERIFIED` when material.
4. Report findings without repository mutation.

## Outputs

- read-only findings;
- evidence references;
- next admissible action when one is established.

## Verifier

Use a verifier explicitly designated by the read-only task when one exists.

Otherwise, the explicit human requester is the acceptance authority for the exact read-only output. Task issuance, silence, or tool access does not imply acceptance.

While required human acceptance is pending, report `BLOCKED` because required verification is unavailable. After explicit human acceptance of the exact output, `PASS` may be recorded. Explicit human rejection or a rejecting designated verifier yields `FAIL` when `.governance/completion.md` applies.

## Stop Conditions

- required authority or admitted input is missing;
- scope expansion is required but not authorized;
- the required verifier is unavailable;
- unexpected repository drift occurs;
- a required governance or contract condition returns `BLOCKED`.

The contract may narrow repository governance. It cannot weaken governance or enlarge explicit human authority.
