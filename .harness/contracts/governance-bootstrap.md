# GOVERNANCE_BOOTSTRAP Task Contract

## Purpose

Establish or repair the governance baseline before that baseline is accepted as repository authority.

## Inputs

### Governing

- externally accepted bootstrap task and authority envelope

### Reference

- `ARCHITECTURE.md`
- accepted bootstrap target
- canonical engineering-rules authority

### Working

- current governance candidate, including `.governance/authority.md`, `.governance/execution.md`, `.governance/security.md`, `.governance/testing.md`, `.governance/verification.md`, `.governance/evidence.md`, and `.governance/completion.md`;
- frozen bootstrap defects and acceptance cases;
- materialized successor candidate.

## Engineering Rules

- **Applicability:** Conditional — required when the bootstrap creates or changes code, tests, schemas, migrations, build logic, CI/CD logic, or harness logic.
- For code-capable bootstrap work, resolve the canonical engineering-rules authority through the externally accepted bootstrap task and authority envelope.
- Treat candidate `.governance/authority.md` only as Working input until the bootstrap baseline is accepted.
- Verify the required identity, read the canonical rules, and satisfy the Pre-Code Readiness Gate before code-capable mutation.
- If the external authority is missing or the gate is unsatisfied, return `BLOCKED`.

## Process

1. Treat existing governance under bootstrap as candidate policy, not self-accepting authority.
2. Freeze the authorized bootstrap requirements and Definition of Done before construction.
3. Materialize one coherent routing and governance graph.
4. Run the required structural and behavioral bootstrap checks.
5. Submit the exact candidate and evidence to an acceptance authority external to the proposer.

## Outputs

- governance-bootstrap candidate;
- exact candidate manifest and hashes;
- bootstrap check results;
- verifier disposition or `BLOCKED`.

## Verifier

The bootstrap acceptance authority designated by the authorized bootstrap task. The proposer cannot designate itself by implication.

## Stop Conditions

- required authority or admitted input is missing;
- scope expansion is required but not authorized;
- the required verifier is unavailable;
- unexpected repository drift occurs;
- a required governance or contract condition returns `BLOCKED`.

The contract may narrow repository governance. It cannot weaken governance or enlarge explicit human authority.
