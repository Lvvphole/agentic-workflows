# Completion

## Purpose

Define terminal states and completion requirements.

## PASS

Use `PASS` only when all required deterministic gates pass for the exact candidate identity.

A PASS record must identify the applicable verifier evidence.

## FAIL

Use `FAIL` when a required deterministic gate ran and rejected the exact candidate.

Preserve the failing evidence.

## BLOCKED

Use `BLOCKED` when a required action cannot continue because authority, evidence, repository state, or an authorized verifier is unavailable.

`BLOCKED` is not PASS.

## Candidate produced

A produced file, patch, workflow, review, or repair is a candidate.

A candidate is not accepted until the applicable acceptance authority accepts it.

## Completion conditions

Do not report the task as complete until:

- The authorized path set is unchanged or an authorized scope change is recorded.
- Required deterministic checks have run on the exact candidate.
- Required generated artifacts are synchronized with their source.
- No required gate is FAIL or BLOCKED.
- Required evidence is preserved.
- No protected state transition was performed without authority.

When any condition is not satisfied, report the actual terminal state and the missing condition.
