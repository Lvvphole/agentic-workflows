# Evidence

## Purpose

Define the evidence that each workflow run and repository change must preserve.

## Evidence record

Record these fields when they apply:

- Repository name.
- Trigger event.
- Actor.
- Commit SHA.
- Pull request number.
- Workflow source path and SHA-256.
- Compiled lock-file path and SHA-256.
- `gh aw` version.
- Deterministic commands or required checks.
- Deterministic result for each required check.
- Agentic workflow version and model or engine identifier when available.
- Safe output type and target when a safe output is proposed or applied.
- Final status: PASS, FAIL, or BLOCKED.
- Run URL or immutable artifact reference.

## Provenance

Keep generated evidence tied to the exact candidate identity.

Do not copy a PASS result from an earlier commit to a later commit.

Do not replace missing evidence with model recollection.

## Evidence classes

Label material facts as `VERIFIED`, `OBSERVED`, or `INFERRED` when the distinction affects a state transition.

A completion claim must identify the `VERIFIED` evidence that supports it.

## Agentic analysis

Store an agent diagnosis as analysis evidence.

Do not store an agent diagnosis as a deterministic verifier result.

When an agent creates a repair candidate, record the predecessor candidate identity and the successor candidate identity.

A successor needs fresh verification.
