# AGENTIC_WORKFLOW Task Contract

## Purpose

Change an agentic workflow, harness, hook, middleware, tool policy, or agent execution policy.

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
- active workflow or harness contract
- platform permission and safe-output requirements

### Working

- authorized agentic behavior;
- affected source and compiled contract when applicable;
- acceptance cases.

## Engineering Rules

- **Applicability:** Yes
- Resolve the canonical engineering-rules authority through `.governance/authority.md` when the task is code-capable.
- Verify the required identity, read the canonical rules, and satisfy the Pre-Code Readiness Gate before code-capable mutation.
- If the authority is missing or the gate is unsatisfied, return `BLOCKED`.

## Process

1. Confirm the agentic boundary and allowed capability surface.
2. Complete Engineering Rules readiness.
3. Make the smallest authorized workflow or harness change.
4. Run deterministic source and compiled-contract checks when applicable.
5. Verify permissions, safe outputs, and frozen acceptance cases.
6. Submit the exact candidate for verification.

## Outputs

- agentic candidate;
- compiled artifacts when applicable;
- acceptance-case results;
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
