# READ_ONLY Task Contract

## Purpose

Inspect, diagnose, explain, review, or gather evidence without repository mutation.

## Inputs

### Governing

- `.governance/authority.md`
- `.governance/evidence.md`

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

No acceptance result is produced unless the explicit read-only task separately designates a verifier.

## Stop Conditions

- required authority or admitted input is missing;
- scope expansion is required but not authorized;
- the required verifier is unavailable;
- unexpected repository drift occurs;
- a required governance or contract condition returns `BLOCKED`.

The contract may narrow repository governance. It cannot weaken governance or enlarge explicit human authority.
